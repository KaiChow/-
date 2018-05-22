背景:移动端的物理屏幕尺寸不同，要在不同分辨率的屏幕根据设计师的设计图比例，前端展示页面随屏幕大小而改变
首先要了解的重要的基础知识点：物理像素，设备独立像素，设备像素比，css像素，像素密度，布局视口，可视视口,理想视口以及css单位px、em、rem、%、vw、wh、vm。
物理像素（设备像素）：设备能控制的最小单位，可以理解为显示器上一个个小点，常用的1920*1080分辨率就是最小单位表示的
设备独立像素（DIP，device-independent pixel，density-independent pixel）：也叫密度无关像素，独立于设备的用于逻辑的衡量像素的单位，可以理解为虚拟像素，程序使用并控制的虚拟像素（其中也包括css像素）
物理像素和独立像素关系：因此在PC端分辨率等于设备的独立像素，可以通过screen.width/height获取，但是在移动端同样的方法获取，得到的设备独立像素并不等于设备的分辨率，例如iphone5s测试的，screen.height=568，screen.width=320，无论在竖屏还是在横屏都一样！所以在一定的条件下，两者是相等的，比如在PC端独立像素可以物理像素是相等的，在移动端不相等！
像素密度（ppi）：pixel per inch,每英寸的像素数点（物理像素），PPI的值越高，画质越好，也就是越细腻。




Css像素（Css pixel）：适用web编程的逻辑像素，抽象概念，单位px，（注意：pc端物理像素代表是1px，在移动端不一定，高清屏）
设备像素比（dpr）：dpr= 物理像素/设备独立像素（在某一方向，x或者y），你可以通过JavaScript 中的window.devicePixelRatio来获取设备中的像素比值。Iphone 5s 使用的是 Retina 视网膜屏幕，什么是Retina视网膜屏幕？PPI 值超过 300 的叫做超高密度屏幕，只是 Apple 给它换了个高大尚的名称：Retina 视网膜屏幕而已。在做移动页面开发的时候，相信你经常会遇到这种情况：不同的手机上看时，里面的图片、文字或者线的大小会不一样，有时候大小区别还非常地大。原因就是刚才说到的设备像素比在作怪。你想啊，如果在普通屏即标准 PPI下一个设备光点对应一个 CSS 像素时，页面不大不小，完美地渲染出来了。但在现在这个高逼格的年代，标准 PPI 已经很少见了。更多的是 Retina视网膜设备。而设备像素比不同的品牌的手机这个值也是不一样的。即使是同一个品牌的手机也不一样。你比如 Iphone 5s 设备像素比为2，Iphone 6s 设备像素比为3。至于安卓机中的设备像素比就更多了，有1.3、1.5、2、3等等
当设备像素比为1:1时，使用1（1×1）个设备像素显示1个CSS像素；
当设备像素比为2:1时，使用4（2×2）个设备像素显示1个CSS像素；
当设备像素比为3:1时，使用9（3×3）个设备像素显示1个CSS像素。

<meta name="viewport" content="width=device-width, initial-scale=1, minimum-scale=1, maximum-scale=1, user-scalable=no">


viewport 视口：以下为属性
width：控制 viewport 的大小，你可以给它指定一个值，如：600，或者甚至还可以给它一个特殊的值，如：device-width，device-width为设备的宽度（单位为缩放为 100% 时的 CSS 的像素）。
height：与 width 相对应，指定viewport 高度。
initial-scale：初始缩放比例，也即是当页面第一次 load 的时候缩放比例。
maximum-scale：允许用户缩放到的最大比例。
minimum-scale：允许用户缩放到的最小比例。
user-scalable：是否允许用户手动缩放。
视觉视窗：设备的屏幕区域，换句话说就是用户通过屏幕所看到的页面内容。但它所对应的并不是指屏幕区域里的物理像素，而是CSS 像素。并且它所包含的 CSS 像素的数量也是随着用户缩放而有所改变。我们可以通过window.innerWidth | window.innerHeight来获得视觉视窗对应的宽和高，


