# CoreWeb
原生WebView与H5混编，高效，简单！

一.基本框架：
===============================
CoreWeb是整体项目的根基。

1.请到CoreWeb复制Lib文件夹到每个页面
2.每个页面的基本模块:
  index,vue,host,list,action,other
3.index已经实现了viewDidLoad方法，且内部已经默认加载了以下基本框架：
  Vue, AppHttp,CoreSVP, CoreAlertView, CoreActionSheet
4.每个页面不再需要引入require.js了，只需要引入
  <script src="/AbcStar/FrameWorks/CoreWeb/CoreWeb.js"></script>







