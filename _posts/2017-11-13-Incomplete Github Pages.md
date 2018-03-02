---
  layout: post
  title: Incomplete Github Pages
  categories: [OPS]
---

## 设置远程仓库的默认分支

在Github远程仓库的Settings中设置Default branch为`gh-pages`

![image_1buo68h96pkl5qdbaf62rpcg23.png-33.1kB][1]

## 克隆远程仓库

将远程仓库克隆至本地仓库

```
$ git clone git@github.com:joriewong/LCTT-Helper.git
```

此时的本地仓库将不再是`master`分支，而是`gh-pages`分支

![image_1buo4c18b1urb15008soijlj3u9.png-3.8kB][2]

通过`git branch`查看本地仓库当前分支

![image_1buo6iacs1a4f1tb61il1mlh15ec3a.png-2kB][3]

## 提交

监听开发过程中文件的变更

```
$ git add .
```

提交`gh-pages`分支，附上提交信息`gh-pages`

```
$ git commit -m 'gh-pages'

[gh-pages 7a63de7] gh-pages
warning: LF will be replaced by CRLF in .idea/LCTT-Helper.iml.
The file will have its original line endings in your working directory.
warning: LF will be replaced by CRLF in .idea/modules.xml.
The file will have its original line endings in your working directory.
warning: LF will be replaced by CRLF in .idea/vcs.xml.
The file will have its original line endings in your working directory.
warning: LF will be replaced by CRLF in .idea/workspace.xml.
The file will have its original line endings in your working directory.
 7 files changed, 807 insertions(+), 16 deletions(-)
 create mode 100644 .idea/LCTT-Helper.iml
 create mode 100644 .idea/modules.xml
 create mode 100644 .idea/vcs.xml
 create mode 100644 .idea/workspace.xml
```

## 推送至远程仓库

`git push`推送至Github远程仓库

```
$ git push origin gh-pages

Counting objects: 529, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (476/476), done.
Writing objects: 100% (529/529), 1.91 MiB | 111.00 KiB/s, done.
Total 529 (delta 46), reused 519 (delta 46)
remote: Resolving deltas: 100% (46/46), done.
To git@github.com:joriewong/LCTT-Helper.git
   595650e..ad94414  gh-pages -> gh-pages
```

可以看到Github已经同步更新

![image_1buo6v1f719grek81112q93aei3n.png-65.2kB][4]

## 配置Github-pages

在远程仓库的Settings中配置Github-pages

![image_1buo7fifh1tmf79j1gegtemmq644.png-48.2kB][5]


  [1]: http://static.zybuluo.com/wongjorie/o8fdfkljz5a52aitct561d4l/image_1buo68h96pkl5qdbaf62rpcg23.png
  [2]: http://static.zybuluo.com/wongjorie/giv6bd1btosz119ahokngl7z/image_1buo4c18b1urb15008soijlj3u9.png
  [3]: http://static.zybuluo.com/wongjorie/ka55adzbfr16texui3hrajoz/image_1buo6iacs1a4f1tb61il1mlh15ec3a.png
  [4]: http://static.zybuluo.com/wongjorie/3q15rvdud3anvkt4zvqk4md6/image_1buo6v1f719grek81112q93aei3n.png
  [5]: http://static.zybuluo.com/wongjorie/mbud6e9g48snpinvcvb9s20j/image_1buo7fifh1tmf79j1gegtemmq644.png
