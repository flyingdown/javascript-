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

+ Math类型封装了所有有关数学计算的方法，Math类型不能new
+ Math.round(num); 四舍五入，返回一个Number类型
+ Math.ceil(num); 向上取整
+ Math.floor(num); 向下取整
+ Math.pow(x,y); x的y次方
+ Math.sqrt(num); num的平方根
+ Math.abs(num); num的绝对值
+ Math.max(v1,v2...); 最大值
+ Math.min(v1,v2...); 最小值
        
#### 7） Error类型

+ 错误或异常是导致程序运行停止的运行时异常状态，错误处理就是在出现异常状态时，保证程序不停止运行的机制
        
+ Error类是所有错误对象的父类
        
+ ECMAScript定义了六种子类型的错误：

	- EvalError
	- RangeError，参数范围错误，比如Number类型的toFixed方法的参数超出[0,20]范围时，就会产生此类异常
        - ReferenceError，引用错误，找不到对象，只要使用未声明的变量都抛出此类异常
        - SyntaxError，语法错误，抛出此类异常
        - TypeError，错误的使用类型和类型的方法，就会抛出此类异常，比如调用String类型的toFixed方法
        - URIError，URI错误

+ 如何处理错误：

		try {
			//可能出错的代码
		} catch ( err ) {
			//错误处理的代码
			1.获得错误信息：err.message
			2.获得错误类型：err.name        
		} finally {
			//最后执行的代码
		}
        
+ 主动抛出异常：throw

		throw new Error("自定义错误信息");

#### 8）Function类型

+ JavaScript中方法也是一个对象，方法名就是指向方法的变量名

		function f(a,b) { return a-b; } 
		相当于：
		var f = new Function("a", "b", "return a-b" );
        	// 在js解释器加载脚本时，会优先加载var声明变量和function声明的语句，所以function定义的函数，可以放置在任意位置，程序都能找到其声明

+ 以声明方式定义方法：

        function 方法名（参数列表） 
        { 
        	方法体； 
        	return 返回值
        }; // 只有声明的方式定义才会被提前解析
        
+ 以创建对象方式定义方法：

        var 方法名 = new Function("参数1", ..., "方法体; return 返回值" ) // 最后一个参数是方法体
        
+ 以匿名函数赋值的方式定义方法：

        var 方法名 = function () 
        { 
        	return 返回值 
        };

+ 重载：方法根据传入的参数列表不同，调用不同的方法

> arguments对象是在方法对象中，保存所有参数的类数组对象(object like array)，其中arguments的length属性保存传入参数的个数，arguments的类数组保存传入的参数，可以用下标访问，如arguments[0]访问第一个参数，arguments[i]访问第i个参数

+ 匿名函数的2个用途：

> 1.回调函数：函数何时执行，程序猿不需要控制，由所在环境自动调用执行
>	应用：比较器、事件处理函数

> 2.自调函数：匿名函数自己调用自己
>	应用：当函数不需要重复使用时，直接使用匿名函数自调

	- 语法：
	
		(function(参数列表) { 函数体 })(实参)
            	(funciton () 
		{
			//代码
		})();

#### 9）Object类型
+ 一切对象的父对象，所有的对象都是从该对象继承来的
+ 创建对象的方式
	- 方式一
	
			var obj = new Object(); // 对象原型是Object.prototype;
			obj.name = 'zhangsan'; // 通过动态方式来增加属性
			obj.name = function () { }; // 通过动态方式来增加方法
	
	- 方式二

			var obj = {}; // json语法,对象原型是Object.prototype

	- 方式三

			function Emp() {}; var obj = new Emp(); // 对象原型是Emp.prototype;
			// 当原型在内部有return this;时，可以省略new关键字。

	- 方式四

			var obj = Object.create(proto);
		
+ prototype属性

> 具有同一个类型的对象，都引用一个相同的隐藏的prototype对象，从而共享相同的方法属性，同样我们可以通过这个属性动态的给对象增加属性和方法。
> 继承的实现可以使用Object.setPrototypeOf ( chlid, parent )，关联连个对象，并设置父子关系