布局视窗（layout viewport）：可以看作是html元素的上一级容器即顶级容器，默认情况或者将html元素的width属性设为100%时，会占满这个顶级容器，此时用document.documentElement.clientWidth 获取到html元素的布局宽度也就是布局视口的宽度，使用媒体查询时 max-width 和 min-width 的值指的也是布局视口的宽。布局视窗跟视觉视窗不一样，它不是指设备屏幕区域，它是为了解决PC 端网站在移动端显示不佳的一个解决方案。布局视窗通常比设备屏幕宽得多，一般为980px，但也不是唯一，在不同的浏览器中也会有所不同如：在Safari iPhone中布局视窗的宽为980px，在Opera中布局视窗宽为850px ，在Android WebKit 中而已视窗宽为800px，而在万恶的IE中布局视窗宽为974px。
注意：布局视窗的宽高值是在页面没添加viewport 时所获得的值。如果你给页面添加了viewport 并且 设置了width = device-width 时，通过上面的代码所获得的值就不是布局视窗的默认值了。在html中一般在meta中的name为viewport字段就是控制的布局视口。布局视口一般都是浏览器厂商给的一个值。在手机互联网没有普及前，网络上绝大部分页面都是为电脑端浏览而做的，根本没有做移动端的适配。
随着移动端的发展，在手机上看电脑端的页面已成为非常普及现象。而电脑端页面宽度较大，移动端宽度有限，要想看到整个网页，会有很长的滚动条，看起来非常麻烦。于是浏览器厂商为了让用户在小屏幕下网页也能够显示地很好，所以把布局视口设置的很大，一般在768px ~ 1024px 之间，最常用的宽度就是 980。
这样用户就能看到绝大部分内容，并根据具体内容选择缩放。
故布局视口是看不见的，浏览器厂商设置的一个固定值，如980px，并将980px的内容缩放到手机屏内。一块手机屏幕，物理像素的数量是固定不变的。


理想视窗：这个理想视窗是为了布局视窗而生的，为什么这么说，因为它是基于布局视窗的。布局视口虽然解决了移动端查看pc端网页的问题，但是完全忽略了手机本身的尺寸。所以苹果引入了理想视口，它对设备来说是最理想的布局视口，用户不需要对页面进行缩放就能完美的显示整个页面。最简单的做法就是使布局视口宽度设置为手机屏幕的宽度。移动端到底怎么适配不同的屏幕呢？最简单的方法是设置如下视口：
<meta name="viewport" content="width=device-width,initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no">,复习一下： dpr = 物理像素 / 设备独立像素。
以iphone6为例，iphone6的物理像素为750，如果没有设置布局视口时，布局视口viewport默认为980px
此时：dpr = 750 / 980 = 0.76531，等于1个CSS像素有0.76531个物理像素。接近于1像素密度所以pc端的页面在手机端看时不会太小。
当在meta中设置了如下配置时:
<meta name="viewport" content="width=device-width">
相当于把布局视口设置为设备的宽度(即设备独立像素)，
iphone6的设备独立像素为 375px。
此时：dpr = 750 / 375 = 2，等于1个CSS像素有2个物理像素。此时把pc端的尺寸拿来手机端看时字体和元素会特别大只。
现在移动端设计稿都是基于iphone设计的，一般为750px或640px，对应的是iphone6和iphone5的物理像素。在设计稿中，1px像素边框对应的是1物理像素。而在iphone5和iphone6中，当布局视口width=device-width时，css的1px显示出来的是2个物理像素，所以用户看到的是2px的边框。怎么解决呢？1px边框效果其实有很多hack方法，其中一种就是通过缩放viewport。
<meta name="viewport" content="width=device-width,initial-scale=0.5, maximum-scale=0.5, minimum-scale=0.5, user-scalable=no"> 

web开发单位：

1、px
px就是pixel的缩写，意为像素。px就是一张图片最小的一个点，一张位图就是千千万万的这样的点构成的，比如常常听到的电脑像素是1024x768的，表示的是水平方向是1024个像素点，垂直方向是768个像素点。
2、em
参考物是父元素的font-size，具有继承的特点。如果自身定义了font-size按自身来计算（浏览器默认字体是16px），整个页面内1em不是一个固定的值。
3、rem
css3新单位，相对于根元素html（网页）的font-size，不会像em那样，依赖于父元素的字体大小，而造成混乱。
4、%
一般宽泛的讲是相对于父元素，但是并不是十分准确。
1、对于普通定位元素就是我们理解的父元素
2、对于position: absolute;的元素是相对于已定位的父元素
3、对于position: fixed;的元素是相对于ViewPort（可视窗口）
5、vw
css3新单位，viewpoint width的缩写，视窗宽度，1vw等于视窗宽度的1%。
举个例子：浏览器宽度1200px, 1 vw = 1200px/100 = 12 px。
6、vh
css3新单位，viewpoint height的缩写，视窗高度，1vh等于视窗高度的1%。
举个例子：浏览器高度900px, 1 vh = 900px/100 = 9 px。
7、vm
css3新单位，相对于视口的宽度或高度中较小的那个。其中最小的那个被均分为100单位的vm
举个例子：浏览器高度900px，宽度1200px，取最小的浏览器高度，1 vm = 900px/100 = 9 px。
由于现在vm的兼容性较差

