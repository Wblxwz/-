- ##### git是分布式(每个设备的本地而非**只**存储在remote server)版本控制

- ##### 采用snapshot存储，快照流，没有改变就存储之前快照的引用

- ##### 存储快照可采用写时copy，即在写入数据前将覆盖的原数据存储到快照卷中，然后再写入原卷，所以快照并不需要存储所有数据，恢复时只需要将快照内容写入原卷中即可

- ##### 也可以直接写入到快照卷中

- ##### hash值区分不同版本，SHA-1

- ##### 不用网也可以进行本地commit操作存储到本地数据库中

- ![Git stores data as snapshots of the project over time](https://git-scm.com/book/en/v2/images/snapshots.png)

- ##### 三种状态 *modified*, *staged*, and *committed*

- ##### 已修改 暂存 已提交

- ![Working tree, staging area, and Git directory](https://git-scm.com/book/en/v2/images/areas.png)

- ##### 对应三种区域 

- ##### working tree(可在本地磁盘上修改) 

- ##### staging area(暂存区，一个文件，存储用来下一次commit的信息)

- ##### Git directory(git clone的就是它，存储快照)

- ##### git config

  - ##### git config --global user.name

  - ##### git config --global user.email

  - ##### git config --list

- ##### git help

  - git help <**command**> 打开doc页面
  - git <**command**> -h 简明的help输出

- ##### git init

  - 仅仅是做了一个初始化的操作，项目里的文件还没有被跟踪

- ##### git add

- ##### git clone

  - 当你执行 `git clone` 命令的时候，默认配置下远程 Git 仓库中的每一个文件的每一个版本都将被拉取下来。
  - git clone [<**options**>] [--] <**repo**> [<**dir**>]
  - 默认使用https协议

- ##### git status

- ##### .gitignore文件

  - 所有空行或者以 `#` 开头的行都会被 Git 忽略。

  - 可以使用标准的 glob 模式匹配，它会递归地应用在整个工作区中。

  - 匹配模式可以以（`/`）开头防止递归。

  - 匹配模式可以以（`/`）结尾指定目录。

  - 要忽略指定模式以外的文件或目录，可以在模式前加上叹号（`!`）取反。

  - https://github.com/github/gitignorehttps://github.com/github/gitignore

    ```
    # 忽略所有的 .a 文件
    *.a
    
    # 但跟踪所有的 lib.a，即便你在前面忽略了 .a 文件
    !lib.a
    
    # 只忽略当前目录下的 TODO 文件，而不忽略 subdir/TODO
    /TODO
    
    # 忽略任何目录下名为 build 的文件夹
    build/
    
    # 忽略 doc/notes.txt，但不忽略 doc/server/arch.txt
    doc/*.txt
    
    # 忽略 doc/ 目录及其所有子目录下的 .pdf 文件
    doc/**/*.pdf
    ```

- ##### git diff

  - 比较工作目录中当前文件和暂存区域快照之间的差异。 也就是修改之后还没有暂存起来的变化内容
  - git diff --staged 比对已暂存文件与最后一次提交的文件差异
  - git diff --check 检查是否有空白错误

- ##### git commit

  - 在commit 命令后添加 -m 选项，将提交信息与命令放在同一行，否则默认进入编辑器
  - git commit -a -m ''  跳过git add将所有文件commit
  - git commit --amend 重新提交，即替换上次commit

- ##### git rm

  - 如果要删除之前修改过或已经放到暂存区的文件，则必须使用强制删除选项-f

- ##### git mv file_from file_to

  - 重命名文件

- ##### git log

  - git log -p -2 显示最近两次commit的差异diff

- ##### git reset

  - 比较危险
  - 可以撤销暂存区内文件(即被add的files) git reset HEAD <**file**>..."

- ##### git checkout -- <**file**>

  - 撤销本地修改，用最近一次提交过的文件替代

- ##### git remote

  - 查看远程仓库
  - git remote -v 查看远程仓库及URL
  - git remote add <**name**> <**ULR**>添加远程仓库及URL

- ##### git fetch <**remote**>

  - 从远程仓库中抓取与拉取，只下载数据，必须手动合并
  - git pull拉取后会自动合并

- ##### git push <**remote**> <**branch**>

  - 当和他人共用一个分支的时候，如果远端仓库发生更改，需要先pull再push
  - git push -u <**remote**> <**branch**> 下次可以直接用git push git pull代替

- ##### git remote show <**remote**>

  - 查看某一个远程仓库的更多信息

- ##### git remote rename <**remote**> name

  - 修改一个远程仓库的简写名

- ##### git remote remove <**remote**>

  - 移除一个远程仓库

- ##### git tag -a <**tag**> -m <**message**>(可以不加message)

  - 为某次提交打tag，例如v1.0 v2.0 push时候会带上
  - git tag -l 列出所有tag
  - git tag <**tag**>轻量标签
  - git tag -d <**tag**>删除本地对应标签
  - git push origin --delete <**tagname**>删除远端仓库对应标签

- ##### git show  <**tag**>

  - 查看对应版本信息

- ##### git分支

  - *blob* 对象（保存着文件快照，git add后计算hash校验和）、树对象（记录着目录结构和 blob 对象索引，git commit后计算hash校验和）以及提交对象（包含着指向前述树对象的指针和所有提交信息，git commit后计算hash校验和）。
  - ![首次提交对象及其树结构。](https://git-scm.com/book/en/v2/images/commit-and-tree.png)
  - 做些修改后再次提交，那么这次产生的提交对象会包含一个指向上次提交对象（父对象）的指针
  - ![提交对象及其父对象。](https://git-scm.com/book/en/v2/images/commits-and-parents.png)

- ##### git branch <**name**>

  - ![分支及其提交历史。](https://git-scm.com/book/en/v2/images/branch-and-history.png)
  - Git 的分支，其实本质上仅仅是指向提交对象的可变指针。
  - ![两个指向相同提交历史的分支。](https://git-scm.com/book/en/v2/images/two-branches.png)
  - git branch 命令仅仅创建一个新分支，并不会自动切换到新分支中去
  - 通过HEAD指针指向当前分支，类似分支的别名
  - git branch -d <**name**> 删除指定分支

- ##### git checkout <**name**>

  - 切换到指定分支
  - 在切换分支之前，保持好一个干净的状态
  - git checkout -b <**name**> 使用这条指令在创建时就切过去，通常直接在创建时就切过去
  - 在不同分支切换时会更改工作目录里的文件。如果是切换到一个较旧的分支，你的工作目录会恢复到该分支最后一次提交时的样子。 如果 Git 不能干净利落地完成这个任务，它将禁止切换分支
  - ![项目分叉历史。](https://git-scm.com/book/en/v2/images/advance-master.png)

- ##### git log --oneline --decorate

  - 查看各个分支当前所指的对象 主要参数是--decorate
  - git log --oneline --decorate --graph --all，会输出提交历史、各个分支的指向以及项目的分支分叉情况。

- ##### git merge <**name**>

  - 合并当前分支与指定分支
  - 按照共同祖先快照进行合并
  - ![一次典型合并中所用到的三个快照。](https://git-scm.com/book/en/v2/images/basic-merging-1.png)
  - 这种情况下Git 会使用两个分支的末端所指的快照（C4 和C5）以及这两个分支的公共祖先（C2），做一个简单的三方合并，最终形成不止一个父提交的快照
  - ![一个合并提交。](https://git-scm.com/book/en/v2/images/basic-merging-2.png)
  - 如果有冲突（即不同分支中对同一个文件的同一个部分进行了不同的修改），git merge会暂停合并分支，此时使用git status查看状态，手动进行修改，再次使用git status查看是否已经解决冲突，如果已解决，使用git commit提交
  - git branch --merged 查看所有已经合并到当前分支的分支，通常使用git branch -d <**name**> 删除掉已合并分支
  - `git merge --abort` 来简单地退出合并

- ##### 分支开发工作流

  - ##### 长期分支：可以只在master分支保留稳定代码，新开平行分支做测试，一旦稳定可以快速合并到主分支

  - ##### 主题分支：一种短期分支，仅为了单一特性或问题做分支，一旦实现或解决即可选择想要分支合并到主分支，然后删除掉已合并分支

  - 当你新建和合并分支的时候，所有这一切都只发生在你本地的 Git 版本库中,没有与服务器发生交互

- ##### git remote show <**remote**>

  - 显示所有远程分支

- ##### git fetch <**remote**>

  - 用来更新本地的远端分支，抓取本地没有的数据，而不进行和本地分支的合并，并且不会修改工作目录中的内容
  - 合并的话需要手动merge
  - git pull 多数情况下是git fetch 后紧跟 git merge

- ##### git push <**remote**> <**branch**>

  - git push <**remote**> <**local branch**>:<**remote branch**> push本地分支到远端指定分支
  - git push <**remote**> --delete <**branch**> 删除远端指定分支

- ##### 跟踪分支

  - 即自动pull push的远端分支
  - git branch -u <**remote**>/<**branch**> 修改正在跟踪的上游分支
  - git checkout -b <**branch**> <**remote**>/<**branch**> 设置跟踪分支（即对远端分支的跟踪）
  - git checkout --track <**remote**>/<**branch**> 为当前分支设置跟踪分支
  - git branch -vv 查看本地分支track的远端分支
  - behind n落后n版本，ahead n领先n版本

- ##### 变基

  - git rebase <**basebranch**> <**topicbranch**>
  - 和三方快照合并是一致的，只是提交历史不同
  - ![将 `C4` 中的修改变基到 `C3` 上。](https://git-scm.com/book/en/v2/images/basic-rebase-3.png)
  - git rebase --onto <**basebranch**> <**diffbranch**> <**topicbranch**>  取出 `topicbranch` 分支，找出它从 `diffbranch` 分支分歧之后的补丁， 然后把这些补丁在 `basebranch` 分支上重放一遍，让 `topicbranch` 看起来像直接基于 `basebranch` 修改一样
  - ![截取主题分支上的另一个主题分支，然后变基到其他分支。](https://git-scm.com/book/en/v2/images/interesting-rebase-2.png)
  - 如果提交存在于你的仓库之外，而别人可能基于这些提交进行开发，那么不要执行变基。因为变基操作的实质是丢弃一些现有的提交，然后相应地新建一些内容一样但实际上不同的提交。
  - 总的原则是，只对尚未推送或分享给别人的本地修改执行变基操作清理历史（不合作的情况下）， 从不对已推送至别处的提交执行变基操作。

- ##### 提交

  - 把每个问题细分成一个提交，而不是一个巨大的提交
  - 首行不超过50个字符（25个汉字）做简要描述，具体看公司规范
  - git fetch 先拉取远端分支到本地，再手动做合并，类似git pull，但是更灵活
  - ![一个简单的多人 Git 工作流程的通常事件顺序。](https://git-scm.com/book/en/v2/images/small-team-flow.png)

- ##### 为公开项目做贡献

  - 使用git request-pull <**remote**> <**branch**>提交PR到没权限的公开项目中
  - git format --patch -M <**remotebranch**> 生成.patch补丁 `format-patch` 命令打印出它创建的补丁文件名字。 `-M` 开关告诉 Git 查找重命名。可以将其通过邮件发送给公开项目，这种情况只能commit后发送patch，而不能push，适用于通过邮件发送的公开项目
  - [Git - 向一个项目贡献 (git-scm.com)](https://git-scm.com/book/zh/v2/分布式-Git-向一个项目贡献) 

- ##### 维护公开项目

  - 建议从master切一个主题分支来测试别人的提交内容，
  - [Git - 维护项目 (git-scm.com) ](https://git-scm.com/book/zh/v2/分布式-Git-维护项目)维护通过邮件发送的公开项目(详细内容)

- ##### GitHub相关

  - git fork 派生项目，即fork到GitHub上自己的仓库副本，与git clone 到本地副本不同
  - 如果想为他人公开项目做贡献，先fork到自己的GitHub仓库，然后再clone自己的派生仓库到本地
  - git push推送到GitHub仓库的副本后，通过GitHub页面创建PR
  - ![拉取请求创建页面](https://git-scm.com/book/en/v2/images/blink-03-pull-request-open.png)
  - 同样，项目拥有者也可以在GitHub上操作合并
  - 双方可以通过GitHub交流
  - 也可以使用命令在本地合并和PR

- ##### 维护GitHub个人项目

  - [Git - 维护项目 (git-scm.com)](https://git-scm.com/book/zh/v2/GitHub-维护项目)

- ##### 管理组织

  - [Git - 管理组织 (git-scm.com)](https://git-scm.com/book/zh/v2/GitHub-管理组织)

- ##### GitHub Hook与API

  - [Git - 脚本 GitHub (git-scm.com)](https://git-scm.com/book/zh/v2/GitHub-脚本-GitHub)

- ##### git show

  - git show <**SHA-1**> 查看该hash对应的提交信息，hash值至少四个字符且没有其他提交以同样字符开头
  - git show <**branch**> 查看该分支最后一次提交信息
  - git show HEAD^ 查看HEAD的父提交信息
  - git show HEAD^n 查看HEAD的第n父提交信息（只适用于合并提交）
  - git show HEAD~n 查看HEAD的前n个第一父提交信息 n个~为前n个（全是第一父提交，可以和^组合）

- ##### git rev-parse <**branch**>

  - 查看该分支最后一次提交的hash值

- ##### git reflog

  - 查看HEAD指向变动记录（即引用记录）
  - 可查看前n条或固定时间段
  - 引用记录只记录本地仓库HEAD变动

- ##### git log <**anthorbranch**>..<**branch**>

  - 显示在一个分支中而不在另一个分支中的提交
  - 等价于**git log ^refA refB**和**git log refB --not refA**

- ##### git log <**branch**>...<**branch**>

  - 选择出被两个引用 之一包含但又不被两者同时包含的提交
  - git log --left-right master...experiment 显示每个提交到底处于哪一侧的分支 例如<代表左侧分支 >代表右侧分支

- ##### git add -i 交互式暂存

  - 类似git status 但更详细且可以进一步进行指令操作
  - 进一步指令的详细操作见[Git - 交互式暂存 (git-scm.com)](https://git-scm.com/book/zh/v2/Git-工具-交互式暂存)

- ##### git stash 或者git stash push

  - 将当前分支工作推入到栈中，适用于暂时不想为了当前分支做提交而只想先切到别的分支的情况
  - git stash list 查看存储在栈上的内容
  - git stash apply 重新应用存储的内容，默认最近的存储，可查看list通过 stash@{n}进行选择
  - git stash drop stash@{n}进行删除已存储内容
  - git stash pop 立即应用存储并从栈上删除它
  - git stash --keep-index 保存进度后不会将暂存区重置。默认会将暂存区和工作区强制重置为 HEAD。
  - git stash -u 包括未跟踪的文件
  - git stash branch <**branch**> 将最近已存储内容中记录的更改应用到新的工作区和暂存区。如果成功，那么它将删除最近已存储内容。
  - git stash --all 移除每一样东西(工作目录中未被追踪且未被忽略的文件)并存放在栈中，相对于git clean更安全

- ##### git clean

  - 清除工作目录中所有未被追踪且未被忽略的文件（即不是 `.gitignore` 或其他忽略文件中的模式匹配的文件）且不保证能找回
  - git clean -d -n 告诉你将要移除什么
  - git clean -d -n -x 清除工作目录中所有未被追踪的文件（包括忽略文件）
  - git clean -x -i 以交互模式运行 clean 命令

- ##### GPG签名

  - [Git - 签署工作 (git-scm.com)](https://git-scm.com/book/zh/v2/Git-工具-签署工作)

- ##### git grep <**search**>

  - 在数据库中浏览代码和提交以搜索
  - 默认查找工作目录的文件
  - git grep -n <**search**> 同时输出 Git 找到的匹配行的行号
  - git grep --count <**search**> 概述的信息， 其中仅包括那些包含匹配字符串的文件，以及每个文件中包含了多少个匹配
  - git grep -p <**search**> 显示每一个匹配的字符串所在的方法或函数
  
- ##### git log -S <**search**>

  - 日志搜索
  
- ##### git commit --amend

  - 替换最后一次commit的提交信息

- ##### 修改多个提交信息

  - 通过git rebase变基实现

- ##### [Git - 重置揭密 (git-scm.com)](https://git-scm.com/book/zh/v2/Git-工具-重置揭密)

  - HEAD 是当前分支引用的指针，它总是指向该分支上的最后一次提交。 这表示 HEAD 将是下一次提交的父结点。 通常，理解 HEAD 的最简方式，就是将它看做 **该分支上的最后一次提交** 的快照。

  - Index是**预期的下一次提交**，我们也会将这个概念引用为 Git 的“暂存区”，这就是当你运行**git commit**时 Git 看起来的样子。

  - 另外两棵树以一种高效但并不直观的方式，将它们的内容存储在 `.git` 文件夹中。**工作目录**会将它们解包为实际的文件以便编辑。 你可以把工作目录当做 **沙盒**。在你将修改提交到暂存区并记录到历史之前，可以随意更改。

  - | 树                | 用途                                 |
    | :---------------- | :----------------------------------- |
    | HEAD              | 上一次提交的快照，下一次提交的父结点 |
    | Index             | 预期的下一次提交的快照               |
    | Working Directory | 沙盒                                 |

  - ![reset ex1](https://git-scm.com/book/en/v2/images/reset-ex1.png)

  - ![reset ex2](https://git-scm.com/book/en/v2/images/reset-ex2.png)

  - ![reset ex3](https://git-scm.com/book/en/v2/images/reset-ex3.png)

  - 此时如果我们运行 `git status`，会发现没有任何改动，因为现在三棵树完全相同。

  - 切换分支或克隆的过程也类似。 当检出一个分支时，它会修改 **HEAD** 指向新的分支引用，将 **索引** 填充为该次提交的快照， 然后将 **索引** 的内容复制到 **工作目录** 中。

- ##### git reset --soft HEAD~

  - 撤销**git commit**指令，**~**代表返回上一个HEAD
  - ![reset soft](https://git-scm.com/book/en/v2/images/reset-soft.png)

- ##### git reset --mixed HEAD~

  - 会用 HEAD 指向的当前快照的内容来更新索引
  - ![reset mixed](https://git-scm.com/book/en/v2/images/reset-mixed.png)

- ##### git reset --hard HEAD~

  - 让工作目录看起来像索引
  - ![reset hard](https://git-scm.com/book/en/v2/images/reset-hard.png)
  - `--hard` 标记是 `reset` 命令唯一的危险用法，它也是 Git 会真正地销毁数据的仅有的几个操作之一。 其他任何形式的 `reset` 调用都可以轻松撤消，但是 `--hard` 选项不能，因为它强制覆盖了工作目录中的文件

- ##### git reset **< file>**

  - 取消git add操作，即仅仅将HEAD这颗树的内容复制到Index树的内容中

- 

