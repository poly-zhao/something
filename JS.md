#### 1. 浏览器提供的对象

JavaScript可以获取浏览器提供的很多对象，并进行操作。

1. `window`

   `window`对象不但充当全局作用域，而且表示浏览器窗口。
   `window`对象有`innerWidth`和`innerHeight`属性，可以获取浏览器窗口的内部宽度和高度。
   `outerWidth`和`outerHeight`属性，可以获取浏览器窗口的整个宽高。

2. `navigator`
   `navigator`对象表示浏览器的信息.

       navigator.appName：浏览器名称；
       navigator.appVersion：浏览器版本；
       navigator.language：浏览器设置的语言；
       navigator.platform：操作系统类型；
       navigator.userAgent：浏览器设定的User-Agent字符串。

3. `screen`
   `screen`对象表示屏幕的信息，常用的属性有：

       screen.width：屏幕宽度，以像素为单位；
       screen.height：屏幕高度，以像素为单位；
       screen.colorDepth：返回颜色位数，如8、16、24。

4. `location`
   `location`对象表示当前页面的URL信息。例如，一个完整的URL：

   ```js
   //完整的URL
   location.href   http://www.example.com:8080/path/index.html?a=1&b=2#TOP   
   //获得URL各个部分的值
   location.protocol; // 'http'
   location.host; // 'www.example.com'
   location.port; // '8080'
   location.pathname; // '/path/index.html'
   location.search; // '?a=1&b=2'
   location.hash; // 'TOP'
   ```

5. `document`
   `document`对象表示当前页面。由于HTML在浏览器中以DOM形式表示为树形结构，`document`对象就是整个DOM树的根节点。
   用`document`对象提供的`getElementById()`和`getElementsByTagName()`可以按ID获得一个DOM节点和按Tag名称获得一组DOM节点
   `document.cookie`读取到当前页面的Cookie



#### 2 `for...in`和`for...of`区别

1. 推荐在循环对象属性的时候，使用`for...in`,在遍历数组的时候的时候使用`for...of`。
2. `for...in`循环出的是key，`for...of`循环出的是value
3. 注意，`for...of`是ES6新引入的特性。修复了ES5引入的`for...in`的不足

```javascript
//ES5引入的for...in的不足
let aArray = ['a',123,{a:'1',b:'2'}]
aArray.name = 'demo';
for(let index in aArray){
    console.log(aArray[index]); //Notice!!aArray.name也被循环出来了
}
for(var value of aArray){
    console.log(value);
}
```

#### 3 使用`.`和`[ ]` 获取对象属性

访问对象的属性和方法：

1. 以 对象.属性 访问，例如：p.name
2. 以 对象["属性"]  访问，例如：p["name"]	      //注意 需要**使用字符串**

#### 4. 类属性,对象属性,局部变量

1)        局部变量：在函数中以普通方式声明的变量，包括以var或不加任何前缀声明的变量。
2)        实例属性：在函数中以this前缀修饰的变量
3)        类属性：在函数中以函数名前缀修饰的变量

```javascript
// 定义函数Person
function Person(national, age)
{
    // this修饰的变量为实例属性
    this.age = age;
    // Person修饰的变量为类属性. 可以通过 类名.national访问
    Person.national =national;
    // 以var定义的变量为局部变量. 外部不能访问
    var bb = 0;
}
```

#### 5. Object.create()

构造函数作为模板，可以生成实例对象。但是，有时拿不到构造函数，只能拿到一个现有的对象。我们希望以这个现有的对象作为模板，生成新的实例对象，这时就可以使用`Object.create()`方法。

```javascript
  var car = {
      speed:100,
      drive:function(){
          console.log("rolling in the deep");
      }
  }  

  var truck = Object.create(car)
  console.log(car.speed);		//100
  console.log(truck.speed);		//100
  car.drive();					//rolling in the deep
  truck.drive();				//rolling in the deep
  console.log(car);				//Object {speed: 100, drive: }
  console.log(truck);			//Object {}
  
  console.log(truck === car);	//false
  console.log(truck == car);	//false
```

**不知道为什么直接打印truck时输出没有带自己的成员**. 

`truck`继承了`car`的属性和方法, `car`是`truck`的模板.

#### 6. this关键字

`this`就是属性或方法“当前”所在的对象。它指向(代表)一个对象。

1. `this`用在构造函数之中，表示实例对象。

   ```javascript
   var Vehicle = function (){
     this.price = 1000;	
   };
   //this表示通过new Vehicle()创建的实例对象
   //在严格模式下直接调用Vehicle()会报错
   ```

