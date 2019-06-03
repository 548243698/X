#JQeury
---
- JQeury是 JS 对 DOM 操作的一个封装,我们可以通过使用jQuery快速简单的操作dom元素.
- JQeury使用之前一定要先引入 引入 引入 ! ! !
- 有两个版本,**压缩版**和**非压缩版(开发板)**
	>在开发中一般使用开发版(可以查看源码)
- 如果使用了第三方jquery插件（日历、滚动、瀑布流等），必须先引入jquery，再引入该插件。
- JQuery的两个变量: $ 和 jQuery 
- <script src="jquery-3.4.1.min.js></script>		该标签如果用来引包，里面不允许写任何js语句！
##冲突问题

- 当有其他框架中使用 $ 造成冲突的时候有两种办法
1.  释放$的使用权: **jQuery.noConflict();**
2.  自定义一个访问符号: **var xxx = jQuery.noConflict();**
 	>  注意点:释放操作必须在编写其他的jQuery代码之前编写,释放之后就不能再使用 $ ,改为使用jQuery或自定义的访问符号
##入口函数
- $() 或 jQuery() 称之为JQ选择器环境，在里面加上引号 ' ' 填写相关选择器即可，就可以获取匹配的元素。
 1.	两者功能都一致，都可以让获取元素的行为发生在渲染元素之后；
 2.	JS入口只允许存在一个，书写多个的话，后面的会覆盖前面的；
 3.	JQ入口允许存在多个，且并行存在，都会生效；
 4.	JS入口需要等待页面上所有资源加载完毕，而JQ入口只需要等待页面上标签渲染完毕即可，JQ入口速度更快。
#####演示
	<script src="../js/jquery-3.3.1.min.js"></script>

	<script> 
	// JS 页面加载完成
    window.onload = function () {
        alert("test1");
    }
 
    window.onload = function () {
        alert("test2");
    }
 
    // $ 符号就是 jquery 的简写方式.
    // 复杂书写 : 
    $(document).ready(function () {
        alert("test3");
    });
 
    // 简化书写
    $(function () {
        alert("test4");
    })
	</script>
##选择器
###回顾CSS基本选择器
- ID选择器---( #id )
	>\#id{xxxxx}
- 类选择器---( .class )
	>.class{xxx}
- 标签选择器
	>P{xxx}
- 通配符选择器---( * )
	>配合其它选择器来使用
- 并集选择器---( , )
	>div,p{}
- 后代选择器---( (空格))
	>div span{}   选择div下面所有后代的span标签
###jQuery基本选择器
- $('#xxxx')
	>选择id为xxxx的第一个元素
	>>$('#demo').css('background','red')
- $('.d1')
	>选择所有类名（样式名）为dl的元素
	>>$('.d1').css('background','red')
- $('div')
	>选择所有标签名为div的元素
	>>$('div').css('background','red')
- $('*')
	>选择所有元素
	>>$('*').css('background','red')
- $('.xxx.xxx-1')
	>选择多个指定的元素
	>>$('.xxx.xxx-1').css('background','red')
###层级选择器
 ![我是图片](../img/1.png)
###过滤选择器
 ![我是图片](../img/2.png)
###属性选择器
 ![我是图片](../img/4.png)
###筛选选择器
 ![我是图片](../img/3.png)
##事件

- JS：js对象.onclick = function(){...}
- JQ：jquery对象.click(function(){...})
- 注意：jq中的事件类型统一不要加on

#####演示
- 注意 : JS 的代码都是写在 = 后面. 
-  jquery 的代码基本上都是写在 () 里面.
-  jquery 入口函数 :
- $(function () {})

######JS代码
	<script src="../js/jquery-3.3.1.min.js"></script>`
	<script>
        	// JS 代码 :
        var btn = document.getElementById("btn");
        btn.onclick = function () {
            alert("按钮被点击了...");
       	});
	</script>
######JQ代码
	<script src="../js/jquery-3.3.1.min.js"></script>
	<script>
        	// jquery 代码 :
       	 $("#btn").click(function () {
            alert("按钮被点击了...");
         });
	</script>


