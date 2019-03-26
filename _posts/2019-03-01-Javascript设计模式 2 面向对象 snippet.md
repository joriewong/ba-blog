---
  layout: post
  title: Javascript设计模式 2 面向对象 snippet
  categories: [Snippet]
---

> snippets

```javascript
var Book = function(id, bookname, price) {
    this.id = id;
    this.bookname = bookname;
    this.price = price;
}
// Book.prototype.display = function() {};
Book.prototype = {
    display: function() {}
}

var book = new Book(10, 'Javascript 设计模式', 50);
console.log(book.bookname); // Javascript 设计模式
```

```javascript
var Book = function(id, name, price) {
  // 私有属性
  var num = 1;
  // 私有方法
  function checkId() {};
  // 特权方法
  this.getName = function() {};
  this.getPrice = function() {};
  this.setName = function() {};
  this.setPrice = function() {};
  // 对象公有属性
  this.id = id;
  // 对象公有方法
  this.copy = function() {};
  // 构造器
  this.setName(name);
  this.setPrice(price);
}
// 类静态公有属性（对象不能访问）
Book.inChinese = true;
// 类静态公有方法（对象不能访问）
Book.resetTime = function() {
  console.log('new Time');
}
Book.prototype = {
  // 共有属性
  isJSBook: false,
  // 共有方法
  display: function() {}
}

var b = new Book(11, 'Javascript 设计模式', 50);
console.log(num) // undefined
console.log(b.isJSBook) // false
console.log(b.id) // 11
console.log(b.isChinese) // undefined

console.log(Book.isChinese); // true
Book.resetTime(); // new Time
```

```javascript
// 利用闭包实现
var Book = (function() {
  // 静态私有变量
  var bookNum = 0;
  // 静态私有方法
  function checkBook(name) {};
  // 返回构造函数
  return function(newId, newName, newPrice) {
    // 私有变量
    var name, price;
    // 私有方法
    function checkId(id) {};
    // 特权方法
    this.getName = function() {};
    this.getPrice = function() {};
    this.setName = function() {};
    this.setPrice = function() {};
    // 公有属性
    this.id = newId;
    // 公有方法
    this.copy = function() {};
    bookNum++;
    if(bookNum > 100) {
      throw new Error('我们仅出版100本书.');
    }
    // 构造器
    this.setName(name);
    this.setPrice(price);
  }
})();

Book.prototype = {
  // 静态公有属性
  isJSBook: false,
  // 静态公有方法
  display: function() {}
}
```

```javascript
// 利用闭包实现
var Book = (function() {
  // 静态私有变量
  var bookNum = 0;
  // 静态私有方法
  function checkBook(name) {};
  // 创建类
  function _book(newId, newName, newPrice) {
    // 私有变量
    var name, price;
    // 私有方法
    function checkId(id) {};
    // 特权方法
    this.getName = function() {};
    this.getPrice = function() {};
    this.setName = function() {};
    this.setPrice = function() {};
    // 公有属性
    this.id = newId;
    // 公有方法
    this.copy = function() {};
    bookNum++;
    if(bookNum > 100) {
      throw new Error('我们仅出版100本书.');
    }
    // 构造器
    this.setName(name);
    this.setPrice(price);
  }
  // 构建原型
  _book.prototype = {
    // 静态公有属性
    isJSBook: false,
    // 静态公有方法
    display: function() {}
  }
  // 返回类
  return _book;
})();
```

```javascript
// 图书安全类
var Book = function(title, time, type) {
  // 判断执行过程中this是否是当前这个对象（如果是说明是用new创建的）
  if(this instanceof Book) {
    this.title = title;
    this.time = time;
    this.type = type;
  // 否则重新创建这个对象
  }else {
    return new Book(title, time, type);
  }
}
var book = Book('JavaScript', '2014', 'js');

console.log(book) // Book
console.log(book.title) // JavaScript
console.log(book.time) // 2014
console.log(book.type) // js
console.log(window.title) // undefined
console.log(window.time) // undefined
console.log(window.type) // undefined
```

