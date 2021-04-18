---
  layout: post
  title: iTerm Oh My Zsh配置powerlevel 10k主题
  categories: [Note]
---

## powerline/fonts字体安装

依赖[powerline/fonts](https://github.com/powerline/fonts)字体库，安装方式如下：

```bash
# clone
git clone https://github.com/powerline/fonts.git --depth=1
# install
cd fonts
./install.sh
# clean-up a bit
cd ..
rm -rf fonts
```

## powerlevle 10k主题安装

主题[powerlevel 10k](https://github.com/romkatv/powerlevel10k)，克隆到Oh My Zsh的主题目录，方式如下：

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

## 配置Oh My Zsh

在 `~/.zshrc`中设置`ZSH_THEME="powerlevel10k/powerlevel10k"`即可。

## 重启iTerm配置p10k

重启iTerm，直接会进入向导程序，第一步的操作必须选`y`，安装字体`MesloLGS NF`，然后根据提示，逐一选择自己的偏好设置。

![image-20210417214017978](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/20210417214018.png)

接下来会有一些字体和图标检测：

![image-20210418084453260](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418084453260.png)

![image-20210418084527253](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418084527253.png)

![image-20210418084549597](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418084549597.png)

![image-20210418084611092](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418084611092.png)

然后就是一些样式选择：

![image-20210418084810556](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418084810556.png)

![image-20210418084830223](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418084830223.png)

![image-20210418084852257](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418084852257.png)

![image-20210418084929812](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418084929812.png)

![image-20210418085001148](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418085001148.png)

![image-20210418085039703](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418085039703.png)

![image-20210418085058828](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418085058828.png)

![image-20210418085110575](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418085110575.png)

![image-20210418085129245](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418085129245.png)

![image-20210418085153352](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418085153352.png)

![image-20210418085209566](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418085209566.png)

![image-20210418085236404](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418085236404.png)

最终效果：

![image-20210417225323245](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/20210417225323.png)

*如果想重新配置，执行`p10k configure`，并在最后一步选择覆盖原有的配置文件。*

![image-20210418085305120](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418085305120.png)

> MesloLGS NF字体的正确安装是保证最终效果不乱码的关键。

所以，例如iTerm需设置字体`MesloLGD NF`

![image-20210418085431497](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/image-20210418085431497.png)

例如，VSCode的terminal也需设置字体`MesloLGD NF`

![image-20210417225638428](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/20210417225638.png)

## 参考链接

- https://github.com/powerline/fonts This repository contains pre-patched and adjusted fonts for usage with the [Powerline](https://github.com/powerline/powerline) statusline plugin. iTerm2 users need to set both the Regular font and the Non-ASCII Font in "iTerm > Preferences > Profiles > Text" to use a patched font.
- https://github.com/romkatv/powerlevel10k Powerlevel10k is a theme for Zsh. It emphasizes speed, flexibility and out-of-the-box experience.