2. `this`的指向是可变的。由于对象的属性(变量和方法)可以赋给另一个对象，所以属性所在的当前对象是可变的

   ```js
   function f() {
     return '姓名：'+ this.name;
   }
   
   var A = {
     name: '张三',
     describe: f
   };
   
   var B = {
     name: '李四',
     describe: f
   };
   //f()内的this会指向调用的f的对象
   A.describe() // "姓名：张三"
   B.describe() // "姓名：李四"
   ```

   JavaScript 语言之中，一切皆对象，运行环境也是对象，所以函数都是在某个对象之中运行，`this`就是函数运行时所在的对象（环境）。

**实质:** 

JavaScript中函数单独保存在内存中. 当函数被赋值给成员属性时, 这个属性会指向函数的内存地址.
JavaScript 允许在函数体内部，引用当前环境的其他变量。
由于函数可以在不同的运行环境执行，所以需要有一种机制，能够在函数体内部获得当前的运行环境（context）。所以，`this`就出现了，它的设计目的就是在函数体内部，指代函数当前的运行环境。

#### 7. 函数的prototype属性

**JavaScript 中一切都是对象, 自然函数也是对象. JavaScript 规定，所有对象都有自己的原型对象（prototype）,但是只有函数有prototype属性, 其他没有prototype属性**. 所以这里所说的prototype属性指的是函数对象的属性

1. 所有对象都有自己的原型对象（prototype）
2. 只有函数有prototype属性

函数可分为普通函数和构造函数. 普通函数的prototype属性无意义. 构造函数生成实例的时候，该属性会自动成为实例对象的原型。在构造函数创建出来的时候，系统会默认的帮构造函数创建并关联一个神秘的对象，这个对象就是原型,就是prototype属性的值(**但是这个神秘对象不是这个函数对象的原型对象, 而是通过这个构造函数创建的实例对象的原型对象**)。js中万物皆对象，因此原型也是对象，而且原型默认的是一个空的对象(**这句话好像不对**)。

```java
function A() {
this.name = "123"
}
var a = new A();

console.log(A.hasOwnProperty("prototype"));		//true
console.log(a.hasOwnProperty("prototype"));		//false
console.log(("prototype") in a);	//false
console.log(("prototype") in A);	//true
console.log(A.prototype===Object.getPrototypeOf(a));		//true
```



JavaScript 继承机制的设计思想就是，原型对象的所有属性和方法，都能被实例对象共享。也就是说，如果属性和方法定义在原型上，那么所有实例对象就能共享，不仅节省了内存，还体现了实例对象之间的联系。

```javascript
　　function Person(){ 

　　} 
　　Person.prototype = { 
　　　　name : "Nicholas", 
　　　　age : 29, 
　　　　job: "Software Engineer", 
　　　　sayName : function () { 
　　　　　　alert(this.name); 
　　　　} 
　　};
```



- 获取原型对象

1. 从 构造函数 获得 原型对象：
   `构造函数.prototype`
2. 从 对象实例 获得 父级原型对象：
   方法一： `对象实例.__proto`__        【 有兼容性问题，不建议使用】
   方法二：`Object.getPrototypeOf`( 对象实例 )

```js
function Student(){
    this.name = "小马扎"; 
    this.age = 18;
}
var lilei = new Student();  // 创建对象实例
console.log(Student.prototype);  //Student{}
console.log(lilei.__proto__);  //Student{}
console.log(Object.getPrototypeOf(lilei));    //Student{}
```

> 按照JavaScript的说法，function定义的这个Student就是一个Object(对象),而且还是一个很特殊的对象，这个使用function定义的对象与使用new操作符生成的对象之间有一个重要的区别。这个区别就是**function定义的对象有一个prototype属性，使用new生成的对象就没有这个prototype属性**，我们一般称为普通对象！

#### 8. constructor 属性

`prototype`对象有一个`constructor`属性，默认指向`prototype`对象所在的构造函数。由于`constructor`属性定义在`prototype`对象上面，意味着可以被所有实例对象继承。

```js

function A () {}
var a = new A();
console.log(Object.getPrototypeOf(a).constructor===A);	//true
console.log(A.prototype.constructor===A);	//true

a.constructor === A // true
a.constructor === A.prototype.constructor // true
a.hasOwnProperty('constructor') // false
```

上面代码中，`a`是构造函数`A`的实例对象，但是`a`自身没有`constructor`属性，该属性其实是读取原型链上面的`P.prototype.constructor`属性。