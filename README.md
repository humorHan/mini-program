# mini-program
勘探-微信小程序

## 注册小程序账号
    [前往注册](https://mp.weixin.qq.com) 
初始化配置
每增加一个页面，必须在全局app.json文件pages参数下增加对应路径配置！！
菜单2-5个！！
如果配置菜单必须把小程序初始页面配成菜单list其中一个，否则无法显示菜单！！
逻辑层
App()参数--object对象
声明周期函数
其他（开发者可以添加任意的函数或数据到 Object 参数中，用 this 可以访问）！！
深层控制： 前台、后台定义 + 什么时候销毁小程序
getApp() —获取App()实例
注意： App() 必须在 app.js 中注册，且不能注册多个。
不要在定义于 App() 内的函数中调用 getApp() ，使用 this 就可以拿到 app 实例。

不要在 onLaunch 的时候调用 getCurrentPages()，此时 page 还没有生成。

通过 getApp() 获取实例之后，不要私自调用生命周期函数。