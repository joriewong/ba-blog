# ba-blog

## 环境

- Windows 10
- Git Bash

## 安装ruby

下载rubyinstaller安装：https://rubyinstaller.org/downloads/ (推荐Ruby 2.2.6版本)

```
$ ruby -v
```

## 安装DevKit

下载DevKit.exe：https://rubyinstaller.org/downloads/ ，解压完成后进入目录，init初始化，review检查，成功添加ruby目录后再install

```
$ ruby dk.rb init
$ ruby dk.rb review
$ ruby dk.rb install
```

## 安装Jekyll
切换gem镜像后再安装Jekyll（可能需要安装bundle）

```
$ gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/
$ gem sources -l
https://gems.ruby-china.org

$ gem install Jekyll
$ gem install bundle
```

## 新建博客

```
$ jekyll new ba-blog
$ jekyll serve
```