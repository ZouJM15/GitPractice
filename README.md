# git 练习
github官方教程，原视频在[YouTube](https://www.youtube.com/watch?v=r8jQ9hVA2qs&list=PL0lo9MOBetEFcp4SCWinBdpml9B2U25-f)。
本人又操作了一遍，这是总结。

## Lecture 1

1. 打开git bash

2. 在某个地方新建文件夹，指令：
mkdir git-practice
cd git-practice
code .

3. vscode 打开了，新建一个hello.md文件，指令：
touch hello.md

4. 运行 git status 指令
![第一次运行git status](images/lecture1/2026-01-16 121212.png)

发现出错，因为git尚未初始化。初始化就是指创建一个新的Git仓库。
所以运行 

git init
这是第一个指令，这样git就可以跟踪我们的更改了
1. 再次运行 git status
就可以看到正在跟踪这个文件夹下的所有文件
这会显示我们的更改以及它们是否暂存，还有git正在跟踪哪些文件
1. 运行 git add . 
这是将工作目录中的所有更改添加到暂存区
然后再运行 git status ，可以看到被跟踪的 文件呈现出不同的颜色，这说明他们目前位于暂存区

1. 返回vscode，然后再hello.md中随便写点什么，保存并返回终端输入 git status ，看到以下内容，说明hello.md，readme.md已发生改变，且有一张刚存入的截图还未被跟踪，再运行 git add . git status，可以看到都存入了暂存区

2. 运行 git commit -m initial commit ，来提交这些更改。此命令允许我们保存更改并附加消息。

**需要注意的是，会经常用到 git status、git add、git commit指令，所以练习这些命令很重要。**
题外话：github和git是一个东西吗？
答案： NO ！！
git是版本控制系统，用于跟踪文件更改; github是一个平台，允许开发人员协作并将代码存储在云端。git与github共同协作，使软件的构建、扩展、保护和存储变得更加容易。

## Lecture 2
