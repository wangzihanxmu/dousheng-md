# 【第三届青训营-后端专场】课后作业 -《Go 语言上手-基础语言》

[![img](Go语言上手-课后作业.assets/fed1a3626ffaa1cd39065e7d1ab104a1300x300.image)](https://juejin.cn/user/967986342789704)

[社区助手 ![lv-2](Go语言上手-课后作业.assets/f597b88d22ce5370bd94495780459040.svg)](https://juejin.cn/user/967986342789704)

2022年05月06日 10:58 · 阅读 11280

关注

> 大家直接在评论区发布答案就可以哦~

### 课后作业：

1. 修改第一个例子猜谜游戏里面的[最终代码](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fwangkechun%2Fgo-by-example%2Fblob%2Fmaster%2Fguessing-game%2Fv5%2Fmain.go)，使用 fmt.Scanf 来简化代码实现

1. 修改第二个例子命令行词典里面的[最终代码](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fwangkechun%2Fgo-by-example%2Fblob%2Fmaster%2Fsimpledict%2Fv4%2Fmain.go)，增加另一种翻译引擎的支持

1. 在上一步骤的基础上，修改代码实现并行请求两个翻译引擎来提高响应速度

   < 作业提交截止时间：5月7日 10:00前 >

### 正确答案：

1. 核心代码就2行，替换之前的 [22-29 行代码](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fwangkechun%2Fgo-by-example%2Fblob%2Fmaster%2Fguessing-game%2Fv5%2Fmain.go%23L22-L29)

```
var guess int
_, err := fmt.Scanf("%d", &guess)
复制代码
```

1. 可以实现代码跑起来就得分

1. 可以实现代码跑起来就得分，常见的实现基于 waitGroup errGroup chan