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

## 主流前端测试框架

### [QUnit](http://qunitjs.com)

<div class="fragment fade-in" markdown="1">
- 老牌的单元测试框架，发布于 2008 年
- jQuery 家族钦定测试框架
</div>

### [Jasmine](http://jasmine.github.io)

<div class="fragment fade-in" markdown="1">
- 发布于 2010 年
- *行为驱动*（*Behavior-Driven*）的测试框架
- 引入*测试套件*（*Test Suite*）概念
- 语法更自然
- 支持异步测试
</div>

### [Mocha](https://mochajs.org/)

<div class="fragment fade-in" markdown="1">
- 发布于 2012 年
- 和 Jasmine 相似度极高
- 支持更多插件，如*断言*（*Assertion*）库 [Chai](http://chaijs.com/)
</div>

</section>



<section markdown="1">

## 大同小异的语法

#### jUnit

~~~
test("pow(2, 2) should return 4", function(){
    equal(math.pow(2, 2), 4, "result was " + result);
});
test("pow(2, 3) should return 8", function(){
    equal(math.pow(2, 3), 8, "result was " + result);
});
~~~

#### Jasmine

~~~
describe("pow", function(){
    it("should raise 2 to the power of 2", function(){
        expect(math.pow(2, 2)).toBe(4);
    });
    it("should raise 2 to the power of 3", function(){
        expect(math.pow(2, 3)).toBe(8);
    });
});
~~~

#### Mocha

~~~
var expect = require('chai').expect;
describe("pow", function(){
    it("should raise 2 to the power of 2", function(){
        expect(math.pow(2, 2)).to.equal(4);
    });
    it("should raise 2 to the power of 3", function(){
        expect(math.pow(2, 3)).to.equal(8);
    });
});
~~~

</section>



<section markdown="1">

## 用户界面相关测试

- 购物车总价是否等于各个商品之和？
- 按钮在某个时刻是否是禁止状态？
- 在某个点击事件后，浏览器的标题是否符合预期？
- ……

<div class="fragment fade-in" markdown="1">
### 如何自动化测试这些场景？
</div>

</section>



<section markdown="1">

## [Nightwatch.js](http://nightwatchjs.org/)

自动化测试浏览器相关操作

~~~
module.exports = {
  'Demo test Google' : function (client) {
    client
      .url('http://www.google.com')
      .waitForElementVisible('body', 1000)
      .assert.title('Google')
      .assert.visible('input[type=text]')
      .setValue('input[type=text]', 'rembrandt van rijn')
      .waitForElementVisible('button[name=btnG]', 1000)
      .click('button[name=btnG]')
      .pause(1000)
      .assert.containsText('ol#rso li:first-child',
        'Rembrandt - Wikipedia')
      .end();
  }
};
~~~

</section>

</section>



<section markdown="1">

## ECharts


</section>




<section markdown="1">

## 扩展阅读

- [Which JavaScript Test Library Should You Use? QUnit vs Jasmine vs Mocha](http://www.techtalkdc.com/which-javascript-test-library-should-you-use-qunit-vs-jasmine-vs-mocha/)

- [Comparison of three major javascript unit testing frameworks](https://github.com/kgroat/javascript-test-framework-comparison)

- [Jasmine vs. Mocha](http://marcofranssen.nl/jasmine-vs-mocha/)

</section>
