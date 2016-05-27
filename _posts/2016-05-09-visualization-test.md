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

## 羡辙

<div class="center">
    <svg id="owl-svg" version="1.1" baseProfile="full" viewBox="0 0 1088 1088" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" style="width: 100px; height: 100px; padding: 20px; border-radius: 25px; background-color: #22C3AA"><g transform="translate(80 32)" fill="white"><path id="owl-body" d="M 0 0 L 0 896 A 128 128 0 0 0 128 1024 L 640 1024 A 64 64 0 0 0 704 960 A 64 64 0 0 0 640 896 L 192 896 A 64 64 0 0 1 128 832 L 128 256 L 768 256 L 768 896 A 128 128 0 0 0 896 1024 A 64 64 0 0 0 960 960 A 64 64 0 0 0 896 896 L 896 768 L 896 0 L 768 128 L 640 128 L 128 128 L 0 0 z "></path><path id="owl-left-eye" d="M 256 288 A 64 64 0 0 0 192 352 A 64 64 0 0 0 256 416 A 128 128 0 0 1 384 544 A 128 128 0 0 1 256 672 A 128 128 0 0 1 128 544 A 64 64 0 0 0 64 480 A 64 64 0 0 0 0 544 A 64 64 0 0 0 0 544 A 256 256 0 0 0 256 800 A 256 256 0 0 0 512 544 A 256 256 0 0 0 256 288 z " class="eye"></path><path id="owl-right-eye" d="M 576 352 A 192 192 0 0 0 384 544 A 192 192 0 0 0 576 736 A 64 64 0 0 0 640 672 A 64 64 0 0 0 576 608 A 64 64 0 0 1 512 544 A 64 64 0 0 1 576 480 A 64 64 0 0 1 640 544 A 64 64 0 0 0 704 608 A 64 64 0 0 0 768 544 A 64 64 0 0 0 767.72656 538.54492 A 192 192 0 0 0 576 352 z " class="eye"></path></g></svg>
    <div><a href="http://zhangwenli.com">zhangwenli.com</a></div>
</div>

### 个人经历

