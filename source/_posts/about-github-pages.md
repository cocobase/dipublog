---
title: about-github-pages
date: 2020-02-20 20:51:28
tags:
    - Github
---

我们可以使用Github的仓库托管关于自己个人博客、组织或者项目的网站。
  
本文将介绍Github Pages站点的基本概念：
- 了解Github Pages
- Github Pages网站的类型
- GitHub Pages 站点的发布来源
- 静态网站生成器
<!-- more -->

## 了解Github Pages
GitHub Pages是一个静态站点托管服务，可直接从GitHub上的存储库获取HTML，CSS和JavaScript文件，还可以选择在构建过程中运行这些文件并发布网站。您可以将站点托管在GitHub的github.io域或您自己的自定义域上。

## Github Pages网站的类型
有三种类型的 GitHub Pages 站点：项目、用户和组织。 项目站点连接到 GitHub 上托管的特定项目，例如 JavaScript 库。 用户和组织站点连接到特定的 GitHub 帐户。
  
用户和组织站点始终从名为 <user>.github.io 或 <organization>.github.io 的仓库发布。 除非您使用自定义域，否则用户和组织站点位于 http(s)://<username>.github.io 或 http(s)://<organization>.github.io。

项目站点的源文件与其项目存储在同一个仓库中。 除非您使用自定义域，否则项目站点位于 http(s)://<user>.github.io/<repository> 或 http(s)://<organization>.github.io/<repository>。
  
您只能为每个 GitHub 账户创建一个用户或组织站点。 项目站点（无论是组织还是用户帐户拥有）没有限制。

## GitHub Pages 站点的发布来源
GitHub Pages 站点的发布来源是存储站点源文件的分支或文件夹。 所有站点都有默认的发布来源，项目站点还有其他可用的发布来源。

用户和组织站点的默认发布来源是 master 分支。 如果用户和组织站点的仓库是 master 分支，您的站点将从该分支自动发布。 您无法为用户或组织站点选择不同的发布来源。

项目站点的默认发布来源是 gh-pages 分支。 如果项目站点的仓库有 gh-pages 分支，您的站点将从该分支自动发布。

项目站点也可以从 master 分支或 master 分支上的 /docs 文件夹发布。 要从这些来源之一发布站点，您必须配置不同的发布来源。 

如果选择 master 分支的 /docs 文件夹作为您的发布来源，GitHub Pages 将读取 /docs 文件夹中的所有内容以发布您的站点（包括 CNAME 文件）。例如，当您通过 GitHub Pages 设置编辑自定义域时，该自定义域将写入 /docs/CNAME。

## 静态网站生成器
GitHub Pages 会发布您推送到仓库的任何静态文件。 您可以创建自己的静态文件或使用静态站点生成器为您构建站点。 您还可以在本地或其他服务器上自定义自己的构建过程。 我们建议使用 Jekyll，它是一个静态站点生成器，内置 GitHub Pages 支持和简化的构建流程。

默认情况下，GitHub Pages 将使用 Jekyll 来构建您的站点。 如果您想使用除 Jekyll 以外的静态站点生成器，通过在发布来源的根目录中创建一个名为 .nojekyll 的空文件来禁用 Jekyll 构建过程，然后按照静态站点生成器的说明在 本地构建站点。

GitHub Pages 不支持服务器端语言，例如 PHP、Ruby 或 Python。