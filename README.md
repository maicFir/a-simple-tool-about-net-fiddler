### a-simple-tool-about-net-fiddler
前言：fidder的官方名词解释是，一款http协议调试的代理工具，能够获取浏览器请求网页的所有信息。通俗来讲就是抓包，能够劫持网页的请求信息，对线上代码css,js,html以及cookie进行修改，同时也可作为调试手机端页面的一种强大利器。
### 长话短说，首先你在看本文，你将从本文中获得什么样的信息：

 * 1：对抓包工具的基本认识，一些自己踩过的坑 
 * 2：如何设置fidder工具，抓取网页页面
 * 3: 如何在本地修改一个线上的网页页面(新浪官网为例)
 * 4：窃取你手机网页信息，做到本地化调试线上数据
 ***
### Fidder长什么样
 * 下载链接：[fiddler](http://baoku.360.cn/soft/show/appid/102430 '下载')
 * 本人用的`fiddler4`，直接下载最新版本即可
 * ![fidder](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/1.png)

 ### fiddler的使用步骤
 * 安装步骤此处省略，直接点击下一步，下一步即可，像安装qq一样简单
 * 当我们安装好后的打开主界面是这样的
 ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/2.png)
 
### Fiddler界面的一些参数
 * (1)	Result:网络响应状态的返回结果
 * (2)	Protocol:请求协议（http or https）
 * (3)	Host:域名
 * (4)	url:请求的地址
 * (5)	Body:请求资源的大小
 * (6)	Caching:请求的缓存(no-cache或者为空)
 * (7)	Content-Type:请求类型(text/html,image/gif等)
 * (8)	Progress:哪个浏览器的id
 * (9)	Enable rules:使用该规则，约束截取网页请求
 * (10)	Unmatched request passthrough:阻断线上页面的请求，捕获本地与线上匹配的页面
 * (11) 要监控的某个特殊的地址
 * (12)	线上地址
 * (13)	本地地址
 ********
      对于Tools这里面的默认菜单栏默认不要动，因新浪网的请求协议是https,所以需按以下步骤操作：Tools>Telerik>fiddler Options>HTTPS(默认不需修改)<br/>
  当你刷新网页时，就会出现以下1标识所监控的网页：
  ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/3.png)
    
### 注意下图标识的网页内容:
  
  ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/4.png)
  
### 如何改掉我标识的两处内容:”今日要闻”改成“今日看点”,2处字体颜色改成绿色？
  * 1:ctrl+u(鼠标右键查看页面源代码)
  * 2：新建一个空白页面命名为index.html,将1中的页面源代码复制粘贴到新建的空白页index.html中
  ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/5.png)
  
###  将上述内容复制到index.html文件中，如下图
  ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/6.png)
* 3：鼠标右键选择1处监控的指定页面，在右侧AutoResonder>Enable rules(勾上)>Add Rule>下面就会出现一个选项4
* 4：然后选择图中的2选项，AutoResonder>Enable rules(勾上)>unmatched requestspassthough(勾上)
    ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/7.png)
* 5：在下方的2处选择步骤2所在的文件目录：
  ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/8.png)
  ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/9.png)
* 6:此时可修改步骤2中的index.html页面
* 7:但是你会发现，当你刷新chrome浏览器，你刚抓取的页面样式全部没有了，怎么会这样?不管怎么刷新都没用（因为fidder劫持了网页信息）
    ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/10.png)
* 8：原来在步骤4上一定要勾住此项unmatched requestspassthough（`勾住`）。
* 9:当上述8操作后，再刷新页面，页面就正常了,如下图
  ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/11.png)
* 10：修改空白页面index.html的”今日看点”且添加内联样式
   ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/12.png) 
* 11：刷新页面后，（https://sina.cn）的页面内容已经被我改变。（本质上线上页面就是我本地的index.html）（注:本地页面一定要是从线上复制粘贴的页面)
   ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/13.png)
* 12:以上步骤就是完成了线上代码的样式调试了，然而，你要调试线上的css和Js怎么办？
* 13:同样将线上的css文件内容拷贝到一个空白的index.css文件中
* 14:找到fiddler所监控到的css
  ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/14.png)
* 15:在下图1处选择 find a file
   ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/15.png)
 * 16:修改本地css相应的代码后，刷新，线上的页面样式也生效了。
  ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/16.png)
* 17:以上步骤完美实现了fiddler抓取网页，并且修改网页信息。
       最后一点，当你取消抓取的信息后网页信息后，
    ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/17.png)  
* 18:此时信息恢复了原来的，样式仍为以前的样式
  ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/18.png)
 ------
### 如何调整线上的手机页面
      #####  跟着下边的步骤操作一遍就ok了
 * 1：打开你的手机，设置wifi,手动设置你wifi的服务器连接地址，和端口<br/>
      Wifi服务器地址填写你笔记本的ip地址(这是我的ip地址192.168.0.101)每个人的电脑ip不一样<br/>
      端口设置与fiddler默认一致：8888
 * 2：在fiddler中打开 Tool>Telerik Fiddler Options>connectors>Allow remote computers to connect(手动勾起)，完成后，关闭fiddler工具，重启该工具
  ![](https://github.com/maicFir/a-simple-tool-about-net-fiddler/blob/master/img/14.png) 
  
  当你手机在浏览任何一个网站页面时，你的抓包工具就可以抓到你想要的页面了。
### 对于使用fiddler遇到的坑
* 1：有时当你无论怎么刷新网页时，你的抓包工具好像都抓不到你的网页请求信息，此时考虑浏览器是否设置缓存，f12审核元素在Network 勾起Disable cache
* 2：当第一条也尝试过时，也没有任何反应，此时你清除fiddler中缓存试试 Tools>clear WinInet cache
* 3: 最好不要修改Tools中的一些默认参数，如果多次无效，请重启fidder或者卸载重新安装即可
-----------------------
  终于写完了，其实fiddler里面还有很多东西，比如你可以捕获ajax传递的参数，获取网页响应的整个html，对于fiddler我知道的都是些凤毛麟角，如果你知道更多，一起学习，分享哦，本人技术有限，第一次用markdown写的，如果觉得看完有帮助，给颗星鼓励一下。后续文章努力提高质量，持续更新中...

### 关于作者
```javascript
  var auhor = {
    Name  : "mcodes",
    site : "https://github.com/maicFir",
    aboutme:"屌丝中的战斗机,菜码一个"
  
  }
```