+ 基于原型的对象创建和继承

> 任何一个js对象都有一个原型对象，即它的父对象；所有js对象的最终父对象都是Object.prototype，而Object.prototype的父对象是null，null没有父对象。

#### 10）Global类型

用来收集一些公用函数，如parseInt()之类的函数

### 3. JavaScript运算


#### 1） 关系运算

和C语言的关系运算大致相同，具体可以查看手册，这里只说下需要注意的地方

> 关系运算比较中，所有和number比较的都自动转换为number，而在"+"运算中，所有和str加运算的都自动转换为str
> NaN从类型上看是number类型
> undefined是从null继承过来的，用来表示基本类型的未定义，null用来表示对象的未定义，所以undefined==null为true，而undefined===null为false
> isNaN（X）；// X是数字或者在关系运算中能自动转换为数字则返回false，不是数字的返回true，此函数只判断值，不判断类型
> unicode中汉字的范围 >='\u4E00' && <='\u9FA5'

#### 2） 逻辑运算

请自行查看手册

### 4. JavaScript闭包

#### 1） 作用域和作用域链

1. JavaScript首先会维护一个作用域范围，即定义变量时，作用域范围已经确定。
2. 程序运行时，再根据作用域范围来创建对象。先创建一个window对象，用来存放全局变量
3. 当调用某个方法时，会产生三个对象，第一个是方法的运行环境对象（上下文对象）指向作用域链对象，第二个是方法的活动对象，用来存放这个方法的局部变量，第三个时作用域链对象，维护一个表格，从0开始，依次指向此方法可以调用的对象资源
4. 调用方法会从作用域链的0索引开始查找所需要的变量，找到即停止寻找

#### 2） 全局变量和局部变量

+ 全局变量时在window对象中的变量；局部变量只有两种，一种是函数的形参，一种是函数内部定义的变量。JavaScript并没有块及的作用域，只有函数级作用域：变量在声明它们的函数体及其子函数内是可见的。

#### 3）  闭包（感觉类似于面向对象语言中的私有变量和其set/get方法）

> 一个对象指向并可以使用一个不属于自己的局部变量，则其所在的作用域就形成了闭包

	- 闭包的三个特点：
        	* 1.局部变量
		* 2.内嵌函数
		* 3.外部使用

+ 例子：

		var getValue, setValue;
		(
			function ()
			 {
				var secret = 0;
				getValue = function () 
				{
					return secret;
				};

				setValue = function (v)
				{
					secret = v;
				}
			}
		)()
		
+ 是不是被上面所说的搞晕了，其实弄明白了JavaScript的内部机制，才能真正理解闭包的原理

> JavaScript是解释性语言，其实，每当负责解释脚本的控制器到达ECMAScript可执行代码的时候，控制器就进入了一个执行上下文(execute context)

> javascript中，EC(execute context)分为三种：

> - 全局级别的代码 – 这个是默认的代码运行环境，一旦代码被载入，引擎最先进入的就是这个环境。
> - 函数级别的代码 – 当执行一个函数时，运行函数体中的代码。
> - Eval的代码 – 在Eval函数内运行的代码。

> EC建立分为两个阶段：进入执行上下文和执行阶段。
> - 1.进入上下文阶段：发生在函数调用时，但是在执行具体代码之前（比如，对函数参数进行具体化之前）
> - 2.执行代码阶段：变量赋值，函数引用，执行其他代码。
> 我们可以将EC看做是一个对象。

		EC={
    			VO:{/* 函数中的arguments对象, 参数, 内部的变量以及函数声明 */},
			this:{},
			Scope:{ /* VO以及所有父执行上下文中的VO */}
		}
		
> VO|AO

> VO

> 每一个EC都对应一个变量对象VO，在该EC中定义的所有变量和函数都存放在其对应的VO中。
> VO分为全局上下文VO（全局对象，Global object，我们通常说的global对象）和函数上下文的AO。

		VO: {
  			// 上下文中的数据 (变量声明（var）, 函数声明（FD), 函数形参（function arguments）)
		}

