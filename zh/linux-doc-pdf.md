
# [linux环境基于python语言docx转pdf](https://www.cnblogs.com/mrtop/p/11995974.html)

windows平台因借助win32com具有多种方法将word转为pdf，但linux环境不具备此环境，win32com包也将import失败，那该如何做呢？


```

# -*- coding: utf-8 -*-
"""

linux platform word to pdf

"""

import  subprocess

import  os

try:

from comtypes import client

except  ImportError:

client =  None

try:

from win32com.client import  constants, gencache

except  ImportError:

constants =  None

gencache =  None

def  doc2pdf_linux(docPath, pdfPath):

"""

convert a doc/docx document to pdf format (linux only, requires libreoffice)

:param doc: path to document

"""

cmd =  'libreoffice6.3 --headless --convert-to pdf'.split() +  [docPath] +  ['--outdir'] +  [pdfPath]

p =  subprocess.Popen(cmd, stderr=subprocess.PIPE, stdout=subprocess.PIPE)

p.wait(timeout=30)

stdout, stderr =  p.communicate()

if  stderr:

raise  subprocess.SubprocessError(stderr)

def  doc2pdf(docPath, pdfPath):

"""

convert a doc/docx document to pdf format

:param doc: path to document

"""

docPathTrue =  os.path.abspath(docPath) # bugfix - searching files in windows/system32

if  client is  None:#判断环境，linux环境这里肯定为None

return  doc2pdf_linux(docPathTrue, pdfPath)

word =  gencache.EnsureDispatch('Word.Application')

doc =  word.Documents.Open(docPathTrue, ReadOnly=1)

doc.ExportAsFixedFormat(pdfPath,

constants.wdExportFormatPDF,

Item=constants.wdExportDocumentWithMarkup,

CreateBookmarks=constants.wdExportCreateHeadingBookmarks)

word.Quit(constants.wdDoNotSaveChanges)

if  __name__ ==  '__main__':

wordpath='/var/db/Report_20191206105753.docx'

pdfpath='/var/db'

doc2pdf(wordpath,pdfpath)

```
