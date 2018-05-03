# Common-code
分享前端开发常用代码片段-值得收藏

## 一、预加载图像

如果你的网页中需要使用大量初始不可见的（例如，悬停的）图像，那么可以预加载这些图像。

![预加载图像][1]

## 二、检查图像是否加载

有时为了继续脚本，你可能需要检查图像是否全部加载完毕。

![检查图像是否加载][2]

你也可以使用 ID 或 CLASS 替换 <img>标签来检查某个特定的图像是否被加载。

## 三、自动修复破坏的图像

逐个替换已经破坏的图像链接是非常痛苦的。不过，下面这段简单的代码可以帮助你。

![自动修复破坏的图像][3]

## 四、悬停切换

当用户鼠标悬停在可点击的元素上时，可添加类到元素中，反之则移除类。

![悬停切换][4]

只需要添加必要的 CSS 即可。更简单的方法是使用 **toggleClass()** 方法。

![悬停切换][5]

## 五、淡入淡出/显示隐藏

![淡入淡出/显示隐藏][6]

## 六、鼠标滚轮

```javascript
$('#content').on("mousewheel DOMMouseScroll", function (event) { 
    // chrome & ie || // firefox
    var delta = (event.originalEvent.wheelDelta && (event.originalEvent.wheelDelta > 0 ? 1 : -1)) || 
        (event.originalEvent.detail && (event.originalEvent.detail > 0 ? -1 : 1));  
    
    if (delta > 0) { 
        console.log('mousewheel top');
    } else if (delta < 0) {
        console.log('mousewheel bottom');
    } 
});
```

## 七、鼠标坐标

### 1、JavaScript实现

```html
X:<input id="xxx" type="text" /> Y:<input id="yyy" type="text" />
```


```javascript
function mousePosition(ev){
    if(ev.pageX || ev.pageY){
        return {x:ev.pageX, y:ev.pageY};
    }
    return {
        x:ev.clientX + document.body.scrollLeft - document.body.clientLeft,
        y:ev.clientY + document.body.scrollTop - document.body.clientTop
    };
}

function mouseMove(ev){
    ev = ev || window.event;
    
    var mousePos = mousePosition(ev);
    
    document.getElementById('xxx').value = mousePos.x;
    document.getElementById('yyy').value = mousePos.y;
}
document.onmousemove = mouseMove;
```

### 2、jQuery实现

```javascript
$('#ele').click(function(event){
    //获取鼠标在图片上的坐标 
    console.log('X：' + event.offsetX+'\n Y:' + event.offsetY); 
    
    //获取元素相对于页面的坐标 
    console.log('X：'+$(this).offset().left+'\n Y:'+$(this).offset().top);
});
```

## 八、禁止移动端浏览器页面滚动

### 1、HTML实现

```html
<body ontouchmove="event.preventDefault()" >
```

### 2、JavaScript实现

```javascript
document.addEventListener('touchmove', function(event) {
    event.preventDefault();
});
```

## 九、阻止默认行为

```javascript
// JavaScript
document.getElementById('btn').addEventListener('click', function (event) {
    event = event || window.event；

    if (event.preventDefault){
        // W3C
        event.preventDefault();
    } else{
        // IE
        event.returnValue = false;
    }
}, false);

// jQuery
$('#btn').on('click', function (event) {
    event.preventDefault();
});
```

## 十、阻止冒泡

```javascript
// JavaScript
document.getElementById('btn').addEventListener('click', function (event) {
    event = event || window.event；

    if (event.stopPropagation){
        // W3C
        event.stopPropagation();
    } else{
        // IE
        event.cancelBubble = true;
    }
}, false);

// jQuery
$('#btn').on('click', function (event) {
    event.stopPropagation();
});
```

## 十一、检测浏览器是否支持svg

```javascript
function isSupportSVG() { 
    var SVG_NS = 'http://www.w3.org/2000/svg';
    return !!document.createElementNS &&!!document.createElementNS(SVG_NS, 'svg').createSVGRect; 
} 

console.log(isSupportSVG());
```

## 十二、检测浏览器是否支持canvas

```javascript
function isSupportCanvas() {
    if(document.createElement('canvas').getContext){
        return true;
    }else{
        return false;
    }
}

console.log(isSupportCanvas());
```

## 十三、检测是否是微信浏览器

```javascript
function isWeiXinClient() {
    var ua = navigator.userAgent.toLowerCase(); 
    if (ua.match(/MicroMessenger/i)=="micromessenger") { 
        return true; 
    } else { 
        return false; 
    }
}

alert(isWeiXinClient());
```

## 十四、检测是否移动端及浏览器内核