2016.4 至今：开源图表库 [ECharts](http://echarts.baidu.com) **@百度**

2009-2016：本科+硕士 **@上海交通大学** 软件学院，数字艺术媒体实验室

### 技术作品

- [《Three.js 入门指南》](http://www.ituring.com.cn/book/1272)**@图灵社区**
- [Polyvia](https://github.com/Ovilia/Polyvia)：基于 JavaScript 的 Low-Poly 图像、视频处理算法
- [jWebAudio](http://01org.github.io/jWebAudio/)：基于 Web Audio 的轻便音频库

*更多作品参见 [github.com/Ovilia](http://github.com/Ovilia)*

</section>






<section>

<section markdown="1">
## [ECharts](http://echarts.baidu.com/)

- 一个纯 Javascript 的图表库
- 兼容主流浏览器，移动友好
- 底层依赖轻量级的 Canvas 类库 [ZRender](https://github.com/ecomfe/zrender)
- 提供直观、生动、可交互，可高度个性化定制的**数据可视化图表**

<div id="echarts-intro" class="echarts"></div>

</section>



<section markdown="1">

## 测试渲染相关部分

### 目标

<div class="fragment fade-in" markdown="1">
- 像素级精确测试渲染结果
</div>
<div class="fragment fade-in" markdown="1">
- 尽可能自动化测试
</div>

<div class="fragment fade-in" markdown="1">
### 问题
- 如何描述测试用例的预期表现？
- 如何保证版本间渲染效果的一致性？
- 如何快速定位到 bug？
- 如何测试不同设备的表现？
- ……
</div>



<div class="center">
<large class="fragment fade-in">
如何测试前端可视化产品？
</large>
</div>

</section>

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
- 老牌的单元测试框架
- jQuery 家族钦定测试框架
</div>

### [Jasmine](http://jasmine.github.io)

<div class="fragment fade-in" markdown="1">
- *行为驱动*（*Behavior-Driven*）的测试框架
- 支持异步测试
</div>

<div class="fragment fade-in" markdown="1">
#### TDD vs. BDD
- TDD（Test-Driven Development）测试驱动开发
- BDD（Behavior-Driven Development）测试驱动开发
</div>

### [Mocha](https://mochajs.org/)

<div class="fragment fade-in" markdown="1">
- BDD，语法和 Jasmine 相似度极高
- 支持更多插件，如*断言*（*Assertion*）库 [Chai](http://chaijs.com/)
</div>

</section>



<section markdown="1">

## 大同小异的语法

~~~
// QUnit
test("pow(2, 2) should return 4", function(){
    equal(math.pow(2, 2), 4, "result was " + result);
});
test("pow(2, 3) should return 8", function(){
    equal(math.pow(2, 3), 8, "result was " + result);
});

// Jasmine
describe("pow", function(){
    it("should raise 2 to the power of 2", function(){
        expect(math.pow(2, 2)).toBe(4);
    });
    it("should raise 2 to the power of 3", function(){
        expect(math.pow(2, 3)).toBe(8);
    });
});

// Mocha
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

- 按钮在屏幕的显示位置是否正确？
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



<section markdown="1">
## 如何自动化测试**渲染**相关部分？

<div class="fragment fade-in" markdown="1">
### HTML、SVG

可使用 Nightwatch.js 这类库测试 DOM 结构
</div>

<div class="fragment fade-in" markdown="1">
### Canvas
</div>

<ul>
  <li class="fragment fade-in">渲染出结果，靠人眼看
    <ul>
      <li class="fragment fade-in">重复工作量大</li>
      <li class="fragment fade-in">人眼无法识别细微差别</li>
    </ul>
  </li>
  <li class="fragment fade-in"><code>toDataURL()</code> 保存成图片
    <ul>
      <li class="fragment fade-in">比较图片相同？</li>
      <li class="fragment fade-in">如何描述期望？</li>
      <li class="fragment fade-in">如何尽可能自动化测试？</li>
    </ul>
  </li>
</ul>

</section>

</section>



<section>

<section markdown="1">

## 对 ECharts 做测试

### 渲染无关部分

**Jasmine 单元测试**

例：线性数据管理模块 `List`

~~~
describe('List', function () {
    var testCase = window.utHelper.prepare(['echarts/data/List']);

    describe('Data Manipulation', function () {
        testCase('initData 1d', function (List) {
            var list = new List(['x', 'y']);
            list.initData([10, 20, 30]);
            expect(list.get('x', 0)).toEqual(10);
            expect(list.get('x', 1)).toEqual(20);
            expect(list.get('x', 2)).toEqual(30);
            expect(list.get('y', 1)).toEqual(20);
        });

        // ...
    });
});
~~~

<div class="fragment fade-in" markdown="1">
如何测试渲染相关部分？
</div>

</section>



<section markdown="1">

### 渲染相关部分

例：配置项 `title.text` 允许 `\n` 表示换行

<div class="fragment fade-in" markdown="1">
#### **手动测试**

- 设置参数
- 人眼查看渲染效果是否换行

~~~
chart.setOption({
    series: [],
    title: {
        text: 'first line\nsecond line'
    }
});
~~~
</div>

<div class="fragment fade-in">
<img class="with-bg center" src="{{ site.url }}/img/posts/2016-05-09-visualization-test-01.png" />
</div>

</section>



<section markdown="1">

#### **半自动测试**

如何测试？

<div class="fragment fade-in" markdown="1">
- 测试不同配置项设置下的渲染一致性
  - 期望相同：如设置等于默认值的字体颜色，期望与默认情况相同
  - 期望不同：如改变字体颜色，期望与默认情况不同
</div>
<div class="fragment fade-in" markdown="1">
- 测试不同版本的渲染一致性
  - 以某次发布版本为基线，手动查看效果
  - 以后每次发布比较和基线比较 Canvas 是否一致
</div>
<div class="fragment fade-in" markdown="1">
- 对于失败的案例
  - 使用 [js-imagediff](https://github.com/HumbleSoftware/js-imagediff) 输出 Canvas 图像的 **diff 图**
  - 比较 Canvas 操作栈
</div>

</section>



<section markdown="1">

## 如何比较 Canvas？

- 使用 `canvas.toDataURL()` 比较 **Canvas 图像**是否一致
- 使用 [Canteen](https://github.com/platfora/Canteen) 比较 **Canvas 操作**是否一致

<div class="fragment fade-in">
对于同一个底层绘图环境，Canvas 操作相同，渲染出的图像一定相同，反之则不成立
</div>

<div class="fragment fade-in">
<p class="center lg-mg"><large>操作一致是图像一致的充分非必要条件</large></p>
</div>

<div class="fragment fade-in" markdown="1">
### 比较 Canvas 内容
操作更简单，不依赖第三方库
</div>

<div class="fragment fade-in" markdown="1">
### 比较 Canvas 操作
更严格的测试，发现潜在错误
</div>

</section>



<section markdown="1">

## Canvas Diff

<table>
  <tr>
    <td><img src="{{ site.url }}/img/posts/2016-05-09-visualization-test-03.png" class="with-bg" /></td>
    <td><img src="{{ site.url }}/img/posts/2016-05-09-visualization-test-04.png" class="with-bg" /></td>
    <td><img src="{{ site.url }}/img/posts/2016-05-09-visualization-test-05.png" class="with-bg" /></td>
  </tr>
  <tr>
    <td class="center">Canvas 1</td>
    <td class="center">Canvas 2</td>
    <td class="center">Canvas Diff</td>
  </tr>
</table>

</section>



<section markdown="1">

## 测试用例 (1)

### 测试标题字重默认值是 `normal`

~~~
var testCase = {
  name: 'should display bold font weight',
  option1: {
    series: [],
    title: {
      text: 'bold font vs. normal font',
      textStyle: {
      }
    }
  },
  option2: {
    series: [],
    title: {
      text: 'bold font vs. normal font',
      textStyle: {
        fontStyle: 'normal'
      }
    }
  }
};

var optionCompare = function(isExpectEqual, title, option1, option2) {
  it(title, function(done) {
    require(['newEcharts'], function (ec) {
      var canvas1 = helper.getRenderedCanvas(ec, option1);
      var canvas2 = helper.getRenderedCanvas(ec, option2);

      // canvas context and images
      var ctx1 = canvas1.getContext('2d');
      var ctx2 = canvas2.getContext('2d');
      var img1 = canvas1.toDataURL();
      var img2 = canvas2.toDataURL();

      // compare canvas content or operation stack
      var compare1 = compare2 = null;
      if (STRATEGY === 'content') {
        compare1 = img1;
        compare2 = img2;
      } else if (STRATEGY === 'stack') {
        compare1 = ctx1.hash()
        compare2 = ctx2.hash();
      }

      // expect to equal, or not
      if (isExpectEqual) {
        expect(compare1).toEqual(compare2);
      } else {
        expect(compare1).not.toEqual(compare2);
      }

      done();
    });
  });
};

optionCompare(true, testCase.name, testCase.option1, testCase.option2);
~~~
</section>



<section markdown="1">
## 用例分析 (1)

<div class="fragment fade-in" markdown="1">
### 比较 Canvas 内容 vs. 操作

测试结果表明：两种配置的 Canvas 内容是一致的，而操作是不一致的。
</div>

<div class="fragment fade-in" markdown="1">
分析操作栈发现，在 Canvas 上绘制时使用了 `bolder` 操作，但是由于该字体家族不存在粗体字重，因此实际的显示效果和 `normal` 相同。

因此，这是一个 bug。
</div>

<div class="fragment fade-in" markdown="1">
在本案例中，比较 Canvas **操作**得到的结论是**正确**的，比较 Canvas **内容**得到的结论是**漏报**（*false negative*）的。
</div>

</section>



<section markdown="1">

## 测试用例 (2)

### 测试标题样式设为 `oblique` 时，没有使用 `italic`<sup>[1]</sup>

~~~
var testCase = {
    name: 'should display oblique different from italic',
    option1: {
        series: [],
        title: {
            text: 'oblique vs. italic',
            textStyle: {
                fontStyle: 'oblique'
            }
        }
    },
    option2: {
        series: [],
        title: {
            text: 'oblique vs. italic',
            textStyle: {
                fontStyle: 'italic'
            }
        }
    }
};
~~~

<div class="footnote" markdown="1">
[1] `italic` 表示由设计师手动绘制的斜体字，而 `oblique` 是在显示时，在原字体样式上做斜切处理。事实上，很少有字体同时存在这两种样式，通常都是互相通用的。参见 [font-style: italic vs oblique in CSS](http://stackoverflow.com/questions/1680624/font-style-italic-vs-oblique-in-css)。
</div>

</section>



<section markdown="1">
## 用例分析 (2)

### 该案例存在的潜在问题

<div class="fragment fade-in" markdown="1">
如果我们希望测试标题样式为 `oblique` 时，是否真正设置正确，我们是无从很难判断的。

我们只能判断该样式与 `normal`、`italic` 等的结果不同，从侧面得出结论。

这一点在软件测试中是一个普遍存在的潜在问题。
</div>

<div class="fragment fade-in" markdown="1">
### 比较 Canvas 内容 vs. 操作

测试结果表明：两种配置的 Canvas 内容是一致的，而操作是不一致的。
</div>

<div class="fragment fade-in" markdown="1">
分析操作栈发现，绘制时的确分别使用了 `oblique` 与 `italic`，但是由于两者显示效果一致，所以产生了以上分歧。

因此，这不是一个 bug。
</div>

<div class="fragment fade-in" markdown="1">
在本案例中，比较 Canvas **操作**得到的结论是**正确**的，比较 Canvas **内容**得到的结论是**误报**（*false positive*）的。
</div>

</section>



<section markdown="1">

## 结论

通常比较 Canvas 操作得到的结论更稳健

<div class="fragment fade-in" markdown="1">
比较操作也不总是符合预期的，取决于测试用例

（思考反例）
</div>

<div class="fragment fade-in" markdown="1">
### 推荐的比较方式
- 先比较 Canvas 操作
- 如果测试失败
  - 查看 Canvas 图像 diff
  - 查看 Canvas 操作栈 diff
</div>

</section>

</section>





<section markdown="1">

## 前端可视化的测试实践

<div class="fragment fade-in" markdown="1">
### 可视化相关测试的思路
- 渲染无关部分做单元测试
- 渲染相关部分做 UI 测试
  - 测试不同配置项设置下的渲染一致性
  - 测试不同版本的渲染一致性
  - 查看 Canvas 图像与操作栈 diff 分析失败原因
</div>

</section>





<section markdown="1">

## 扩展阅读

- [Which JavaScript Test Library Should You Use? QUnit vs Jasmine vs Mocha](http://www.techtalkdc.com/which-javascript-test-library-should-you-use-qunit-vs-jasmine-vs-mocha/)

- [Comparison of three major javascript unit testing frameworks](https://github.com/kgroat/javascript-test-framework-comparison)

- [Jasmine vs. Mocha](http://marcofranssen.nl/jasmine-vs-mocha/)

- [font-style: italic vs oblique in CSS](http://stackoverflow.com/questions/1680624/font-style-italic-vs-oblique-in-css)

</section>





<section markdown="1">

{% include author.html %}

</section>





<section markdown="1">

## 调研问卷

<p><img src="{{ site.url }}/img/posts/2016-05-09-visualization-test-02.png" /></p>

</section>





<script type="text/javascript" src="{{ site.url }}/js/echarts.min.js"></script>

<script type="text/javaScript">

window.onload = function() {
    Reveal.addEventListener( 'slidechanged', function( event ) {
        if (event.indexh === 2 && event.indexv === 0) {
            setEChart();
        }
    });

};

function setEChart() {
    console.log(document.getElementById('echarts-intro').clientHeight);
    var introChart = echarts.init(document.getElementById('echarts-intro'));

    var xAxisData = [];
    var data = [];
    for (var i = 0; i < 50; i++) {
        xAxisData.push(i);
        data.push((Math.sin(i / 5) * (i / 5 -10) + i / 6) * 5)
    }

    introChart.setOption({
        backgroundColor: '#08263a',
        xAxis: {
            show: false,
            data: xAxisData
        },
        visualMap: {
            show: false,
            min: 0,
            max: 50,
            dimension: 0,
            inRange: {
                color: ['#41D9C5', '#CDFF5D', '#FF8BBA']
            }
        },
        grid: {
          left: 50,
          right: 30,
          top: 30,
          bottom: 30
        },
        yAxis: {
            axisLine: {
                show: false
            },
            axisLabel: {
                textStyle: {
                    color: '#4a657a'
                }  
            },
            splitLine: {
                show: true,
                lineStyle: {
                    color: '#08263f'
                }
            },
            axisTick: {
                show: false
            }
        },
        series: [{
            type: 'bar',
            data: data,
            itemStyle: {
                normal: {
                    barBorderRadius: 5,
                    shadowBlur: 10,
                    shadowColor: '#111'
                }
            },
            animationEasing: 'elasticOut',
            animationEasingUpdate: 'elasticOut',
            animationDelay: function (idx) {
                return idx * 20;
            },
            animationDelayUpdate: function (idx) {
                return idx * 20;
            }
        }]
    });
}

</script>