实际的解决问题的场景：
vh vw是不包含页面滚动条的视窗宽度(innerwidth)，%包含了滚动条的宽度在里面了(outerwidth)。
一般的情况下%就可以满足大部分自适应设计的需求，可以用height：100vh做一个高度占满屏幕的自适应，没有滚动条。
用vw，vh设定的大小只和视窗大小有关，所以用来开发多种屏幕设备的应用用这个单位还是挺合适的。


多种适配方案探究

1，固定高度，使其宽度自适应
这个方案使用了理想视口,使得布局视口等于设备宽度。
<meta name="viewport" content="width=device-width,initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no">
在布局方面纵向使用固定px值,横向使用自适应布局(百分比，felx，小额定值)。
这种方案相对简单，ui还原度比较低。

2，固定布局视口宽度，使用viewport进行缩放
固定布局视口，宽度设置固定的值，总宽度为640px，根据屏幕宽度动态生成viewport。（设计稿宽度为640px）
这种布局方案页面宽度始终为640px通过设置缩放比例scale实现适配:
var scale = window.screen.width / 640;
当设计稿为640px时，我们可以直接用1：1px来写像素单位。这种布局方案中的1px不一定等于1px，当设备为iphone6时
1px(css) = window.screen.widthdpr = 640 = 375 2 / 640 = 1.171875(设备物理像素)

3，根据不同屏幕动态写入font-size，以rem作为宽度单位，固定布局视口
首先设置理想视口:
<meta name="viewport" content="width=device-width,initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no">
接下来计算 html 元素的 font-size,将可视视口的宽度乘以一个系数: 750px 是设计稿的宽度（以iphone6的物理像素数为标准），100是期望的换算比例，即设计稿中 100px 的长度对应css中 1rem，将设计稿中的长度数值除以 100 得到的就是以 rem 为单位的 css 长度的数值，设计稿的宽换算为以 rem 为单位的 css 长度应为 (750/100) rem，同时设计稿的宽对应可视视口的宽，即有 (750/100) rem = 可视视口宽，1 rem = 可视视口宽 * (100/750)，(100/750)就是我们要的系数
在页面初始化时设置一下 html 元素的 font-size:
在750宽的设计稿：document.documentElement.style.fontSize = window.innerWidth / 7.5 + 'px';
在640宽的设计稿：document.documentElement.style.fontSize = window.innerWidth / 7.5 + 'px';
这套方案能百分百还原设计稿。

4，根据不同屏幕动态写入font-size和viewport，以rem作为宽度单位.
  将屏幕分为固定的块数10：
var width = document.documentElement.clientWidth; // 屏幕的布局视口宽度
var rem = width / 10; // 将布局视口分为10份
这样在任何屏幕下，总长度都为10rem。1rem对应的值也不固定，与屏幕的布局视口宽度有关。
var devicePixelRatio = window.devicePixelRatio;
var isIPhone = window.navigator.appVersion.match(/iphone/gi);
var dpr,scale;
if (isIPhone) {
  if (devicePixelRatio >=3) {
    dpr = 3;
  } else if (devicePixelRatio >=2) {
    dpr = 2;
  } else {
    dpr = 1;
  }
} else {
  dpr = 1;
}
scale = 1 / dpr;
淘宝只对iphone做了缩放处理，对于android所有dpr=1，scale=1即没有缩放处理。
此方案与方案三相似，增进了viewport缩放使得在iphone上1px(css) = 1px(物理像素)，这套方案能百分百还原设计稿。


两种解决方案分析
网易的方案：
先拿设计稿竖着的横向分辨率除以100得到body元素的宽度：
如果设计稿基于iphone6，横向分辨率为750，body的width为750 / 100 = 7.5rem
如果设计稿基于iphone4/5，横向分辨率为640，body的width为640 / 100 = 6.4rem
布局时，设计图标注的尺寸除以100得到css中的尺寸
在dom ready以后，通过以下代码设置html的font-size:
document.documentElement.style.fontSize = document.documentElement.clientWidth / 6.4 + 'px';
font-size可能需要额外的媒介查询，并且font-size不能使用rem 
@media screen and (max-width:321px){
    .m-navlist{font-size:15px}
}

