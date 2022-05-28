# 第十一节：Git 的正确使用姿势与最佳实践

## 概述

本节课程学习主要分成三个部分

1. Git 是什么

1. Git 命令的基本使用方式及原理

1. Git 常用的研发流程，我们应该选择怎样的研发流程

本课程围绕这三个部分进行描述，并通过演示 Git 操作，观察 Git 目录的来理解 Git 的原理。以及通过在 Github 上进行操作演示，来带领同学们了解什么是研发流程，符合最佳实践的研发流程是什么。

## 课前 (必修)

#### Git 安装

[git-scm.com/book/zh/v2/…](https://link.juejin.cn?target=https%3A%2F%2Fgit-scm.com%2Fbook%2Fzh%2Fv2%2F%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)

#### Git 基本命令学习

学习 Git Add / Commit 等命令，需要用 Shell 的方式执行，不要直接用图形化页面

[www.runoob.com/git/git-bas…](https://link.juejin.cn?target=https%3A%2F%2Fwww.runoob.com%2Fgit%2Fgit-basic-operations.html)

#### Github 账号创建

1. 完成 Github 账号创建

1. 配置公私钥认证

1. 创建一个个人仓库，并在该仓库上进行基本的 clone / push 操作

## 课中

### 引言

为什么要学习 Git ?

- Git 在开源社区，协同工作中非常重要

为什么要安排这个课程 ？

- 许多新同学，对 Git 完全不了解，或者是只知道基本命令，不了解正确的使用姿势和最佳实践

### Git 是什么

#### 版本控制

本地版本控制

- 依托于本地磁盘进行版本控制

集中式版本控制

- 存在一个统一的远端服务器，用于版本控制，本地不存储版本控制

分布式版本控制

- 每个库都拥有所有的版本控制信息，远端服务器用于不同库之间进行版本信息同步

#### 发展历史

最初版由 Liunx 创始人 Linus Torvalds 花两周时间开发而成，主要是为了用于 Linux 项目的维护

#### 衍生平台

- Gitlab [github.com/](https://link.juejin.cn?target=https%3A%2F%2Fgithub.com%2F)

- Github [gitlab.com/gitlab-org](https://link.juejin.cn?target=https%3A%2F%2Fgitlab.com%2Fgitlab-org)

- Gerrit [android-review.googlesource.com/q/status:op…](https://link.juejin.cn?target=https%3A%2F%2Fandroid-review.googlesource.com%2Fq%2Fstatus%3Aopen%2B-is%3Awip)

除此之外，还有 bitbucket, Coding, 码云 等一系列平台

### Git 命令基本使用方式和原理

#### Git 配置

- Git Config

Git 配置，分成本地，用户，系统基本的配置

- Git Remote

Git Remote 配置，分成 SSH 和 HTTP 两种协议实现，不同协议有不同的免密配置方式

#### 代码提交

- Git Add

将代码从工作区提交到暂存区

- Git Commit

将暂存区代码提交到 Git 存储

#### Git 存储基本概念

- Ref
  - Tag 仓库标签
  - Branch 仓库分支

- Object
  - Blob 存储文件内容信息
  - Tree 存储目录树信息
  - Commit 存储提交信息
  - Tag 存储附注标签信息

#### 代码同步

- Git Clone

将代码从远端拉取到本地

- Git Fetch & Git Pull

将远端仓库代码同步到本地仓库

- Git Push

将本地代码同步到远端仓库

### Git 研发流程

#### 集中式工作流

- Gerrit 平台

围绕主分支进行开发

#### 分支管理工作流

- Git Flow

- Github Flow

- Gitlab Flow

#### 如何合并代码

- Three Way Merge

- Fast Forward Merge

#### 选择合适的工作流

- 少量多次提交

- 保证 CR / CI 等流程通过后才可合入

- 尽量保证主分支整洁

## 课后

1. 寻找一个开源项目进行学习，并将学习笔记整理发布到 Github

1. 尝试向一个开源项目提交 PR


作者：青训营官方账号
链接：https://juejin.cn/post/7098182433941651492
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。