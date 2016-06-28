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
#### 4） 内置对象和内置类型
#### 5） Math类型
#### 6） Date类型
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


