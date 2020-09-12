
# [libreoffice python 操作word及excel文档](https://www.cnblogs.com/zl1991/p/10615881.html)

1、开始、关闭libreoffice服务；

开始之前同步字体文件时间，是因为创建soffice服务时，服务会检查所需加载的文件的时间，如果其认为时间不符，则其可能会重新加载，耗时较长，因此需事先统一时间。

使用时如果需要多次调用，最后每次调用均开启后关闭，否则libreoffice会创建一个缓存文档并越用越大，处理时间会增加。

```

class OfficeProcess(object): def __init__(self):
        self.p = 0
        subprocess.Popen('find /usr/share/fonts | xargs touch -m -t 201801010000.00', shell=True) def start_office(self):
        self.p = subprocess.Popen('soffice --pidfile=sof.pid --invisible --accept="socket,host=localhost,port=2002;urp;"', shell=True) while True: try:
                local_context = uno.getComponentContext()
                resolver = local_context.getServiceManager().createInstanceWithContext('com.sun.star.bridge.UnoUrlResolver', local_context)
                resolver.resolve('uno:socket,host=localhost,port=2002;urp;StarOffice.ComponentContext') return
            except: print(ts(), "wait for connecting soffice...")
                time.sleep(1) continue

    def stop_office(self):
        with open("sof.pid", "rb") as f: try:
                os.kill(int(f.read()), signal.SIGTERM)
                self.p.wait() except: pass

```

2、init service manager

```

local_context = uno.getComponentContext()
        service_manager = local_context.getServiceManager()
        resolver = service_manager.createInstanceWithContext('com.sun.star.bridge.UnoUrlResolver', local_context)
        self.ctx = resolver.resolve('uno:socket,host=localhost,port=2002;urp;StarOffice.ComponentContext')
        self.smgr = self.ctx.ServiceManager
        self.desktop = self.smgr.createInstanceWithContext('com.sun.star.frame.Desktop', self.ctx)

```

3、从二进制数据中读取doc文档

```

def ImportFromMemory(self, data):
        istream = self.smgr.createInstanceWithContext('com.sun.star.io.SequenceInputStream', self.ctx)
        istream.initialize((uno.ByteSequence(data), ))
        pv = PropertyValue()
        pv.Name = 'InputStream' pv.Value = istream
        self.doc = {'doc': []} try:
            self.document = self.desktop.loadComponentFromURL('private:stream/swriter', '_blank', 0, (pv, ))
            self.text = self.document.getText() except:
            self.text = None

```

4、读取doc文档中的数据

```

def ExportToJson(self): try:
            l = self.__ParseText(self.text, self.__Callback(self.doc['doc']))
            self.doc['length'] = l except:
            self.doc = {'doc': [], 'length': 0} return json.dumps(self.doc)

@staticmethod def __Callback(alist): def Append(sth):
            alist.append(sth) return Append

```

```

def __ParseText(self, text, func):
        l = 0
        text_it = text.createEnumeration() while text_it.hasMoreElements():
            element = text_it.nextElement() if element.supportsService('com.sun.star.text.Paragraph'):
                l += self.__ParseParagraph(element, func) elif element.supportsService('com.sun.star.text.TextTable'):
                l += self.__ParseTable(element, func) else: pass
        return l

```

