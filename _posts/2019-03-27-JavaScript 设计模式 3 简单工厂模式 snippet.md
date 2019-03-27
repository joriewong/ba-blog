---
  layout: post
  title: Javascript设计模式 3 简单工厂模式 snippet
  categories: [Snippet]
---

> snippets

工厂模式-类的实例化

```javascript
// 篮球基类
var Basketball = function() {
    this.intro = '篮球盛行于美国';
}
Basketball.prototype = {
    getMember: function() {
        console.log('每个队伍需要5名队员');
    },
    getBallSize: function() {
        console.log('篮球很大');
    }
}
// 足球基类
var Football = function() {
    this.intro = '足球在世界范围内很流行';
}
Football.prototype = {
    getMember: function() {
        console.log('每个队伍需要11名队员');
    },
    getBallSize: function() {
        console.log('足球很大');
    }
}
// 网球基类
var Tennis = function() {
    this.intro = '每年有很多网球系列赛';
}
Tennis.prototype = {
    getMember: function() {
        console.log('每个队伍需要1名队员');
    },
    getBallSize: function() {
        console.log('网球很小');
    }
}
// 运动工厂
var SportsFactory = function(name) {
    switch(name) {
        case 'NBA': return new Basketball();
        case 'WorldCup': return new Football();
        case 'FrenchOpen': return new Tennis();
    }
}
// 为世界杯创建一个足球，只需要记住运动工厂SportsFactory，调用并创建
var football = SportsFactory('WorldCup');
console.log(football); // > Football {intro: "足球在世界范围内很流行"}
console.log(football.intro); // 足球在世界范围内很流行
football.getMember(); // 每个队伍需要11名队员
```

工厂模式-对象扩展

```javascript
// 工厂模式
function createBook(name ,time ,type) {
    // 创建一个对象，并对对象拓展属性和方法
    var o = new Object();
    o.name = name;
    o.time = time;
    o.type = time;
    o.getName = function() {
        console.log(this.name);
    }
    // 处理差异
    // ...
    // 返回对象
    return o;
}

var book1 = createBook('js book', '2014', 'js');
var book2 = createBook('css book', '2013', 'css');

book1.getName() // js book
book2.getName() // css book
```