# git课程记录

前言：课程挺好的，原理+实践

## 1. Git 是什么

- 介绍版本控制的发展历史，为什么会出现Git
- 介绍Git的发展历史

### 分布式版本控制

![image-20220524103102652](git-test.assets/image-20220524103102652.png)

![image-20220524103154019](git-test.assets/image-20220524103154019.png)

### 1.1 版本控制方式

- 最初：文件夹，v1-20220101，v2-20220303

  ![image-20220524103414979](git-test.assets/image-20220524103414979.png)

- 集中式版本控制

  ![image-20220524110256264](git-test.assets/image-20220524110256264.png)

- 现在：分布式版本控制

  ![image-20220524110447908](git-test.assets/image-20220524110447908.png)

### 1.2 Git历史

![image-20220524110753704](git-test.assets/image-20220524110753704.png)

![image-20220524111050022](git-test.assets/image-20220524111050022.png)

## 2. Git 基本使用方式

- Git的基本命令介绍，如何使用这些命令，以及命令的原理

![image-20220524111152562](git-test.assets/image-20220524111152562.png)

![image-20220524112020562](git-test.assets/image-20220524112020562.png)

### 实操环节

```bash
# 更新git bash
$ git update-git-for-windows
$ mkdir demo
$ cd demo
$ git init
# 在git bash中添加别名，实现类似原生使用windows自带的tree
# 在这个目录下
$ echo "# Set alias for tree command" >> ./etc/bash.bashrc
$ echo "alias tree='winpty tree.com'" >> ./etc/bash.bashrc
$ source ./etc/bash.bashrc
# 重启git bash，回到项目目录
$ tree .git
卷 Windows-SSD 的文件夹 PATH 列表
卷序列号为 0000007B DE72:9455
C:\USERS\14224\DESKTOP\STUDY\DEMO\.GIT
├─hooks
├─info
├─objects
│  ├─info
│  └─pack
└─refs
    ├─heads
    └─tags
$ cat .git/HEAD
ref: refs/heads/master
$ cat .git/config
[core]
        repositoryformatversion = 0
        filemode = false
        bare = false
        logallrefupdates = true
        symlinks = false
        ignorecase = true
# 用户名配置
$ git config --global user.name "Baojiazhong"
$ git config --global user.email 1422401429@qq.com
14224@LAPTOP-BHE0I84M MINGW64 ~
$ cat .gitconfig
[credential]
        helper = store
[user]
        email = 1422401429@qq.com
        name = Baojiazhong
[color]
        ui = auto
[filter "lfs"]
        clean = git-lfs clean -- %f
        smudge = git-lfs smudge -- %f
        process = git-lfs filter-process
        required = true
# Instead of配置，没做
$ git config --global url.git@github.com:.insteadOf https://github.com/
# Git 命令别名配置,没做
$ git config --global alias.cin "commit --amend --no-edit"
# Remote配置，http和https两种
# 查看Remote配置
$ git remote -v

# 添加Remote
$ git remote add origin_ssh git@github.com:git/git.git
$ git remote add origin_http https://github.com/git/git.git
# 再次查看Remote
$ git remote -v
origin_http     https://github.com/git/git.git (fetch)
origin_http     https://github.com/git/git.git (push)
origin_ssh      git@github.com:git/git.git (fetch)
origin_ssh      git@github.com:git/git.git (push)
$ cat .git/config
[core]
        repositoryformatversion = 0
        filemode = false
        bare = false
        logallrefupdates = true
        symlinks = false
        ignorecase = true
[remote "origin_ssh"]
        url = git@github.com:git/git.git
        fetch = +refs/heads/*:refs/remotes/origin_ssh/*
[remote "origin_http"]
        url = https://github.com/git/git.git
        fetch = +refs/heads/*:refs/remotes/origin_http/*
$ git remote -h
usage: git remote [-v | --verbose]
   or: git remote add [-t <branch>] [-m <master>] [-f] [--tags | --no-tags] [--mirror=<fetch|push>] <name> <url>
   or: git remote rename [--[no-]progress] <old> <new>
   or: git remote remove <name>
   or: git remote set-head <name> (-a | --auto | -d | --delete | <branch>)
   or: git remote [-v | --verbose] show [-n] <name>
   or: git remote prune [-n | --dry-run] <name>
   or: git remote [-v | --verbose] update [-p | --prune] [(<group> | <remote>)...]
   or: git remote set-branches [--add] <name> <branch>...
   or: git remote get-url [--push] [--all] <name>
   or: git remote set-url [--push] <name> <newurl> [<oldurl>]
   or: git remote set-url --add <name> <newurl>
   or: git remote set-url --delete <name> <url>

    -v, --verbose         be verbose; must be placed before a subcommand
# 同一个Origin设置不同的Push和Fetch URL
$ git remote add origin git@github.com:git/git.git
$ git remote set-url --add --push origin git@github.com:MY_REPOSITY/git.git
$ git remote -v
origin  git@github.com:git/git.git (fetch)
origin  git@github.com:MY_REPOSITY/git.git (push)
origin_http     https://github.com/git/git.git (fetch)
origin_http     https://github.com/git/git.git (push)
origin_ssh      git@github.com:git/git.git (fetch)
origin_ssh      git@github.com:git/git.git (push)
$ cat .git/config
[core]
        repositoryformatversion = 0
        filemode = false
        bare = false
        logallrefupdates = true
        symlinks = false
        ignorecase = true
[remote "origin_ssh"]
        url = git@github.com:git/git.git
        fetch = +refs/heads/*:refs/remotes/origin_ssh/*
[remote "origin_http"]
        url = https://github.com/git/git.git
        fetch = +refs/heads/*:refs/remotes/origin_http/*
[remote "origin"]
        url = git@github.com:git/git.git
        fetch = +refs/heads/*:refs/remotes/origin/*
        pushurl = git@github.com:MY_REPOSITY/git.git
# 直接用vim编辑上述文件也可以
# HTTP Remote 不推荐
# 免密配置
# 内存
$ git config --global credential.helper 'cache --timeout=3600'
# 硬盘，不指定目录的情况默认是 ~/.git-credentials
$ git config --global credential.helper "store --file /path/to/credential-file"
# 将密钥信息存在指定文件中
# SSH Remote 推荐使用
$ ssh-keygen -t ed25519 -C "1422401429@qq.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/c/Users/14224/.ssh/id_ed25519):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/14224/.ssh/id_ed25519
Your public key has been saved in /c/Users/14224/.ssh/id_ed25519.pub
The key fingerprint is:
SHA256:ow3It0slfgYEas09Xy3CIYph9ib4KlylVA9WyPVck94 1422401429@qq.com
The key's randomart image is:
+--[ED25519 256]--+
|  + o+=o.  o.    |
| + Bo*ooo..o.    |
|. =.*.+.oo+ o    |
| o.+oo o o o E   |
|  .oo = S        |
|...  o O .       |
|o.    = +        |
|.    . +         |
|      .          |
+----[SHA256]-----+
$ touch readme.md
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        readme.md

nothing added to commit but untracked files present (use "git add" to track)
$ echo hello > readme.md
$ git add .
warning: LF will be replaced by CRLF in readme.md.
The file will have its original line endings in your working directory

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/demo (master)
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   readme.md
# ce + ce目录下的文件名
$ git cat-file -p ce013625030ba8dba906f756967f9e9ca394464a
hello
$ git commit -m "add readme"
[master (root-commit) 50e1a45] add readme
 1 file changed, 1 insertion(+)
 create mode 100644 readme.md
# 多了50，f0
14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/demo (master)
$ git cat-file -p 50e1a4540074f0d1241c639c1e00382480129705
tree f071d59456a38f47c1bb65edbc1c11b405aed491
author Baojiazhong <1422401429@qq.com> 1653370649 +0800
committer Baojiazhong <1422401429@qq.com> 1653370649 +0800

add readme

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/demo (master)
$ git cat-file -p f071d59456a38f47c1bb65edbc1c11b405aed491
100644 blob ce013625030ba8dba906f756967f9e9ca394464a    readme.md
$ git log
commit 50e1a4540074f0d1241c639c1e00382480129705 (HEAD -> master)
Author: Baojiazhong <1422401429@qq.com>
Date:   Tue May 24 13:37:29 2022 +0800

    add readme
$ cat .git/refs/heads/master
50e1a4540074f0d1241c639c1e00382480129705
# 创建一个新的分支
$ git checkout -b test
Switched to a new branch 'test'
$ cat .git/refs/heads/test
50e1a4540074f0d1241c639c1e00382480129705
$ git tag v0.0.1
$ cat .git/refs/tags/v0.0.1
50e1a4540074f0d1241c639c1e00382480129705
# 附注标签
$ git tag -a v0.0.2 -m "add feature 1"
# objects 多了 f3
$ cat .git/refs/tags/v0.0.2
f36f2681c37ac8c4e6f62173c063f5bb165839d1
$ git cat-file -p f36f2681c37ac8c4e6f62173c063f5bb165839d1
object 50e1a4540074f0d1241c639c1e00382480129705
type commit
tag v0.0.2
tagger Baojiazhong <1422401429@qq.com> 1653371753 +0800

add feature 1
# 追溯历史版本
# 获取历史版本代码
$ vim readme.md
$ git add .
warning: LF will be replaced by CRLF in readme.md.
The file will have its original line endings in your working directory

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/demo (test)
$ git commit -m "update readme"
[test b0496a4] update readme
 1 file changed, 1 insertion(+), 1 deletion(-)
# 多了不少object啊。多了3个（blob，commit，tree）
$ git log
commit b0496a40ae3c004340e708a0b43e573b07f713fb (HEAD -> test)
Author: Baojiazhong <1422401429@qq.com>
Date:   Tue May 24 14:02:16 2022 +0800

    update readme

commit 50e1a4540074f0d1241c639c1e00382480129705 (tag: v0.0.2, tag: v0.0.1, master)
Author: Baojiazhong <1422401429@qq.com>
Date:   Tue May 24 13:37:29 2022 +0800

    add readme
$ git cat-file -p b0496a40ae3c004340e708a0b43e573b07f713fb
tree 386eb799bbfd0826f510b6587c5afaae2a962279
parent 50e1a4540074f0d1241c639c1e00382480129705
author Baojiazhong <1422401429@qq.com> 1653372136 +0800
committer Baojiazhong <1422401429@qq.com> 1653372136 +0800

update readme
$ git cat-file -p 386eb799bbfd0826f510b6587c5afaae2a962279
100644 blob 2be7c65ae93b54b988416f280298b0b8b5f20385    readme.md

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/demo (test)
$ git cat-file -p 2be7c65ae93b54b988416f280298b0b8b5f20385
# hello world
$ git commit --amend
[test 48d8662] update readme!!!!
 Date: Tue May 24 14:02:16 2022 +0800
 1 file changed, 1 insertion(+), 1 deletion(-)
$ git log
commit 48d8662ab123fffad6e96b7f2f5c9b100ddbe106 (HEAD -> test)
Author: Baojiazhong <1422401429@qq.com>
Date:   Tue May 24 14:02:16 2022 +0800

    update readme!!!!

commit 50e1a4540074f0d1241c639c1e00382480129705 (tag: v0.0.2, tag: v0.0.1, master)
Author: Baojiazhong <1422401429@qq.com>
Date:   Tue May 24 13:37:29 2022 +0800

    add readme
$ tree .git
卷 Windows-SSD 的文件夹 PATH 列表
卷序列号为 000000B4 DE72:9455
C:\USERS\14224\DESKTOP\STUDY\DEMO\.GIT
├─hooks
├─info
├─logs
│  └─refs
│      └─heads
├─objects
│  ├─2b
│  ├─38
│  ├─48
│  ├─50
│  ├─b0
│  ├─ce
│  ├─f0
│  ├─f3
│  ├─info
│  └─pack
└─refs
    ├─heads
    └─tags
# 就是新增了一个commit，之前的commit悬空了，没有用了
$ git fsck --lost-found
Checking object directories: 100% (256/256), done.
dangling commit b0496a40ae3c004340e708a0b43e573b07f713fb
# 删除悬空的commit
# Git GC
$ git reflog expire --expire=now --all
$ git gc --prune=now
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 12 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (7/7), done.
Total 7 (delta 0), reused 0 (delta 0), pack-reused 0
$ tree .git/
卷 Windows-SSD 的文件夹 PATH 列表
卷序列号为 00000012 DE72:9455
C:\USERS\14224\DESKTOP\STUDY\DEMO\.GIT
├─hooks
├─info
├─logs
│  └─refs
│      └─heads
├─lost-found
│  └─commit
├─objects
│  ├─info
│  └─pack
└─refs
    ├─heads
    └─tags
$ git cat-file -p b0496a40ae3c004340e708a0b43e573b07f713fb
fatal: Not a valid object name b0496a40ae3c004340e708a0b43e573b07f713fb

```