```javascript
var browser = { 
    versions: function() { 
        var u = navigator.userAgent; 
        return { 
            trident: u.indexOf('Trident') > -1, //IE内核 
            presto: u.indexOf('Presto') > -1, //opera内核 
            webKit: u.indexOf('AppleWebKit') > -1, //苹果、谷歌内核 
            gecko: u.indexOf('Firefox') > -1, //火狐内核Gecko 
            mobile: !!u.match(/AppleWebKit.*Mobile.*/), //是否移动终端 
            ios: !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/), //ios 
            android: u.indexOf('Android') > -1 || u.indexOf('Linux') > -1, //android 
            iPhone: u.indexOf('iPhone') > -1 , //iPhone 
            iPad: u.indexOf('iPad') > -1, //iPad 
            webApp: u.indexOf('Safari') > -1 //Safari 
        }; 
    }
} 

if (browser.versions.mobile() || browser.versions.ios() || browser.versions.android() || browser.versions.iPhone() || browser.versions.iPad()) { 
    alert('移动端'); 
}
```

## 十五、检测是否电脑端/移动端

```javascript
var browser={ 
    versions:function(){
        var u = navigator.userAgent, app = navigator.appVersion;
        var sUserAgent = navigator.userAgent;
        return {
        trident: u.indexOf('Trident') > -1,
        presto: u.indexOf('Presto') > -1, 
        isChrome: u.indexOf("chrome") > -1, 
        isSafari: !u.indexOf("chrome") > -1 && (/webkit|khtml/).test(u),
        isSafari3: !u.indexOf("chrome") > -1 && (/webkit|khtml/).test(u) && u.indexOf('webkit/5') != -1,
        webKit: u.indexOf('AppleWebKit') > -1, 
        gecko: u.indexOf('Gecko') > -1 && u.indexOf('KHTML') == -1,
        mobile: !!u.match(/AppleWebKit.*Mobile.*/), 
        ios: !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/), 
        android: u.indexOf('Android') > -1 || u.indexOf('Linux') > -1,
        iPhone: u.indexOf('iPhone') > -1, 
        iPad: u.indexOf('iPad') > -1,
        iWinPhone: u.indexOf('Windows Phone') > -1
        };
    }()
}
if(browser.versions.mobile || browser.versions.iWinPhone){
    window.location = "http:/www.baidu.com/m/";
} 
```

## 十六、检测浏览器内核

```javascript
function getInternet(){    
    if(navigator.userAgent.indexOf("MSIE")>0) {    
      return "MSIE";       //IE浏览器  
    }  

    if(isFirefox=navigator.userAgent.indexOf("Firefox")>0){    
      return "Firefox";     //Firefox浏览器  
    }  

    if(isSafari=navigator.userAgent.indexOf("Safari")>0) {    
      return "Safari";      //Safan浏览器  
    }  

    if(isCamino=navigator.userAgent.indexOf("Camino")>0){    
      return "Camino";   //Camino浏览器  
    }  
    if(isMozilla=navigator.userAgent.indexOf("Gecko/")>0){    
      return "Gecko";    //Gecko浏览器  
    }    
} 
```

## 十七、强制移动端页面横屏显示

```javascript
$( window ).on( "orientationchange", function( event ) {
    if (event.orientation=='portrait') {
        $('body').css('transform', 'rotate(90deg)');
    } else {
        $('body').css('transform', 'rotate(0deg)');
    }
});
$( window ).orientationchange();
```

## 十八、电脑端页面全屏显示

```javascript
function fullscreen(element) {
    if (element.requestFullscreen) {
        element.requestFullscreen();
    } else if (element.mozRequestFullScreen) {
        element.mozRequestFullScreen();
    } else if (element.webkitRequestFullscreen) {
        element.webkitRequestFullscreen();
    } else if (element.msRequestFullscreen) {
        element.msRequestFullscreen();
    }
}

fullscreen(document.documentElement);
```

## 十九、获得/失去焦点

### 1、JavaScript实现

```html
<input id="i_input" type="text" value='会员卡号/手机号'/>
```

```javascript
// JavaScript
window.onload = function(){
    var oIpt = document.getElementById("i_input");

    if(oIpt.value == "会员卡号/手机号"){
        oIpt.style.color = "#888";
    }else{
        oIpt.style.color = "#000";
    };

    oIpt.onfocus = function(){
        if(this.value == "会员卡号/手机号"){
            this.value="";
            this.style.color = "#000";
            this.type = "password";
        }else{
            this.style.color = "#000";
        }
    };
    
    oIpt.onblur = function(){
        if(this.value == ""){
            this.value="会员卡号/手机号";
            this.style.color = "#888";
            this.type = "text";
        }
    };
}
```


----------

### 2、jQuery实现


```html
<input type="text"  class="oldpsw" id="showPwd" value="请输入您的注册密码"/>
<input type="password" name="psw" class="oldpsw" id="password" value="" style="display:none;"/>
```

