### 事件
- JS是以事件驱动为核心的一门语言。  
js是采用事件驱动(event-driven)响应用户操作的。比如通过鼠标或者按键在浏览器窗口或者网页元素(按钮，文本框...)上执行的操作，我们称之为事件(Event),由鼠标或热键引发的一连串程序的动作，称之为事件驱动(Event-Driver)。对事件进行处理程序或函数，我们称之为事件处理程序(Event Handler)。
- 事件三要素
- 事件源 , 事件 , 事件驱动程序
- 事件源: 要触发的对象 , (一般是名词 , 事件发起者)
- 事件: 怎么触发这个事情 , (一般是动词 , 触发事件)
- 事件驱动程序: 发生了什么事情 , (处理结果)
- JS做什么 :  获取事件源 ===> 绑定时间 ===> 书写事件驱动程序

### DOM
- HTML DOM是HTML Document Object Model(文档对象模型)的缩写 , 可以将DOM理解为网页的API , 她将网页中的各个元素都看作一个个对象 , 从而使网页中的元素也可以被JS获取或者编辑 , JavaScript就可以利用DOM动态的修改网页
- DOM将文档解析为一个由节点和对象(包含属性和方法的对象)组成的结构集合 , 是web页面的完全面向对象表述 , 它将web页面和脚本程序语言连接起来 , 它能够使用如JavaScript等脚本语言进项修改
- DOM 是载入到浏览器中的文档模型，以节点树的形式来表现文档，每个节点代表文档的构成部分（例如:页面元素、字符串或注释等等）
- 在HTML当中一切都是节点
- 每一个HMTL标签都是一个元素节点（标签）
- 标签中的文字则是文字节点。（文本）
- 标签的属性是属性节点。（属性）

### DOM节点的获取
- 要想操作节点(标签) , 必须先找到该元素 , 有三种方法
- **document.getElementById( );**
- 通过 ID , 最准确的 , 需要获取的DOM元素 ,  必须要有ID , 而且一个页面不能由重复的ID
- **document.getElementsByTagName( );**
- 通过标签(元素) , 效率低 , 没办法定位元素
- **document.getElementsByClassName**
- 通过类名 , 在移动端浏览器完全支持 , 但是在**IE5,6,7,8无效**

### 获取节点
- DOM的节点并不是孤立的 , 因此可以通过DOM节点之间的相对关系对它们进行访问
- 节点的访问关系 , 是以属性的方式存在的

#### 父节点 parentNode
- 调用者就是节点 , 一个节点只有一个父节点 , 调用方式是: **节点.parentNode**

#### 兄弟节点
- nextSibling :调用者是节点 , **存在浏览器兼容问题**
>在IE 6,7,8中指下一个元素节点(包括标签和注释)  
在高级浏览器中指下一个元素节点(包括空文档和换行符)
- nextElementSibling
>在高级浏览器中指的是下一个元素节点
- 兼容写法
```
    var nextEl = xxx.nextElementSibling || xxx.nextSibling;
```

- previousSibling
>在IE 6,7,8中指上一个元素节点(包括标签和注释)   
在高级浏览器中指上一个元素节点(包括空文档和换行符)
- previousElementSibling
>在高级浏览器中指的是上一个元素节点
- 兼容写法
```
    var nextEl = xxx.previousElementSibling || xxx.previousSibling;
```

#### 孩子节点
- firstChild
>在IE 6,7,8 : 第一个子元素节点(标签)  
高级浏览器 :第一个子元素节点(包括空文档和注释)
- firstElementChild
>高级浏览器:第一个子元素节点(标签)

- lastChild
>IE6,7,8 :最后一个子元素节点(标签)  
高级浏览器:最后一个节点(包括空文档,注释)
-lastElementChild
>高级浏览器:最后一个元素节点(标签)
- 兼容写法
```
    var lastChild = xxx.lastElementChild || xxx.lastChild;
```
#### 所有子节点

- hildNodes IE6,7,8 包括换行,注释  
children 高级浏览器 只包括元素节点 ,但是在IE6,7,8中包含注释节点  
所以之前的兼容方法不可用  
需要自己封装方法

- nodeType  ==  1 元素节点  
- nodeType  ==  2 属性节点   
- nodeType  ==  3 文本节点   
- nodeType  ==  8 注释  

```
    function myChildren(el) {
		var children = el.children;
		var myChildrenArr = [];
		for (var i = 0; i < children.length; i++) {
			// 如何判断他是注释节点还是元素节点
			// nodeType = 8 注释
			// nodeType = 1 节点
			// nodeType = 3 文本
			if(children[i].nodeType === 1){
				myChildrenArr.push(childreb[i]);
			}
		}
		return myChildrenArr;
	}
	var ulElchildren = myChildren(ulEl);
```

