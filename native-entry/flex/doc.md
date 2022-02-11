图文+N种经典案例，这一次彻底掌握Flex布局
---
highlight: a11y-dark
---
> 前言

每次使用Flex布局时，总会在网上搜一堆资料，自己不会写？即使效果出来了，涉及到的属性配置也是一知半解？我就是这种情况。根据我个人的经验总结，主要有2点，1理解的不够透彻，2没有对知识点进行系统性的梳理和归纳总结。拒绝“Copy大法，眼会手不会，别人开口跪，咱们开口卒”，再简单的知识点都要过手。这一次就让我们彻底搞懂Flex，轻松实现各种响应式页面布局。

```css
{
  display: flex;
}
```

这张图包含了 Flex 的核心概念。接下来，我们逐一进行拆分：
1. Flex Container 被称为 Flex 容器，即需要声明 `display: flex`；
2. 里面的元素 Flex Item 被称为 Flex 元素，这里需要强调一下，是容器的`直系子元素`才能被称为 Item；
3. CSS Flexbox 是一种一维的布局模型。包含2根轴线，Main Axis 被称为主轴，Cross Axis 被称为交叉轴；
4. 过去，CSS的书写模式主要被认为是水平的，从左到右的。而 Flex 涵盖了书写模式的范围，所以我们不再假设一行文字是从文档的左上角开始向右书写, 新的行也不是必须出现在另一行的下面。它包含了 Start（起始线）和 End（终止线），后面会详细讲解；
5. Container 容器上有5个属性配置项和1个简写配置项；
6. Item 元素上有5个属性配置项。

#### flex 容器上的配置项


- flex-direction: row | row-reverse | column | column-reverse;
主轴方向：inline 向右 | inline 向左 | block 向下 | block 向上
另外，主轴方向也确定了交叉轴的方向。

- justify-content: flex-start | flex-end | center | space-between | space-around; 
主轴排列方式：起始线 | 终止点 | 居中 | 两侧分布 | 等间隔分布

- align-items: flex-start | flex-end | center | baseline | stretch; 
交叉轴排列方式：容器顶部 | 底部 | 垂直居中 | 基线 | 撑满整个高度

- flex-wrap: nowrap | wrap | wrap-reverse;
主轴排列方式：不换行 | 换行 | 反向排序并换行

- align-content: flex-start | flex-end | center | space-between | space-around | stretch; 
前置条件：多行弹性盒子模型才有效（flex-wrap: nowrap; 单行无效，单行使用 align-items）
项目在交叉轴上排列方式：起始点 | 终止点 | 中点 | 均匀分布 | 等间隔分布 | 拉伸‘自动’-大小的项目以充满容器

- flex-flow: <'flex-direction'> <'flex-wrap'>;
组合简写，常规配置为：`flex-flow: row nowrap;`

#### item 配置项

一般情况下，我们不会去设置 flex 配置项，采用默认配置.那默认值是什么？flex的默认配置为：`flex: 0 1 auto`。

- flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]

flex-grow: <number>;
flex-shrink: <number>;
flex-basis: <width | content | fill | length> | auto;
order: <number>;
align-self: auto | normal | start | end | center | self-start;

**参数详解**
- flex-grow: <number>;
定义 item 在 flex 中分配剩余空间的相对比例。默认为0（即为即使有剩余空间，也不会放大）

- flex-shrink: <number>;
定义了项目的缩小比例，默认为1（item宽度总和大于容器宽度时，等比缩小item宽度）,设置为0，当宽度不够时，也不会压缩宽度。

- flex-basis: <width | content | fill | length> | auto;
项目占据的主轴空间，默认 auto，即为本来的大小。
PS: flex-basis 的权重高于 item 本身设置的 width 值。

- order: <number>;
值越小，排序越靠前。默认为 0。

- align-self: auto | normal | start | end | center | self-start ...
覆盖 align-items 的值，个性化配置某一个元素在交叉轴上的对齐方式。默认为 auto。


#### 汇总默认配置
- justify-content: flex-start;
- align-items: flex-start;
- flex-direction: row;
- flex-wrap: nowrap;
- align-content: flex-start;
- flex-flow: row nowrap;

- flex: 0 1 auto;
- flex-grow: 0;
- flex-shrink: 1;
- flex-basis: auto;
- order: 0;
- align-self: auto;





---
临时使用

实际项目中，大多采用默认的 row 配置，即为 inline 向右；
###### justify-content 属性

`justify-content: flex-start | flex-end | center | space-between | space-around; `

设置主轴排列方式：起始线 | 终止点 | 居中 | 两侧分布 | 等间隔分布；


```html
<h3>justify-content: flex-start | flex-end | center | space-between | space-around; </h3>
<div class="main-flex">
  <div class="flex-container" style="justify-content: flex-start">
    <div class="flex-item">1</div>
    <div class="flex-item">2</div>
  </div>
  <div class="flex-container" style="justify-content: flex-end">
    <div class="flex-item">1</div>
    <div class="flex-item">2</div>
  </div>
  <div class="flex-container" style="justify-content: center">
    <div class="flex-item">1</div>
    <div class="flex-item">2</div>
  </div>
  <div class="flex-container" style="justify-content: space-between">
    <div class="flex-item">
      <button>1</button>
      <button>2</button>
    </div>
    <div class="flex-item" style="text-align: right;">
      <button>3</button>
      <button>4</button>
    </div>
  </div>
  <div class="main-flex">
    <div class="flex-container" style="justify-content: space-around;">
      <div class="flex-item">1</div>
      <div class="flex-item">2</div>
      <div class="flex-item">3</div>
    </div>
  </div>
</div>
```

实际项目中，居中分布、两侧分布、等间隔分布都会经常使用。




