# 将基于云的开发添加到 Chainlink 初学者工具包中

> 原文：<https://blog.chain.link/chainlink-starter-kits-cloud-development/>

现在可以在 Gitpod 中打开 Chainlink 初学者工具包。这对开发者意味着什么？启动开发环境的摩擦已经大大减少。您不需要担心安装需求或者合适的工具版本——这些都会为您处理。寻找 Chainlink Starter Kits repos 上的 `Open in Gitpod` 按钮。只需一次点击，您就可以进入基于云的开发环境，一切就绪！

## 将学习带到云端

学习一门新的编程语言或框架本身就够难的了。如果您想开始，而不担心设置整个开发环境，那么通过 Gitpod 选择使用初学者工具包是最简单的开始方式。让我们走一遍这个过程。

[https://www.youtube.com/embed/_epSwqMEydY?feature=oembed](https://www.youtube.com/embed/_epSwqMEydY?feature=oembed)

### 让它成为你自己的

您已经决定构建您的项目，或者可能注意到您想在现有的初学者工具包存储库中改进一些东西。两者的第一步是相同的。您将需要派生存储库。在 GitHub 页面右上方寻找 `Fork` 按钮。

<video width="800" height="498" autoplay="" loop="" muted="" playsinline=""><source src="https://blog.chain.link/wp-content/uploads/2022/07/unnamed-4.webm" type="video/webm">T2】</video>

### 叉子到底是什么？

根据 GitHub 的定义，fork 是您管理的存储库的副本。Forks 允许您在不影响原始存储库的情况下对项目进行更改。您可以通过拉请求从原始存储库中获取更新或将更改提交到原始存储库中。

一旦你创建了一个分支，你仍然可以使用 Gitpod。但是， `Open in Gitpod` 就需要稍加改动。

您可以使用 URL 技巧将 `gitpod.io/#` 添加到新的分叉存储库中。或者，如果您想更新 `README.md` ，您将需要更改下面的行。

```
[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)]
(https://gitpod.io/#https://github.com/smartcontractkit/hardhat-starter-kit)
```

你需要用你的 GitHub 账户替换 `<YOUR_ACCOUNT_HERE>` 。

```
[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)]
(https://gitpod.io/#https://github.com/<YOUR_ACCOUNT_HERE>/hardhat-starter-kit)
```

## 从这里去哪里

一旦你完成了回购，你就可以开始你的项目了。

如果您想打开一个拉动式请求(PR)来帮助改进初学者工具包，还有几个步骤。

首先，在你的分叉回购中，做出改变。

保存更改后，创建一个分支，并使用该分支将您的更改推送到 GitHub。

```
$ git fetch upstream

$ git merge upstream/main

$ git rebase main

$ git add README.md 

$ git commit -m "Fix: correct quickstart npm command"

$ git push

$ git push --set-upstream origin new_feature
```

一旦你的更改被上传到 GitHub，你应该会看到一条新消息。

![a screenshot of new feature pushes notification on GitHub](img/384ffdfb71073e7426fb6c10ad82b8d2.png)

如果您点击 `Compare & pull request` ，您将能够打开一个包含对上游存储库的更改的拉式请求。

![a screenshot of how to create pull requests to change the upstream repository](img/2d44d255ec2e47286ba287c5390fae13.png)

一旦您填写了解释您的更改的详细信息，请点击 `Create pull request` 。恭喜你！您已经向初学者工具包存储库发出了“拉”请求！

## 摘要

随着基于云的开发被添加到 Chainlink 初学者工具包中，开发人员现在有了一个更简单的入门途径。我们很期待看到你的作品。

访问[chain . link](https://chain.link/)或阅读[docs . chain . link](https://docs.chain.link/)上的文档，了解更多关于 Chainlink 的信息。 [要讨论一个集成，就去找专家。](https://chainlinkcommunity.typeform.com/to/OYQO67EF)