#### 除了自己以外所有的兄弟节点
```
        <ul class="ul">
			<li>li_1</li>
			<li class="li2">li_2</li>
			<!-- 这依旧是一条正经的注释 -->
			<li>li_3</li>
			<li>li_4</li>
			<li>li_5</li>
		</ul>
		
		<script>
			// 获取 li2 所有的兄弟节点
			
			
			// 方式一
			// 获取 li2 的父节点====>获取所有的子节点====>再把 li2 筛出来
			var li2 = document.getElementsByClassName('li2')[0];
			console.log(getSiblings(li2));
			// 封装方法
			function getSiblings(el) {
				var siblings = []; // 创建一个空数组用来接收不是 li2 的其他节点
				var pNode = el.parentNode; // 找到父节点
				var children = pNode.children; // 通过父节点找到所有子节点
				// 遍历所有子节点
				for (var i = 0; i < children.length; i++) {
					// 兼容
					if (children[i].nodeType === 1){
						// 遍历到不是 li2 的时候, 就push进数组
						if (children[i] !== el) {
							siblings.push(children[i])
						}
					}
				}
				return siblings; // 返回新的数组(没有li2)
			}
			
			// 方式二
			// 锁的思想
			function getNextSiblings(el) {
				var pNode = el.parentNode;
				var children = pNode.children;
				var siblings = [];
				var lock = false;
				for (var i = 0; i < children.length; i++){
					if (children[i].nodeType === 1) {
						if (children[i] === el) {
							lock = true;
						}else {
							if (lock) {
								siblings.push(children[i])
							}
						}
					}
				}
				return siblings;
			}
			console.log(getNextSiblings(li2));
		</script>
```

#### 操作节点
```
        <div class="box">
			一个盒子
		</div>
		<div class="btn">添加图片</div>
		<div class="btn2">删除图片</div>
		<div class="btn3">克隆节点</div>
		<script>
			var btn = document.getElementsByClassName('btn')[0];
			var btn2 = document.getElementsByClassName('btn2')[0];
			var btn3 = document.getElementsByClassName('btn3')[0];
			var box = document.getElementsByClassName('box')[0];
			// 把节点填到页面当中
			// 先创建节点
			var imgEl = document.createElement('img');// 创建标签节点
			var pEl = document.createElement('p');
			imgEl.src = 'img/a.jpg';
			// 节点需要添加才会出现在页面
			btn.onclick = function () {
				// 插入节点(使用节点)
				// 使用方法:父节点.appendChild();
				box.appendChild(imgEl);
				// 同一个节点只能添加一次
				// 使用方法: 父节点.insertBrfore(要插入的节点,参考节点)
				box.insertBefore(pEl, imgEl);
				// 如果参考节点为 null 那么它将在节点最后插入一个节点
			};
			
			btn2.onclick = function () {
				//删除节点
				// box.removeChild(imgel);
				// 不知道父节点的情况下 可以这样写
				imgEl.parentNode.removeChild(imgEl);
			};
			
			// oldNode.cloneNode(true)
			// 想要复制的节点调用这个函数cloneNode() , 得到一个新节点
			// 方法内部可以传参 , true是深层复制(内容也会复制) , false只复制节点
			btn3.onclick = function () {
				var boxClone = box.cloneNode(true);
				document.body.appendChild(boxClone);
			};
		</script>
```

#### 节点属性
- 获取：getAttribute(名称)
- 设置：setAttribute(名称, 值)
- 删除：removeAttribute(名称)
```
     <h1 id="h1" class="title danger">嘤嘤嘤</h1>
     
	var h1El = document.getElementsByTagName('h1')[0];
	console.log(h1El.getAttribute('class')); // 获取class属性
	console.log(h1El.getAttribute('id')); // 获取id属性

	h1El.setAttribute('id', 'new'); // 把之前的所有属性替换掉了
	h1El.removeAttribute('id'); // 把id属性删除了
```
#### 内容操作
- Value 只对表单有效 , 是属性
- 插入文本内容===> xxx.innerText
- 插入标签===> xxx.innerHTML
```
            var inputEl = document.getElementsByTagName('input')[0];
			var btn = document.getElementsByClassName('btn')[0];
			var btn2 = document.getElementsByClassName('btn2')[0];
			var btn3 = document.getElementsByClassName('btn3')[0];
			
			var boxEl = document.getElementsByClassName('box')[0];
			btn.onclick = function() {
				inputEl.value = Math.floor(Math.random() * 10);
			}
			
			//插入文本内容
			btn2.onclick = function () {
				boxEl.innerText = '今天天气超级热';
				boxEl.innerText = '<p></p>';
				// 当做了文本处理,并没有解析为标签
				// 而且每一次 innerText 都会替换掉 box 里面之前的所有内容
			}
			
			// 插入标签
			btn3.onclick = function () {
				boxEl.innerHTML = '<p>嘤嘤嘤嘤</p>';
				// 解析成了标签
				// 每一次 innerHTML 都会替换掉 box 里面之前的所有内容
				// 可以动态生成页面
			}
```