```

def __ParseParagraph(self, paragraph, func):
        p = {'paragraph': []}
        l = 0
        paragraph_it = paragraph.createEnumeration() while paragraph_it.hasMoreElements():
            portion = paragraph_it.nextElement() if portion.TextPortionType == 'Text':
                l += self.__ParsePortionText(portion, self.__Callback(p['paragraph'])) elif portion.TextPortionType == 'SoftPageBreak': pass
            elif portion.TextPortionType == 'TextField':
                l += self.__ParsePortionText(portion, self.__Callback(p['paragraph'])) else:
                l += self.__ParseTextContent(portion, self.__Callback(p['paragraph'])) if hasattr(paragraph, 'createContentEnumeration'):
            l += self.__ParseTextContent(paragraph, self.__Callback(p['paragraph']))
        p['length'] = l
        func(p) return l def __ParseTextContent(self, textcontent, func):
        l = 0
        content_it = textcontent.createContentEnumeration('com.sun.star.text.TextContent') while content_it.hasMoreElements():
            element = content_it.nextElement() if element.supportsService('com.sun.star.text.TextGraphicObject'):
                l += self.__ParsePortionGraphic(element, func) elif element.supportsService('com.sun.star.text.TextEmbeddedObject'): pass
            elif element.supportsService('com.sun.star.text.TextFrame'):
                l += self.__ParseFrame(element, func) elif element.supportsService('com.sun.star.drawing.GroupShape'):
                l += self.__ParseGroup(element, func) else: pass
        return l def __ParseFrame(self, frame, func):
        f = {'frame': []}
        l = self.__ParseText(frame.getText(), self.__Callback(f['frame']))
        f['length'] = l
        func(f) return l def __ParseGroup(self, group, func):
        l = 0 for i in range(group.getCount()):
            it = group.getByIndex(i) if it.supportsService('com.sun.star.drawing.Text'):
                l += self.__ParseFrame(it, func) else: pass
        return l def __ParsePortionText(self, portion_text, func):
        func({'portion': portion_text.String, 'length': len(portion_text.String)}) return len(portion_text.String) def __ParsePortionGraphic(self, portion_graphic, func):
        gp = self.smgr.createInstanceWithContext('com.sun.star.graphic.GraphicProvider', self.ctx)
        stream = self.smgr.createInstanceWithContext('com.sun.star.io.TempFile', self.ctx)
        pv1 = PropertyValue()
        pv1.Name = 'OutputStream' pv1.Value = stream
        pv2 = PropertyValue()
        pv2.Name = 'MimeType' pv2.Value = 'image/png' gp.storeGraphic(portion_graphic.Graphic, (pv1, pv2))
        stream.getOutputStream().flush()
        stream.seek(0)
        l = stream.getInputStream().available()
        b = uno.ByteSequence(b'')
        stream.seek(0)
        l, b = stream.getInputStream().readBytes(b, l)
        img = {'image': base64.b64encode(b.value).decode('ascii')}
        img['height'] = portion_graphic.Height
        img['width'] = portion_graphic.Width
        img['actualheight'] = portion_graphic.ActualSize.Height
        img['actualwidth'] = portion_graphic.ActualSize.Width
        img['croptop'] = portion_graphic.GraphicCrop.Top
        img['cropbottom'] = portion_graphic.GraphicCrop.Bottom
        img['cropleft'] = portion_graphic.GraphicCrop.Left
        img['cropright'] = portion_graphic.GraphicCrop.Right
        img['length'] = 0
        func(img) return 0 def __ParseTable(self, table, func):
        l = 0 try:
            matrix = self.__GetTableMatrix(table)
            seps = self.__GetTableSeparators(table)
            t = {}
            count = 0 for ri in matrix.keys():
                t[ri] = {} for ci in matrix[ri].keys():
                    t[ri][ci] = dict(matrix[ri][ci]) del t[ri][ci]['cell']
                    t[ri][ci]['content'] = []
                    l += self.__ParseText(matrix[ri][ci]['cell'], self.__Callback(t[ri][ci]['content']))
                    count += t[ri][ci]['rowspan'] * t[ri][ci]['colspan'] if count != len(t) * len(seps): raise ValueError('count of cells error')
            func({'table': t, 'row': len(t), 'column': len(seps), 'length': l, 'tableid': self.table_id})
            self.table_id += 1
        except:
            l = 0 print('discard wrong table') return l

    @staticmethod def __GetTableSeparators(table):
        result = [table.TableColumnRelativeSum] for ri in range(table.getRows().getCount()):
            result += [s.Position for s in table.getRows().getByIndex(ri).TableColumnSeparators]
        result = sorted(set(result)) for i in range(len(result) - 1):
            result[i] += 1 if result[i] + 1 == result[i + 1] else 0 return sorted(set(result))

    @staticmethod def __NameToRC(name):
        r = int(re.sub('[A-Za-z]', '', name)) - 1 cstr = re.sub('[0-9]', '', name)
        c = 0 for i in range(len(cstr)): if cstr[i] >= 'A' and cstr[i] <= 'Z':
                c = c * 52 + ord(cstr[i]) - ord('A') else:
                c = c * 52 + 26 + ord(cstr[i]) - ord('a') return r, c

    @staticmethod def __GetTableMatrix(table):
        result = {} for name in table.getCellNames():
            ri, ci = WordToJson.__NameToRC(name)
            cell = table.getCellByName(name) if ri not in result:
                result[ri] = {}
            result[ri][ci] = {'cell': cell, 'rowspan': cell.RowSpan, 'name': name}

        seps = WordToJson.__GetTableSeparators(table) for ri in result.keys():
            sep = [s.Position for s in table.getRows().getByIndex(ri).TableColumnSeparators] + [table.TableColumnRelativeSum]
            sep = sorted(set(sep)) for ci in result[ri].keys():
                right = seps.index(sep[ci]) if sep[ci] in seps else seps.index(sep[ci] + 1)
                left = -1 if ci == 0 else seps.index(sep[ci - 1]) if sep[ci - 1] in seps else seps.index(sep[ci - 1] + 1)
                result[ri][ci]['colspan'] = right - left return result

```

