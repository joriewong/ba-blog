---
  layout: post
  title: Number Repeat snippet
  categories: [Snippet]
---

String.prototype.repeat()

```javascript
/** 
 * str: String
 * count: Number
 */

let resultString = str.repeat(count);
```

`repeat()`构造并返回一个新字符串，该字符串包含被连接在一起的指定数量的字符串的副本。

```javascript
function f(n) {
  for (let i = -n; i <= n; i++) {
    if (i === 0 || i === 1) {
      continue
    }
    let k = Math.abs(i)
    console.log(k.toString().repeat(k))
  }
}
```