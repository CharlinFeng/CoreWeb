# CoreWeb
原生WebView与H5混编，高效，简单！

前言：
===============================
#### 1.层级关系：<br/>
 CoreIV: 100<br/>
 NavVC: 200<br/>

Swiper：手动导入
===============================
#### 1.基本使用：

    Key: SwiperKey
    Class: SwiperClass
    object: 第三方框架，需手动实例化

#### 2.实例化对象：(js和css已自动引入)


    中文文档： http://www.swiper.com.cn/api/start/new.html
    
    
    参考dom：
    
	<div class="content width_100 height_100">
		<div class="swiper-wrapper">
			<div v-for="(v,i) in vs" class="swiper-slide">
				<video class="width_100 height_100" v-bind:src="v" loop="loop"></video>
			</div>
		</div>
	</div>
    
    
    
    
    
    参考js代码
    

	var swiper = new Swiper('.content', {
	     direction: "vertical",
	     speed: 300,
	     roundLengths: true,
	     loop: true,
	     effect: 'coverflow',
	     coverflowEffect: {
	      rotate: 60,
	      stretch: 20,
	      depth: 200,
	      modifier: 2,
	      slideShadows: true
	     },
	     on: {
	      slideChangeTransitionStart: function() {

	       weak_self.vue.activeIndex = this.activeIndex
	       weak_self.playCurrentVideo()
	      }
	     },

   	 })

   
   



CoreList：手动导入
===============================
#### 1.基本使用：

    Key: CoreListKey
    Class: CoreListClass
    object: corelist

#### 2.基本使用：
单列表快速使用：refreshNow（初始化后是否立即刷新，默认是true）


    //初始化并立即刷新：请配置vue中的key为dataList（默认值）
    coreList.prepare(url,params,refreshNow = true)

    //后续再次刷新: params(null表示使用旧参数刷新页面，也可以传入新参数刷新)
    coreList.refresh(params=null)
    

#### 3.自定义多列表：


    //初始化一个corelist
    let list1 = new CoreListClass()

    //指定cls，vue中的数组key
    list1.cls="cls1"
    list1.dataListKey="listkey1" //同时请到vue中配置对应的key
    //初始化并立即刷新：
    list1.prepare(url,params,refreshNow = true)




一. 基本框架：
===============================
#### CoreWeb是整体项目的根基。

1.请到CoreWeb复制Lib文件夹到每个页面<br/>

2.每个页面的基本模块:<br/>

    nav,index,vue,host,list,action,other
    
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



六. CoreIV： iv （全屏加载视图）
===============================

#### 1.隐藏(一般在网络请求结束后，移除全屏的加载视图)


        iv.dismiss()


七. Nav： 混编底层框架,开发中....
===============================

#### 1.配置导航条：并自定义导航条
title: 标题
theme 0:白色背景(默认)，theme 1:颜渐变背景， theme 2:纯蓝色背景， theme 3:切换（开发中）
border：0 不要线，1要线(默认)

 
    //此方法是CoreWeb内部调用，请勿手动调用
    function navBarLoad(){
      showNavBar(title,theme=0,border=1)
    }

#### 2.页面跳转与原生混编相关api

    function pop(params){

     //普通的返回一个页面
     window.location.href = "charlin://pop?index=-1"
    }

    //url:页面地址，相对地址
    //页面可滑动返回
    //url:页面地址，相对地址
    //页面可滑动返回
    
    function push(url, params, bartype = StatusBarType.white, backtype=BackType.allow){}

 ##### 相关枚举定义：

     //电池栏样式
     StatusBarType = {}; //电池栏样式　　　　　　　　　　　
     StatusBarType.white = 0 //白色(默认)　　　　　　　　　　
     StatusBarType.black = 1　//黑色　　　
    
     //侧滑返回
     BackType = {};　//是否可以侧滑返回　　　　　　　　　　　
     BackType.allow = 0 //可以　　　　　　　　　　
     BackType.forbid = 1　//不可以　　



     //原生客户端：
     charlin://push?json={"url":"a.html","bartype":0/1,"backtype":0/1}



    //刷新
    function reload(){
    }


#### 3.右侧barItem添加

    addRightItem("登录",function(){
             console.log("登录")
     })

#### 4.添加seg切换

     showNavBar_seg(["英语星球","天天向上"],function(i){

        console.log(i)     
     })




八. PreLoad： 页面预加载 pl
===============================

1.首先到PreLoad框架内部，预定义好所有的页面

     let Home = "/Home/home.html" //首页

2.到逻辑页面

      
    pl.preload(pages_arr)



九. CoreCountBtn： 倒计时按钮 countbtn
===============================

    //安装 cls是按钮的类（需要.），btn父级div要和按钮一样大
    countbtn.setup(cls)

    //点击按钮，成功请求服务器数据之后
    countbtn.counting()



十. CorePicker： 高仿iOS各种3D选取控件(单行,多行,时间选取,省市级联),开发中
===============================