![image-20220524112557385](git-test.assets/image-20220524112557385.png)

![image-20220524115648465](git-test.assets/image-20220524115648465.png)

![image-20220524115947105](git-test.assets/image-20220524115947105.png)

![image-20220524120200802](git-test.assets/image-20220524120200802.png)

![image-20220524124038251](git-test.assets/image-20220524124038251.png)

![image-20220524132118224](git-test.assets/image-20220524132118224.png)

![image-20220524132213653](git-test.assets/image-20220524132213653.png)

![image-20220524132338673](git-test.assets/image-20220524132338673.png)

![image-20220524133459407](git-test.assets/image-20220524133459407.png)

![image-20220524133805369](git-test.assets/image-20220524133805369.png)

![image-20220524134632602](git-test.assets/image-20220524134632602.png)

![image-20220524134715600](git-test.assets/image-20220524134715600.png)

![image-20220524134805664](git-test.assets/image-20220524134805664.png)

![image-20220524135149208](git-test.assets/image-20220524135149208.png)

![image-20220524135251130](git-test.assets/image-20220524135251130.png)

![image-20220524135514074](git-test.assets/image-20220524135514074.png)

![image-20220524140033945](git-test.assets/image-20220524140033945.png)

![image-20220524140759700](git-test.assets/image-20220524140759700.png)

