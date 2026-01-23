# Git Practice
Git官方教程，原视频在[YouTube](https://www.youtube.com/watch?v=r8jQ9hVA2qs&list=PL0lo9MOBetEFcp4SCWinBdpml9B2U25-f)。
本人又操作了一遍，这是总结。

常用指令
```bash
git init
git status
git remote add origin <git url>
git add .
git commit -m "初次提交"
git branch -M main
git push -u origin main

git remote set-url origin <git url>
```

<!-- [TOC]{level=2} -->

## 目录
- [Lecture 1](#Lecture-1)
- [Lecture 2](#lecture-2)
- [Lecture 3](#lecture-3)
- [Lecture 4](#lecture-4)
- [Lecture 5](#lecture-5)
- [Lecture 6](#lecture-6)
- [Lecture 7](#lecture-7)
- [Lecture 8](#lecture-8)



## Lecture 1

1. 打开 git bash

2. 在某个地方新建文件夹，指令：
`mkdir git-practice`
`cd git-practice`
`code .`

3. vscode 打开了，新建一个hello.md文件，指令：
`touch hello.md`

4. 运行 `git status` 指令
![第一次运行git status](images\lecture1\121212.png)
发现出错，因为git尚未初始化。初始化就是指创建一个新的Git仓库。
所以运行 `git init` 。这是第一个指令，这样git就可以跟踪我们的更改了

5. 再次运行 `git status`
![再次运行git status](images\lecture1\121909.png)  
就可以看到正在跟踪这个文件夹下的所有文件
这会显示我们的更改以及它们是否暂存，还有git正在跟踪哪些文件

6. 运行 `git add .`
这是将工作目录中的所有更改添加到暂存区。
然后再运行 `git status` ，可以看到被跟踪的文件呈现出不同的颜色，这说明他们目前位于暂存区
![再次运行git status](images\lecture1\22031.png)

7. 返回vscode，然后再hello.md中随便写点什么，保存并返回终端输入 `git status` ，看到以下内容:![再次运行git status](images\lecture1\122457.png)
说明hello.md，readme.md已发生改变，且有一张刚存入的截图还未被跟踪，再运行 `git add .`、`git status`，可以看到都存入了暂存区
![再次运行git status](images\lecture1\122852.png)

8. 运行 `git commit -m "initial commit"` ，来提交这些更改。此命令允许我们保存更改并附加消息。
![运行git commit](images\lecture1\130622.png)

**需要注意的是，会经常用到 `git status`、`git add`、`git commit`指令，所以练习这些命令很重要。**

题外话：GitHub和Git是一个东西吗？
答案： NO ！！
Git是版本控制系统，用于跟踪文件更改; GitHub是一个平台，允许开发人员协作并将代码存储在云端。Git与GitHub共同协作，使软件的构建、扩展、保护和存储变得更加容易。

## Lecture 2
<!-- 需要知道的git command
git config 设置git配置值
git config --global user.name "xxx"
git config --global user.email "xxx@xxx"
将工作与xx的用户名和电子邮件关联起来
git config --list查看所有目前为止创建的所有设置
git config --global alias.i init 给指令起别名，git i将代替git init来创建一个新的git仓库

git init相当于一个打开git的开关，如果想查看在新的git仓库中到目前为止所做的工作，就可以使用 git status 。“untracked file”指的是尚未被添加到暂存区的文件，要向暂存区添加文件，就使用 git add 指令。

使用这个命令有几种方式，
git add . 将所有的文件同时添加到暂存区
git add [filename] 将特定文件添加到暂存区
文件添加到暂存区后，意味着在提交之前它们会得到妥善保管
git add相当于告诉git：“请跟踪此文件的当前状态”
如果对正在跟踪的文件进行了其他更改，需要再次使用git add，以便git跟踪这些新的更改。

做好更改后们就可以提交了，提交时将项目的某个版本存储在git历史记录中
git commit -m "initial commit"
通过运行git add 与 git commit -m来跟踪并保存工作中的更改

如果现在有个远程文件的链接，需要将其下载到你的笔记本上，该怎么办？git中成为克隆clone，也就是将远程仓库复制到本地，使用 git clone 完成
在远程仓库的主页中获得链接，打开终端，输入指令 `git clone https://github.com/xxxx/xxxx.git`

在与团队一起使用git仓库时，务必将更改添加到新分支（branch），分支就像创建文档的副本一样，这样就不会破坏原始文档，使团队合作更高效
`git check -b <branch name>`
这个命令创建一个新分支并同时切换到这个分支。
要查看拥有的分支列表： `git branch`
如果要切换到其他分支，使用 `git switch <branch name>`

使用分支对项目进行更改后，想把本地的更改同步到之前克隆的远程仓库中，就需要将更改推送（push）到远程仓库
git push相当于告诉git：“感谢你跟踪这些文件更改，现在我想将这些更改上传到主项目文件中。” 当推送更改时，是将本地存储库中已提交（commit）的内容更新到远程仓库中。
`git push <remote> <branch name>`
remote是指远程仓库，branch是指当前处理的分支
例如：git push origin xxx origin 是远程仓库，xxx是要上传的分支

我们可以在githun上发起拉取请求将我们的更改合并（merge）到住分支中，合并请求是指将一组更改从一个分支合并到另一个分支的请求。
例如将xxx分支下的更改合并到main分支中，合并过后，在终端切换到main分支，再将文件用vscode打开，不对！为什么没有变化？这是因为我们改变的是远程仓库的主分支，而不是本地副本。请记住本地仓库是远程仓库的副本或克隆，每个分支都有自己的历史记录。
由于我们在本地分支xxx上进行了更改，并推送到了远程仓库，因此我们需要在本地执行相同的操作，将我们的更改合并到主分支的本地副本中，我们可以用 git pull，用远程分支更新本地分支。此指令将获取所有更改并将他们合并到主分支。
在终端的主分支下，运行 pit pull，便可以更新本地主分支，获取到所有更改。git pull可以保持本地与远程仓库同步。

所以我们做了一系列改动，我们如何记录迄今为止所做的一切？可以使用 git show 指令。
git show 可以让我们查看到当前分支上所作的更改，这是了解项目历史的好方法。
在终端中，对主分支运行 git show，会显示很多信息：
commit id （也称为SHA）、提交消息的作者、时间和日期 以及对文件所做的实际内容更改（即diff）

至此，已具备作为专业人士使用Git的技能。练习这些指令，将成为更高效的Git用户。这就引出了所谓的GitHub 工作流程。GitHub flow是一种面向所有人的基于分支的工作流程，这意味着，无论何时你在代码仓库中工作，你都在遵循GitHub工作流程：
克隆了存储库，创建了一个新分支，在这个分支上进行了更改，再将该分支推送到GitHub，并提交了一个拉取请求，通常在这个阶段，我们会向队友征求对我们工作的反馈意见，并处理这些意见，所有问题解决后，我们将 PR 合并到主分支，然后删除我们的分支。

GitHub工作流程的最后一个阶段，删除我们的分支。
删除本地分支：`git branch -d <branch name>`
删除远程分支：`git branch --delete origin <branch name>` -->


### 一、Git 基础配置（git config）

在正式使用 Git 之前，需要先完成基本的用户信息配置，这些信息会出现在每一次提交记录中，用于标识提交者身份。

#### 1. 设置用户名和邮箱

```bash
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱"
```

* `--global`：表示对当前系统用户下的所有 Git 仓库生效
* 作用：将你的 Git 操作与用户名和电子邮件关联起来

#### 2. 查看当前所有 Git 配置

```bash
git config --list
```

用于查看目前为止创建的所有 Git 配置项。

#### 3. 设置 Git 命令别名

```bash
git config --global alias.i init
```

* 给 Git 指令起别名
* 之后可以使用 `git i` 代替 `git init`
* 提高日常操作效率

---

### 二、初始化仓库与状态查看

#### 1. 初始化 Git 仓库

```bash
git init
```

* 相当于“打开 Git 的开关”
* 在当前目录下创建一个新的 Git 仓库

#### 2. 查看仓库当前状态

```bash
git status
```

* 用于查看当前仓库中：

  * 哪些文件被修改了
  * 哪些文件尚未被跟踪（untracked）

**untracked file 的含义** 

* **untracked file**：尚未被 Git 跟踪的文件
* 需要通过 `git add` 将其加入暂存区

---

### 三、暂存区（Staging Area）与 git add

#### 1. 将文件添加到暂存区

Git 通过暂存区来管理即将提交的内容。

**常见用法**

```bash
git add .              # 添加所有文件到暂存区
git add <filename>     # 添加指定文件
```

#### 2. git add 的核心含义

* `git add` 相当于告诉 Git：

  > “请开始跟踪这个文件当前的状态”

* 文件进入暂存区后，表示它们会在下一次提交中被保存

⚠️ **注意**：

* 如果对已经被跟踪的文件再次进行了修改
* 需要重新执行 `git add`，Git 才能记录最新的更改

---

### 四、提交更改（git commit）

当所有需要的文件都已添加到暂存区后，就可以进行提交。

```bash
git commit -m "initial commit"
```

#### 提交的意义

* 将项目当前状态保存为一个版本
* 记录在 Git 的历史记录中
* 通过提交信息（commit message）说明本次修改内容

#### 常见工作流程

```bash
git add .
git commit -m "描述本次更改"
```

---

### 五、克隆远程仓库（git clone）

当你已经有一个远程 Git 仓库（例如 GitHub 上的项目），需要将其下载到本地时，可以使用 **clone**。

```bash
git clone https://github.com/xxx/xxx.git
```

* 将远程仓库完整复制到本地
* 包含所有分支与历史记录

---

### 六、分支（Branch）与团队协作

在团队协作中，**所有更改都应在新分支中进行**，避免直接影响主分支（main / master）。

#### 1. 创建并切换到新分支

```bash
git checkout -b <branch-name>
```

> 该命令同时完成：
>
> * 创建新分支
> * 切换到该分支

（在较新版本中，也可以使用 `git switch -c <branch-name>`）

#### 2. 查看当前所有分支

```bash
git branch
```

#### 3. 切换分支

```bash
git switch <branch-name>
```

#### 分支的核心思想

* 分支就像是项目的“副本”
* 在不影响主分支的情况下进行开发
* 提高团队协作效率与安全性

---

### 七、推送到远程仓库（git push）

当你在本地分支完成开发并提交后，需要将更改同步到远程仓库。

```bash
git push <remote> <branch-name>
```

#### 参数说明

* `remote`：远程仓库名称（通常是 `origin`）
* `branch-name`：要推送的分支名称

**示例**

```bash
git push origin xxx
```

#### git push 的含义

* 告诉 Git：

  > “我已经完成并提交了更改，现在请把这些提交上传到远程仓库”

⚠️ 注意：

* 只有 **已 commit 的内容** 才能被 push

---

### 八、Pull Request（合并请求）与 git pull

#### 1. 发起 Pull Request（PR）

在 GitHub 上将功能分支（如 `xxx`）的更改请求合并到主分支（如 `main`）

Pull Request 本质上是：

> 将一组更改从一个分支合并到另一个分支的请求

#### 2. 为什么本地主分支没有变化？

即使 PR 已在 GitHub 上合并成功：

* **远程主分支已更新**
* **本地主分支仍然是旧版本**

这是因为：

> 本地仓库只是远程仓库的一个克隆副本

#### 3. 使用 git pull 同步远程更改

```bash
git pull
```

* 获取远程分支的最新更改
* 并自动合并到当前本地分支

##### 正确操作流程

```bash
git switch main
git pull
```

`git pull` 可以保持本地仓库与远程仓库同步。

---

### 九、查看历史记录（git show）

当你想回顾项目历史或查看具体一次提交内容时，可以使用：

```bash
git show
```

#### git show 会展示的信息

* 提交 ID（SHA）
* 作者信息
* 提交时间和日期
* 提交说明（commit message）
* 实际修改内容（diff）

这是了解项目演进历史的非常重要的工具。

---

### 十、GitHub 工作流程（GitHub Flow）

GitHub Flow 是一种 **基于分支的协作流程**，适用于个人与团队开发。

#### 标准 GitHub Flow 流程

1. 克隆仓库（clone）
2. 创建新分支（branch）
3. 在分支上进行开发与提交（add + commit）
4. 推送分支到 GitHub（push）
5. 创建 Pull Request（PR）
6. 团队评审与修改
7. 合并 PR 到主分支（merge）
8. 删除分支（cleanup）

---

### 十一、删除分支（清理工作）

#### 1. 删除本地分支

```bash
git branch -d <branch-name>
```

#### 2. 删除远程分支

```bash
git branch --delete origin <branch-name>
```

（或常见写法：`git push origin --delete <branch-name>`）

---

## Lecture 3

**总结了视频中创建 GitHub Repository 时的关键概念、许可协议、Fork、.gitignore文件 以及仓库核心功能标签页**

---

### 一、为什么要选择许可协议（License）？

#### 1. 许可协议的本质

**许可协议（License）本质上是在法律层面告诉别人：**

* 他们 **可以** 对你的代码做什么
* 他们 **不可以** 对你的代码做什么

只要你的仓库是 **Public（公开）** 的，任何人都可以：

* 查看你的代码
* 下载（clone）你的代码
* 使用你的代码

但 **如何使用**，取决于你选择的许可证。

---

#### 2. 为什么创建仓库时要选择 License？

如果你不添加许可证：

* 法律上 **默认他人无权使用、修改或分发你的代码**
* 即使代码是公开的，也可能存在法律风险

👉 **选择 License = 明确授权规则，降低协作和使用成本**。

---

#### 3. 什么是 MIT 许可协议？为什么常选它？

MIT License 是一种**宽松型（Permissive）开源许可证**。

它的核心特点：

* ✅ 允许任何人使用、复制、修改、合并、发布、分发代码
* ✅ 可用于商业用途
* ❗ 唯一要求：

  * 保留原始许可证和版权声明

**你等于是在说：**

> 你可以随便用我的代码，怎么改都行，只要别删 License。

这也是为什么 **MIT 是 GitHub 上最常见的 License 之一**。

---

#### 4. License 在仓库页面里意味着什么？

当你在仓库中看到：

> License: MIT

表示：

* 这个仓库的代码受 MIT License 保护
* 使用者必须遵守 MIT 的条款

📌 **推荐工具**：

* [https://choosealicense.com](https://choosealicense.com)
* 用于了解不同许可证的区别，帮助你选择合适的 License

---

### 二、Fork 是什么？为什么要 Fork？

#### 1. Fork 的定义

**Fork = 基于现有仓库，复制一份到你自己的 GitHub 账户下**。

特点：

* 不是从零开始
* 保留原仓库的所有历史
* 你对 Fork 仓库的修改 **不会影响原仓库**

---

### 2. Fork 的典型使用场景

在开源协作中，常见流程是：

1. Fork 原仓库到自己账户
2. 在 Fork 仓库中修改代码
3. 提交 Pull Request（PR）
4. 原作者决定是否合并你的修改

👉 Fork 本质是一种 **“我基于你的成果继续构建” 的方式**。

---

### 三、.gitignore 文件是什么？为什么很重要？

#### 1. .gitignore 的作用

`.gitignore` 用于告诉 Git：

* 哪些文件 / 文件夹 **不需要被追踪（track）**

常见被忽略的内容：

* 编译产物（如 `.class`, `dist/`）
* 临时文件
* 日志文件
* 本地配置文件（如 `.env`）
* IDE 配置文件（如 `.idea/`、`.vscode/`）
* 系统文件（如 `.DS_Store`）

---

#### 2. 为什么 .gitignore 很重要？

* 防止无关文件污染仓库
* 避免提交敏感信息（如配置、密钥）
* 保持仓库干净、可维护

📌 **实用工具**：

* [https://gitignore.io](https://gitignore.io)
* 可根据语言和框架自动生成 `.gitignore` 模板

---

### 四、仓库页面核心功能标签说明

GitHub 仓库不仅是代码存储工具，也是一个 **协作与项目管理平台**。

---

#### 1. Issues

用途：

* 追踪 Bug
* 记录任务 / 功能需求
* 讨论问题

---

#### 2. Projects

用途：

* 项目管理
* 看板（Kanban）式任务管理
* To Do / In Progress / Done

适合：

* 小型项目
* 开源协作任务管理

---

#### 3. Pull Requests（PR）

用途：

* 合并不同分支的代码
* 接受 Fork 仓库的贡献

典型流程：

* Fork → 修改 → Pull Request → Review → Merge

---

#### 4. Fork

用途：

* 将他人的仓库复制到你自己的账户
* 用于二次开发或贡献代码

---

#### 5. Actions

用途：

* 自动化工作流（CI / CD）

例如：

* 自动测试
* 自动构建
* 自动部署

📌 基于 **GitHub Actions** 实现

---

#### 6. Wiki

用途：

* 项目文档
* FAQ
* 使用说明

⚠️ 如果你不打算使用：

* 可以在 Settings → Features 中直接关闭

---

#### 7. Security

用途：

* 查看和管理仓库的安全状态
* 依赖漏洞（Dependabot alerts）
* 安全策略（Security Policy）
* 漏洞报告入口

👉 主要面向：

* 开源项目
* 对安全性有要求的工程项目

---

### 7. Settings（设置）

Settings 主要用于**仓库层面的配置与管理**。

#### （1）Collaborators

* 管理协作者
* 控制谁可以访问和修改仓库

#### （2）Actions

* 配置自动化流程（CI / CD）

#### （3）Features

* 启用或禁用仓库功能（如 Wiki、Projects、Discussions 等）

👉 不用的功能可以关闭，保持仓库简洁。

---

## Lecture 4

**如何将本地文件或项目上传到 GitHub 仓库**，包括使用 GitHub 网页端（UI）和使用 Git 命令行两种方式。

---

### 一、使用 GitHub 网页端（UI）上传文件

这种方式适合：

* **快速上传少量文件**
* 不熟悉 Git 命令行的新手

#### 1. 创建一个新的仓库（Repository）

在 GitHub 上：

1. 点击 **New Repository**
2. 选择仓库所有者（Owner）
3. 输入仓库名称（Repository name）
4. 添加仓库描述（Description，可选）
5. 选择仓库权限：Public 或 Private
6. 勾选 **Initialize this repository with a README**
7. 点击 **Create repository**

#### 2. 上传文件或文件夹

1. 在仓库页面点击右上角 **“+”**
2. 选择 **Upload files**
3. 点击 **Choose your files**，选择要上传的文件或文件夹
4. 等待文件上传完成
5. 填写提交信息（Commit message，可使用默认）
6. 点击 **Commit changes**

✅ 优点：简单直观
⚠️ 缺点：不适合大型项目或频繁更新

---

### 二、使用 Git 命令行上传项目（推荐）

这种方式适合：

* **完整项目（多文件、多文件夹）**
* 后续需要持续更新代码

#### 1. 在 GitHub 上创建一个空仓库

1. 点击 **Create new repository**
2. 输入项目名称和描述
3. **不要勾选 README、.gitignore 或 license**（保持空仓库）
4. 点击 **Create repository**

创建完成后，GitHub 会显示一组 **终端命令提示**，用于将本地项目推送到远程仓库。

---

#### 2. 在本地初始化 Git 仓库

1. 打开终端（Terminal）
2. 进入你要上传的项目目录：

```bash
cd your_project_folder
```

3. 初始化 Git：

```bash
git init
```

---

#### 3. 创建 README 文件（推荐）

```bash
touch README.md
```

然后在 `README.md` 中写一个简短的项目说明。

---

#### 4. 添加并提交文件

1. 将所有文件添加到暂存区：

```bash
git add .
```

2. 提交文件：

```bash
git commit -m "Initial commit"
```

3. 可使用以下命令检查状态：

```bash
git status
```

---

#### 5. 设置主分支（main）

```bash
git branch -M main
```

---

#### 6. 关联远程仓库

```bash
git remote add origin <GitHub 仓库地址>
```

📌 这一步的含义是：

> 告诉 Git：本地仓库对应的远程仓库在哪里

---

#### 7. 推送代码到 GitHub

```bash
git push -u origin main
```

完成后，刷新 GitHub 仓库页面，即可看到所有文件已经成功上传 🎉

---

### 三、已有本地 Git 仓库的情况

如果你的项目 **之前已经执行过 `git init`**：

* **不需要再次执行 `git init`**
* 其余步骤完全相同：

  * 添加远程仓库
  * 提交代码
  * 推送到 GitHub

---

## Lecture 5

介绍 **GitHub Flow** 以及如何通过命令行和 GitHub Desktop 向仓库添加代码，并完成 Pull Request（PR）流程。

---

### 一、什么是 GitHub Flow

GitHub Flow 是一种常见且简单的 Git 协作流程，核心思想是：

* **主分支（main）始终保持稳定、可部署**
* 所有新功能或修改都在 **新分支（branch）** 上进行
* 通过 **Pull Request（PR）** 将代码合并回 main 分支

这样可以有效保护主分支，便于多人协作和代码审查。

---

### 二、使用命令行向仓库添加代码（Terminal Flow）

#### 1. 克隆远程仓库

首先，从 GitHub 上克隆仓库到本地：

```bash
git clone <仓库地址>
cd <仓库目录>
```

克隆完成后，默认位于 `main` 分支。

---

#### 2. 创建并切换到新分支

在开始编写代码前，创建一个新分支（例如：`version-one`）：

```bash
git checkout -b version-one
```

> 创建新分支是 GitHub Flow 中非常关键的一步，用于保护 main 分支。

---

#### 3. 打开项目并编写代码

如果使用 VS Code，可直接在终端中运行：

```bash
code .
```

随后开始编写代码。

例如创建 HTML 和 JavaScript 文件：

```bash
touch index.html script.js
```

在编辑器中补充所需代码内容。

---

#### 4. 查看文件状态

查看当前仓库状态：

```bash
git status
```

这一步可以确认哪些文件被修改或新建。

---

#### 5. 添加文件到暂存区（Stage）

将所有修改加入暂存区：

```bash
git add .
```

---

#### 6. 提交（Commit）代码

为本次修改创建提交记录：

```bash
git commit -m "created initial project"
```

提交信息应简洁且能说明本次修改内容。

---

#### 7. 推送分支到远程仓库

将本地分支推送到 GitHub：

```bash
git push origin version-one
```

此时，代码已经安全存储在远程仓库中。

---

#### 8. 创建 Pull Request（PR）

回到 GitHub 仓库主页，会看到提示：

> `version-one had recent changes`

点击 **Compare & Pull Request**，然后：

* 填写 PR 标题
* 添加修改说明（Summary）
* 点击 **Open Pull Request**

🎉 这样就成功创建了你的第一个 PR。

---

### 三、使用 GitHub Desktop 添加代码（GUI Flow）

视频中由 Christina 演示了使用 **GitHub Desktop** 添加 CSS 的流程。

#### 1. 克隆仓库

* 打开 GitHub Desktop
* 选择 **Clone a repository from the Internet**
* 输入仓库 URL 并完成克隆

---

#### 2. 创建新分支

在 GitHub Desktop 中：

* 创建一个新分支，例如：`CSS`

---

#### 3. 添加文件并保存

* 创建 `style.css`
* 将文件保存到仓库目录中（可通过编辑器或文件管理器）

GitHub Desktop 会自动检测到文件变化。

---

#### 4. 提交并推送代码

在 GitHub Desktop 中：

* 填写提交信息（如：`create styling`）
* 点击 **Commit to CSS**
* 然后 **Push** 到远程仓库

此时可以在 GitHub 上创建对应的 PR。

---

### 四、同步他人代码到本地分支（Merge Flow）

当其他协作者（如 Christina）已经向远程仓库提交了代码，需要同步到自己的分支。

#### 1. 切换到 main 分支并拉取更新

```bash
git switch main
git pull
```

这一步会将远程的最新代码（如 CSS）拉到本地 main 分支。

---

#### 2. 将 main 分支合并到自己的功能分支

```bash
git switch version-one
git merge main
```

这样，其他人提交的代码就被合并进了你的当前分支。

---

#### 3. 推送并完成合并

合并完成后，再次推送分支并在 GitHub 上完成最终合并（Merge）。

---

### 五、完整 GitHub Flow 总结

**标准流程如下：**

1. 从 main 创建新分支
2. 在新分支上编写代码
3. 提交（commit）并推送（push）到远程
4. 创建 Pull Request
5. 审查并合并到 main
6. 同步最新 main 到本地

---

### 六、一些问题及思考

> 以下问题来自初学 GitHub Flow 时**最容易产生混淆的关键点**，用于帮助真正理解分支、PR 与 merge 的关系。

---

#### Q1：为什么要先切换到 `main` 再拉取更新？不能直接在功能分支拉吗？

**简要结论**：

* 技术上：可以直接在功能分支拉取
* 规范上：推荐先更新 `main`，再用 `main` 更新功能分支

**原因解释**：

* `main` 被视为项目的**权威时间线（source of truth）**
* 先让本地 `main` 与远程 `origin/main` 保持一致
* 再将 `main` 的最新状态合并进自己的功能分支

这样可以：

* 提前发现冲突
* 保证功能分支基于最新项目状态
* 让 PR 更干净、可预测

---

#### Q2：Christina 的代码不是在 `CSS` 分支吗？为什么后来会在 `origin/main`？

**关键理解**：

* 分支不是文件夹，而是**指向提交的指针**
* Christina 最初确实在 `CSS` 分支写代码
* 但当她的 **PR 被 merge** 后：

> 她的提交已经成为 `main` 时间线的一部分

因此：

* `origin/main` 包含了 CSS 代码
* `origin/CSS` 可能仍存在，但已不再是“官方来源”

---

#### Q3：push 完代码后，可以直接 merge 吗？

**标准 GitHub Flow：不建议**。

正确顺序是：

```text
git push
→ 创建 Pull Request
→ 检查 / Review
→ Merge 到 main
```

原因：

* merge 代表“代码正式成为项目版本的一部分”
* PR 是最后的安全检查与对比窗口

个人练习项目中可以简化，但在协作中应始终通过 PR。

---

#### Q4：merge 前发现冲突怎么办？

**推荐做法：在本地解决冲突**

流程：

```bash
git switch main
git pull
git switch version-one
git merge main
```

若出现冲突：

* 打开冲突文件
* 手动决定保留/合并哪段代码
* 删除冲突标记（`<<<<<<< ======= >>>>>>>`）
* `git add` + `git commit`

解决后再 push，PR 会自动更新。

---

#### Q5：PR 到底是什么？出现在哪个环节？

**一句话定义**：

> Pull Request 是 GitHub 提供的“合并申请 + 对比 + 审核”机制

**位置非常固定**：

```text
git push
→ 【PR】
→ Merge
```

* PR 不是 Git 命令
* 只存在于 GitHub / GitLab 等平台
* PR ≠ merge，而是 merge 之前的决策窗口

---

#### Q6：别人的代码必须 PR 且 merge 之后，我才能拿到吗？

**不必须。**

只要代码存在于远程分支，你就可以获取。

例如 Christina 在网页向 `CSS` 分支上传文件，但未 PR：

你可以：

* 直接切换分支查看：

```bash
git fetch
git switch CSS
```

* 或合并进你的功能分支：

```bash
git fetch
git switch version-one
git merge origin/CSS
```

**PR 只决定：是否进入 main**，
**不决定：你能不能拿到代码**。

---

### 七、核心理解总结

* 分支 = 提交指针，不是文件夹
* PR = 合并申请，不是代码本身
* merge = 正式进入 main
* main = 项目当前“官方状态”

> **代码是否可信，看它在不在 main；
> 代码是否能拿到，看它在哪个分支。**

---

## Lecture 6

Pull Request 是 GitHub 协作开发的核心流程。

### 一、什么是 Pull Request（PR）

Pull Request（PR）是指**将一个分支中的修改，提议合并到另一个分支**的一种协作方式。

作用：

* 在合并前进行代码审查和讨论
* 清晰展示分支之间的代码差异（diff）
* 提高代码质量，降低错误风险

---

### 二、使用 Git 创建 Pull Request（核心流程）

#### 1️⃣ 创建并切换到新分支

```bash
git clone <repo-url>
git checkout -b update-name
```

---

#### 2️⃣ 修改代码并提交

```bash
git add .
git commit -m "update game name"
```

---

#### 3️⃣ 推送分支到 GitHub

```bash
git push origin update-name
```

---

#### 4️⃣ 在 GitHub 上创建 PR

* 打开仓库页面
* 点击 **Compare & Pull Request**
* 选择：

  * Base：目标分支（如 `main`）
  * Compare：当前分支（如 `update-name`）
* 填写标题和描述
* 创建 Pull Request（或 Draft PR）

---

#### 5️⃣ Review 并合并

* 邀请他人 Review
* Review 通过后合并到主分支

---

### 三、Pull Request 三个最佳实践

1. **PR 要小**：小改动更容易 Review，也更安全
2. **先自查**：提交前自己先 Build / Test / Review
3. **写清楚说明**：

   * 修改目的（Why）
   * 修改内容（What）
   * 相关 Issue / 文档链接

---

## Lecture 7
如何在 GitHub 上合并第一个 Pull Request（PR），以及如何处理常见的 **Merge Conflict（合并冲突）**。

---

### 一、Pull Request（PR）是什么？

在开始之前，先快速回顾 Pull Request 的概念。

**Pull Request（简称 PR）** 是一种请求，表示你希望将 **一个分支中的更改合并到另一个分支**（通常是 `main` 或 `master` 分支）。

PR 的核心作用包括：

* 提议合并代码变更
* 让团队成员进行 **代码审查（Code Review）**
* 在合并前发现问题、讨论改进方案

---

### 二、Pull Request 的基本流程

一个完整的 PR 流程通常包括以下步骤：

1. 在本地或远程创建一个新分支
2. 在该分支中进行代码修改
3. 将修改推送到 GitHub 仓库
4. 在 GitHub 上创建 Pull Request
5. 邀请团队成员进行代码审查
6. 根据反馈修改代码
7. 所有问题解决后，合并 PR

当所有审查意见（requested changes）都被解决后，就可以点击 GitHub 页面上的 **Merge** 按钮，将 PR 合并到目标分支。

---

### 三、什么是 Merge Conflict（合并冲突）？

在实际开发中，你**几乎一定会遇到合并冲突**。

#### 1. 合并冲突的定义

**Merge Conflict（合并冲突）** 发生在以下情况：

* 两个不同的分支
* 对 **同一个文件的同一部分（同一行或相邻区域）**
* 做了不同的修改

Git 无法自动判断该保留哪一份修改，于是就会提示冲突。

> ⚠️ 注意：
> 在 GitHub 上，**所有合并冲突必须被解决，PR 才能被合并**。

---

### 四、冲突示例说明

假设当前存在以下情况：

* 一个 PR 来自 `update-name` 分支
* 该分支修改了某个文件中的一行内容

此时，如果你：

1. 在本地创建了一个新分支（例如 `add-new-name`）
2. 在 **同一个文件的同一行** 也进行了修改
3. 将该分支的 PR 合并进了 `main`

那么，当你回到最初的 `update-name` PR 时，就会看到 GitHub 提示：

> ⚠️ This branch has conflicts that must be resolved

这就是一个典型的 **合并冲突场景**。

---

### 五、解决 Merge Conflict 的两种方式

GitHub 提供了两种解决冲突的方式：

1. **直接在 GitHub 网页端解决冲突**
2. **在本地使用 Git 命令行解决冲突（推荐）**

本教程主要演示的是 **终端方式（Terminal Route）**。

---

### 六、使用终端解决合并冲突（推荐流程）

以下是完整的命令行解决流程。

#### Step 1：切换到 main 分支

```bash
git switch main
```

#### Step 2：拉取远程 main 分支的最新代码

```bash
git pull origin main
```

> 这一步的目的是：
> 获取已经被合并到远程 `main` 分支中的最新更改。

---

#### Step 3：切回发生冲突的分支

```bash
git switch update-name
```

---

#### Step 4：将 main 分支合并到当前分支

```bash
git merge main
```

此时，Git 会提示存在冲突，并在冲突文件中插入 **冲突标记（conflict markers）**，类似：

```text
<<<<<<< HEAD
当前分支的改动
=======
main 分支的改动
>>>>>>> main
```

---

#### Step 5：手动解决冲突

你需要：

* 打开冲突文件
* 决定保留哪一部分代码

  * 例如选择 **Accept Current Change**（保留当前分支的修改）
* 删除冲突标记
* 保存文件

---

#### Step 6：提交解决后的结果

```bash
git add .
git commit -m "resolve merge conflict"
```

---

#### Step 7：检查当前状态（推荐）

```bash
git status
```

如果看到 working tree clean，说明冲突已成功解决。

---

#### Step 8：推送修复后的分支到远程

```bash
git push origin update-name
```

---

### 七、在 GitHub 上完成合并

回到 GitHub 的 Pull Request 页面：

* 冲突提示将会消失
* 绿色的 **Merge** 按钮重新可用

此时，你就可以 **安全地合并 PR** 了 🎉

---

合并冲突是 **正常现象，而不是错误**。不要害怕它，理解它、解决它，才是开发者成长的重要一步。

## Lecture 8

介绍了 **如何提升 GitHub 账户安全性（开启两步验证）** 以及 **如何创建和美化 GitHub 个人主页 README**。

---

### 一、第一步：保护你的 GitHub 账号（2FA）

#### 为什么要开启 2FA？

* 单一密码容易被破解或复用泄露
* 2FA（两步验证）能显著提升账号安全性

#### GitHub 支持的 2FA 方式

* 认证器 App（推荐）
* 短信 / SMS
* GitHub Mobile
* 硬件安全密钥

#### 使用认证器 App 开启 2FA（流程）

1. 下载认证器（如 Microsoft / Google Authenticator）
2. GitHub → **Settings** → **Password and authentication**
3. 点击 **Enable two-factor authentication**
4. 扫描二维码 → 输入验证码
5. **下载并妥善保存 Recovery Codes（非常重要）**

✅ 完成后，你的 GitHub 账号安全性将大幅提升。

---

### 二、第二步：创建 GitHub Profile README

#### 什么是 Profile README？

* GitHub 个人主页顶部展示的「关于我」
* 相当于你的 **技术名片 / 迷你作品集**

#### 创建规则（关键）

> 仓库名 **必须与你的 GitHub 用户名完全一致**

例如：

* 用户名：`yourname`
* 仓库名：`yourname`

#### 创建步骤

1. 新建仓库（Public）
2. 勾选 **Initialize with README**
3. GitHub 会提示：这是一个特殊仓库
4. 编辑 README（使用 Markdown）

你可以加入：

* 自我介绍
* 技术栈 / 工具
* 项目或学习方向
* GitHub 数据统计
* 图片、GIF、徽章（Badges）

---

### 三、自己找到的一些 GitHub Profile README 模板

#### 1️⃣ 官方&社区精选

* [https://github.com/abhisheknaiidu/awesome-github-profile-readme](https://github.com/abhisheknaiidu/awesome-github-profile-readme)

  > ⭐ 最全合集，收录大量高质量 Profile README 示例

#### 2️⃣ 简洁专业风（程序员常用）

* [https://github.com/rzashakeri/beautify-github-profile](https://github.com/rzashakeri/beautify-github-profile)
* [https://github.com/rahuldkjain/github-profile-readme-generator](https://github.com/rahuldkjain/github-profile-readme-generator)

#### 3️⃣ 自动生成工具（新手友好）

* [https://rahuldkjain.github.io/gh-profile-readme-generator/](https://rahuldkjain.github.io/gh-profile-readme-generator/)

  > 填表生成 README，无需手写 Markdown

#### 4️⃣ GitHub 数据统计组件

* [https://github.com/anuraghazra/github-readme-stats](https://github.com/anuraghazra/github-readme-stats)
* [https://github.com/DenverCoder1/github-readme-streak-stats](https://github.com/DenverCoder1/github-readme-streak-stats)

#### 5️⃣ 徽章 / 技术栈图标

* [https://github.com/Ileriayo/markdown-badges](https://github.com/Ileriayo/markdown-badges)
* [https://shields.io/](https://shields.io/)

---
