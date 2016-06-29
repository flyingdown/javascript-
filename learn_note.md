### 1. JavaScript基础

#### 1） JavaScript简介
网景公司开发的一种用于与页面进行交互的脚本语言，所以JavaScript程序在浏览器端执 行，通常JavaScript写在扩展名为js的文件中。
主要作用：
+ 前端验证，通过对用户提交的表单中的数据进行验证，若验证不通过，则浏览器不会将数据提交给服务器。
+ ajax核心技术之一，用于异步向服务器发送请求并动态更新页面。
+ 与页面进行交互，生成动态效果。
+ 获得浏览器相关的信息。


#### 2） JavaScript的组成部分
+ ECMAScript，主要内容为语法基础，其内容已经标准化
+ DOM（document object modole）文档对象模型，其内容只有部分标准化
+ BOM（browser object modole）浏览器对象模型，没有标准化，但大部分浏览器都支持window，location，history，screen等对象

### 2. JavaScript数据类型


#### 1）  数据类型总结
- 值类型 ( number、string、boolean )
- 特殊类型 （undefined、null）
- 引用类型
  * 原生对象----ECMAScript标准定义 ( String Number Boolean Array Date Math Error Function Object Global )
  * 宿主对象----W3C组织定义 ( 所有的DOM对象和BOM对象 )
  * 自定义对象

#### 2） String类型
+ length属性，返回字符串的长度
+ charAt(index)方法，返回index指定位置的字符，下标从0开始
+ charCodeAt(index)方法，返回inxdex指定位置的字符的unicode码
+ slice(start[,end])方法，返回[start,end)子字符串，下标从0开始，参数支持负数
+ substring(from[, to]);方法，返回[from, to)子字符串，下标从0开始，参数不支持负数
+ substr(start[,count]);方法，返回从start开始count个字符的字符串
+ indexOf(str[,from=0]);方法，从from位置开始查找，返回字符串在原字符串中第一次出现的位置
+ lastIndexOf(str[,from=0]);方法，从from位置开始查找，返回字符串在原字符串最后一次出现的位置
+ match(reg);方法，返回匹配指定正则表达式的字符串，返回的结构是一个数组
+ replace(regexp,newstr);方法，替换匹配reg指定的字符串为newstr，返回替换后的字符串
+ toLowerCase/toUpperCase方法，返回小写/大写
+ search(reg);方法，返回匹配reg的字符串的下表
+ split(reg [,count]);方法，以字符串中str为分隔，返回前count个数组
+ trim();方法，去除字符串开始和结尾的空格。
+ String.fromCharCode(code);方法，类方法，将code对应unicode码转换为其对应的str

+ 在开发中，由于JavaScript没有提供其它语言常用的trim函数和isspace函数，需要自己开发一个

		function myTrim(str) 
		{
			reg = /(^\s+)|(\s+$)/g; // 这里用到了正则表达式，在后面章节会介绍到
	    	return str.replace(reg,"");
		}

+ 自定义isspace方法

		function isEmpty(str) 
    	{
        	if ( str === undefined )
            	return true;
        	else if ( str == null )
            	return true;
        	else 
        	{
            	reg = /^\s+$/;
            	return reg.test(str);
        	}
    	}



#### 3） Number类型

+ num.toFixed(n); 按照n为小数四舍五入，返回一个字符串
+ num.toString(n); 按照n进制输出数字的字符串

#### 4） Array类型

+ length属性返回数组的长度
+ toString()方法，返回数组的字符串表示
+ concat()方法，用于连接两个数组，不修改原数组
+ join()方法，用于将数组中的各元素连接成字符串
+ reverse()方法，用于将数组反转，直接修改原数组
+ slice(index1,index2)方法，用于截取数组的一部分，并以数组的形式返回，截取下标index1到index2的部分，左闭右开区间
+ splice(index,count)方法，从index位置开始删除count个元素，直接修改原数组
+ splice(index,count,val1,val2...),从index位置开始将count个元素替换为val1，val2,...；count为0时，即将val1,,val2...插入到index位置后，其返回值为被删除的元素

+ 数组可以当做堆栈和队列来使用
	- push(); // 从后面压入
	- pop(); // 从后面弹出，返回弹出的元素
	- unshift();//从前面压入
	- shift(); // 从前面弹出，返回弹出的元素

#### 5） Date类型

具体API可以查看手册，这里只提供一个具体例子来感受Date类型

+ Date常用方法

		// 封装一个时间点数据，提供对时间、日期的常用API
		var date = new Date(); // 创建了一个Date类型的对象，并且获取当前时间点

		// 自定义时间
		var date = new Date("2016/4/4 18:01"); // 创建了一个Date类型的对象，并用输入的时间初始化
		var date = new Date(毫秒数);

+ API：可以用三句话总结

	- 每个时间分量（年月日时分秒）都有一对get/set方法，获取/设置该分量的值
	- 命名：年/月/日 没有s，时/分/秒 有s
	- 除了日之外，其余的都是从0开始计数，日从1开始计数

		date.toLocaleString(); // 获得日期和时间的本地格式
		date.toLocaleDateString(); // 仅获得日期部分的本地格式
		date.toLocaleTimeString(); // 仅获得时间部分的本地格式
	
	以上三种方法，在不同浏览器上输出的格式不同，所以一般会自定义一个函数用来格式化时间。
	
		function timeFormat ( date ) 
		{
			var week = [  '日', '一', '二', '三', '四', '五', '六' ] ;
			var year = date.getFullYear()+"年";
			var month = date.getMonth()+"月";
			var day = date.getDate() + "日";
			var wk = "星期"+week[date.getDay()];

			var hours =  date.getHours();
			var flag =hours<=12?"上午":"下午";
			h = h>12?h-12:h;
			h = h<10?"0"+h:""+h;

			var  mins = date.getMinutes();
			mins = mins < 10 ? "0"+mins : ""+mins;

			var secs = date.getSeconds();
			secs = secs < 10 ? "0"+secs : "" + secs;

			return year + month + day + " " + hours + ":" + mins + ":" + secs;

		}

#### 6） Math类型
#### 7） Error类型

### 3. JavaScript运算


#### 1） 关系运算
#### 2） 逻辑运算

### 4. JavaScript闭包


#### 1） 作用域和作用域链
#### 2） 全局变量和局部变量
#### 3）  闭包
#### 4） ECMAScript5中属性的分类
#### 5） ECMAScript5中新添内容：属性(property)的特性(attribute)

### 5. JavaScript DOM


#### 1） 核心DOM
    - 当前主流的动态web开发技术
    - DHTML
    - DOM树

### 6. JavaScript BOM


