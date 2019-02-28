---
  layout: post
  title: Javascript设计模式 1 snippets
  categories: [Snippet]
---

> snippets

```javascript
var CheckObject = {
    checkName: function() {},
    checkEmail: function() {},
    checkPassword: function() {}
}
```

```javascript
var CheckObject = function() {};
CheckObject.checkName = function() {};
CheckObject.checkEmail = function() {};
CheckObject.checkPassword = function() {};
```

```javascript
var CheckObject = function() {
  return {
    checkName: function() {},
    checkEmail: function() {},
    checkPassword: function() {}
  }
}

var a = CheckObject();
a.checkEmail();
```

```javascript
var CheckObject = function() {
    this.checkName =  function() {},
    this.checkEmail = function() {},
    this.checkPassword =  function() {}
}

var a = new CheckObject();
a.checkEmail();
```

```javascript
var CheckObject = function() {};
CheckObject.prototype.checkName = function() {};
CheckObject.prototype.checkEmail = function() {};
CheckObject.prototype.checkPassword = function() {};
```

```javascript
var CheckObject = function() {};
CheckObject.prototype = {
  checkName: function() {},
  checkEmail: function() {},
  checkPassword: function() {}
}
```

```javascript
var CheckObject = function() {};
CheckObject.prototype = {
  checkName: function() { return this; },
  checkEmail: function() { return this; },
  checkPassword: function() { return this; }
}

var a = new CheckObject();
a.checkName().checkEmail().checkPassword(); 
```

```javascript
Function.prototype.checkEmail = function() {};

// var f = function() {};
// f.checkEmail();
// or
var f = new Function();
f.checkEmail();
```

```javascript
Function.prototype.addMethod = function(name, fn) {
  this[name] = fn;
};

// var methods = function() {};
// or
var methods = new Function();
methods.addMethod('checkName', function() {});
methods.addMethod('checkEmail', function() {});
methods.checkName();
methods.checkEmail();
```

```javascript
Function.prototype.addMethod = function(name, fn) {
  this[name] = fn;
  return this;
};

// var methods = function() {};
// or
var methods = new Function();
methods
  .addMethod('checkName', function() {
    return this;
  })
  .addMethod('checkEmail', function() {
    return this;
  });
methods.checkName().checkEmail();
```

```javascript
Function.prototype.addMethod = function(name, fn) {
  this.prototype[name] = fn;
  return this;
};

// var Methods = function() {};
// or
var Methods = new Function();
Methods
  .addMethod('checkName', function() {})
  .addMethod('checkEmail', function() {});

var m = new Methods();
m.checkName();
```
