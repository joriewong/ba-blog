---
  layout: post
  title: js循环里的async和await最佳实践
  categories: [FE]
---

一些`async/await`在js循环里的最佳实践。

## 准备工作

```javascript
const entries = {
  foo: 0,
  bar: 1,
  baz: 2,
};

const keys = ["foo", "bar", "baz"];

const sleep = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

const getValue = (key) => sleep(1000).then((v) => entries[key]);
```

## 最佳实践 1

不要在`forEach`里使用`await`，用`for`循环或其他不带`callback`的循环替代。

```javascript
// bad
const run = async (_) => {
  console.log('start');
  keys.forEach(async key => {
    const value = await getValue(key);
    console.log(value)
  })
  console.log('end');
};

run();
// start
// end
// 0
// 1
// 2
```

如果想串行执行`await`，使用`for`循环或任何不带`callback`的循环。

```javascript
// good
const run = async (_) => {
  console.log('start');
    for (let index = 0; index < keys.length; index++) {
      const key = keys[index]
      const value = await getValue(key)
      console.log(value);
    }
  console.log('end')
};

run();
// start
// 0
// 1
// 2
// end
```

并行执行`await`。

```javascript
// good
const run = async (_) => {
  console.log('start');
  const promises = keys.map(async key => {
    const value = await getValue(key)
    console.log(value);
  });
  await Promise.all(promises)
  console.log('end');
};

run();
// start
// 0 1 2
// end
```



## 最佳实践 2

不要在`filter`和`reduce`里使用`await`，可以`await` `map`返回的`promise`数组然后再进行`filter`或`reduce`操作。

### filter

```javascript
const run = async (_) => {
  const promises = keys.map(getValue);
  const values = await Promise.all(promises)
  const lessThan1 = keys.filter((key, index) => {
    const value = values[index]
    return value < 1
  })
  console.log(lessThan1);
};

run();
// ['foo']
```

### reduce

```javascript
const run = async (_) => {
  const promises = keys.map(getValue)
  const values = await Promise.all(promises)
  const sum = values.reduce((sum, value) => sum + value)
  console.log(sum);
};

run();
// 3
```

## 参考链接

- [JavaScript loops - how to handle async/await (lavrton.com)](https://lavrton.com/javascript-loops-how-to-handle-async-await-6252dd3c795/)
- https://zellwk.com/blog/async-await-in-loops/
