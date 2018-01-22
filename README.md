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

    ah.post(url, params, type, successBlock(o), errorBlock(e))




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

        showAlert.showAlert2(title, content, resClosure(i))


五. CoreActionSheet： actionSheet (窗口底部选项列表)
===============================
#### 展示可选列表:<br/>
labels: 可选的内容(默认已经添加了取消,所以不要包含取消)<br/>

resClosure(可选):用户点击了各种选项后回调,点击取消i=0,点击最后面的灰色半透明背景i=-1,其他i从1开始按labels顺序依次递增<br/>
    
        actionSheet.show(labels, resClosure(i))


六. CoreArchive： Key:CoreArchiveKey, 全局变量:arc (缓存)
===============================

#### 1.设置一个key-value:<br/>

        arc.set(key,value)



#### 2.读取一个key对应的value:<br/>


        arc.get(key)



六. CoreIV： CoreWeb底层架构,应该用不到,文档略
===============================

七. Nav： 混编底层框架,开发中....
===============================

八. CorePicker： 高仿iOS各种3D选取控件(单行,多行,时间选取,省市级联),开发中
===============================


