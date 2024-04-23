## git init
使用当前目录为Git仓库->初始化仓库:
```git
git init
```
指定newrepo目录为Git仓库->初始化仓库:
```git
git init newrepo
```
初始化后，会在 newrepo 目录下会出现一个名为 .git 的目录，所有 Git 需要的数据和资源都存放在这个目录中。

如果当前目录下有几个文件想要纳入版本控制，需要先用 git add 命令告诉 Git 开始对这些文件进行跟踪，然后提交：
```git
git add *.c
git add README
git conmmit -m '初始化项目版本'
```
以上命令将目录下以 .c 结尾及 README 文件提交到仓库中。
* 想要提交当前目录所有文件 则为:
```git
git add .
```
     注： 在 Linux 系统中，commit 信息使用单引号 '，Windows 系统，commit 信息使用双引号 "。

    所以在 git bash 中 git commit -m '提交说明' 这样是可以的，在 Windows 命令行中就要使用双引号 git commit -m "提交说明"。

## git clone
克隆仓库的命令格式为：
```git
git clone <repo>
```
克隆到指定目录:
```git
git clone <repo> <directory>
```
参数说明：

    repo:Git 仓库。
    directory:本地目录。
比如，要克隆 Ruby 语言的 Git 代码仓库 Grit，可以用下面的命令：
```
git clone git://github.com/schacon/grit.git
```
执行该命令后，会在当前目录下创建一个名为grit的目录，其中包含一个 .git 的目录，用于保存下载下来的所有版本记录。
如果要自己定义要新建的项目目录名称，可以在上面的命令末尾指定新的名字：
```
git clone git://github.com/schacon/grit.git mygrit
```
## git 配置
显示当前的 git 配置信息:
```
git config --list
```
    credential.helper=osxkeychain
    core.repositoryformatversion=0
    core.filemode=true
    core.bare=false
    core.logallrefupdates=true
    core.ignorecase=true
    core.precomposeunicode=true
编辑 git 配置文件:
```git
git config -e # 针对当前仓库
git config -e --global # 针对系统上所有仓库
```
例子:
```git
git config --global user.name "runoob"
git config --global user.email test@runoob.com
```
如果去掉 --global 参数只对当前仓库有效。


# 基本操作
```
git init    
git add .    
git commit  
```
    git init - 初始化仓库。
    git add . - 添加文件到暂存区。
    git commit - 将暂存区内容添加到仓库中。

### 提交与修改
| 命令                          | 说明                   |
|-----------------------------|----------------------|
| git add                     | 添加文件到暂存区             |
| git status                  | 查看仓库当前的状态，显示有变更的文件。  |
| git diff                    | 比较文件的不同，即暂存区和工作区的差异。 |
| git commit                  | 提交暂存区到本地仓库。          |
| git reset                   | 回退版本。                |
| git rm                      | 将文件从暂存区和工作区删除        |
| git mv                      | 移动或重命名工作区文件          |
| git checkout                | 分支切换                 |
| git switch (git 2.23版本引入）   | 更清晰地切换分支             |
| git restore (git 2.23 版本引入） | 恢复或撤销文件更改            |

1. git checkout:主要用途是切换分支和恢复文件

        切换分支：通过git checkout <branch>命令可以切换到已存在的分支。
                这会将HEAD指向该分支，并将工作目录的文件更新为该分支的最新状态。

        恢复文件：通过git checkout <commit> <file>命令可以将文件恢复到指定提交（commit）的状态。
                这在意外更改文件或需要恢复特定版本的文件时非常有用。
   - 例如：
   ```git
    git checkout develop  // 切换到名为"develop"的分支
    git checkout master   // 切换到名为"master"的分支
    git checkout HEAD~2 index.html  // 将"index.html"文件恢复到前两个提交的状态
    ```
2. git switch:主要目的是切换分支

       切换分支：通过git switch <branch>命令可以切换到已存在的分支。
                这会将HEAD指向该分支，并将工作目录的文件更新为该分支的最新状态。
    - 例如：
    ```git
    git switch develop  // 切换到名为"develop"的分支
    git switch feature  // 切换到名为"feature"的分支
    ```

注意：`git switch`只能用于切换分支，不能恢复文件。如果要恢复文件到特定提交的状态，仍需要使用`git checkout`命令。

# 权限问题
1. 使用root的密钥与git仓库进行ssh设置,此时clone下来的文件夹是属于root的,如果想要用普通用户进行`add .`等操作需要将拥有者进行更改.
` sudo chown -R username:usergroup .`
