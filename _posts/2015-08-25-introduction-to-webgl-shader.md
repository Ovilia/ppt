---
title: 着色器编程之 WebGL 实现
layout: ppt
---

<section>

# 着色器编程

### 之 WebGL 实现

<a href="http://zhangwenli.com" target="_blank">羡辙</a>

<small>2015.08.26</small>

</section>





<section>

## 分享提纲

- 着色器是什么
- 着色器能做什么
- 着色器长什么样
- 着色器应用

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

## **着色**器（**shade**r）

</section>



<section data-transition="fade-in">

## **着色**器（**shade**r）

<div class="fragment">
    如果把渲染看做给屏幕上每个点<strong>上色</strong>的过程，
</div>
<div class="fragment">
    那么着色器就是用来指定上色规则的一段程序。
</div>

</section>



<section>

## 可以没有着色器吗？

### OpenGL

可以，按 <a href="https://www.opengl.org/wiki/Rendering_Pipeline_Overview" target="_blank">OpenGL 固定管线</a>渲染。

### WebGL

不可以，WebGL 强制要求指定着色器。

### Three.js

可以，默认帮你指定了固定管线的着色器。

</section>

</section>





<section>
    
<section>

## 着色器能做什么

<div>
    <small>
        <a href="https://www.shadertoy.com/view/4dXGR4" target="_blank">例一</a>
        <a href="https://www.shadertoy.com/view/XlsGRs" target="_blank">例二</a>
        <a href="https://www.shadertoy.com/view/MdX3zr" target="_blank">例三</a>
    </small>
</div>

<div class="fragment">
    <p>猜一下，火焰效果多少行着色器代码？</p>
</div>

<div class="fragment">
    <h3>64</h3>
</div>

</section>



<section>

## 看一下代码

<pre><code data-trim>
// https://www.shadertoy.com/view/MdX3zr
float noise(vec3 p) //Thx to Las^Mercury
{
    vec3 i = floor(p);
    vec4 a = dot(i, vec3(1., 57., 21.)) + vec4(0., 57., 21., 78.);
    vec3 f = cos((p-i)*acos(-1.))*(-.5)+.5;
    a = mix(sin(cos(a)*a),sin(cos(1.+a)*(1.+a)), f.x);
    a.xy = mix(a.xz, a.yw, f.y);
    return mix(a.x, a.y, f.z);
}

float sphere(vec3 p, vec4 spr)
{
    return length(spr.xyz-p) - spr.w;
}

float flame(vec3 p)
{
    float d = sphere(p*vec3(1.,.5,1.), vec4(.0,-1.,.0,1.));
    return d + (noise(p+vec3(.0,iGlobalTime*2.,.0)) + noise(p*3.)*.5)*.25*(p.y) ;
}

float scene(vec3 p)
{
    return min(100.-length(p) , abs(flame(p)) );
}

vec4 raymarch(vec3 org, vec3 dir)
{
    float d = 0.0, glow = 0.0, eps = 0.02;
    vec3  p = org;
    bool glowed = false;
    
    for(int i=0; i<64; i++)
    {
        d = scene(p) + eps;
        p += d * dir;
        if( d>eps )
        {
            if(flame(p) < .0)
                glowed=true;
            if(glowed)
                glow = float(i)/64.;
        }
    }
    return vec4(p,glow);
}

void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    vec2 v = -1.0 + 2.0 * fragCoord.xy / iResolution.xy;
    v.x *= iResolution.x/iResolution.y;
    
    vec3 org = vec3(0., -2., 4.);
    vec3 dir = normalize(vec3(v.x*1.6, -v.y, -1.5));
    
    vec4 p = raymarch(org, dir);
    float glow = p.w;
    
    vec4 col = mix(vec4(1.,.5,.1,1.), vec4(0.1,.5,1.,1.), p.y*.02+.4);
    
    fragColor = mix(vec4(0.), col, pow(glow*2.,4.));
    //fragColor = mix(vec4(1.), mix(vec4(1.,.5,.1,1.),vec4(0.1,.5,1.,1.),p.y*.02+.4), pow(glow*2.,4.));

}
</code></pre>

</section>

</section>





<section>

<section>

## 着色器编程

大坑！慎入！

<div class="fragment">
    <h4>OpenGL Shading Language (GLSL)</h4>
    <p>OpenGL 对应的着色器语言</p>
</div>

<div class="fragment">
    <p>类似 C 语言</p>
    <p>超强类型</p>
    <p><small>一开始只当 JavaScript 写，结果 0.0 写成 0 就挂了，甚至<code>float a = (float)1;</code>也是不行的</small></p>
</div>