```javascript
// jQuery
$("#showPwd").focus(function() {
    var text_value=$(this).val();
    if (text_value =='请输入您的注册密码') {
        $("#showPwd").hide();
        $("#password").show().focus();
    }
});
$("#password").blur(function() {
    var text_value = $(this).val();
    if (text_value == "") {
        $("#showPwd").show();
        $("#password").hide();
    }
}); 
```

## 二十、获取上传文件大小

```html
<input type="file" id="filePath" onchange="getFileSize(this)"/>
```

```javascript
// 兼容IE9低版本
function getFileSize(obj){
    var filesize;
    
    if(obj.files){
        filesize = obj.files[0].size;
    }else{
        try{
            var path,fso; 
            path = document.getElementById('filePath').value;
            fso = new ActiveXObject("Scripting.FileSystemObject"); 
            filesize = fso.GetFile(path).size; 
        }
        catch(e){
            // 在IE9及低版本浏览器，如果不容许ActiveX控件与页面交互，点击了否，就无法获取size
            console.log(e.message); // Automation 服务器不能创建对象
            filesize = 'error'; // 无法获取
        }
    }
    return filesize;
}
```

## 二十一、限制上传文件类型

### 1、高版本浏览器

```html
<input type="file" name="filePath" accept=".jpg,.jpeg,.doc,.docxs,.pdf">
```

### 2、限制图片

```html
<input type="file" class="file" value="上传" accept="image/*"/>
```

### 3、低版本浏览器

```html
<input type="file" id="filePath" onchange="limitTypes()"/>
```

```javascript
/* 通过扩展名，检验文件格式。
 * @parma filePath{string} 文件路径
 * @parma acceptFormat{Array} 允许的文件类型
 * @result 返回值{Boolen}：true or false
 */

function checkFormat(filePath,acceptFormat){
    var resultBool= false,
        ex = filePath.substring(filePath.lastIndexOf('.') + 1);
        ex = ex.toLowerCase();
        
    for(var i = 0; i < acceptFormat.length; i++){
    　　if(acceptFormat[i] == ex){
            resultBool = true;
            break;
    　　}
    }
    return resultBool;
};
        
function limitTypes(){
    var obj = document.getElementById('filePath');
    var path = obj.value;
    var result = checkFormat(path,['bmp','jpg','jpeg','png']);
    
    if(!result){
        alert('上传类型错误，请重新上传');
        obj.value = '';
    }
}
```


## 二十二、正则表达式

```javascript
//验证邮箱 
/^\w+@([0-9a-zA-Z]+[.])+[a-z]{2,4}$/ 

//验证手机号 
/^1[3|5|8|7]\d{9}$/ 

//验证URL 
/^http:\/\/.+\./

//验证身份证号码 
/(^\d{15}$)|(^\d{17}([0-9]|X|x)$)/ 

//匹配字母、数字、中文字符 
/^([A-Za-z0-9]|[\u4e00-\u9fa5])*$/ 

//匹配中文字符
/[\u4e00-\u9fa5]/ 

//匹配双字节字符(包括汉字) 
/[^\x00-\xff]/
```

## 二十三、限制字符数

```html
<input id="txt" type="text">
```

```javascript
//字符串截取
function getByteVal(val, max) {
    var returnValue = '';
    var byteValLen = 0;
    for (var i = 0; i < val.length; i++) { if (val[i].match(/[^\x00-\xff]/ig) != null) byteValLen += 2; else byteValLen += 1; if (byteValLen > max) break;
        returnValue += val[i];
    }
    return returnValue;
}

$('#txt').on('keyup', function () {
    var val = this.value;
    if (val.replace(/[^\x00-\xff]/g, "**").length > 14) {
        this.value = getByteVal(val, 14);
    }
});
```

## 二十四、验证码倒计时

```html
<input id="send" type="button" value="发送验证码">
```

```javascript
// JavaScript
var times = 60, // 时间设置60秒
    timer = null;
            
document.getElementById('send').onclick = function () {
    // 计时开始
    timer = setInterval(function () {
        times--;
        
        if (times <= 0) {
            send.value = '发送验证码';
            clearInterval(timer);
            send.disabled = false;
            times = 60;
        } else {
            send.value = times + '秒后重试';
            send.disabled = true;
        }
    }, 1000);
}
```

```jquery
var times = 60,
    timer = null;

$('#send').on('click', function () {
    var $this = $(this);
    
    // 计时开始
    timer = setInterval(function () {
        times--;
        
        if (times <= 0) {
            $this.val('发送验证码');
            clearInterval(timer);
            $this.attr('disabled', false);
            times = 60;
        } else {
            $this.val(times + '秒后重试');
            $this.attr('disabled', true);
        }
    }, 1000);
});
```

