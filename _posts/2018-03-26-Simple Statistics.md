---
  layout: post
  title: Simple Statistics snippet
  categories: [Snippet]
---

JS函数式编程计算标准差

```javascript

const sample = [];

const mean = sample.reduce((x, y) => x + y)/sample.length;

const deviation = sample.map((x) => x - mean);

const std_deviation = Math.sqrt(
  deviation
  .map((x) => x*x)
  .reduce((x,y) => x + y) / (sample.length-1)
);
```

