---
title: "博客开张:关于这里会写什么"
date: 2026-04-22T10:00:00+08:00
draft: false
tags: ["杂谈", "博客"]
categories: ["随笔"]
description: "用 Hugo + Cloudflare Pages 搭了个安卓开发博客,第一篇先聊聊打算写什么。"
cover:
  image: ""
  alt: ""
  caption: ""
  relative: false
---

## 为什么开这个博客

工作里折腾安卓源码、framework、kernel 的时间不少,踩过的坑、查过的资料、临时起意的实验,如果不记下来,过半年基本就忘光了。这里打算做一个自己的外部记忆。

## 会写什么

大致三块:

- **源码阅读笔记**:AOSP 里感兴趣的模块,从 SystemServer 到 WindowManager 到 Binder,慢慢啃。
- **调优与排障**:线上遇到过的性能问题、ANR、内存泄漏、冷启动优化的实战。
- **工具链折腾**:repo、AIDEGen、git worktree、perfetto、systrace,自己摸索出的工作流。

## 技术栈

博客本身的选型:

| 组件 | 选择 |
| --- | --- |
| 静态框架 | Hugo(extended) |
| 主题 | [PaperMod](https://github.com/adityatelange/hugo-PaperMod) |
| 托管 | Cloudflare Pages |
| 域名 / CDN | Cloudflare |
| 源码仓库 | GitHub |
| 评论(待接) | Waline(自托管在 GCP VPS) |
| 统计(待接) | Umami(自托管) |

选 Cloudflare Pages 而不是 GitHub Pages,主要是域名就在 Cloudflare 后台,DNS、证书、部署一站式,还免费。

## 一段代码示意

顺便试一下代码高亮:

```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        lifecycleScope.launch {
            val data = withContext(Dispatchers.IO) { loadData() }
            render(data)
        }
    }
}
```

```bash
# 本地预览
hugo server -D

# 发布新文章
hugo new content posts/xxx.md
git add . && git commit -m "post: xxx" && git push
```

---

就这样,先占个地方。下一篇大概率写 SystemServer 启动流程。
