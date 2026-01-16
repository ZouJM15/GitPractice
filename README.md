# git 练习

1. 打开git bash
2. 在某个地方
mkdir git-practice
cd git-practice
code .
3. vscode 打开了，新建一个hello.md文件
touch hello.md

4. git status
发现出错，因为git尚未初始化。初始化就是指创建一个新的Git仓库。
所以运行 
git init
这是第一个指令，这样git就可以跟踪我们的更改了
5. 再次运行 git status
就可以看到正在跟踪这个文件夹下的所有文件
这会显示我们的更改以及它们是否暂存，还有git正在跟踪哪些文件
6. 运行 git add . 
这是将工作目录中的所有更改添加到暂存区
然后再运行 git status ，可以看到被跟踪的 文件呈现出不同的颜色，这说明他们目前位于暂存区

7. 返回vscode，然后再hello.md中随便写点什么，保存并返回终端输入 git status ，看到以下内容，说明hello.md，readme.md已发生改变，且有一张刚存入的截图还未被跟踪，再运行 git add . ，
