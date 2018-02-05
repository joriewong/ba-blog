---
  layout: post
  title: IndexedDB
---

# {{ page.title }}

## IndexedDB

IndexedDB 是一种可以让你在用户的浏览器内持久化存储数据的方法。IndexedDB 为生成 Web Application 提供了丰富的查询能力，使我们的应用在在线和离线时都可以正常工作。

### 基本模式

- 打开数据库并且开始一个事务
- 创建一个objectStore
- 构建请求进行数据库操作

## 打开数据库

```
var request = window.indexedDB.open("zybuluoIndexedDB");
```

### 生成处理函数

```
var db;
request.onerror = function(event) {
  alert("Why didn't you allow my web app to use IndexedDB?!");
};
request.onsuccess = function(event) {
  db = request.result;
};
```

## 链式创建objectStore

```
var objectStore = db.transaction("localNoteActions").objectStore("localNoteActions");
```

## 游标

使用遍历对象存储空间中的所有值。

```
objectStore.openCursor().onsuccess = function(event) {
  var cursor = event.target.result;
  if (cursor) {
    alert("The key is " + cursor.key + ",and its value is " + cursor.value);
    cursor.continue();
  }
  else {
    alert("No more entries!");
  }
};
```

## 参考链接

> [MDN Using_IndexedDB](https://developer.mozilla.org/zh-CN/docs/Web/API/IndexedDB_API/Using_IndexedDB) 



