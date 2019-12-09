---
  layout: post
  title: Similar Array
  categories: [Snippet]
---

实现判断传入的两个数组是否相似。具体需求：

1. 数组中的成员类型相同，顺序可以不同。例如[1, true] 与 [false, 2]是相似的。

2. 数组的长度一致。

3. 类型的判断范围，需要区分:String, Boolean, Number, undefined, null, 函数，日期, window。

```javascript
function arraySimilar(arr1, arr2) {

  if(!(arr1 instanceof Array) || !(arr2 instanceof Array)) return false;

  if(arr1.length !== arr2.length ) return false;

  var i = 0,
      n = arr1.length,
      countMap1 = {},
      countMap2 = {},
      t1, t2,
      TYPES = ['string', 'boolean', 'number', 'undefined', 'null', 'function', 'date', 'window'];

  for( ; i < n; i++) {
    t1 = typeOf(arr1[i]);
    t2 = typeOf(arr2[i]);
    if(countMap1[t1]) {
      countMap1[t1]++;
    } else {
      countMap1[t1] = 1;
    }
    if(countMap2[t2]) {
      countMap2[t2]++;
    } else {
      countMap2[t2] = 1;
    }
  }

  function typeOf(ele) {
    var r;
    if(ele === null) r = 'null';
    else if(ele instanceof Array) r = 'array';
    else if(ele === window) r = 'window';
    else if(ele instanceof Date) r = 'date';
    else r = typeof ele;
    return r;
  }

  for (i = 0, n = TYPES.length; i < n; i++) {
    if(countMap1[TYPES[i]] !== countMap2[TYPES[i]]) {
      return false;
    }
  }

  return true;
}
```

```javascript
function typeOf(ele) {
  if(ele === null) return 'null';
  else if(ele instanceof Array) return 'array';
  else if(ele === window) return 'window';
  else if(ele instanceof Date) return 'date';
  else return typeof ele;
}
        
function arraysSimilar(arr1, arr2){

  if(!(arr1 instanceof Array) || !(arr2 instanceof Array) ||arr1.length!=arr2.length) return false;
  const types1 = arr1.map(ele => typeOf(ele));
  const types2 = arr2.map(ele => typeOf(ele));
    
  for(let i = 0; i < types1.length; i++) {
    let flag = types2.includes(types1[i]);
    if(!flag) return false;
  }
    
  for(let j = 0; j < types2.length; j++) {
    let flag = types1.includes(types2[j]);
    if(!flag) return false;
  }
    
  return true;
}
```