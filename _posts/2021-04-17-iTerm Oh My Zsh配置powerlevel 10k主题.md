---
  layout: post
  title: iTerm Oh My Zsh配置powerlevel 10k主题
  categories: [Note]
---

## 字体安装

依赖[powerline-fonts](https://github.com/powerline/fonts)字体库，安装方式如下：

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

## 主题安装

依赖[powerlevel 10k](https://github.com/romkatv/powerlevel10k)，下载方式如下：

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

## 配置Oh My Zsh

在 `~/.zshrc`中设置`ZSH_THEME="powerlevel10k/powerlevel10k"`即可。

## 重启iTerm配置p10k

重启iTerm，直接会进入向导程序，第一步的操作必须选`y`，安装字体`MesloLGS NF`，然后根据提示，逐一选择自己的偏好设置。

![image-20210417214017978](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/20210417214018.png)

最终效果：

![image-20210417225323245](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/20210417225323.png)

*如果想重新配置，执行`p10k configure`即可。*

> MesloLGS NF字体的正确安装是保证最终效果不乱码的关键。

所以，例如iTerm需设置字体`MesloLGD NF`

![image-20210417225603231](/Users/wangjieyu/Library/Application Support/typora-user-images/image-20210417225603231.png)

例如，VSCode的terminal也需设置字体`MesloLGD NF`

![image-20210417225638428](https://mds-1303228113.cos.ap-chongqing.myqcloud.com/imgs/20210417225638.png)