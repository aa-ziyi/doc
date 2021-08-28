#  meta 标签的作用
```
The <meta> tag provides metadata about the HTML document. Metadata will not be displayed on the page, but will be machine parsable.
```

不难看出，其中的关键是metadata，中文名叫元数据，是用于描述数据的数据。它不会显示在页面上，但是机器却可以识别。这么一来meta标签的作用方式就很好理解了。

# meta 便签的使用
所有的浏览器都支持meta标签，用于提供页面相关信息，信息都是以名（http-equiv和name标示）/值（content标示）对的形式现实。属性content，用于定义http-equiv(定义http头部信息，服务器向浏览器提供的信息)和name（指定网页信息的相关的名称）相关的信息；

# http-equiv
http-equiv就是在HTTP头部指定了一些服务器返回给浏览器的有用信息
## content-type	设置页面的字符集	
```html
  ＜meta http-equiv="content-Type" content="text/html; charset=utf-8"＞ 
  //html5页面的做法是直接使用
  <meta charset="utf-8"/>
``` 
## expires	设置页面的过期时间	
```html
＜meta http-equiv="expires" content="Wed, 20 Jun 2007 22:33:00 GMT"/＞
```
## refresh	自动刷新到新页面	
```
＜meta http-equiv="Refresh" content="2；URL=http://www.net.cn/"＞ 
//2代表页面停留多长时间后跳转都后面的网址上
```
## set-cookie	如果cookie过期，则自动删除本地cookie
```	
＜meta http-equiv="Set-Cookie" content="cookievalue=xxx;expires=Wednesday, 20-Jun-2007 22:33:00 GMT； path=/"＞
```
## pragma	禁止浏览器从本地调用缓存	
```
＜meta http-equiv="Pragma" content="no-cache"＞
```
## window-target	强制页面在浏览器窗口独立显示	
```
＜meta http-equiv="Window-target" content="_top"＞
```
## page_enter, page_exit	设定进入页面和退出页面的效果
```
<meta http-equiv="Page-Exit"    content="revealTrans(duration=1.0,transtion= 12)">
```
## cache-control	清除缓存
```	
<meta http-equiv="cache-control" content="no-cache">
```

# name
name把content的内容关联到一个名称上，html和xhtml都没有执行固定的name值，可以自由使用对自己和源文档的读者来说富有意义的名称

　
## name	author	指定页面的所有者	
<meta name="author" content="James Bond"/>

## description	页面描述，用于搜索引擎收录	
<meta name="description" content="中国设计网是中国起步最早的设计门户网站，设计师的网上家园"/>

## keywords	页面关键词，用于被搜索引擎收录	
<meta name="keywords" content="设计, 师妹"/>

## generator	用于说明网站制作生成工具	
<meta name="generator" content="Microsoft"/>

## revised	网页文档的修改时间	
<meta name="revised" content="设计网, 6/24/2015"/>
 	
## viewport	用于控制页面缩放	
<meta name=”viewport” content=”width=240, height=320, user-scalable=yes, initial-scale=2.5, maximum-scale=5.0, minimun-scale=1.0”> //width指定页面的可视宽度, 像素值或device-width, initial-scale设置页面初始化时的缩放比例,user-scalable指定是否可以缩放可视区域, maximum-scale, minimun-scale页面最大最小缩放比例。 如果想要页面在不同的设备都按照页面的设计尺寸缩放（那些宽度固定的网站）就不要使用viewport属性

## copyright	网页版权信息	
<meta name="copyright" name="Copyright 2015 Ironside"/>
 	
## renderer	使用哪种模式显示网页	
<meta name="renderer" content="webkit|ie-comp|ie-stand"> 
webkit标示使用webkit内核打开页面, ie-comp 使用IE兼容模式打开,


# 从功能区分，常用meta标签大总结


## SEO 优化部分
<!-- 页面标题<title>标签(head 头部必须) -->
<title>your title</title>
<!-- 页面关键词 keywords -->
<meta name="keywords" content="your keywords">
<!-- 页面描述内容 description -->
<meta name="description" content="your description">
<!-- 定义网页作者 author -->
<meta name="author" content="author,email address">
<!-- 定义网页搜索引擎索引方式，robotterms 是一组使用英文逗号「,」分割的值，通常有如下几种取值：none，noindex，nofollow，all，index和follow。 -->
<meta name="robots" content="index,follow">


## viewport
viewport主要是影响移动端页面布局的，例如：

<meta name="viewport" content="width=device-width, initial-scale=1.0">

content 参数：
width viewport 宽度(数值/device-width)
height viewport 高度(数值/device-height)
initial-scale 初始缩放比例
maximum-scale 最大缩放比例
minimum-scale 最小缩放比例
user-scalable 是否允许用户缩放(yes/no)

