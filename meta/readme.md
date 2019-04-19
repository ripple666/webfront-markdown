# meta知识点详解

## http-equiv
##### Expires(期限) 
可以用于设定网页的到期时间。一旦网页过期，必须到服务器上重新传输。
	＜meta http-equiv="expires" content="Wed, 20 Jun 2007 22:33:00 GMT"＞  
 
##### Pragma(cache模式) 
是用于设定禁止浏览器从本地机的缓存中调阅页面内容，设定后一旦离开网页就无法从Cache中再调出 
    ＜meta http-equiv="Pragma" content="no-cache"＞  

##### Refresh(刷新) 
自动刷新并指向新页面。 
	＜meta http-equiv="Refresh" content="2；URL=http://www.net.cn/"＞  

##### Set-Cookie(cookie设定)
如果网页过期，那么存盘的cookie将被删除。
	＜meta http-equiv="Set-Cookie" content="cookievalue=xxx;expires=Wednesday, 20-Jun-2007 22:33:00 GMT； path=/"＞ 

##### Window-target(显示窗口的设定) 
强制页面在当前窗口以独立页面显示。 
	＜meta http-equiv="Window-target" content="_top"＞   

##### content-Type(显示字符集的设定) 
设定页面使用的字符集。 
	＜meta http-equiv="content-Type" content="text/html; charset=gb2312"＞  

##### Pics-label(网页等级评定) 
在IE的internet选项中有一项内容设置，可以防止浏览一些受限制的网站，而网站的限制级别就是通过meta属性来设置的。 
	<meta http-equiv="Pics-label" content=""> 
 
##### Page_Enter、Page_Exit 
设定进入页面时的特殊效果
	<meta http-equiv="Page-Enter"    content="revealTrans(duration=1.0,transtion=    12)">    

##### cache-control
设定离开页面时的特殊效果
	<meta http-equiv="Page-Exit"    content="revealTrans(duration=1.0,transtion=    12)">    

##### expires
设定网页的到期时间 
	<meta http-equiv="expires" content="0">  

##### keywords
关键字,给搜索引擎用的 
	<meta http-equiv="keywords" content="keyword1,keyword2,keyword3">  

##### description
页面描述 
	<meta http-equiv="description" content="This is my page">  