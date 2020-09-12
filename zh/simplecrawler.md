
# python最简单的小爬虫

![](https://csdnimg.cn/release/phoenix/template/new_img/reprint.png)

[keeper_zdl](https://me.csdn.net/weixin_40596016)  2017-12-21 09:45:32  ![](https://csdnimg.cn/release/phoenix/template/new_img/articleReadEyes.png)  28307 ![](https://csdnimg.cn/release/phoenix/template/new_img/tobarCollect.png)  收藏  31

分类专栏：  [python](https://blog.csdn.net/weixin_40596016/category_7300872.html)

# 网络爬虫：

网络爬虫（又被称为网页蜘蛛，网络机器人，在FOAF社区中间，更经常的称为网页追逐者），是一种按照一定的规则，自动地抓取万维网信息的程序或者脚本。另外一些不常使用的名字还有蚂蚁、自动索引、模拟程序或者蠕虫。

## 爬虫通用流程：

### [1]发送请求  
[2]获得页面  
[3]解析页面  
[4]下载内容  
[5]存储内容

```

#!/usr/bin/python
# coding:utf-8
# 实现一个简单的爬虫，爬取百度贴吧图片
import urllib
import re
 
# 根据url获取网页html内容
def getHtmlContent(url):
    page = urllib.urlopen(url)
    return page.read()
 
# 从html中解析出所有jpg图片的url
# 百度贴吧html中jpg图片的url格式为：<img ... src="XXX.jpg" width=...>
def getJPGs(html):
    # 解析jpg图片url的正则
    jpgReg = re.compile(r'<img.+?src="(.+?\.jpg)" width')  # 注：这里最后加一个'width'是为了提高匹配精确度
    # 解析出jpg的url列表
    jpgs = re.findall(jpgReg, html)
    return jpgs
 
# 用图片url下载图片并保存成制定文件名
def downloadJPG(imgUrl, fileName):
    urllib.urlretrieve(imgUrl, fileName)
 
# 批量下载图片，保存到F盘zdl文件夹
def batchDownloadJPGs(imgUrls, path='F:/zdl/'):
    # 用于给图片命名
    count = 1
    for url in imgUrls:
        downloadJPG(url, ''.join([path, '{0}.jpg'.format(count)]))
        print '正在下载第'+str(count)+'张'
        count = count + 1
 
# 封装：从百度贴吧网页下载图片
def download(url):
    html = getHtmlContent(url)
    jpgs = getJPGs(html)
    batchDownloadJPGs(jpgs)
 
def main():
    url = 'http://tieba.baidu.com/p/2256306796'
    download(url)
 
if __name__ == '__main__':
    main()
```

# requests方式爬取豆瓣top250电影名

```
#!/usr/bin/python
# coding:utf-8
 
import requests
from bs4 import BeautifulSoup
 
test_url = 'http://movie.douban.com/top250/'
 
def download_page(url):
    headers = {
        'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/47.0.2526.80 Safari/537.36'
    }
    data = requests.get(url,headers=headers).content
    return data
 
movie_name_list = []
def parse_html(html):
    soup = BeautifulSoup(html)
    movie_list_soup = soup.find('ol', attrs={'class': 'grid_view'})
    if movie_list_soup != None:
        for movie_li in movie_list_soup.find_all('li'):
            detail = movie_li.find('div', attrs={'class': 'hd'})
            movie_name = detail.find('span', attrs={'class': 'title'}).getText()
            movie_name_list.append(movie_name)
 
        next_page = soup.find('span', attrs={'class': 'next'}).find('a')
        if next_page:
            parse_html(download_page(test_url + next_page['href']))
        return movie_name_list
 
def main():
    handle = parse_html(download_page(test_url))
    if handle != None:
        handle = list(handle)
        for ele in handle:
            print ele
 
if __name__ == '__main__':
    main()
```

### 成果：

![](https://img-blog.csdn.net/20180117105538660?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2VpeGluXzQwNTk2MDE2/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

1. 请求http://movie.douban.com/top250/  
2. 获取内容  
3. 解析内容  
4. 查找我们要的内容

具体按照自己要的数据，和解析格式爬取。

---


作者：知乎用户  
链接：https://www.zhihu.com/question/64385692/answer/220156451  
来源：知乎  
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。  
  

## Python：

看一下标准库，告诉你：别看了，推荐更高级的包requests：

![](https://pic2.zhimg.com/50/v2-7a3abdb79029fc0261977068d3856fe6_hd.jpg?source=1940ef5c)![](https://pic2.zhimg.com/80/v2-7a3abdb79029fc0261977068d3856fe6_720w.jpg?source=1940ef5c)

  

然后request包文档长成这样，问题就解决了：

![](https://pic2.zhimg.com/50/v2-67baa48c73ffdeb1f87077990557fcd1_hd.jpg?source=1940ef5c)![](https://pic2.zhimg.com/80/v2-67baa48c73ffdeb1f87077990557fcd1_720w.jpg?source=1940ef5c)

  

  

```python3
# Python3 requests:跟curl区别不大
import requests
req = requests.put("https://api.tenxcloud.com/api/v2/clusters/{cluster-id}/services/batch-stop", headers={"username":"<your-user-name>","Authorization": "token <your-api-token>"}, data='{"services": ["<your-service-name>"]')
# 其实标准库也没多复杂，为什么要“妄自菲薄”呢
from urllib.request import urlopen, Request

req = urlopen(
    Request("https://api.tenxcloud.com/api/v2/clusters/CID-ff8a9093353f/services/batch-stop", 
                           data=b'{"services": ["socksoffice"]}', 
                           headers={"username":"<your-user-name>","Authorization": "token <your-api-token>"},method="PUT")
)
```

  

然后你就完活可以走人了，对http还是什么也不知道。照猫画虎，Time - 5m HTTP +1XP