![image-20220524141350806](git-test.assets/image-20220524141350806.png)

![image-20220524141648168](git-test.assets/image-20220524141648168.png)

![image-20220524142102570](git-test.assets/image-20220524142102570.png)

![image-20220524142358623](git-test.assets/image-20220524142358623.png)

![image-20220524142545765](git-test.assets/image-20220524142545765.png)

![image-20220524142702804](git-test.assets/image-20220524142702804.png)




## 3. Git 研发流程
- 依托代码管理平台 Gitlab/Github/Gerrit介绍我们如何进行代码的开发及团队合作

![image-20220524142922106](git-test.assets/image-20220524142922106.png)

![image-20220524142940055](git-test.assets/image-20220524142940055.png)

![image-20220524143133043](git-test.assets/image-20220524143133043.png)

![image-20220524143234509](git-test.assets/image-20220524143234509.png)

![image-20220524143321368](git-test.assets/image-20220524143321368.png)

![image-20220524143342153](git-test.assets/image-20220524143342153.png)

![image-20220524143552671](git-test.assets/image-20220524143552671.png)

![image-20220524143759657](git-test.assets/image-20220524143759657.png)

```bash
# 克隆仓库
$ git clone git@github.com:Baojiazhong/demo.git
Cloning into 'demo'...
warning: You appear to have cloned an empty repository.
# push
14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (main)
$ vim readme.md

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (main)
$ git add .
warning: LF will be replaced by CRLF in readme.md.
The file will have its original line endings in your working directory

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (main)
$ git commit -m "add readme"
[main (root-commit) a52c521] add readme
 1 file changed, 1 insertion(+)
 create mode 100644 readme.md

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (main)
$ git push origin main
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 224 bytes | 224.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:Baojiazhong/demo.git
 * [new branch]      main -> main
# 创建新分支
14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (main)
$ git checkout -b feature
Switched to a new branch 'feature'

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (feature)
$ vim readme.md

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (feature)
$ git add .
warning: LF will be replaced by CRLF in readme.md.
The file will have its original line endings in your working directory

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (feature)
$ git commit -m "update readme"
[feature 9423187] update readme
 1 file changed, 1 insertion(+), 1 deletion(-)

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (feature)
$ git push origin feature
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Writing objects: 100% (3/3), 259 bytes | 259.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote:
remote: Create a pull request for 'feature' on GitHub by visiting:
remote:      https://github.com/Baojiazhong/demo/pull/new/feature
remote:
To github.com:Baojiazhong/demo.git
 * [new branch]      feature -> feature
14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (feature)
$ git checkout main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (main)
$ git pull origin main
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), 623 bytes | 124.00 KiB/s, done.
From github.com:Baojiazhong/demo
 * branch            main       -> FETCH_HEAD
   a52c521..2b4b0fd  main       -> origin/main
Updating a52c521..2b4b0fd
Fast-forward
 readme.md | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (main)
$ git log
commit 2b4b0fd3308d79f9b9eaa14f56134ac5ae534eba (HEAD -> main, origin/main)
Merge: a52c521 9423187
Author: Baojiazhong <50916042+Baojiazhong@users.noreply.github.com>
Date:   Tue May 24 14:52:34 2022 +0800

    Merge pull request #1 from Baojiazhong/feature

    update readme

commit 94231871408c38228c09e2d02397166da3435787 (origin/feature, feature)
Author: Baojiazhong <1422401429@qq.com>
Date:   Tue May 24 14:47:18 2022 +0800

    update readme

commit a52c5213032a568648a6368067c3ff60009573e3
Author: Baojiazhong <1422401429@qq.com>
Date:   Tue May 24 14:43:35 2022 +0800

    add readme
14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (main)
$ vim readme.md

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (main)
$ git add .

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (main)
$ git commit -m "test rules"
[main f48fd27] test rules
 1 file changed, 1 insertion(+)

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (main)
$ git push origin main
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Writing objects: 100% (3/3), 274 bytes | 274.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: error: GH006: Protected branch update failed for refs/heads/main.
remote: error: Changes must be made through a pull request.
To github.com:Baojiazhong/demo.git
 ! [remote rejected] main -> main (protected branch hook declined)
error: failed to push some refs to 'github.com:Baojiazhong/demo.git'
# 代码合并
# 1 fast-forword
14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (main)
$ git checkout -b test
Switched to a new branch 'test'

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (test)
$ ls
readme.md

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (test)
$ vim readme.md

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (test)
$ git add .

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (test)
$ git commit -m "test"
[test 6429ec1] test
 1 file changed, 1 insertion(+)

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (test)
$ git checkout main
Switched to branch 'main'
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (main)
$ git merge test --ff-only
Updating f48fd27..6429ec1
Fast-forward
 readme.md | 1 +
 1 file changed, 1 insertion(+)

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (main)
$ git log
commit 6429ec1597ccbd643e4057aea4bbbbdb6fca59c5 (HEAD -> main, test)
Author: Baojiazhong <1422401429@qq.com>
Date:   Tue May 24 15:05:24 2022 +0800

    test

commit f48fd2713979dc8efd5f4ab6229f60404de844a6
Author: Baojiazhong <1422401429@qq.com>
Date:   Tue May 24 14:58:58 2022 +0800

    test rules

commit 2b4b0fd3308d79f9b9eaa14f56134ac5ae534eba (origin/main)
Merge: a52c521 9423187
Author: Baojiazhong <50916042+Baojiazhong@users.noreply.github.com>
Date:   Tue May 24 14:52:34 2022 +0800

    Merge pull request #1 from Baojiazhong/feature

    update readme

commit 94231871408c38228c09e2d02397166da3435787 (origin/feature, feature)
Author: Baojiazhong <1422401429@qq.com>
14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (main)
$ git checkout test
Switched to branch 'test'

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (test)
$ vim readme.md

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (test)
$ git add .

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (test)
$ git commit -m "test third party"
[test 799f8f5] test third party
 1 file changed, 1 insertion(+)

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (test)
$ git checkout main
Switched to branch 'main'
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (main)
$ git merge test --no-ff
Merge made by the 'ort' strategy.
 readme.md | 1 +
 1 file changed, 1 insertion(+)

14224@LAPTOP-BHE0I84M MINGW64 ~/Desktop/study/study/demo (main)
$ git log
commit 15a7085eb07ccab2704904edaca90093606ccb30 (HEAD -> main)
Merge: 6429ec1 799f8f5
Author: Baojiazhong <1422401429@qq.com>
Date:   Tue May 24 15:12:34 2022 +0800

    Merge branch 'test'

commit 799f8f5446bfd06e1f95aaf0c4795a9cbca3f6ff (test)
Author: Baojiazhong <1422401429@qq.com>
Date:   Tue May 24 15:10:58 2022 +0800

    test third party

commit 6429ec1597ccbd643e4057aea4bbbbdb6fca59c5
Author: Baojiazhong <1422401429@qq.com>
Date:   Tue May 24 15:05:24 2022 +0800

    test

commit f48fd2713979dc8efd5f4ab6229f60404de844a6
Author: Baojiazhong <1422401429@qq.com>
Date:   Tue May 24 14:58:58 2022 +0800

```



![image-20220524145457764](git-test.assets/image-20220524145457764.png)

![image-20220524150110259](git-test.assets/image-20220524150110259.png)

![image-20220524150253970](git-test.assets/image-20220524150253970.png)

![image-20220524150304771](git-test.assets/image-20220524150304771.png)

![image-20220524151557247](git-test.assets/image-20220524151557247.png)

![image-20220524151823195](git-test.assets/image-20220524151823195.png)

![image-20220524152215144](git-test.assets/image-20220524152215144.png)

## 下载了SourceTree

高级设置中，勾选了自动处理LF，以及全局的gitignore（忽略vs和windows产生的一些文件）

![image-20220526100023024](git-test.assets/image-20220526100023024.png)

![image-20220524120200802](git-test.assets/image-20220524120200802.png)

### tips

- 忽略无需进行版本管理的文件：在仓库下建立 .gitignore文件，写入规则即可

- 忽略已经提交的文件：在sourcetree下，停止跟踪，添加到.gitignore

- 想要返回，修改内容时->先checkout回过去的时间点，再开创新分支

- 撤销过去的提交

  revert->通过新建与过去某次提交完全相反内容的提交来安全的撤销历史提交

- ss







