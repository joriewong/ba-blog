---
  layout: post
  title: Typora集成PicGo腾讯云图床实践
  categories: [Note]
---

## 应用概述

**PicGo: 一个用于快速上传图片并获取图片 URL 链接的工具**

PicGo 本体支持如下图床：

- `七牛图床` v1.0
- `腾讯云 COS v4\v5 版本` v1.1 & v1.5.0
- `又拍云` v1.2.0
- `GitHub` v1.5.0
- `SM.MS V2` v2.3.0-beta.0
- `阿里云 OSS` v1.6.0
- `Imgur` v1.6.0

**本体不再增加默认的图床支持。你可以自行开发第三方图床插件。详见 [PicGo-Core](https://picgo.github.io/PicGo-Core-Doc/)**。

## 特色功能

- 支持拖拽图片上传
- 支持快捷键上传剪贴板里第一张图片
- Windows 和 macOS 支持右键图片文件通过菜单上传 (v2.1.0+)
- 上传图片后自动复制链接到剪贴板
- 支持自定义复制到剪贴板的链接格式
- 支持修改快捷键，默认快速上传快捷键：`command+shift+p`（macOS）| `control+shift+p`（Windows\Linux)
- 支持插件系统，已有插件支持 Gitee、青云等第三方图床
  - 更多第三方插件以及使用了 PicGo 底层的应用可以在 [Awesome-PicGo](https://github.com/PicGo/Awesome-PicGo) 找到。欢迎贡献！
- 支持通过发送 HTTP 请求调用 PicGo 上传（v2.2.0+)

## 下载安装

点击此处下载 [应用](https://github.com/Molunerfinn/PicGo/releases)。

## 应用截图

![](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/picgo-2.0.gif)

![picgo-menubar](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/34242310-b5056510-e655-11e7-8568-60ffd4f71910.gif)

## 配置腾讯云图床

PicGo->打开详细窗口->图床设置->腾讯云COS，选择v5版本，从腾讯云COS拿到对应配置，设置如下：

![image-20210415110405695](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210415110405695.png)

## 集成到Typora

Typora->偏好设置->图像->上传服务，设置如下：

![image-20210415105918036](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210415105918036.png)