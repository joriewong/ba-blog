---
  layout: post
  title: Trim snippet
  categories: [Snippet]
---

高效移除字符串开始和末尾的空格

```javascript
  String.prototype.trim = function() {
    var str = this.replace(/^\s+/, "");
          end = str.length - 1;
          ws = /\s/;

    while(ws.test(str.charAt(end))) {
      end--;
    }

    return str.slice(0, end+1);
  }
```