5、写doc文档

self.doco = self.desktop.loadComponentFromURL('private:factory/swriter', '_blank', 0, ())
        self.texto = self.doco.getText()
        self.cursoro = self.texto.createTextCursor()
        self.cursoro.ParaBottomMargin = 500

```

def __WriteText(self, text, texto, cursoro): for it in text: if 'paragraph' in it:
                self.__WriteParagraph(it, texto, cursoro) elif 'image' in it:
                self.__WritePortionGraphic(it, texto, cursoro) elif 'table' in it:
                self.__WriteTable(it, texto, cursoro) def __WriteParagraph(self, paragraph, texto, cursoro): if paragraph['length'] > 0: if 'result' in paragraph: for it in paragraph['result']:
                    texto.insertString(cursoro, it['trans_sen'], False) else:
                texto.insertString(cursoro, paragraph['paragraph'], False)
            texto.insertControlCharacter(cursoro, ControlCharacter.PARAGRAPH_BREAK, False) def __WritePortionGraphic(self, portion_graphic, texto, cursoro):
        png_base64 = portion_graphic['image']
        png = base64.b64decode(png_base64)
        gp = self.smgr.createInstanceWithContext('com.sun.star.graphic.GraphicProvider', self.ctx)
        istream = self.smgr.createInstanceWithContext('com.sun.star.io.SequenceInputStream', self.ctx)
        istream.initialize((uno.ByteSequence(png), ))
        pv = PropertyValue()
        pv.Name = 'InputStream' pv.Value = istream

        actualsize = uno.createUnoStruct('com.sun.star.awt.Size')
        actualsize.Height = portion_graphic['actualheight'] if 'actualheight' in portion_graphic else portion_graphic['height']
        actualsize.Width = portion_graphic['actualwidth'] if 'actualwidth' in portion_graphic else portion_graphic['width']
        graphiccrop = uno.createUnoStruct('com.sun.star.text.GraphicCrop')
        graphiccrop.Top = portion_graphic['croptop'] if 'croptop' in portion_graphic else 0
        graphiccrop.Bottom = portion_graphic['cropbottom'] if 'cropbottom' in portion_graphic else 0
        graphiccrop.Left = portion_graphic['cropleft'] if 'cropleft' in portion_graphic else 0
        graphiccrop.Right = portion_graphic['cropright'] if 'cropright' in portion_graphic else 0

        image = self.doco.createInstance('com.sun.star.text.TextGraphicObject')
        image.Surround = NONE
        image.Graphic = gp.queryGraphic((pv, ))
        image.Height = portion_graphic['height']
        image.Width = portion_graphic['width']
        image.setPropertyValue('ActualSize', actualsize)
        image.setPropertyValue('GraphicCrop', graphiccrop)
        texto.insertTextContent(cursoro, image, False)
        texto.insertControlCharacter(cursoro, ControlCharacter.PARAGRAPH_BREAK, False) def __WriteTable(self, table, texto, cursoro):
        tableo = self.doco.createInstance('com.sun.star.text.TextTable')
        tableo.initialize(table['row'], table['column'])
        texto.insertTextContent(cursoro, tableo, False) # texto.insertControlCharacter(cursoro, ControlCharacter.PARAGRAPH_BREAK, False)
        tcursoro = tableo.createCursorByCellName("A1")

        hitbug = False if table['row'] > 1:
            tcursoro.goDown(1, True)
            hitbug = tcursoro.getRangeName() == 'A1'

        for ri in sorted([int(r) for r in table['table'].keys()]):
            rs = table['table'][str(ri)] for ci in sorted([int(c) for c in rs.keys()]):
                cell = rs[str(ci)] if hitbug == False and (cell['rowspan'] > 1 or cell['colspan'] > 1):
                    tcursoro.gotoCellByName(cell['name'], False) if cell['rowspan'] > 1:
                        tcursoro.goDown(cell['rowspan'] - 1, True) if cell['colspan'] > 1:
                        tcursoro.goRight(cell['colspan'] - 1, True)
                    tcursoro.mergeRange()
                ctexto = tableo.getCellByName(cell['name']) if ctexto == None: continue ccursoro = ctexto.createTextCursor()
                ccursoro.CharWeight = FontWeight.NORMAL
                ccursoro.CharWeightAsian = FontWeight.NORMAL
                ccursoro.ParaAdjust = LEFT
                self.__WriteText(cell['content'], ctexto, ccursoro)

```