@media screen and (min-width:321px) and (max-width:400px){
    .m-navlist{font-size:16px}
}

@media screen and (min-width:400px){
    .m-navlist{font-size:18px}
}

情况说明：
如果采用网易这种做法，视口要如下设置：
<meta name="viewport" content="initial-scale=1,maximum-scale=1, minimum-scale=1"
当deviceWidth大于设计稿的横向分辨率时，html的font-size始终等于横向分辨率/body元素宽：
var deviceWidth = document.documentElement.clientWidth;
if(deviceWidth > 640) deviceWidth = 640;
document.documentElement.style.fontSize = deviceWidth / 6.4 + 'px';
淘宝的解决方案：
动态设置viewport的scale
var scale = 1 / devicePixelRatio;
document.querySelector('meta[name="viewport"]').setAttribute('content','initial-scale=' + scale + ', maximum-scale=' + scale + ', minimum-scale=' + scale + ', user-scalable=no');
动态计算html的font-size
document.documentElement.style.fontSize = document.documentElement.clientWidth / 10 + 'px';
布局的时候，各元素的css尺寸=设计稿标注尺寸/设计稿横向分辨率/10
font-size可能需要额外的媒介查询，并且font-size不使用rem，这一点跟网易是一样的。
最后还有一个情况要说明，跟网易一样，淘宝也设置了一个临界点，当设备竖着时横向物理分辨率大于1080时，html的font-size就不会变化了，原因也是一样的，分辨率已经可以去访问电脑版页面了。


flexible的实质
flexible实际上就是能过JS来动态改写meta标签，代码类似这样：
动态改写<meta>标签
给<html>元素添加data-dpr属性，并且动态改写data-dpr的值
给<html>元素添加font-size属性，并且动态改写font-size的值
!function(a,b){function c(){var b=f.getBoundingClientRect().width;b/i>540&&(b=540*i);var c=b/10;f.style.fontSize=c+"px",k.rem=a.rem=c}var d,e=a.document,f=e.documentElement,g=e.querySelector('meta[name="viewport"]'),h=e.querySelector('meta[name="flexible"]'),i=0,j=0,k=b.flexible||(b.flexible={});if(g){console.warn("将根据已有的meta标签来设置缩放比例");var l=g.getAttribute("content").match(/initial\-scale=([\d\.]+)/);l&&(j=parseFloat(l[1]),i=parseInt(1/j))}else if(h){var m=h.getAttribute("content");if(m){var n=m.match(/initial\-dpr=([\d\.]+)/),o=m.match(/maximum\-dpr=([\d\.]+)/);n&&(i=parseFloat(n[1]),j=parseFloat((1/i).toFixed(2))),o&&(i=parseFloat(o[1]),j=parseFloat((1/i).toFixed(2)))}}if(!i&&!j){var p=a.navigator.userAgent,q=(!!p.match(/android/gi),!!p.match(/iphone/gi)),r=q&&!!p.match(/OS 9_3/),s=a.devicePixelRatio;i=q&&!r?s>=3&&(!i||i>=3)?3:s>=2&&(!i||i>=2)?2:1:1,j=1/i}if(f.setAttribute("data-dpr",i),!g)if(g=e.createElement("meta"),g.setAttribute("name","viewport"),g.setAttribute("content","initial-scale="+j+", maximum-scale="+j+", minimum-scale="+j+", user-scalable=no"),f.firstElementChild)f.firstElementChild.appendChild(g);else{var t=e.createElement("div");t.appendChild(g),e.write(t.innerHTML)}a.addEventListener("resize",function(){clearTimeout(d),d=setTimeout(c,300)},!1),a.addEventListener("pageshow",function(a){a.persisted&&(clearTimeout(d),d=setTimeout(c,300))},!1),"complete"===e.readyState?e.body.style.fontSize=12*i+"px":e.addEventListener("DOMContentLoaded",function(){e.body.style.fontSize=12*i+"px"},!1),c(),k.dpr=a.dpr=i,k.refreshRem=c,k.rem2px=function(a){var b=parseFloat(a)*this.rem;return"string"==typeof a&&a.match(/rem$/)&&(b+="px"),b},k.px2rem=function(a){var b=parseFloat(a)/this.rem;return"string"==typeof a&&a.match(/px$/)&&(b+="rem"),b}}(window,window.lib||(window.lib={}));

在设置font-size的时候可以使用rem作为单位；整体与px有关的都设置为rem，使用atom转化，基础设置为75，







