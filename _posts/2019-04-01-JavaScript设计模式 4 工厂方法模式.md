---
  layout: post
  title: Javascript设计模式 4 工厂方法模式 snippet
  categories: [Snippet]
---

> snippets

```javascript
var Demo = function() {
  if(!(this instanceof Demo)) {
    return new Demo();
  }
}
Demo.prototype = {
  show: function () {
    console.log('成功获取！');
  }
}
var d = Demo();
d.show() // 成功获取！
```

```javascript
// 安全模式创建的工厂类
var Factory = function(type, content) {
  if(this instanceof Factory) {
    var s = new this[type](content);
    return s
  } else {
    return new Factory(type, content);
  }
}
```