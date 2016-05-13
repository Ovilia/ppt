---
title: 前端可视化的测试实践
layout: ppt
sharedate: 2016.05.28
fullpage: <svg version="1.1" baseProfile="full" width="400" height="400" xmlns="http://www.w3.org/2000/svg"></svg>
---

<section markdown="1" class="home-section">

# 前端可视化的测试实践

<div class="home-author">
    <h2 class="subject">SegmentFault D-Day 厦门站分享</h2>
    <div class="author">
        <a href="http://zhangwenli.com" target="_blank">羡辙</a>
    </div>
    <div class="from">百度前端工程师</div>
    <div class="date">{{ page.sharedate }}</div>
</div>

</section>


<section markdown="1">

## 羡辙其人

<div style="text-align: center;">
    <svg id="owl-svg" version="1.1" baseProfile="full" viewBox="0 0 1088 1088" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" style="width: 100px; height: 100px; padding: 20px; border-radius: 25px; background-color: #22C3AA"><g transform="translate(80 32)" fill="white"><path id="owl-body" d="M 0 0 L 0 896 A 128 128 0 0 0 128 1024 L 640 1024 A 64 64 0 0 0 704 960 A 64 64 0 0 0 640 896 L 192 896 A 64 64 0 0 1 128 832 L 128 256 L 768 256 L 768 896 A 128 128 0 0 0 896 1024 A 64 64 0 0 0 960 960 A 64 64 0 0 0 896 896 L 896 768 L 896 0 L 768 128 L 640 128 L 128 128 L 0 0 z "></path><path id="owl-left-eye" d="M 256 288 A 64 64 0 0 0 192 352 A 64 64 0 0 0 256 416 A 128 128 0 0 1 384 544 A 128 128 0 0 1 256 672 A 128 128 0 0 1 128 544 A 64 64 0 0 0 64 480 A 64 64 0 0 0 0 544 A 64 64 0 0 0 0 544 A 256 256 0 0 0 256 800 A 256 256 0 0 0 512 544 A 256 256 0 0 0 256 288 z " class="eye"></path><path id="owl-right-eye" d="M 576 352 A 192 192 0 0 0 384 544 A 192 192 0 0 0 576 736 A 64 64 0 0 0 640 672 A 64 64 0 0 0 576 608 A 64 64 0 0 1 512 544 A 64 64 0 0 1 576 480 A 64 64 0 0 1 640 544 A 64 64 0 0 0 704 608 A 64 64 0 0 0 768 544 A 64 64 0 0 0 767.72656 538.54492 A 192 192 0 0 0 576 352 z " class="eye"></path></g></svg>
    <div><a href="http://zhangwenli.com">zhangwenli.com</a></div>
</div>


<div class="fragment fade-in" markdown="1">
### 个人经历

2016.4 至今：开源图表库 [ECharts](http://echarts.baidu.com) **@百度**

2009-2016：本科+硕士 **@上海交通大学** 软件学院，数字艺术媒体实验室
</div>

<div class="fragment fade-in" markdown="1">
### 技术作品

- [《Three.js 入门指南》](http://www.ituring.com.cn/book/1272)**@图灵社区**
- [Polyvia](https://github.com/Ovilia/Polyvia)：基于 JavaScript 的 Low-Poly 图像、视频处理算法
- [jWebAudio](http://01org.github.io/jWebAudio/)：基于 Web Audio 的轻便音频库

*更多作品参见 [github.com/Ovilia](http://github.com/Ovilia)*

</div>

</section>




<section>
<section markdown="1">

## 当我们谈论前端测试的时候，<br>我们在谈论什么

<div class="fragment fade-in" markdown="1">
### 功能测试

- 逻辑
- **用户界面**
- 兼容性
- ……

### 性能测试

- 时间
- 空间
- ……
</div>

</section>


<section markdown="1">

## 用户界面应该怎么测？

### 自动测试

### 半自动测试

### 手动测试

</section>


<section markdown="1">

## 事实上，<br>我们是如何在测用户界面的？

<div class="fragment fade-in" markdown="1">
不测……
</div>

</section>
</section>





<section markdown="1">

## ECharts



</section>
