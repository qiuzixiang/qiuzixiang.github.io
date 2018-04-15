# Github建立blog

## 前言
最近各种投简历找工作，发现GitHub是HR很看重的一个点，明知现在搞个blog已经太晚，但总比没有好（滑稽）。
先说一下，我也是边做边学边写blog,如有哪里写错还请指出。
废话不多说，开始自己的首个blog生涯。


---

首先

注册GitHub账号（废话），电脑端（本人使用远端ubuntu16.04）
电脑端安装 git （全新ubuntu 谅解一下）
```
>sudo apt-get install git
```

接下来配置username和email
```
>git config --global user.name "输入你的github账号"

>git config --global user.email "输入你github所使用的邮箱"
```

## 设置ssh连接github（？

首先输入下方指令生成秘钥
```	
>ssh-keygen -t rsa -C "输入你github所使用的邮箱" 
```
系统会先询问秘钥存放地址（默认直接按Enter）
```
Enter a file in which to save the key (~/user/.ssh/id_rsa):[Press enter]
```
接下来系统会问让你输入一串密码（passphrase）并验证一次 之后登录时需使用 
```
Enter new passphrase (empty for no passphrase): [Type new passphrase]
Enter same passphrase again: [One more time for luck]
Your identification has been saved with the new passphrase.
```
然后在你存放秘钥的地址找到id_rsa.pub 用你能想到的方法将其中内容复制到[github add ssh](https://github.com/settings/keys) (因为档案在远端 一时想不到什么方法 蠢蠢的用filezilla 将id_rsa.pub搞到本地打开)

然后在[github ssh](https://github.com/settings/keys)可以看到![图](https://lh4.googleusercontent.com/AhYtN-X-zP5YSacnm-Ss5zEcBgEUkNQHbs0fIG-QO7PVX3ubf_gW1gvqYLChzC5QJIDcC0asEIW9DA=w2560-h987-rw)

还未连接会显示灰色并显示Never used

下一步来测试ssh
```
>ssh -T git@github.com
```
然后输入刚刚设置的密码（passphrase）

![](https://lh4.googleusercontent.com/QKiqBxyoTLCvkZ2Y2QBHe9vtB6-MaoeyWUTehyBzNji07Qjx4cWYH0PtCiJbv9a6OIhhzIN9Xr5ZsA=w958-h969)

看到上面指令表示连接测试成功


参考
http://magicse7en.github.io/2016/03/06/ubuntu-github-hexo-blog-setup/
https://help.github.com/articles/testing-your-ssh-connection/
http://hungchicheng.me/2017/05/11/how-to-make-blog-on-github/

---

建立专案（repository）

专案名必须是 
```
github账号.github.io
```

![](https://lh4.googleusercontent.com/aQly7q-uWNQNClaQcyXu46Fk4_YrR-93ac7gxlaEL2KM6HxLpVRYTjsdXmpfL4cg-JgsAxEp8zGuW6Vyg58R=w1987-h775-rw)

接下来一段git操作 emmmmmm

在专案中建立一个index.html 做测试 内容随意 
```
<html>This is my personal blog</html>
```
像上面这样就好 

然后push到github
```
>git add .
>git commit -m "add index.html"
>git push origin master
```
git小白 有问题还请纠正

确认index.html有进入专案 可以用浏览器打开 github账号名.github.io 来确认是否传输成功
应该会看到网页如下
```
This is my personal blog
```



---

使用Jekyll ([为什么使用Jekyll](http://hungchicheng.me/2017/05/11/how-to-make-blog-on-github/))


```
>sudo apt install jekyll
>jekyll new myblog
>mv myblog/* 你专案的目录
```

然后push到github 就能看到一个初始化的jekyll 网站

如果想要在本地架设个web serve 可以直接输入
```
>cd 专案目录
>jekyll serve
```

然后就能在 http://localhost:4000 看到网站

如需外网访问 
```
>jekyll serve -w -host=0.0.0.0
```
就能通过 ip:4000 来访问


