[toc]


# 1. Git究竟是什么？？
- 为什么git容易让人迷惑？？
- 究竟是哪些点产生的这些迷惑？？
- 为什么git会让人觉得很复杂？？

## 何为 版本控制 ？？

## 何为 版本控制软件？？

## 何为分布式版本控制软件？？


# 2. Git环境配置
1. 下载-安装
[官方](https://git-scm.com/download/win)
使用国内镜像下载更快
[镜像](https://npm.taobao.org/mirrors/git-for-windows/)

2. 测试安装成功
```
king-kong@DESKTOP-MJEHNBQ MINGW64 ~
$ which git
/mingw64/bin/git

king-kong@DESKTOP-MJEHNBQ MINGW64 ~
$ git --version
git version 2.31.1.windows.1
```

3. congratulations ! success installed ! have fun!


# 3. 设置Git(命令行版)
1. 用户配置
- 设置全局用户  使用--global
```
$git config --global user.name "nuomikang"
$git config --global user.email "811632930@qq.com"
```

- 设置局部用户
```
$git config --local user.name nuomikang
$git config --local user.email 811632930@qq.com
```

- 为什么local版的不用加 " "

2. git配置文件的位置
- 不管是终端机or图形界面完成的配置 --> 所有Git相关的设置都默认保存在自己账号下的.gitconfig文件
- 使用外部的文字编辑器手动修改该文件也有一样的效果

- .gitconfig 为什么在 C:\Users\king-kong这个目录下？
- 
3. 其他的设置
- 更换编辑器, 不一定非要用vim，vim的非人性化设计之一能活是历史原因
```
$git config --global core.editor emacs
```

- 设置缩写
	- 手动在 ~/.gitconfig中更改
	- 使用命令+alias更改
```
$git config --global alias.co checkout
$git config --global alias.br branch
$git config --global alias.st status
$git config --global alias.l "log --online --graph"

// alias设置时一定要加上
// 使用时不用加上alias
$git st
$git co
```

# 4. 开始使用Git
## 全新的开始
### 1. 对目录开启控制
1. 创建一个新目录，使用git对这个目录进行版本控制
- git一旦正确安装好后，可以在cmd+powershell进行使用，不一定非要用git bash
```
// 在cmd中运行命令
PS C:\>mkdir git-first
PS C:\git-first>cd git-first
// 对目录进行版本控制
PS C:\git-first>git init
PS C:\git-first>cd .git
PS C:\git-second\.git>ls
```

- git init 后会生成一个 .git 隐藏目录

2. 对本来就存在的目录，开启版本控制
- 进入目录
- git init

3. 取消对目录的版本控制
- git的版本控制全靠.git目录在做事 -> 移除.git隐藏目录 -> 解除版本控制
- 整个项目目录中哪一个文件or目录被删除均能找回，只有.git目录一旦被删除就没办法找回

### 2. 


#### 文件 -> 缓存区
1. 将文件交给git控制
- git add filename(含后缀的)
```
PS C:\git-second> git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        welcome.html

nothing added to commit but untracked files present (use "git add" to track)

PS C:\git-second> git add welcome.html
PS C:\git-second> git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   welcome.html

PS C:\git-second>
```

2. 文件的几种状态
- Untracked file：未加入控制的
- new file：表明文件进入了暂存区(Staging Area),稍后会与其他文件一起被存储到存储库中
3. 一次add一个 -> add all -> 灵活add
- git add welcome.html
- git add --all && git add .
	- git add --all 不管在哪一个目录下，均是将all 新增文件、改动文件、删除文件加入 暂存区
	- git add . 只会将所在目录的 当前目录、子目录、子子目录、子..目录中的全部加入进去
- git add *.html

4. 对加入缓存区的文件再次编辑 -> 实际会产生一个副本，对副本进行编辑 -> 必须对这个文件再次 git add 否则更改后的不会进入缓存区
- 后进入缓存区的会覆盖掉同名的先进入缓存区的吗?

#### 缓存区 -> 存储库 (归档)(永远保存下来)
1. git commit
- git commit -m “此处填写对归档的文件进行的描述”
- -m 后的信息很重要，不填写这个信息无法vommit成功
	- 强制对这次存储的版本进行说明

2. 每次git commit只会存储暂存区中的内容
3. 二段式
- 二段式 -> 一端式
	- git commit -a -m "descript here"
	- -a参数只对已在repository中的文件有效，对新加入的文件(Untracked files)无效
- 二段式的好处
	- 防止每一个文件都进行commit带来的commit繁琐 -> 聚成小堆再commit
	- 实际意义，因为一个项目版本往往会含有多个文件，他们作为一个时间节点的整体
	- 

4. 如果commit之前不配置用户，会报下面的错误
```
PS C:\git-second> git add index.html
PS C:\git-second> git commit -m "di er ci"
Author identity unknown

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got 'king-kong@DESKTOP-MJEHNBQ.(none)')
PS C:\git-second>
```
#### 查看之前commit的记录
1. 使用git log
```
PS C:\git-second> git config --global user.email "811632930@qq.com"
PS C:\git-second> git commit -m "di 2 ci"
[master (root-commit) b826e08] di 2 ci
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 index.html
 create mode 100644 welcome.html
PS C:\git-second> git log
commit b826e08ac4a03409e88a3026ea5aa8fb49ad7c1b (HEAD -> master)
Author: nuomikang <811632930@qq.com>
Date:   Fri Apr 30 02:32:43 2021 +0800

    di 2 ci
PS C:\git-second>
```

2. git log --oneline 排成一行查看
```
PS C:\git-second> git log
commit b826e08ac4a03409e88a3026ea5aa8fb49ad7c1b (HEAD -> master)
Author: nuomikang <811632930@qq.com>
Date:   Fri Apr 30 02:32:43 2021 +0800

    di 2 ci
PS C:\git-second> git log --oneline
b826e08 (HEAD -> master) di 2 ci
PS C:\git-second>
```
#### 智能查看commmit
1. 查找__某个人__的commit
- git log --oneline --author="nuomikang"
2. 查找多个人的commit
- git log --oneline --author="nuomikang\|lorri"
	- 是 \| 而不是 |
3. 查找符合__关键词__的commit
- git log -S "Go"
- git log -S "bug fixed"

4. 按时间查找commit
- git log --oneline --since="9am" --until="12am"
	- 查找时间段内的
- git log --oneline --since="9am" --until="12am" --after="2017-01"
	- after表示2017年1月以后的

5. 按文件名查看commit
- git log welcome.html

6. 查看某一文件整个生涯的的commit轨迹
- git log -p welcome.html

7. 查看某一文件的commit的某一行代码是谁写的
- git blame index.html
- git blame -L 5,10 index.html
	- -L 表示只显示指定行数的内容


#### 删除文件
1. 删除文件也是一种改动 
- 可以添加至缓存区
- 可以commit
- 会对之前的版本的(已经commit的)产生影响吗?
	- 不能，要是会产生影响，就无法回溯到过去的时间节点了

2. 分离式删除
- 1. 在工作区删除 rm welcome.html
- 2. 将删除(改动)加入暂存区 git add welcome.html
- 3. 可以进行commit
- 删除本质上是一种改动

3. 使用git合并式进行删除
- git rm welcome.html
```
PS C:\git-second> git rm welcome.html
rm 'welcome.html'
PS C:\git-second> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    welcome.html
```

4. 使用 --cached 将文件移除git的控制(文件状态变回Untracked files)，而不是真的删除
- git rm welcome --cached
```
PS C:\git-second> git rm index.html --cached
rm 'index.html'
PS C:\git-second> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    index.html
        deleted:    welcome.html

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        index.html

PS C:\git-second>
```

- 真删除工作区不存在了(真正的被删除了)，伪删除只是变回了Untracked的状态
```
PS C:\git-second> ls


    目录: C:\git-second


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----         2021/4/30      3:44                empty
-a----         2021/4/30      2:28             14 index.html


PS C:\git-second> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    index.html
        deleted:    welcome.html

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        index.html

PS C:\git-second>
```

#### 恢复已被删除的文件or目录
- checkout 对应 rm来使用
1. 单个恢复
- git checkout welcome.html
2. 恢复所有被删除的
- git checkout .
##### git checkout恢复的原理
1. __使用git checkout会进行分支切换，当前的是master分支，之前commit的是历史分支__
```
PS C:\git-second> git log --oneline
bb9ef1d (HEAD -> master) version 3
b826e08 di 2 ci
PS C:\git-second>
```

2. git checkout后接__文件名__or__工作目录__,git不会进行分支切换，而是把文件从.git目录中复制一份到当前的工作目录
- 即，会把暂存区(.git中的)(上一次commit的就是这个区的内容 == 让一次commit的备份)中的内容or文件拿来覆盖掉工作目录中的内容or文件

3. 使用>=2个版本以上的进行覆盖
- git checkout HEAD~2 welcome.html , 但此命令也会强制同时更新缓存区的状态




#### 更改文件名(文件名称不重要 -> Git根据文件的内容计算SHA-1的值)

- 使用mv命令 ， 和rm命令对偶

1. 分开式

#### 修改commit记录(历史版本)

##### 更改-m后的评论信息
1. 使用git rebase命令改动历史记录
2. 先把commit用git reset命令删除 -> 整理后再重新Commit
3. 使用 --amend参数改动最后一次的Commit
##### 更改commit的内容??
- 直接在某一个时间节点处进行更改 -> add -> commit可以吗？？(== 插入了)
##### 追加文件到最后一次commit
- 刚刚commit，但发现有几个文件忘了加，但是又不值得重新新建一个version

1. 使用git reset吧最后一次的commit删除 -> 文件回到暂存区 ，git add加入遗漏的文件后，再commit

2. 使用 --amend 参数进行commit
- 1. 先将遗漏的文件add -> 缓存区
- 2. git commit --amend --no-edit
	- --no-edit表示不要编辑commit信息


#### 新增目录
- 1. 空目录无法被git感知 -> 无法使用git add ,git commit -m " "
- 2. 解决办法：在空目录下放置一个空文件 -> 目录就可以被正常感知 -> 像文件一样对目录进行处理

#### 有些文件不想被git控制
##### 忽略文件
1. 设置 .gitignore 文件
2. 编辑 .gitignore 的内容
3. 只要  .gitignore 文件存在，即使这个文件没有被commit or push到git服务器，也会有效果
4. 新增文件时，只要符合 .gitignore 文件中的规定，这个文件就会被忽略
5. 
##### 清除忽略的文件
- git clean -fX
	- -f是指强制删除

#### 拆掉重做（最后一次做的不满意，拆掉最后一次的重做）
- 有“绝对”拆解和“相对”的拆解
- 使用 git reset 进行退回
##### 相对拆解
1. 指定文件的上一次

2. 主分支(master,header,最近一次提交的commit)
- git reset master^
- git reset HEAD^
- ^ 表示前一次的，header^则是最后一次commit的前一次的
	- 则此时的缓存区、工作区也被退回到最后一次commit前的状态？则，此时对工作区、缓存区的更改 == 对commit进行更改，提交进行覆盖即可

3. 退回到前多次
- git reset master^^
- git reset master^^^
- git reset master~5
- git reset 85e7e30^
- git reset 85e7e30^^
- git reset 85e7e30~6

4. 退回到指定版本commit处, （== 拆解了此版本后面的那个commit）
- git reset 85e7e30

#### commit拆出来的文件去哪了? 
##### reset的3个模式
- git reset 常用参数有三个，分别是 --mixed, --soft, --hard
1. mixed模式
- --mixed是默认参数，如果没有另外加参数，git reset 命令将使用 --mixed模式
- 1. 该mode -> __暂存区__的文件删除，但不影响__工作目录__的文件 ( == commit拆解出来的文件留在工作目录，但不会留在暂存区 )（其实是不是拆解，而是退回到commit上一次的末尾，==comiit提交前的状态）

2. soft模式
- 该模式下，工作目录和暂存区的文件都不会删除

3. hard模式
- 该模式下，工作目录、暂存区的文件都删除。
- 那这种模式有何意义？

#### 拆解commit后又后悔了，能补救吗
- 使用 --hard模式进行拆解的都能恢复
1. 退回到git reset前的分支
2. 使用Reflog
#### 

# .git目录中有什么？





# git commit后这些文件被保存到哪里去了？
- 在网络中的哪些位置？
- 在哪个github账户上？                            

# 实际使用的一些组合
## 1. 分布式记录文档使用
### 需要的功能
1. 多台电脑分布式更新维护同一份
2. 能永久记录某一版本，并在某一时刻回溯
- 这一点是微云同步不具备的
- 但微云同步具备别的，实时同步的功能

### 使用git实现的步骤
1. 上传记录(保存)
2. 更改记录
3. 查看记录
- 查看commit内容
- 下载某一版本的完整内容?
	- 像github中下载asset那样？？
- 