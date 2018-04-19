# python 模拟登录小爬虫 +  line Notify

## 模拟登录

使用工具：
* chromedriver
* selenium

到[下载地址](https://chromedriver.storage.googleapis.com/index.html)下载最新chromedriver（使用旧版可能报错） 并解压

测试连接
```python
from selenium import webdriver
chromePath = r'解压后chromedriver路径'
wd=webdriver.Chrome(executable_path= chromePath)  #Chrome C大写

loginUrl ='测试登录的网站'
wd.get(loginUrl)
```


填写账号密码
```python

wd.find_element_by_xpath('//*[@id="userid"]').send_keys('你要填写的账号名') 
# '//*[@id="userid"]' 为xpath  抓取方法到chrome打开开发者模式 找到所要填写的栏位 右键 copy ->xpath

wd.find_element_by_xpath('//*[@id="passwd"]').send_keys('输入密码')

#如果是按键提交
wd.find_element_by_xpath('//*[@id="login_btn"]').click()

#如果是表单提交
wd.find_element_by_xpath('//*[@id="login_btn"]').submit()

```

登录完成 这样所有的cookies都存在'wd'里面 随时可以调用

```python
#额外补充 密码输入
import getpass
input = getpass.getpass("Please input your password:")

#input即密码 可直接调用
#如：wd.find_element_by_xpath('//*[@id="passwd"]').send_keys(input)
#调用完清除？？
```


## 将selenium的cookies传入requests

构建Session()
```python
import reqeusts
req = requests.Session()

#从'wd'里调出cookies
cookies = wd.get_cookies()

#将selenium形式的cookies转换为requests可用的cookies。
for cookie in cookies:
        req.cookies.set(cookie['name'],cookie['value'])
        
#Done 来测试要抓取的网站
req.get('待测试的链接')
```


### 小小补充抓取后的网页格式 
```python
html1=req.get('网站').content #byte格式 需要decode
html2=req.get('网站').content.decode('utf-8') #str 格式 

#如str是json 可使用json直接paser
import json
html_paser=json.loads(html2)
```


## line Notify 

要想使用首先登录 https://notify-bot.line.me/my/ 登录账号 

（中间好像有个申请开发者之类的动作）

然后到 Generate access token (For developers) ->Generate token ->选择发送到的群组（好像只能群组）

完成后生成一个token （复制下来）

然后python端

安装linetool库
```
>sudo pip install linetool
```

代码部分很简单 

```python
import os
import lineTool

token = "刚刚的token"
msg = "Hello world" #所要发的消息
 
lineTool.lineNotify(token, msg)
```

Done 

简不简单XDDD


