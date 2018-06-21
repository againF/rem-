# REM适配实践
作者：吴业飞
时间：2018.06.21


---
## js动态修改html的font-size
因为所有页面都要使用`rem`适配，所以修改`html`的`font-size`的代码应该写在`Global.js`中然后在`layout.html`中将`Global.js`引入
		
	//get viewport
	var htmlWidth = document.documentElement.clientWidth || document.body.clientWidth;
	console.log("htmlWidth is " + htmlWidth);
	//get html dom
	var htmlDom = document.getElementsByTagName('html')[0];
	
	//set html fontsize，here 116.125 = htmlWidth/16,16 is html default font-size
	htmlDom.style.fontSize = htmlWidth /116.125 + 'px';
	
	window.addEventListener('resize', function(){
	    var htmlWidth = document.documentElement.clientWidth || document.body.clientWidth;
	    htmlDom.style.fontSize = htmlWidth /116.125 + 'px';
	})
	/*use rem end */
## 定义px到rem的转换函数
我们使用`sass`，新建一个`pxToRem.scss`文件，内容为

	//A function help you change px to rem
	@function pxToRem($px) {
		$rem: 16px;
		@return ($px / $rem) + rem;
	}
然后在需要使用这个函数的`scss`文件中使用`@import 'pxToRem.scss';`引入
## 使用起来像这样

	.banner-title {
	    font-size: pxToRem(96px);
	    line-height: pxToRem(96px);
	    margin-bottom: pxToRem(270px);
	}
## 最后别忘了将scss编译成css

---

版权声明：自由转载-非商用-非衍生-保持署名
