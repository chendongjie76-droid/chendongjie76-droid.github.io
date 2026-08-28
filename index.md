---
layout: home
title: 首页
---

## 欢迎来到我的博客

这里记录我在 **Python 学习**、**算法练习**和**技术成长**道路上的思考与总结。

### 最新文章

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      <small>{{ post.date | date: "%Y-%m-%d" }}</small>
    </li>
  {% endfor %}
</ul>

### 关于我

- GitHub：[@chendongjie76-droid](https://github.com/chendongjie76-droid)
- 学习笔记：[learning-notes](https://github.com/chendongjie76-droid/learning-notes)

> 持续学习，持续输出。