<div class="fragment">
    <h4>调试非常困难</h4>
    <p>报错信息很不具体，很多时候只有一个行号，甚至行号还是错的</p>
</div>

<div class="fragment">
    <h4>如果你一定要跳这个坑的话……</h4>
    <ul>
        <li>
            <a href="http://benvanik.github.io/WebGL-Inspector/" target="_blank">WebGL Inspector</a>
        </li>
        <li>
            <a href="https://chrome.google.com/webstore/detail/threejs-inspector/dnhjfclbfhcbcdfpjaeacomhbdfjbebi" target="_blank">Three.js Inspector</a>
        </li>
    </ul>
</div>

</section>



<section>

## 着色器分类

### 顶点着色器（Vertex Shader）

对每个面片的顶点运行一次

### 片段着色器（Fragment Shader）

对每个片段（可以简单理解为屏幕像素）运行一次

</section>



<section>

## 存储限定符（Storage Qualifiers）

<small><a href="https://www.khronos.org/files/webgl/webgl-reference-card-1_0.pdf" target="_blank">WebGL 1.0 API Quick Reference Card</a></small>

<div class="fragment">
    <h3><code>const</code></h3>
    <p>我们熟悉的常量</p>
</div>

<div class="fragment">
    <h3><code>attribute</code></h3>
    <p>每个顶点对应各自的值</p>
</div>

<div class="fragment">
    <h3><code>uniform</code></h3>
    <p>所有顶点共用同一个值</p>
</div>

<div class="fragment">
    <h3><code>varying</code></h3>
    <p>把数据从顶点着色器传到片段着色器</p>
</div>

</section>



<section>

## 着色器实例

<a href="http://zhangwenli.com/DepthOfField" target="_blank">景深模糊渲染</a>

<!--iframe src="http://zhangwenli.com/DepthOfField" width="800" height="600"></iframe-->

</section>



<section>

### 深度着色器

#### 顶点着色器

<pre><code data-trim>
void main()
{
    gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0);
}
</code></pre>

#### 片段着色器

<pre><code data-trim>
uniform float farmostDepth;

void main()
{
    float zbuffer = gl_FragCoord.z * gl_FragCoord.w * farmostDepth;
    gl_FragColor = vec4(zbuffer, zbuffer, zbuffer, 1.0);
}
</code></pre>

</section>

<section>

#### Three.js 中传入参数

<pre><code data-trim>
new THREE.ShaderMaterial({
    uniforms: {
        farmostDepth: {
            type: 'f',
            value: 500
        }
    },
    attributes: {},
    vertexShader: DofDemo.shader.depthVert,
    fragmentShader: DofDemo.shader.depthFrag,
    transparent: true
});
</code></pre>

<small><a href="https://github.com/Ovilia/DepthOfField" target="_blank">GitHub</a></small>

</section>



<section>

### 景深模糊着色器

#### 顶点着色器

<pre><code data-trim>
varying vec2 vUv;

void main()
{    
    // passing texture to fragment shader
    vUv = uv;
    
    gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0);
}
</code></pre>

#### 片段着色器

<pre><code data-trim>
varying vec2 vUv;
uniform sampler2D texture;
uniform sampler2D depth;

// ...

texture2D(texture, vUv); // get color of current fragment
</code></pre>

</section>

<section>

#### Three.js 中传入参数

<pre><code data-trim>
new THREE.ShaderMaterial({
    texture: {
        type: 't',
        value: DofDemo.rttTexture
    },
    depth: {
        type: 't',
        value: DofDemo.rttDepth
    }, // ...
});
</code></pre>

<small><a href="https://github.com/Ovilia/DepthOfField" target="_blank">GitHub</a></small>

</section>

</section>





<section>

<section>

<div class="fragment">
    <h2>现在，你已经学会了写字</h2>
</div>

<div class="fragment">
    <h2>离成为一个作家</h2>
</div>

<div class="fragment">
    <h2>只差</h2>
</div>

<div class="fragment">
    <h2>一万小时的努力了</h2>
</div>

</section>



<section>

## 延伸阅读

- <a href="https://www.opengl.org/wiki/Rendering_Pipeline_Overview" target="_blank">Rendering Pipeline Overview</a>
- <a href="http://book.douban.com/subject/1392483/" target="_blank">《计算机图形学》</a>
- <a href="https://developer.nvidia.com/gpugems/GPUGems/gpugems_pref01.html" target="_blank">《GPU Gems》</a>
- <a href="http://book.douban.com/subject/1312194/" target="_blank">《OpenGL 编程指南》</a>
- <a href="http://book.douban.com/subject/4186709/" target="_blank">《OpenGL Shading Language》</a>

</section>

</section>