>> 1. 进入执行上下文时，VO的初始化过程具体如下：
>> 函数的形参（当进入函数执行上下文时）
>> —— 变量对象的一个属性，其属性名就是形参的名字，其值就是实参的值；对于没有传递的参数，其值为undefined

>> 函数声明（FunctionDeclaration, FD） ——变量对象的一个属性，其属性名和值都是函数对象创建出来的；如果变量对象已经包含了相同名字的属性，则替换它的值

>> 变量声明（var，VariableDeclaration） —— 变量对象的一个属性，其属性名即为变量名，其值为undefined;如果变量名和已经声明的函数名或者函数的参数名相同，则不会影响已经存在的属性。

>> 注意：该过程是有先后顺序的。

>> 2. 执行代码阶段时，VO中的一些属性undefined值将会确定。


> AO

> 在函数的执行上下文中，VO是不能直接访问的。它主要扮演被称作活跃对象（activation object）（简称：AO）的角色。
> 这句话怎么理解呢，就是当EC环境为函数时，我们访问的是AO，而不是VO。

		VO(functionContext) === AO;
> AO是在进入函数的执行上下文时创建的，并为该对象初始化一个arguments属性，该属性的值为Arguments对象。

		AO = {
  			arguments: {
    				callee:,
    				length:,
    				properties-indexes: //函数传参参数值
  			}
		};
		
> FD的形式只能是如下这样：

		functionf(){

		}
		
+ 示例

		VO示例：
		alert(x); // functionvar x = 10;
		alert(x); // 10

		x = 20;

		functionx() {};

		alert(x); // 20

	进入执行上下文时
	
		ECObject={
  			VO:{
    				x:<referencetoFunctionDeclaration "x">
  			}
		};
		
	执行代码时：
	
		ECObject={
  			VO:{
    				x:20//与函数x同名，替换掉，先是10，后变成20
  			}
		};
		
	对于以上的过程，我们详细解释下。
	在进入上下文的时候，VO会被填充函数声明； 同一阶段，还有变量声明“x”，但是，正如此前提到的，变量声明是在函数声明和函数形参之后，并且，变量声明不会对已经存在的同样名字的函数声明和函数形参发生冲突。因此，在进入上下文的阶段，VO填充为如下形式：

		VO = {};

		VO['x'] = <引用了函数声明'x'>

		// 发现var x = 10;
		// 如果函数“x”还未定义
		// 则 "x" 为undefined, 但是，在我们的例子中
		// 变量声明并不会影响同名的函数值

		VO['x'] = <值不受影响，仍是函数>
		
	执行代码阶段，VO被修改如下：
	
		VO['x'] = 10;
		VO['x'] = 20;
		
	如下例子再次看到在进入上下文阶段，变量存储在VO中（因此，尽管else的代码块永远都不会执行到，而“b”却仍然在VO中）
	
		if (true) {
  			var a = 1;
		} else {
  			var b = 2;
		}

		alert(a); // 1
		alert(b); // undefined, but not "b is not defined"


		AO示例：
		functiontest(a, b) {
  			var c = 10;
  			functiond() {}
  			var e = function_e() {};
  			(functionx() {});
		}

		test(10); // call

	当进入test(10)的执行上下文时，它的AO为：
	
		testEC={
			AO:{
				arguments:{
					callee:test
					length:1,
					0:10
				},
			a:10,
			c:undefined,
			d:<referencetoFunctionDeclaration "d">,
			e:undefined
			}
		};
		
	由此可见，在建立阶段，VO除了arguments，函数的声明，以及参数被赋予了具体的属性值，其它的变量属性默认的都是undefined。函数表达式不会对VO造成影响，因此，(function x() {})并不会存在于VO中。
	当执行test(10)时，它的AO为：
	
		testEC={
			AO:{
				arguments:{
					callee:test,
					length:1,
					0:10
				},
				a:10,
				c:10,
				d:<referencetoFunctionDeclaration "d">,
				e:<referencetoFunctionDeclaration "e">
			}
		};
		
	可见，只有在这个阶段，变量属性才会被赋具体的值。
	
	作用域链

	> 在执行上下文的作用域中查找变量的过程被称为标识符解析(indentifier resolution)，这个过程的实现依赖于函数内部另一个同执行上下文相关联的对象——作用域链。作用域链是一个有序链表，其包含着用以告诉JavaScript解析器一个标识符到底关联着哪一个变量的对象。而每一个执行上下文都有其自己的作用域链Scope。
	> 一句话：作用域链Scope其实就是对执行上下文EC中的变量对象VO|AO有序访问的链表。能按顺序访问到VO|AO，就能访问到其中存放的变量和函数的定义。
	
	Scope定义如下：
	
		Scope = AO|VO + [[Scope]]
	其中，AO始终在Scope的最前端，不然为啥叫活跃对象呢。即：
	
		Scope = [AO].concat([[Scope]]);
	这说明了，作用域链是在函数创建时就已经有了。而在代码执行时，控制器会根据作用域链来寻找变量，这就是闭包的原理。
		
