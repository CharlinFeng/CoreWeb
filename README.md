# CoreWeb
原生WebView与H5混编，高效，简单！

一.基本框架：
===============================
CoreWeb是整体项目的根基。

1.请到CoreWeb复制Lib文件夹到每个页面<br/>

2.每个页面的基本模块:<br/>

    index,vue,host,list,action,other
    
3.index已经实现了viewDidLoad方法，且内部已经默认加载了以下基本框架：<br/>

    Vue, AppHttp,CoreSVP, CoreAlertView, CoreActionSheet
    
4.每个页面不再需要引入require.js了，只需要引入<br/>

    <script src="/AbcStar/FrameWorks/CoreWeb/CoreWeb.js"></script>


二.AppHttp： ah
===============================

url: 地址,直接写相对地址,不需要host了,内部已经拼接了baseUrl
params: 参数
type: 0没有hud,1有hud
successBlock: 成功回调(回调参数o)
errorBlock: 失败回调(回调参数e)

    ah.post(url, params, type, successBlock, errorBlock)







