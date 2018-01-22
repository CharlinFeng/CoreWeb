# CoreWeb
原生WebView与H5混编，高效，简单！

一. 基本框架：
===============================
#### CoreWeb是整体项目的根基。

1.请到CoreWeb复制Lib文件夹到每个页面<br/>

2.每个页面的基本模块:<br/>

    index,vue,host,list,action,other
    
3.index已经实现了viewDidLoad方法，且内部已经默认加载了以下基本框架：<br/>

    Vue, AppHttp,CoreSVP, CoreAlertView, CoreActionSheet
    
4.每个页面不再需要引入require.js了，只需要引入<br/>

    <script src="/AbcStar/FrameWorks/CoreWeb/CoreWeb.js"></script>


二. AppHttp： ah
===============================

url: 地址,直接写相对地址,不需要host了,内部已经拼接了baseUrl<br/>
params: 参数<br/>
type: 0没有hud,1有hud<br/>
successBlock: 成功回调(回调参数o)<br/>
errorBlock(可选): 失败回调(回调参数e)<br/>

    ah.post(url, params, type, successBlock, errorBlock)




三. CoreSVP： svp (提示窗)
===============================

#### 1.提示成功(显示2s后自动关闭):<br/>
str: 提示文字,默认文字是"操作成功"<br/>
resClosure(可选): 提示结束后的回调

        svp.showSuccess(str = "操作失败", resClosure)
    
#### 2.提示失败(显示3s后自动关闭):<br/>
str: 提示文字,默认文字是"操作成功"<br/>
resClosure(可选): 提示结束后的回调   

        svp.showError(str = "操作失败", resClosure)

#### 3.加载中:<br/>
str: 提示文字,默认文字是"加载中"

        svp.showLoading(str = "加载中")
  
  
    
#### 4.关闭加载中:(成功和失败是自动关闭,不需要主动关闭)<br/>
resClosure(可选): 关闭结束后的回调 

        svp.dismiss(resClosure)



四. CoreAlertView： alertView (模态窗口)
===============================
#### 1.一个按钮的弹窗:<br/>
title: 标题<br/>
content: 内容文字<br/>
label1: 最下面按钮的文字"知道了"<br/>
resClosure(可选):用户点击了我知道了这个按钮后的回调<br/>


        alertView.showAlert1(title, content, label1 = "知道了", resClosure)



#### 2.两个按钮的弹窗:<br/>
title: 标题<br/>
content: 内容文字<br/>
最下面两个按钮默认值:取消,确定(不可更改).<br/>
resClosure(可选):用户点击了按钮后的回调,取消(i=0),确定(i=1)<br/>

        showAlert2.showAlert1(title, content, resClosure(i))