+ 总结：
	1. EC分为两个阶段，进入执行上下文和执行代码。
	2. ECStack管理EC的压栈和出栈。
	3. 每个EC对应一个作用域链Scope，VO|AO（AO，VO只能有一个），this。
	4. 函数EC中的Scope在进入函数EC时创建，用来有序访问该EC对象AO中的变量和函数。
	5. 函数EC中的AO在进入函数EC时，确定了Arguments对象的属性；在执行函数EC时，其它变量属性具体化。
	6. 函数的[[scope]]属性在函数创建时就已经确定，并保持不变。

作用域链、执行上下文、函数声明的先后顺序为：EC-->arguments-->[[Scope]]-->形参实例化-->函数声明-->变量实例化-->this
而this创建遵循5个规则：

	- 1.Regular function (myFunction(1,2,3)). The value of this points to the global object (i.e. window).普通函数调用，this等于window
	- 2.Object method (myObject.myFunction(1,2,3)). The value of this points to the object containing the function (i.e. the object before the dot). The value is myObjectin our example.作为对象方法调用，this等于对象
	- 3.Callback for setTimeout() or setInterval(). The value of this points to the global object (i.e. window).作为回调函数，this等于window
	- 4.Callback for call() or apply(). The value of this is the first argument ofcall()/apply().call和apply会指定this的值，this等于call和apply的第一个参数
	- 5.As constructor (new myFunction(1,2,3)). The value of this is an empty object withmyFunction.prototype as prototype.作为构造函数，this等于要创建的对象，其原型是构造函数的prototype属性。

由此也可以确定this的作用于是在调用时确定的，而不是的定义时。




#### 4） ECMAScript5中属性的分类

+ 数据属性（Data Property）
+ 访问器属性（accerssor Property）

		var obj = {
			get 属性名() {
                    		return 属性值；    
			},
			set 属性名(value) {
                    		//TODO...
			}
		}
> 注意：访问器属性的本质是两个函数，若读取访问属性的值，会自动调用get访问器；若为访问器属性赋值，会自动调用set访问器，并把等号右边的值作为参数传入。
> 1. 访问器属性不能存储数据，所以访问器属性的值要依赖于一个数据属性来存储数据
> 2. 访问器属性一般用于两个场合：用于冗余属性和有意控制数据的读写属性。

#### 5） ECMAScript5中新添内容：属性(property)的特性(attribute)

+ 属性：对象中可以保存数据的变量，包括数据属性和访问器属性
	- 属性的特性：包括数据属性的特性和访问器属性的特性
		数据属性的特性：value，保存其值
				writeable，是否可写
				enumerable，是否可枚举（是否能用for...in列举属性和Object.keys()操作）
				configurable，属性的特性是否可以被修改

                用Object.defineProperty添加属性，并描述其特性
                Object.defineProperty (
                    obj, //对象名
                    "property", //属性名
                    { //特性描述符对象
                        value:99, 
                        writable:true, 
                        enumerable:true, 
                        configurable:true
                    }
                );
                
		访问器属性的特性：get，保存其get访问器
				set，保存其set访问器
				enumerable，同上
				configurable，同上
				
		同样用Object.defineProperty添加属性，并描述其特性
		
                Object.defineProperty (
                    obj, // 属性名
                    "property", // 访问器属性名
                    { // 特性描述符对象
                        get : function () {},
                        set : function () {},
                        enumerable : true,
                        configurable : true
                    }
                )

