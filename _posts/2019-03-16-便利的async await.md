---
  layout: post
  title: 便利的async/await
  categories: [Note]
---

- 使用async/await能够让你少写代码。每一次你使用async/await你都能跳过一些不必要的步骤：写一个`.then`，创建一个匿名函数来处理响应，在回调中命名响应。

```javascript
async function loadData() {
    let response = await request(url);
}
```

- async/await使得我们可以使用try/catch语句结构处理同步或者异步的错误。

```javascript
async function loadData() {
    try {
        let response = await request(url);
    } catch(e) {
        // catch exception here
    }
}
```

- async/await比起promise链返回的错误堆栈信息使得我们可以容易定位异常位置。

```javascript
async function loadData() {
  await Promise1()
  await Promise2()
  await Promise3()
  await Promise4()
  await Promise5()
  throw new Error("Error !!!");
}
loadData()
  .catch(function(e) {
    console.log(e);
});
```

- 通过async/await进行断点调试，它就像是一个同步函数一样，而不是像promise链无法行进下去。