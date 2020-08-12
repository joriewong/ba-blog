---
  layout: post
  title: Javascript设计模式 7 原型模式 snippet
  categories: [Snippet]
---

> snippet

``` javascript
// 图片轮播类
var LoopImages = function(imgArr, container) {
    this.imagesArray = imgArr; // 轮播图片数组
    this.container = container; // 轮播图片容器
}

LoopImages.prototype = {
    // 创建轮播图片
    createImage: function() {
        console.log('LoopImages createImage function');
    },
    // 切换下一张图片
    changeImage: function() {
        console.log('LoopImages changeImage function');
    }
}

// 上下滑动切换类
var SlideLoopImg = function(imgArr, container) {
    // 构造函数继承图片轮播类
    LoopImages.call(this, imgArr, container);
}
SlideLoopImg.prototype = new LoopImages();
// 重写继承的切换下一张图片方法
SlideLoop.prototype.changeImage = function() {
    console.log('SlideLoopImg changeImage function');
}
// 渐隐切换类
var FadeLoopImage = function(imgArr, container, arrow) {
    LoopImages.call(this, imgArr, container);
    // 切换箭头私有变量
    this.arrow = arrow;
}
FadeLoopImage.prototype = new LoopImages();
FadeLoopImage.prototype.changeImage = function() {
    console.log('FadeLoopImg changeImage function');
}
```

``` javascript
var fadeImg = new FadeLoopImg([
    '01.jpg',
    '02.jpg',
    '03.jpg',
    '04.jpg'
], 'slide', [
    'left.jpg',
    'right.jpg'
]);
console.log(fadeImg.container); // slide
fadeImg.changeImage(); // FadeLoopImg changeImage function
LoopImages.prototype.getImageLength = function() {
    return this.imagesArray.length;
}
FadeLoopImg.prototype.getContainer = function() {
    return this.container;
}
console.log(fadeImg.getImageLength()); // 4
console.log(fadeImg.getContainer()); // slide
```

``` javascript
function prototypeExtend() {
    var F = function() {}, // 缓存类，为实例化返回对象临时创建
        args = arguments, // 模板对象参数序列
        i = 0,
        len = args.length;
    for (; i < len; i++) {
        // 遍历每个模板对象中的属性
        for (var j in args[i]) {
            // 将这些属性复制到缓存类原型中
            F.prototype[j] = args[i][j];
        }
    }
    // 返回缓存类的一个实例
    return new F();
}
```

``` javascript
var penguin = prototypeExtend({
    speed: 20,
    swim: function() {
        console.log('游泳速度' + this.speed);
    }
}, {
    run: function(speed) {
        console.log('奔跑速度' + speed);
    }
}, {
    jump: function() {
        console.log('跳跃动作');
    }
});

penguin.swim(); // 游泳速度 20
penguin.run(10); // 奔跑速度 10
penguin.jump(); // 跳跃动作
```