### 5. JavaScript DOM


#### 1） 核心DOM
+ 当前主流的动态web开发技术
    
> 动态：网页的内容，可以在不同的时间、针对不同的客户呈现出不同的内容。
    JSP = HTML + JAVA
    ASPX = HTML + C#
    PHP = HTML + PHT
    
+ DHTML

> Dynamic HTML，动态HTML、动态网页，值得是页面表现、样式是可以随着用户的操作而发生不同的变化。DHTML = HTML + CSS + JAVASCRIPT，DHTML是把已经存在的三项技术整合起来进行组合应用，就是使用JavaScript来增删改查HTML元素和CSS样式，最终使得页面呈现一个更友好的交互效果。
> DHTML对象：

> 1. BOM : window/hsitory/location/document/navigtor/screen/event
	用于JavaScript脚本与浏览器进行交互

> 2. DOM：所有的HTML元素都是一个DOM对象
	用于JavaScript脚本与当前显示的HTML文档进行交互

							              window
		_____________________________________________________________________________________________________________________________
		|                       |                              |                         |                    |                     |
		history               navigator                   document                   location              screen                 event
		                                                       |
		_______________________________________________________________________________________________________________
		|                            |                  |                              |                               |
		iframe                       anchor              image                         form                           table
		                                                                               |                               |
		                                                                    ________________________              TableCell
		                                                                    |          |           |                   |
		                                                                   input     select      Textarea          TableRow
    - DOM树
    
	* DOM元素树：以document对象为根，每个HTML标签都是元素树的一个节点
	
		parentElementNode // Node类型，当前节点的唯一父节点对象
		children // NodeList类型，当前节点的所有子节点，组成一个类数组对象
		firstElementChild // Node类型，当前节点的第一个子节点
		lastElementChild // Node类型，当前节点的最后一个子节点
		previousElementSibling // Node类型，当前节点的上一个兄弟节点
		nextElementSibling // Node类型，当前节点的下一个兄弟节点

		* DOM节点树：以document对象为根，每个标签、文本、属性、注释都是一个节点树的一个节点。
		
		parentNode：Node类型，当前节点的唯一父节点对象
		childNodes：NodeList类型，当前节点的所有子节点，组成一个类数组对象
		firstChild：Node类型，当前节点的第一个子节点
		lastChild：Node类型，当前节点的最后一个子节点
		nextSibling：Node类型，当前节点的下一个兄弟节点
		previousSibling：Node类型，当前节点的上一个兄弟节点

	* Node类型的常用属性
		
		innerHTML // 获取html内容
		textContent // 获取纯文本内容
		innerText // 获取纯文本内容
		parentNode
		childNodes
		attributes 	// NamedNodeMap类型（一个类数组对象，有lenght属性，可以用下表访问其元素）
				// element.attributes[下标].value
				// element.attributes['属性名']
				// element.getAttributeNode('属性名').value
				// element.getAttributeNode('属性名')

	* Node类型的常用方法
		
		getElementById() // 普通的元素节点没有这个方法
		getElementsByName() // 普通的元素节点没有这个方法
		getElementsByTagName()
		getElementsByClassName()
		appenChild()
		removeChild()
		replaceChild()
		insertBefore()
		createAttribute()
		createElement()
		createTextNode()
		getAttribute()
		setAttribute('属性名', '属性值') // IE8一下不支持，可以用element.setAttributeNode(attr)代替
		removeAttribute('属性名')
		hasAttribute('属性名') // 判断某元素是否有这个属性，返回true或false

		

### 6. JavaScript BOM


