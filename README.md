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
<img width="50%" src="https://mp.weixin.qq.com/debug/wxadoc/dev/image/new_project.png?t=2017727">

## 文件结构
<img width="50%" src="https://ks3-cn-beijing.ksyun.com/static.toptest.yidianzixun.com/public/file/1502438902721/2324F974-6980-4103-A1F3-762517A441DA.png">

小程序有全局的配置、样式、逻辑也有每个页面自己的配置、样式、逻辑文件
> app.json: 全局配置--(小程序公共设置)

> app.js: 全局配置--(小程序逻辑)

> app.wxss: 全局配置--(小程序公共样式)

> pages: 页面数组--(小程序可单独有自己的配置、样式、逻辑文件，还有一个页面结构文件)


## 配置部分注意项~
配置部分相对简单，So 只列出如下注意点，顺带附上个人配置：

 > 为了方便开发者减少配置项，我们规定描述页面的这四个文件必须具有相同的路径与文件名。

 > 每增加一个页面，必须在全局app.json文件pages参数下增加对应路径配置！

 > 如果有菜单项，强制要求控制在2-5个！

 > 如果配置菜单必须把小程序初始页面配成菜单list其中一个，否则无法显示菜单！！

<img width="50%" src="https://ks3-cn-beijing.ksyun.com/static.toptest.yidianzixun.com/public/file/1502464076072/88DB58C9-6F3A-493C-B9D5-1F3C745D1CA2.png">
## 逻辑层

| 函数    | 出现位置        |          可能值                                                |  说明 |
|:---|:--|:--|:--|
| App()  | app.js         | 1. **小程序**生命周期函数<br/>2. 自定义函数<br/>3. 数据              |  1.其中自定义函数和数据为全局的<br/> 2.本文件内通过this调用自定义函数和数据，其他文件需要getApp()或者实例后调用  |
| Page() | pages下的页面内 | 1. 初始数据<br/>2.**页面**生命周期函数<br/>3.自定义函数<br/>4.数据    |  1. Page.prototype.route可以获取当前路由路径<br/>2.Page.prototype.setData()可更改数据，并相应到视图层，<br/>直接修改this.data不会更新到页面，且单次设置数据不能超过1024kb。
| 模块化  |               | 1.module.exports(推荐) 2.exports                                |  1. 文件具有单独作用域<br/>2.可以抽离公共代码module.exports 或者 exports对外暴露接口<br/>3.不支持绝对路径以及node_modules              |
|路由    |                |                                                                | 在小程序中所有页面的路由全部由框架进行管理。|
|场景值  |                |                                                                | 自行查看文档|
|API    |                |                                                                |自行查看文档|

###### 有兴趣的话可以自行去了解一下 【前台、后台定义】以及【销毁小程序的时机】

老规矩，剩下的列出需要注意的点：

> App() 必须在 app.js 中注册，且不能注册多个。

>不要在定义于 App() 内的函数中调用 getApp() ，使用 this 就可以拿到 app 实例。

>不要在 onLaunch 的时候调用 getCurrentPages()，此时 page 还没有生成。>

>通过 getApp() 获取实例之后，不要私自调用生命周期函数。


## WXML

| 语法   |  说明  |  注意  |    eg    |
|:---|:---|:---|:---|
|  {{}}     | 1. 用于data对象下存在的字段 出现的位置 <br/> 2. 支持简单计算及组合   | 1. 关键字(需要在双引号之内) <br/> 2. 花括号和引号之间如果有空格，将最终被解析成为字符串 | 1. `<checkbox checked="{{false}}"> </checkbox>` ，不加{{}}会当成字符串false而判定为true <br/> 2. <view>{{"hello" + name}}</view>|
|  wx:for   |   循环数组 | 默认数组的当前项的下标变量名默认为 index，数组当前项的变量名默认为 item         |                    |
| block wx:for |渲染一个包含多节点的结构块。 | | |
| wx:key |指定列表中项目的唯一的标识符。 | | |
| wx:if <br/> wx:elif <br/>  wx:else <br/> wx:if vs hidden | 1. 条件渲染 <br/> 2. wx:if 有更高的切换消耗而 hidden 有更高的初始渲染消耗 | | 1. `<view wx:if="{{condition}}"> True </view>`|
| block wx:if | 方便整体控制 | | |
| template | 1. 定义代码片段 <br/> 2. name属性定义模板名字<br/> 3. is属性声明需要的使用的模板并需要传入data <br/> 4. 模板有自己的作用域，只能使用data传入数据 | | |
| import和include | 1. import引用目前文件定义的模板 <br/> 2. include可以将目标文件除了`<template/>`的整个代码引入，相当于是拷贝到include位置  |  1. import 有作用域的概念，即只会 import 目标文件中定义的 template，而不会 import 目标文件 import 的 template。 |  |
| 事件 | 1. touchstart、touchmove、touchcancel、touchend、、taplongtap <br/> 2. 如无特殊说明，当组件触发事件时，逻辑层绑定该事件的处理函数会收到一个事件对象。(说白了，就是绑定事件js位置会带一个对象，其中包括很多属性) | bind事件绑定不会阻止冒泡事件向上冒泡，catch事件绑定可以阻止冒泡事件向上冒泡。|   `bindtap` <br/>  ` catchtouchstart` |


## WXSS和组件等持续更新中...

觉得还不错就点个赞吧~