```javascript
// 类式继承
// 声明父类
function SuperClass() {
  this.superValue = true;
}
// 为父类添加共有方法
SuperClass.prototype.getSuperValue = function() {
  return this.superValue;
}
// 声明子类
function SubClass() {
  this.subValue = false;
}
// 继承父类
SubClass.prototype = new SuperClass();
SubClass.prototype.getSubValue = function() {
  return this.subValue;
}

var instance = new SubClass();
console.log(instance.getSuperValue()); // true
console.log(instance.getSubValue()); // false

console.log(instance instanceof SuperClass); // true
console.log(instance instanceof SubClass); // true
console.log(SubClass instanceof SuperClass); // false
console.log(SubClass.prototype instanceof SuperClass); // true
console.log(SubClass instanceof Object); // true
```

```javascript
function SuperClass() {
  this.books = ['JavaScript', 'html', 'css'];
}
function SubClass() {}
SubClass.prototype = new SuperClass();
var instance1 = new SubClass();
var instance2 = new SubClass();
console.log(instance2.books); // ['JavaScript', 'html', 'css']
instance1.books.push('设计模式');
console.log(instance2.books); // ['JavaScript', 'html', 'css', '设计模式']
```

```javascript
// 构造函数继承式
// 声明父类
function SuperClass(id) {
  // 引用类型共有属性
  this.books = ['JavaScript', 'html', 'css'];
  // 值类型共有属性
  this.id = id;
}
// 父类声明原型方法
SuperClass.prototype.showBooks = function() {
  console.log(this.books);
}
// 声明子类
function SubClass(id) {
  // 继承父类
  SuperClass.call(this, id);
}
// 创建第一个子类的实例
var instance1 = new SubClass(10);
// 创建第二个子类的实例
var instance2 = new SubClass(11);

instance1.books.push('设计模式');
console.log(instance1.books); // ['JavaScript', 'html', 'css', '设计模式']
console.log(instance1.id); // 10
console.log(instance2.books); // ['JavaScript', 'html', 'css']
console.log(instance2.id); // 11

instance1.showBooks(); // TypeError
```

```javascript
// 组合式继承
// 声明父类
function SuperClass(name) {
  // 值类型公有属性
  this.name = name;
  // 引用类型公有属性
  this.books = ['html', 'css', 'JavaScript'];
}
// 父类型共有方法
SuperClass.prototype.getName = function() {
  console.log(this.name);
}
// 声明子类
function SubClass(name, time) {
  // 构造函数式继承父类name属性
  SuperClass.call(this, name);
  // 子类中新增公有属性
  this.time = time;
}
// 类式继承 子类原型继承父类
SubClass.prototype = new SuperClass();
// 子类原型方法
SubClass.prototype.getTime = function() {
  console.log(this.time);
};

var instance1 = new SubClass('js book', 2014);
instance1.books.push('设计模式');
console.log(instance1.books); // ['JavaScript', 'html', 'css', '设计模式']
instance1.getName(); // js book
instance1.getTime(); // 2014
var instance2 = new SubClass('css book', 2013);
console.log(instance2.books); // ['JavaScript', 'html', 'css']
instance1.getName(); // css book
instance1.getTime(); // 2013
```

```javascript
// 原型式继承
function inheritObject(o) {
  // 声明一个过渡函数对象
  function F() {}
  // 过渡对象的原型继承父对象
  F.prototype = o;
  return new F();
}

var book = {
  name: 'js book',
  alikeBook: ['css book', 'html book']
};
var newBook = inheritObject(book);
newBook.name = 'ajax book';
newBook.alikeBook.push('xml book');
var otherBook = inheritObject(book);
otherBook.name = 'flash book';
otherBook.alikeBook.push('as book');

console.log(newBook.name); // ajax book
console.log(newBook.alikeBook); // ['css book', 'html book', 'xml book', 'as book']
console.log(otherBook.name); // flash book
console.log(otherBook.alikeBook); // ['css book', 'html book', 'xml book', 'as book']
console.log(book.name); // js book
console.log(book.alikeBook) // ['css book', 'html book', 'xml book', 'as book']

// 寄生式继承
// 声明基对象
var book = {
  name: 'js book',
  alikeBook: ['css book', 'html book']
};
function createBook(obj) {
  // 通过原型继承方式创建新对象
  var o = new inheritObject(obj);
  // 拓展新对象
  o.getName = function() {
    console.log(name);
  };
  // 返回拓展后的新对象
  return o;
}

/**
 * 寄生式继承 继承原型
 * 传递参数 subClass 子类
 * 传递参数 superClass 父类
 **/
function inheritPrototype(subClass, superClass) {
  // 复制一份父类的原型副本保存在变量中
  var p = inheritObject(superClass.prototype);
  // 修正因为重写子类原型导致子类的constructor属性被修改
  p.constructor = subClass;
  // 设置子类的原型
  subClass.prototype = p;
}

// 定义父类
function SuperClass(name) {
  this.name = name;
  this.colors = ['red', 'blue', 'green'];
}
// 定义父类型原型方法
SuperClass.prototype.getName = function() {
  console.log(this.name);
}
// 定义子类
function SubClass(name ,time) {
  // 构造函数式继承
  SuperClass.call(this, name);
  // 子类新增属性
  this.time = time;
}
// 寄生式继承父类原型
inheritPrototype(SubClasss, SuperClass);
// 子类新增原型方法
SubClass.prototype.getTime = function() {
  console.log(this.time);
}
// 创建两个测试方法
var instance1 = new SubClass('js book', 2014);
var instance2 = new SubClass('css book', 2013);

instance1.colors.push('black');
console.log(instance1.colors); // ['red', 'blue', 'green', 'black'] 
console.log(instance2.colors); // ['red', 'blue', 'green']
instance2.getName(); // css book
instance2.getTime(); // 2013
```

