**目录**：

>笔记持续更新，原地址: https://github.com/Niefee/Wangyi-Note ;

<ul>
<li><a href="#基本语法">基本语法</a><ul>
<li><a href="#语法重点">语法重点</a></li>
<li><a href="#变量标识符">变量标识符</a></li>
<li><a href="#关键字和保留字">关键字和保留字</a></li>
<li><a href="#大小写敏感">大小写敏感</a></li>
<li><a href="#严格模式">严格模式</a></li>
<li><a href="#注释">注释</a></li>
</ul>
</li>
</ul>

#基本语法
##语法重点
![Alt text](img/1433815776559.png)
##变量标识符
![Alt text](img/1433815905401.png)
##关键字和保留字
![Alt text](img/1433815968721.png)
>保留字(Reserved Words)一般是等同于关键字(Keywords)的。
从字面含义上理解，保留字是语言中已经定义过的字，使用者不能再将这些字作为变量名或过程名使用。而关键字则指在语言中有特定含义，成为语法中一部分的那些字。在一些语言中，一些保留字可能并没有应用于当前的语法中，这就成了保留字与关键字的区别。一般出现这种情况可能是由于考虑扩展性。例如，Javascript有一些未来保留字，如abstract、double、goto等等。它可能未来要增加直接跳转的功能，那么为了使当前版本的程序代码能向后兼容，所以不允许使用goto作为变量名，但当前版本的语言并不支持goto的直接跳转功能，它目前就不是关键字。

##大小写敏感
![Alt text](img/1433816032663.png)
>arr跟Arr的涵义不一样。
>**For**是错误，正确的是**for**。


##严格模式
![Alt text](img/1433816243116.png)
 - 区别
	 - 隐式声明或定义变量
	![Alt text](img/1433816323718.png)
	![Alt text](img/1433816416083.png)
	 - 对象重名的属性
	![Alt text](img/1433816595667.png)
	![Alt text](img/1433816617971.png)

	 - arguments.callee
	
	
	![Alt text](img/1433816675556.png)
	![Alt text](img/1433816697359.png)

	 - with语句

	![Alt text](img/1433816738776.png)
	![Alt text](img/1433816756811.png)
##注释
![Alt text](img/1433816870135.png)





