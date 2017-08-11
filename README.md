# mini-program
勘探-微信小程序
## 注册小程序账号
   [前往官网注册](https://mp.weixin.qq.com)--流程简单，不赘述.

   在网站的“设置”-“开发者设置”中,得到AppId
## 下载开发者工具
   [mac](https://servicewechat.com/wxa-dev-logic/download_redirect?type=darwin&from=mpwiki)

   [window 32](https://servicewechat.com/wxa-dev-logic/download_redirect?type=ia32&from=mpwiki)

   [windows 64](https://servicewechat.com/wxa-dev-logic/download_redirect?type=x64&from=mpwiki)
## 通过开发者工具创建小程序
<img src="https://mp.weixin.qq.com/debug/wxadoc/dev/image/new_project.png?t=2017727">

## 文件结构
<img src="https://ks3-cn-beijing.ksyun.com/static.toptest.yidianzixun.com/public/file/1502438902721/2324F974-6980-4103-A1F3-762517A441DA.png">

小程序有全局的配置、样式、逻辑也有每个页面自己的配置、样式、逻辑文件

`app.json`: 全局配置--(小程序公共设置)

`app.js`: 全局配置--(小程序逻辑)

`app.wxss`: 全局配置--(小程序公共样式)

`pages`: 页面数组--(小程序可单独有自己的配置、样式、逻辑文件，还有一个页面结构文件)


## 配置部分注意项~
配置部分相对简单，So 只列出如下注意点，顺带附上个人配置：

 `为了方便开发者减少配置项，我们规定描述页面的这四个文件必须具有相同的路径与文件名。`

 `每增加一个页面，必须在全局app.json文件pages参数下增加对应路径配置！`

 `如果有菜单项，强制要求控制在2-5个！`

 `如果配置菜单必须把小程序初始页面配成菜单list其中一个，否则无法显示菜单！！`

<img src="https://ks3-cn-beijing.ksyun.com/static.toptest.yidianzixun.com/public/file/1502440109024/88DB58C9-6F3A-493C-B9D5-1F3C745D1CA2.png">

## 逻辑层

| 函数    | 出现位置  |          可能值                                 |  说明 |
|:---|:--|:--|:--|
| App()  | app.js   | 1. 小程序生命周期函数<br/>2. 自定义函数<br/>3. 数据 |  1.`其中自定义函数和数据为全局的` <br/> 2.`本文件内通过this调用自定义函数和数据，其他文件需要getApp()或者实例后调用`   |

###### 有兴趣的话可以自行去了解一下 【前台、后台定义】以及【销毁小程序的时机】

老规矩，剩下的列出需要注意的点：

`App() 必须在 app.js 中注册，且不能注册多个。`

`不要在定义于 App() 内的函数中调用 getApp() ，使用 this 就可以拿到 app 实例。`

`不要在 onLaunch 的时候调用 getCurrentPages()，此时 page 还没有生成。`

`通过 getApp() 获取实例之后，不要私自调用生命周期函数。`