```javascript
// 单继承 属性复制
var extend = function(target, source) {
  // 遍历对象中的属性
  for(var property in source) {
	// 将源对象中的属性复制到目标对象中
	target[property] = source[property];
  }
  // 返回目标对象
  return target;
}

var book = {
	name: 'JavaScript 设计模式',
	alike: ['css', 'html', 'JavaScript']
}
var anotherBook = {
	color: 'blue'
}
extend(anotherBook, book);
console.log(anotherBook.name); // JavaScript 设计模式
console.log(anotherBook.alike); // ['css', 'html', 'JavaScript']

anotherBook.alike.push('ajax');
anotherBook.name = '设计模式';
console.log(anotherBook.name); // 设计模式
console.log(anotherBook.alike); // ['css', 'html', 'JavaScript', 'ajax']
console.log(book.name); // JavaScript 设计模式
console.log(book.alike); //  ['css', 'html', 'JavaScript', 'ajax']

// 多继承 属性复制
var mix = function() {
  var i = 1,                                   // 从第二个参数起为被继承的对象
        len = arguments.length,   // 获取参数长度
        target = arguments[0],     // 第一个对象为目标对象
        arg;                                    // 缓存参数对象
  // 遍历被继承的对象
  for(; i < len; i++) {
    // 缓存当前对象
    arg = arguments[i];
    // 遍历被继承对象中的属性
    for(var property in arg) {
      // 将被继承对象中的属性复制到目标对象中
      target[property] = arg[property];
    }

    // 返回目标对象
    return target;
  }
}

Object.prototype.mix = function() {
  var i = 1,                                   // 从第二个参数起为被继承的对象
        len = arguments.length,   // 获取参数长度
        arg;                                    // 缓存参数对象
  // 遍历被继承的对象
  for(; i < len; i++) {
    // 缓存当前对象
    arg = arguments[i];
    // 遍历被继承对象中的属性
    for(var property in arg) {
      // 将被继承对象中的属性复制到目标对象中
      this[property] = arg[property];
    }
  }
}

otherBook.mix(book1, book2)
```

```javascript
// 多态
function add() {
  // 获取参数
  var arg = arguments,
  // 获取参数长度
      len = arg.length;
  switch(len) {
    // 如果没有参数
    case 0:
      return 10;
    // 如果只有一个参数
    case 1:
      return 10 + arg[0];
    // 如果有两个参数  
    case 2:
      return arg[0] + arg [1];  
  }
}
// 测试用例
console.log(add()); // 10
console.log(add(5)); // 15
console.log(add(6, 7)); // 13
```

```javascript
function Add() {
  // 无参数算法
  function zero() {
    return 10;
  }
  // 一个参数算法
  function one(num) {
    return 10 + num;
  }
  // 两个参数算法
  function two(num1, num2) {
    return num1 + num2;
  }
  // 相加共有方法
  this.add = function() {
    var arg = arguments,
    // 获取参数长度
        len = arg.length;
    switch(len) {
      // 如果没有参数
      case 0:
        return zero();
      // 如果只有一个参数  
      case 1:
        return one(arg[0]);
      // 如果有两个参数
      case 2:
        return two(arg[0], arg[1]);
    }
  }
}
// 实例化类
var A = new Add();
// 测试
console.log(A.add()); // 10
console.log(A.add(5)); // 15
console.log(A.add(6, 7)); // 13
```