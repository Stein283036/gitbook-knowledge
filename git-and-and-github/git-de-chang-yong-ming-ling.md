# Git 的常用命令

### Git 仓库下文件的三个状态

1. 工作区
2. 暂存区
3. 本地仓库区

### git config

当初次下载 Git 后，需要配置用来提交代码的用户名和邮箱，Git 有一个默认的 `master` 分支，而 GitHub 的默认分支从之前的 master 分支切换成了 main 分支，所以如果想让 Git 的默认分支和 GitHub 的默认分支保持一致时，也可以切换 Git 的默认分支，这三个的命令示例如下：

```git
git config --global user.name "your name"
git config --global user.email "your email"
git config --global init.default branch main
```

上面的 `--global` 参数的意思是在全局范围内配置信息，这样你每一个使用 Git 管理的项目就不用单独在配置这些信息了，注意用自己实际的姓名和邮箱替换上面的占位信息。

在上面的配置做完以后，可以通过 `git config -l` 查看配置项。

### git init

如果一个项目不是从版本管理中心如 `GitHub` 上 `clone` 下来的，并且本地想通过 `Git` 来管理当前系统上的目录和文件，那么可以使用 `git init` 来激活。

当你运行此命令时，你应该会看到在你正在处理的当前文件夹中自动创建了一个名为 `.git` 的文件夹。

### git status

通过这个命令来查看当前仓库下的文件状态，可以显示哪些文件未被跟踪、哪些文件已被修改导致与之前提交的版本不一致、哪些文件在暂存区中可以被提交到本地仓库。

### git add

此命令将你的文件添加到暂存区。暂存区域是添加我们对其进行更改的文件以及它们等待下一次提交的区域。

要将文件添加到暂存区域，请使用 `git add` 命令。它将文件夹中的所有文件添加到暂存区域。

`git add (file name)` 将指定文件添加到暂存区进行跟踪管理。也可以通过 `git all .` 将当前目录下所有受 Git 管理的文件添加到暂存区，或者通过正则匹配规则添加指定的文件到暂存区中，例如：

```git
git add todo.txt // 只将 todo.txt 文件添加到暂存区中
git add . // 将所有的文件添加到暂存区中
git add code* // 将名称以 code 开头的文件添加到暂存区中
```

### git commit

当我们想把本地暂存区的文件提交到本地仓库区的时候，就可以使用这个命令并附上一条提交信息。例如：

```git
git commit -m "commit message"
```

### git clone 命令

使用这个命令来从分布式代码管理中心（GitHub、GitLab 等）拉取使用 Git 管理的仓库到本地，从而进行协同开发等工作，这种方式会自动和远程仓库建立起映射关系。例如：

```git
git clone https://github.com/papers-we-love/papers-we-love.git
```

### git push

当使用 `git clone` 命令拉取了远程仓库后，如果在本地进行了修改并且希望将代码推送到远程代码仓库，那么可以使用 `git push` 命令。

### git rm

可以使用此 Git 命令从工作仓库中删除文件，例如：

```git
git rm filename
```

### git branch

通过这个命令查看当前的所在分支或者创建一个新的分支，例如：

```git
git branch // 查看当前本地所在的分支
git branch dev // 在本地新创建一个 dev 分支
```

修改主分支的名称：

```git
git branch -M main
```

### git checkout

通过这个命令对分支进行操作。

切换到上一个命令创建的新分支：

```git
git checkout dev // 切换到 dev 分支
```

直接使用这个命令创建并切换分支

```git
git checkout -b test // 创建一个新的 test 分支并切换到该分支
```

通常在一个分支提交修改到本地仓库以后，主分支会合并它，接着，就可以删除该分支，例如：

```git
git branch -d dev // 删除 dev 分支
```

### git merge

分支合并操作。

通常在一个仓库下，只有一个主分支，但是可以有多个其它分支，比如 dev 分支、bugfix 分支、feature 分支 等用来对代码的不同功能和部分就行修改，方便一个团队内的责任工作划分，在当前从分支提交修改到分支以后，可以切换到主分支使用 `git merge 命令合并一个分支，例如：`

```git
git merge dev // 合并主分支
```

### git remote

当需要将本地的 Git 仓库与远程的仓库中心建立起关联映射时，可以使用这个命令，例如：

```git
git remote add origin https://github.com/stein283036/git-and-github-tutorial.git
git push origin master // 推送到远程的 master 分支中
git remote -v // 查看关联的远程仓库
```

### git log

当想要查看当前仓库的提交历史时，可以使用这个命令来查看这条提交历史的作者、日期、提交消息和提交 ID，例如：

```git
git log
```

通过 git log --stat 额外地查看每次提交的文件变化，查看文件变化的统计信息，如文件的删除、新增等。