6、生成二进制的doc文档数据

```
        streamo = self.smgr.createInstanceWithContext('com.sun.star.io.Pipe', self.ctx)
        self.doco.storeToURL('private:stream', (PropertyValue('FilterName', 0, 'MS Word 2007 XML', 0), PropertyValue('OutputStream', 0, streamo, 0)))
        streamo.flush()
        _, datao = streamo.readBytes(None, streamo.available())
```

7、从doc文档数据生成pdf的二进制数据

```
        streamo = self.smgr.createInstanceWithContext('com.sun.star.io.Pipe', self.ctx)
        self.doco.storeToURL('private:stream', (PropertyValue('FilterName', 0, 'writer_pdf_Export', 0), PropertyValue('OutputStream', 0, streamo, 0)))
        streamo.flush()
        _, datap = streamo.readBytes(None, streamo.available())
```

8、读取excel二进制数据

```

　　def ImportFromMemory(self, data):
        istream = self.smgr.createInstanceWithContext('com.sun.star.io.SequenceInputStream', self.ctx)
        istream.initialize((uno.ByteSequence(data), ))
        pv = PropertyValue()
        pv.Name = 'InputStream' pv.Value = istream
        self.doc = {'doc': []} try: print("before loadComponentFromURL")
            self.document = self.desktop.loadComponentFromURL('private:stream/scalc', '_blank', 0, (pv, ))
            self.sheets = self.document.getSheets() print("ImportFromMemory done") except: print("ImportFromMemory failed")
            self.sheets = None

```

9、读取excel的文本数据

```

    def ExportToJson(self): try:
            l = self.__ParseText(self.sheets, self.__Callback(self.doc['doc']))
            self.doc['length'] = l except:
            self.doc = {'doc': [], 'length': 0} return json.dumps(self.doc)

```

