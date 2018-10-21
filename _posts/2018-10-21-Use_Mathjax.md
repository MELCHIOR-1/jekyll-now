---
layout: post
title: "Github Jekyll使用Mathjax显示公式"
date: 2018-10-21
categories: opinion
tags: [resources, jekyll]
image: http://gastonsanchez.com/images/blog/mathjax_logo.png
---

One of the rewards of switching my website to [Jekyll](http://jekyllrb.com/) is the
ability to support **MathJax**, which means I can write LaTeX-like equations that get
nicely displayed in a web browser, like this one \\( \sqrt{\frac{n!}{k!(n-k)!}} \\) or
this one \\( x^2 + y^2 = r^2 \\).

<!--more-->

<img class="centered" src="https://www.mathjax.org/badge/mj-logo.svg" />

在写一些技术文章或偏理论文章的时候，难免会需要输入几个公式。因此，要求博客支持公式显示功能。目前最常用的公式输入方式就是使用LaTeX代码或类似的代码，在网页中，使用Mathjax进行解析，从而生成我们可读的公式。这篇文章介绍如何使用jekyll在github搭建的博客中显示公式。

### 什么是Mathjax？

如果你浏览 MathJax 的官网 [(www.mathjax.org)](http://www.mathjax.org/) 你会发现它 *是一个能在任何浏览器中显示数学公式的一个开源JS引擎*.

### 怎么在Jekyll中集成MathJax？
**废弃的方案：**

参考Dason Kurkiewicz的博客[using Jekyll and Mathjax](http://dasonk.github.io/blog/2012/10/09/Using-Jekyll-and-Mathjax/).

1、在```_config.yml```文件的markdown字段改为```markdown: redcarpet```，默认的是使用 kramdown。

2、在```_layouts```文件夹的```page.html```中，添加如下代码：
{% highlight r %}
<script type="text/javascript"
    src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
{% endhighlight %}

**新方案：**

在准备改```_config.yml```文件的时候，发现提示：'redcarpet' is unsupported on GitHub Pages now.

也就是说，要在github上使用，就必须使用 kramdown。在知乎上找到了一个满意的答案 [如何在基于jekyll的github上发布的博客中支持MathJax(LaTex数学公式)？](https://www.zhihu.com/question/62114522).

步骤很简单，在_includes/head.html （我使用的是NexT主题，对应的文件在_includes/_partials/head.html ）中添加如下代码：
```
<!-- 数学公式 -->
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
      inlineMath: [['$','$']]
    }
  });
</script>
```
### 如何使用？
使用方法跟写LaTeX一样。对于行内公式，使用```$\$...\$$```；对于需要单独成行的公式，使用```$\$\$...\$\$ $```。

如勾股定理：

$$ \alpha^2+\beta^2=\gamma^2 $$

其中，$\alpha, \beta, \gamma$为正实数。
