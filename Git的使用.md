#### 一、关于git版本控制系统

##### 1.1 版本控制系统

1. 含义：版本控制系统（Version Control System，VCS）是一种软件，可以帮助软件团队的开发人员**协同工作**，并存档他们工作的完整历史记录

2. 分类：![img](https://ttt-pictures.oss-cn-hangzhou.aliyuncs.com/v2-a65cce9395b52fd175d9891a05d1b840_r.jpg)

##### 1.2 Git

Git是一个开源的分布式版本控制系统，可以有效、高速的处理从很小到非常大的项目版本管理，是现在最流行的版本控制系统。



#### 二、下载安装Git

##### 2.1 下载git

【下载地址】： https://git-scm.com/download

下载系统对应版本即可。`window64`下载如下版本：

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006231322553.png" alt="image-20231006231322553" style="zoom:50%;" />



##### 2.2 点击安装==>`Next`

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006232524128.png" alt="image-20231006232524128" style="zoom:80%;" />



==后面几乎都是一路next，嫌麻烦可以跳过这一part，安装完成后直接进入第三部分==

##### 2.3 选择组件

- 可选：添加一个桌面图标
- 可选：在windows终端添加一个git选项

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006232650948.png" alt="image-20231006232650948" style="zoom:80%;" />



##### 2.4 选择Git的默认编辑器

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006233045532.png" alt="image-20231006233045532" style="zoom:80%;" />



##### 2.5 选择执行git init命令时创建的分支名

- 默认即可

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006233212287.png" alt="image-20231006233212287" style="zoom:80%;" />



##### 2.6 设置环境变量

- 默认即可

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006233413263.png" alt="image-20231006233413263" style="zoom:80%;" />



##### 2.8 选择SSH连接工具

- 默认即可

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006233504694.png" alt="image-20231006233504694" style="zoom:80%;" />



##### 2.9 选择在加密连接时使用的证书

- 默认即可

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006233603249.png" alt="image-20231006233603249" style="zoom:80%;" />



##### 2.10 配置行尾符号转换

- 默认即可

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006233649909.png" alt="image-20231006233649909" style="zoom:80%;" />



##### 2.11 配置终端模拟器以与Git Bash一起使用

- 默认也可

- 选项一：“使用 MinTTY（ MSYS2 的默认终端）”
  - 优点：窗口可调整大小，非矩形文本选择和显示 Unicode 字体。

- 选项二：“使用 Windows 的默认控制台窗口”。Git 将使用 Windows 的默认控制台窗口cmd.exe
  - 优点：可以与 Windows 控制台程序（如交互式 Python 或 node.js ）一起使用
  - 缺点：默认的回滚非常有限，需要配置 Unicode 字体才能正确显示非 ASCII 字符，并且在 Windows 10 之前，其窗口不能自由调整大小，并且只允许矩形文本选择

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006233703962.png" alt="image-20231006233703962" style="zoom:80%;" />



##### 2.12 使用git pull命令时默认的模式

- 默认即可

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006234014039.png" alt="image-20231006234014039" style="zoom:80%;" />



##### 2.13 是否启用 `credential helper` 登录凭证管理助手

- 默认即可

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006234046976.png" alt="image-20231006234046976" style="zoom:80%;" />



##### 2.14 配置额外的选项

- 默认即可

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006234141332.png" alt="image-20231006234141332" style="zoom:80%;" />



##### 2.15 是否启用新的实验功能。点击`install`

- 默认不选择，如果想尝试新功能，官网查阅资料即可

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006234151855.png" alt="image-20231006234151855" style="zoom:80%;" />



##### 2.16 开始安装，等待片刻，点击`finish`

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006234446935.png" alt="image-20231006234446935" style="zoom: 60%;" />





## 三、连接Git和Github

#### 3.1 进入Git Bash

在桌面右键鼠标 ==> 点击 `显示更多选项` ==> `Open Git Bash here`

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006234432693.png" alt="image-20231006234432693" style="zoom: 67%;" />

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006234633065.png" alt="image-20231006234633065" style="zoom:67%;" />

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006234744546.png" alt="image-20231006234744546" style="zoom:67%;" />



#### 3.2 配置 Git 用户信息

- 用户名：`github`用户名
- 邮箱：`github`账户邮箱
- 注：**引号**也要加上

```bash
$ git config --global user.name "用户名"
```

```bash
$ git config --global user.email "邮箱"
```



#### 3.3 检查是否配置成功

可以使用如下两条命令查看Git用户信息

- 获取当前用户名

```bash
$ git config user.name
```

- 获取当前邮箱

```bash
$ git config user.email
```



#### 3.4 配置ssh连接

基于GIt的代码托管平台例如Github，Gitlab，Gitee等，都提供了基于 SSH 协议的 Git 服务，使用SSH公钥可以让你的电脑和Git远程仓库建立安全连接。

##### 3.4.1 windows系统

在git bash中输入如下命令生成SSH KEY

- 引号内的内容可以随意填写。直接把下面的命令复制过去，不做任何修改也行。

```bash
$ $ ssh-keygen -t rsa -C "XXXXX.com"
```

- 进入C:/users/用户名/.ssh目录。发现其中多了两个文件：`id_rsa`和`id_rsa.pub`

  <img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006235724437.png" alt="image-20231006235724437" style="zoom: 80%;" />

- 用记事本打开`id_rsa.pub`文件

  <img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231006235842982.png" alt="image-20231006235842982" style="zoom:80%;" />

- 将**id_rsa.pub**的内容复制到Github的**SSH keys**当中

  - 进入`github`的`setting`界面

  - 点击左侧的`SSH and GPG keys`
  - 点击`New SSH key`

  ![](https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-2023052013121341.png)

  

  - 将刚刚从**id_rsa.pub**中复制的内容粘贴到Github的**Key**中，设置`title`，点击`Add SSH key`

    - `Title`可以自己填写

    <img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231007000250797.png" alt="image-20231007000250797" style="zoom:60%;" />

  

##### 3.4.2 Linux系统

- `Ubuntu`环境下安装ssh
  
  ```bash
  sudo apt install ssh
  ```
  
- 查看主目录下有没有**.ssh**这个隐藏文件
  
  ```bash
  ls -ah
  ```
  
- 若没有，则生成SSH KEY（引号内的内容可以随意填写）

  ```bash
  ssh-keygen -t rsa -C "XXXXX.com"
  ```

- 进入 **/root/.ssh**目录，查看**id_rsa**和**id_rsa.pub**文件

- 将**id_rsa.pub**的内容复制到Github的**SSH keys**当中（同windows）



## 四、常用 git 命令

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231007005114934.png" alt="image-20231007005114934" style="zoom:80%;" />

##### 4.1 ` git add`将工作区的修改添加到本地暂存区

- 添加所有修改

```bash
$ git add .
```

- 添加对某个文件的修改

```bash
$ git add <文件名>
```

##### 4.2 `git commit`将暂存区的修改提交到本地版本库

- 引号中需要填写此次修改的描述

```bash
$ git commit -m "添加修改信息"
```

##### 4.3 `git push`将本地版本库中的修改提交到github远程仓库中

```bash
$ git push
```

##### 4.5 `git status`查看文件的状态

```bash
$ git status
```

##### 4.6 `git branch`管理分支

- 列出所有分支

```bash
$ git branch
```

- 创建新的分支

```bash
$ git branch <branch_name>
```

- 删除分支

```bash
$ git branch -d <branch_name>
```

##### 4.7 `git checkout`切换分支

```bash
$ git checkout <branch_name>
```

##### 4.8 从远程库中克隆文件到本地文件夹

```bash
$ git clone <url> [directory]
```

- url可以通过ssh、http获取
  - 进入项目==>`Code` ==> `SSH/Http` ==> 复制即可
- 如果不填写directory就是默认在当前文件夹存储克隆的文件

<img src="https://raw.githubusercontent.com/fograinwater/PicGo-img/master/image-20231007002558235.png" alt="image-20231007002558235" style="zoom:50%;" />

##### 4.9 `git fetch`

- 将某个远程主机的更新全部取回本地

```bash
$ git fetch <远程主机名>
```

- 只拉取特定分支的更新

```bash
$ git fetch <远程主机名> <分支名> //注意之间有空格
```

- 查看远程主机分支的最新状态

```bash
$ git log -p FETCH_HEAD
```

##### 4.10 `git pull`

将远程主机的某个分支的更新取回，并与本地指定的分支合并。

相当于git fetch+git merge。

```bash
$ git pull <远程主机名> <远程分支名>:<本地分支名>
```



## 五、其他 git 命令

#### 5.1 创建本地仓库

##### 5.1.1 在本地电脑上选择一个合适的位置创建一个空目录作为仓库

```bash
$ mkdir learngit
```

##### 5.1.2 进入目录，点击右键打开Git bash窗口，执行`git init` 将其变成Git可以管理的仓库

```bash
$ git init
```

- 同时可以发现当前目录下多了一个`.git`的目录（一般是隐藏文件），这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件



#### 5.2 远程仓库

##### 5.2.1 在github上创建一个仓库，比如名为`Android`

##### 5.2.2 `git remote`关联远程库

远程库的名字就是`origin`

```bash
$ git remote add <shortname> <url>
```

- 举例：

```bash
$ git remote add origin git@github.com:fograinwater/Android.git
//$ git remote add origin https://github.com/tugenhua0707/testgit
```

##### 5.2.3 `git push`把当前main / master分支推送到远程库

```bash
$ git push -u <short_name> <your_branch_name>
```

举例：

```bash
$ git push origin main:main
$ git push –u(第一次要用-u 以后不需要) origin master//把当前master分支推送到远程库
```

由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`**分支关联**起来，在以后的推送或者拉取时就可以简化命令

##### 5.2.4 从远程库中克隆文件

- 可以使用ssh

```bash
$ git clone git@github.com:fograinwater/Android.git
```

- 也可以使用http

```bash
$ git clone https://github.com/fograinwater/Android.git
```

##### 5.2.5 查看远程库信息

```bash
$ git remote -v
```

##### 5.2.6 删除远程库

```bash
$ git remote rm <name>
```

“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库

##### 5.2.7 克隆远程库到本地库

```bash
$ git clone git@github.com:fograinwater/Android.git
```



#### 5.3 分支管理（简）

```bash
$ git branch //查看本地所有分支 

$ git branch -r //查看远程所有分支

$ git branch -a //查看本地和远程的所有分支

$ git branch <branchname> //新建分支

$ git branch -d <branchname> //删除本地分支

$ git branch -d -r <branchname> //删除远程分支，删除后还需推送到服务器
$ git push origin:<branchname>  //删除后推送至服务器

$ git branch -m <oldbranch> <newbranch> //重命名本地分支
```



#### 5.4 其他

##### 5.4.1 查看文件修改详情

`git diff <filename>`

##### 5.4.2 显示提交日志

`git log`

- 只显示简要的日志信息

​	`git log --pretty=oneline`

（前面显示的一串数字是`commit id`）

##### 5.4.3 把文件回退到历史版本

- 利用HEAD回退

  `HEAD`：当前版本

  `HEAD^`：上一个版本

  `HEAD^^`：上上个版本

  `HEAD~100`：第前100个版本

  

  如回退到上一个版本：

  `git -reset  --hard HEAD^`

- 利用`commit id `回退

  `git reset --hard <commit id>`（一般而言commit id只需要写出前几位即可，git可以自动查找）

##### 5.4.4 显示可引用的历史版本记录

`git reflog`

**可引用历史提交版本，什么意思？**

- 使用`git log`命令只可以查看到HEAD指针及其之前的版本信息，如果版本发生过回退操作，则可能会出现，HEAD指针之后仍存在历史提交版本的情况，而这些提交版本信息通过`git log`命令是看不到的。

  【即：`git log`命令是显示当前的`HEAD`和它的祖先，递归是沿着当前指针的父亲，父亲的父亲，……，这样的原则】

- 我们可以通过使用`git reflog`命令，就可查看到所有历史版本信息。由于查看所有历史版本信息的目的，大多是为了进行版本回退或恢复操作所使用，从中找到所需的commit索引，所以该命令被命名为`reflog`(reference log)，即：引用日志。

- `	git log`命令与`git reflog`命令作用范围示意图：

<img src="https://upload-images.jianshu.io/upload_images/2495229-b7cefe27813a4489.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp" alt="img" style="zoom: 80%;" />

- `reflog`并不是Git仓库的一部分，它单独存储，它纯属是本地的

- `git reflog`命令显示的内容，应该是存储在`.git/logs/HEAD`文件中，或者是`.git/logs/refs`目录中的文件，也就是说`git reflog`命令中保留了从clone仓库开始，用户所有在本地库中的操作。

##### 5.4.5 把文件在工作区的修改全部撤销

（在工作区内误改、误删了文件）

`git checkout -- readme.txt`

##### 5.4.6 把暂存区的修改撤销掉（unstage），重新放回工作区

（在工作区内误改了文件，并add进了缓存区）

`git reset HEAD <file>`

然后根据步骤6将工作区中的修改删除



## 六、工作区与暂存区

<img src="https://ttt-pictures.oss-cn-hangzhou.aliyuncs.com/image-20230521145914378.png" alt="image-20230521145914378" style="zoom: 67%;" />

<img src="https://ttt-pictures.oss-cn-hangzhou.aliyuncs.com/image-20230521143744413.png" alt="image-20230521143744413" style="zoom: 50%;" />



<img src="https://ttt-pictures.oss-cn-hangzhou.aliyuncs.com/o_220208040230_91-484624131.png" alt="img" style="zoom:67%;" />

1. 工作区：当前操作的目录（文件夹）
2. 版本库：.git目录

- 暂存区（stage/index）：存放add进来的所有修改
- HEAD
- master

`git commit`只负责把暂存区的修改提交了，如果某些修改没有通过`git add`加入到暂存区中，则无法通过`git commit`提交到本地库中



## 七、分支管理

##### 1.查看分支

`git branch`

##### 2.创建分支

`git branch <name>`

##### 3.切换分支

`git checkout <name>`或者`git switch <name>`

##### 4.创建+切换分支

`git checkout -b <name>`或者`git switch -c <name>`

##### 5.合并某分支到当前分支

`git merge <name>`

- 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成
- 解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交
- 用`git log --graph`命令可以看到分支合并图
- 合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并

##### 6.删除分支

`git branch -d <name>`

##### 7.将当前工作区（分支）的修改储藏来实现清空工作区

`git stash`

##### 8.开发一个新feature，最好新建一个分支

- 如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除

##### 9.多人协作

- 查看远程库信息，使用`git remote -v`；
- 本地新建的分支如果不推送到远程，对其他人就是不可见的；
- 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
- 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
- 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
- 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。



## 九、标签管理

标签实际上是版本库的快照，跟某个commit绑在一起

标签的创建和删除都是瞬间完成的

默认标签是打在新提交的commit上的

##### 1.创建标签

- 创建普通标签

  - 先切换到需要打标签的分支上

    `git checkout master`

  - 打标签

    `git tag <tagname>`

- 创建带有说明的标签

  `git tag -a <tagname> -m <说明文字>`

- 在历史commit上创建标签

  `git tag <name> <commit id> ` 

##### 2.**查看所有标签**

`git tag`

##### 3.查看标签信息

`git show <tagname>`

##### 4.删除标签

`git tag -d <tagname>`

##### 5.将标签push到远程仓库

- push单个标签

  `git push origin <tagname>`

- push所有尚未推送到远程的本地标签

  `git push origin --tags`

##### 6.删除远程仓库中的标签

`git push origin :refs/tags/<tagname>`



