---
title: 工具栈 —— Linux与Windows切换使用Obsidian，出现 unexplained changes 问题的解决
date: 2026-03-05
description: Obsidian工具的使用问题记录
tags:
  - 工具
categories:
  - 工具栈
image: /cover/Obsidian.png
draft: false
---

如果你的Obsidian文档在Linux与Windows间来回切换，可能会涉及到文件的保存换行符问题，但这样的话就容易导致一个问题，那就是内容无差异，Obsidian却提示unexplained changes。我们首先分析原因。

Obsidian编辑器，默认以`LF`为结尾保存文件，这也是Linux系统的默认换行符。当我们在Windows上使用`git clone`某个Obsidian编辑的仓库时，可以知道，这个仓库目前所有的文件的换行符都是`LF`，而Windows的换行符默认是`CRLF`，所以，所以，在git clone 或者checkout的时候，就还得保证clone下来的所有文件，继续以`LF`为换行符，如果clone下来的文件以`CRLF`为换行符，这样Obsidian保存的时候，就会出现换行符的差异，此时就会提示`unchanged lines`，而这不是我们想要的。

```shell
# 确保clone下来的文件继续是LF结尾，而不会在clone到本地时，将仓库里的LF结尾自动转换成CRLF
git -c core.autocrlf=false clone https://github.com/user/repo.git
# 继续修改repo的.git/config
cd repo
git config core.autocrlf false
```

# Windows系统配置

```ini
[core]
        autocrlf = false
```

# Mac/Linux系统配置

```ini
[core]
        autocrlf = input
```

| 一、参考文章或视频链接                                                                                                                                                                                                                                     |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [1] [**Workaround for: Rendering markdown files on Windows results in timestamp changes (Detected by Git) - Obsidian**](https://forum.obsidian.md/t/workaround-for-rendering-markdown-files-on-windows-results-in-timestamp-changes-detected-by-git/53039) |
| [2] [**Viewing a file with different line endings causes file to save with new line endings**](https://forum.obsidian.md/t/viewing-a-file-with-different-line-endings-causes-file-to-save-with-new-line-endings/37955)                                     |
| [3] [**git中配置autocrlf来正确处理crlf**](https://blog.csdn.net/lysc_forever/article/details/42835203)                                                                                                                                                     |
| [4] [**10 Problems with Obsidian You’ll Realize When It’s Too Late**](https://medium.com/@theo-james/10-problems-with-obsidian-youll-realize-when-it-s-too-late-17e903886847)                                                                              |
| [5] [**解决不同系统换行符号导致的Git同步问题**](https://forum-zh.obsidian.md/t/topic/43203)                                                                                                                                                                |