```

    def __ParseText(self, sheets, func):
        l = 0
        sheets_it = sheets.createEnumeration() while sheets_it.hasMoreElements():
            element = sheets_it.nextElement() if element.supportsService('com.sun.star.sheet.Spreadsheet'):
                l += self.__ParseSpreadsheet(element, func) return l def __ParseSpreadsheet(self, spreadsheet, func):
        l = 0
        p = {'spreadsheet': []}
        visible_cells_it = spreadsheet.queryVisibleCells().getCells().createEnumeration() while visible_cells_it.hasMoreElements():
            cell = visible_cells_it.nextElement()
            type = cell.getType() if type == self.EMPTY: print("cell.type==empty") elif type == self.VALUE: print("cell.type==VALUE", "value=", cell.getValue(), cell.getCellAddress ()) elif type == self.TEXT: print("cell.type==TEXT","content=", cell.getString().encode("UTF-8"), cell.getCellAddress ())
                l += self.__ParseCellText(spreadsheet, cell, self.__Callback(p['spreadsheet'])) print("__ParseCellText=", p) elif type == self.FORMULA: print("cell.type==FORMULA", "formula=", cell.getValue())
        p['length'] = l
        func(p) return l def __ParseCellText(self, sheet, cell, func): try:
            x = cell.getCellAddress().Column
            y = cell.getCellAddress().Row
            sheetname = sheet.getName() except:
            x = -1 y = -1 sheetname = None
        func({'celltext': cell.getString(), 'x': x, 'y': y, 'sheetname': sheetname, 'length': len(cell.getString())}) return len(cell.getString())

```

　　　　　self.EMPTY = uno.Enum("com.sun.star.table.CellContentType", "EMPTY")
        self.TEXT = uno.Enum("com.sun.star.table.CellContentType", "TEXT")
        self.FORMULA = uno.Enum("com.sun.star.table.CellContentType", "FORMULA")
        self.VALUE = uno.Enum("com.sun.star.table.CellContentType", "VALUE")

10、替换excel的文本信息

```

    def ImportFromJson(self, data):
        doc = json.loads(data) try:
            self.__WriteText(doc['doc']) except: pass

```

```

    def __WriteText(self, text): print("__WriteText begin:", text)
        sheet = None for it in text: if 'paragraph' in it and 'sheetname' in it: if sheet == None or sheet.getName() != it['sheetname']: try:
                        sheet = self.sheets.getByName(it['sheetname']) print("getsheet:", it['sheetname'], "=", sheet.getName()) except:
                        sheet = None continue self.__WriteParagraph(it, sheet) def __WriteParagraph(self, paragraph, sheet): print("__WriteParagraph") if paragraph['length'] > 0: try:
                x = paragraph['x']
                y = paragraph['y'] print("getcell:", x, y)
                cell = sheet.getCellByPosition(x, y) print("getcell done") except: return
            if 'result' in paragraph: for it in paragraph['result']: print("cell=", cell.getString())
                    cell.setString(it['trans_sen']) print("cell,", cell.getString(), ",done")

```

11、生成excel文档二进制数据

```
　　　　  streamo = self.smgr.createInstanceWithContext('com.sun.star.io.Pipe', self.ctx)
        self.document.storeToURL('private:stream', (PropertyValue('FilterName', 0, 'Calc MS Excel 2007 XML', 0), PropertyValue('OutputStream', 0, streamo, 0)))
        streamo.flush()
        _, datao = streamo.readBytes(None, streamo.available())
```

12、生成excel的pdf文档

```
        streamo = self.smgr.createInstanceWithContext('com.sun.star.io.Pipe', self.ctx)
        self.document.storeToURL('private:stream', (PropertyValue('FilterName', 0, 'calc_pdf_Export', 0), PropertyValue('OutputStream', 0, streamo, 0)))
        streamo.flush()
        _, datap = streamo.readBytes(None, streamo.available())
```		