## 二十五、时间倒计时

```html
<p id="_lefttime"></p>
```

```javascript
function countdown() {

    var endtime = new Date("May 2, 2018 21:31:09");
    var nowtime = new Date();

    if (nowtime >= endtime) {
        document.getElementById("_lefttime").innerHTML = "倒计时间结束";
        return;
    }

    var leftsecond = parseInt((endtime.getTime() - nowtime.getTime()) / 1000);
    if (leftsecond < 0) {
        leftsecond = 0;
    }

    __d = parseInt(leftsecond / 3600 / 24);
    __h = parseInt((leftsecond / 3600) % 24);
    __m = parseInt((leftsecond / 60) % 60); 
    __s = parseInt(leftsecond % 60);

    document.getElementById("_lefttime").innerHTML = __d + "天" + __h + "小时" + __m + "分" + __s + "秒";
}

countdown();

setInterval(countdown, 1000);
```

## 二十六、倒计时跳转

```html
<div id="showtimes"></div>
```

```javascript
// 设置倒计时秒数  
var t = 10;  

// 显示倒计时秒数  
function showTime(){  
    t -= 1;  
    document.getElementById('showtimes').innerHTML= t;  

    if(t==0){  
        location.href='error404.asp';  
    }  

    //每秒执行一次 showTime()  
    setTimeout("showTime()",1000);  
}  

showTime();
```

## 二十七、时间戳、毫秒格式化

```javascript
function formatDate(now) { 
    var y = now.getFullYear();
    var m = now.getMonth() + 1; // 注意 JavaScript 月份+1 
    var d = now.getDate();
    var h = now.getHours(); 
    var m = now.getMinutes(); 
    var s = now.getSeconds();
    
    return y + "-" + m + "-" + d + " " + h + ":" + m + ":" + s; 
} 

var nowDate = new Date(1442978789184);

alert(formatDate(nowDate));
```

## 二十八、当前日期

```javascript
var calculateDate = function(){

    var date = new Date();
    var weeks = ["日","一","二","三","四","五","六"];

    return date.getFullYear()+"年"+(date.getMonth()+1)+"月"+
    date.getDate()+"日 星期"+weeks[date.getDay()];
}

$(function(){
    $("#dateSpan").html(calculateDate());
});
```

## 二十九、判断周六/周日

```html
<p id="text"></p>
```

```javascript
function time(y,m){
    var tempTime = new Date(y,m,0);
    var time = new Date();
    var saturday = new Array();
    var sunday = new Array();
    
    for(var i=1;i<=tempTime.getDate();i++){
        time.setFullYear(y,m-1,i);
        
        var day = time.getDay();
        
        if(day == 6){
            saturday.push(i);
        }else if(day == 0){
            sunday.push(i);
        }
    }
    
    var text = y+"年"+m+"月份"+"<br />"
                +"周六："+saturday.toString()+"<br />"
                +"周日："+sunday.toString();
                
    document.getElementById("text").innerHTML = text;
}
 
time(2018,5);
```

## 三十、AJAX调用错误处理

当 Ajax 调用返回 404 或 500 错误时，就执行错误处理程序。如果没有定义处理程序，其他的 jQuery 代码或会就此罢工。定义一个全局的 Ajax 错误处理程序

![AJAX调用错误处理][7]

## 三十一、链式插件调用

jQuery 允许“链式”插件的方法调用，以减轻反复查询 DOM 并创建多个 jQuery 对象的过程。

![链式插件调用][8]

通过使用链式，可以改善

![链式插件调用][9]

还有一种方法是在（**前缀$**）变量中高速缓存元素

![链式插件调用][10]

链式和高速缓存的方法都是 jQuery 中可以让代码变得更短和更快的最佳做法。

[阅读更多][11]

参考文章 [『总结』web前端开发常用代码整理][12]


  [1]: https://segmentfault.com/img/bV9GOl?w=630&h=179
  [2]: https://segmentfault.com/img/bV9GOp?w=461&h=77
  [3]: https://segmentfault.com/img/bV9GOJ?w=787&h=127
  [4]: https://segmentfault.com/img/bV9LXp?w=370&h=129
  [5]: https://segmentfault.com/img/bV9MaN?w=367&h=78
  [6]: https://segmentfault.com/img/bV9M2B?w=380&h=201
  [7]: https://segmentfault.com/img/bV9M44?w=643&h=78
  [8]: https://segmentfault.com/img/bV9M5r?w=271&h=77
  [9]: https://segmentfault.com/img/bV9M5E?w=159&h=102
  [10]: https://segmentfault.com/img/bV9M50?w=259&h=98
  [11]: https://segmentfault.com/u/webing123
  [12]: https://segmentfault.com/a/1190000011087315#articleHeader21
