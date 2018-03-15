---
  layout: post
  title: Lambda Calculus
  categories: [Note]
---

(λ`y`.x(`y`z) (`ab`)
=>
x(`ab`z)


```javascript
// λ演算的写法
fix = λf.(λx.f(λv.x(x)(v)))(λx.f(λv.x(x)(v)))

// ES6的写法
var fix = f => (x => f(v => x(x)(v)))
               (x => f(v => x(x)(v)));
```