## 各浏览器平台 Microsoft Internet Explorer
<!-- 优先使用最新的ie版本 -->
<meta http-equiv="x-ua-compatible" content="ie=edge">
<!-- 是否开启cleartype显示效果 -->
<meta http-equiv="cleartype" content="on">
<meta name="skype_toolbar" content="skype_toolbar_parser_compatible">
<!-- Pinned Site -->
<!-- IE 10 / Windows 8 -->
<meta name="msapplication-TileImage" content="pinned-tile-144.png">
<meta name="msapplication-TileColor" content="#009900">
<!-- IE 11 / Windows 9.1 -->
<meta name="msapplication-config" content="ieconfig.xml">

## Google Chrome
<!-- 优先使用最新的chrome版本 -->
<meta http-equiv="X-UA-Compatible" content="chrome=1" />
<!-- 禁止自动翻译 -->
<meta name="google" value="notranslate">

## 360浏览器
<!-- 选择使用的浏览器解析内核 -->
<meta name="renderer" content="webkit|ie-comp|ie-stand">

## UC手机浏览器
<!-- 将屏幕锁定在特定的方向 -->
<meta name="screen-orientation" content="landscape/portrait">
<!-- 全屏显示页面 -->
<meta name="full-screen" content="yes">
<!-- 强制图片显示，即使是"text mode" -->
<meta name="imagemode" content="force">
<!-- 应用模式，默认将全屏，禁止长按菜单，禁止手势，标准排版，强制图片显示。 -->
<meta name="browsermode" content="application">
<!-- 禁止夜间模式显示 -->
<meta name="nightmode" content="disable">
<!-- 使用适屏模式显示 -->
<meta name="layoutmode" content="fitscreen">
<!-- 当页面有太多文字时禁止缩放 -->
<meta name="wap-font-scale" content="no">


## QQ手机浏览器
<!-- 锁定屏幕在特定方向 -->
<meta name="x5-orientation" content="landscape/portrait">
<!-- 全屏显示 -->
<meta name="x5-fullscreen" content="true">
<!-- 页面将以应用模式显示 -->
<meta name="x5-page-mode" content="app">

## Apple iOS
<!-- Smart App Banner -->
<meta name="apple-itunes-app" content="app-id=APP_ID,affiliate-data=AFFILIATE_ID,app-argument=SOME_TEXT">
<!-- 禁止自动探测并格式化手机号码 -->
<meta name="format-detection" content="telephone=no">
<!-- Add to Home Screen添加到主屏 -->
<!-- 是否启用 WebApp 全屏模式 -->
<meta name="apple-mobile-web-app-capable" content="yes">
<!-- 设置状态栏的背景颜色,只有在 “apple-mobile-web-app-capable” content=”yes” 时生效 -->
<meta name="apple-mobile-web-app-status-bar-style" content="black">
<!-- 添加到主屏后的标题 -->
<meta name="apple-mobile-web-app-title" content="App Title">

## Google Android
<meta name="theme-color" content="#E64545">
<!-- 添加到主屏 -->
<meta name="mobile-web-app-capable" content="yes">
<!-- More info: https://developer.chrome.com/multidevice/android/installtohomescreen -->

## App Links
<!-- iOS -->
<meta property="al:ios:url" content="applinks://docs">
<meta property="al:ios:app_store_id" content="12345">
<meta property="al:ios:app_name" content="App Links">
<!-- Android -->
<meta property="al:android:url" content="applinks://docs">
<meta property="al:android:app_name" content="App Links">
<meta property="al:android:package" content="org.applinks">
<!-- Web Fallback -->
<meta property="al:web:url" content="http://applinks.org/documentation">
<!-- More info: http://applinks.org/documentation/ -->

## 最后——移动端常用的meta
<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no" />
<meta name="apple-mobile-web-app-capable" content="yes" />
<meta name="apple-mobile-web-app-status-bar-style" content="black" />
<meta name="format-detection"content="telephone=no, email=no" />
<meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no" />
<meta name="apple-mobile-web-app-capable" content="yes" />
<!-- 删除苹果默认的工具栏和菜单栏 -->
<meta name="apple-mobile-web-app-status-bar-style" content="black" />
<!-- 设置苹果工具栏颜色 -->
<meta name="format-detection" content="telphone=no, email=no" />
<!-- 忽略页面中的数字识别为电话，忽略email识别 -->
<!-- 启用360浏览器的极速模式(webkit) -->
<meta name="renderer" content="webkit">
<!-- 避免IE使用兼容模式 -->
<meta http-equiv="X-UA-Compatible" content="IE=edge">

<!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
<meta name="HandheldFriendly" content="true">
<!-- 微软的老式浏览器 -->
<meta name="MobileOptimized" content="320">
<!-- uc强制竖屏 -->
<meta name="screen-orientation" content="portrait">
<!-- QQ强制竖屏 -->
<meta name="x5-orientation" content="portrait">
<!-- UC强制全屏 -->
<meta name="full-screen" content="yes">
<!-- QQ强制全屏 -->
<meta name="x5-fullscreen" content="true">
<!-- UC应用模式 -->
<meta name="browsermode" content="application">
<!-- QQ应用模式 -->
<meta name="x5-page-mode" content="app">
<!-- windows phone 点击无高光 -->
<meta name="msapplication-tap-highlight" content="no">
<!-- 适应移动端end --> 
