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

