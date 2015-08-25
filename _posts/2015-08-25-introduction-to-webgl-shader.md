---
title: 着色器编程之 WebGL 实现
layout: ppt
---

<section>

# 着色器编程

### 之 WebGL 实现

<a href="http://zhangwenli.com" target="_blank">羡辙</a>

2015.08.26

</section>





<section>

## 分享提纲

- 着色器是什么
- 着色器能做什么
- 着色器长什么样
- 学写简单的着色器

</section>





<section>

<section>

## 着色器（shader）是什么

<div class="fragment">
    <blockquote>指一组供计算机图形资源在执行渲染任务时使用的指令。——<a href="https://zh.wikipedia.org/wiki/%E7%9D%80%E8%89%B2%E5%99%A8" target="_blank">Wiki</a></blockquote>
</div>

<div class="fragment">
    <h3>说人话！</h3>
</div>

</section>



<section data-transition="fade-out">

## 着色器（shader）

</section>



<section data-transition="fade-in fade-out">

## **着色**器（shader）

</section>



<section data-transition="fade-in fade-out">

## **着色**器（**shader**）

</section>



<section data-transition="fade-in fade-out">

## **着色**器（**shader**）

<div class="fragment">
    如果把渲染看做给屏幕上每个点<strong>上色</strong>的过程，
</div>
<div class="fragment">
    那么着色器就是用来指定上色规则的一段程序。
</div>

</section>

</section>





<section>
    
<section>

## 着色器能做什么

<iframe width="640" height="360" frameborder="0" src="https://www.shadertoy.com/embed/4dXGR4?gui=true&t=10&paused=false" allowfullscreen></iframe>

<div>
    <small><a href="https://www.shadertoy.com/view/4dXGR4" target="_blank">查看源码</a></small>
</div>

</section>



<section>

<iframe width="640" height="360" frameborder="0" src="https://www.shadertoy.com/embed/Ms2SD1?gui=true&t=10&paused=false" allowfullscreen></iframe>

<div>
    <small><a href="https://www.shadertoy.com/view/Ms2SD1" target="_blank">查看源码</a></small>
</div>

</section>



<section>

<iframe width="640" height="360" frameborder="0" src="https://www.shadertoy.com/embed/MdX3zr?gui=true&t=10&paused=false" allowfullscreen></iframe>

<div>
    <small><a href="https://www.shadertoy.com/view/MdX3zr" target="_blank">查看源码</a></small>
</div>

</section>



<section>

<iframe width="640" height="360" frameborder="0" src="https://www.shadertoy.com/embed/XlsGRs?gui=true&t=10&paused=false" allowfullscreen></iframe>

<div>
    <small><a href="https://www.shadertoy.com/view/XlsGRs" target="_blank">查看源码</a></small>
</div>
<div>
    <small>更多着色器效果：<a href="https://www.shadertoy.com/" target="_blank">www.shadertoy.com</a></small>
</div>

</section>

</section>





