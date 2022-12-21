---
title: RTL布局适配
date: 2018-05-01
layout: layouts/post.njk
---

![](../../img/rtl-styling-intro@2x.jpg)

全世界有超过2.92亿人将阿拉伯语作为他们的第一语言。阿拉伯语（al-Arabiyyah，发音为al ʕarabijja/, /ʕarabiː/）是我的母语，而且我时常开发同时支持从左到右（LTR）和从右到左（RTL）文字布局的网站。

译注：下文将用LTR指代主流的从左到右的文字布局，用RTL指代阿拉伯文、希伯来文等从右到左的文字布局。

## RTL文字适配介绍

CSS默认的文档方向为从左到右。如果你检查你的浏览器并检查浏览器的默认样式，你会发现`html`元素的`dir`（或者“direction”）属性默认值为`ltr`。下面是一个简单的例子来展示LTR和RTL布局的区别。

```html

![](../../img/rtl-intro-1.png)

注意看RTL部分，文字阅读方向是从右到左，和LTR相反。幸运的是，浏览器已经为这个简单的例子做了所有的工作。要切换文档的方向，你只需要在根元素上添加`dir`属性。

```html
<html dir="rtl">...</html>
```

当`dir`改变后，下面的元素也会自动翻转：标题、段落、链接、图片和表单元素。

值得一提的是，有一个`dir="auto"`属性，它会根据解析的内容自动切换方向。根据[HTML规范](https://www.w3.org/TR/2011/WD-html5-author-20110809/global-attributes.html)的说法：

> 作者应该只在不确定文本方向，同时也没有更好的服务端解析方法​的时候使用这个值

<p class="codepen" data-height="428" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="7662a5f048c5a6a1bbdb89905327c965" style="height: 428px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Basic Example">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/7662a5f048c5a6a1bbdb89905327c965">
  RTL Styling - Basic Example</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

除了在HTML元素上设置`dir=rtl`属性，我们还可以将`direction: rtl`作为CSS样式添加。

```css
.element { direction: rtl; }
```

然而，CSSWG建议将文本方向定义在`html`根元素上，以确保在缺少CSS的情况下显示正确的布局。

## 翻转设计图的基础案例

让我们看一个更详细的例子，来了解如何将LTR布局的设计翻转为RTL布局。

![rtl-intro-ltr.jpg](../../img/rtl-intro-ltr.jpg)

```html
<article class="media">
    <img src="blueberry-cheesecake.jpg" alt="">
    <div class="media__content">
      <h2>Blueberry Cheesecake</h2>
      <p>...</p>
      <p><a href="#" class="link">View Recipe</a></p>
    </div>
</article>
```

最开始，我使用了传统的float来将图片左对齐，然后使用了clearfix来清除浮动。

```css
.media:after {
    content: "";
    display: block;
    clear: both;
}

.media__photo {
    float: left;
    width: 200px;
    margin-right: 16px;
}
```

当我们添加`dir="rtl"`后，结果如下所示：
![](../../img/rtl-intro-ltr-2.jpg)

所有元素除了图片都被翻转了。这是因为图片设置了`float: left`和`margin-right: 16px`。为了修复这个问题，我们需要覆盖这些样式：
```css
.media[dir="rtl] img {
    float: right;
    margin-right: 0;
    margin-left: 16px;
}
```

<p class="codepen" data-height="572" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="8f6024ed27c37f51b17198fc3c321a63" style="height: 572px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Example 1 - Floats">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/8f6024ed27c37f51b17198fc3c321a63">
  RTL Styling - Example 1 - Floats</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

## 在LRT布局中混排英文和阿拉伯文

在LTR布局中混排英文和阿拉伯文，会是什么效果？嗯，结果看起来会有点奇怪。

![](../../img/ltr-mix-1.jpg)

浏览器没有正确显示标题。对于阿拉伯语的读者来说，这个标题会让人感到难以阅读，除非你是作者本人。标题应该按照下图所示的顺序阅读。

![](../../img/ltr-mix-2.jpg)

为了避免此类问题，尽可能地设置好文字的正确方向。一旦在元素上设置了`dir="rtl"`，它就会按照预期的方式显示。

![](../../img/ltr-mix-3.jpg)

<p class="codepen" data-height="563" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="b254fb1c68ce1f8cce9c5b0917228326" style="height: 563px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/b254fb1c68ce1f8cce9c5b0917228326">
  RTL Styling - Test</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

当标题更长的时候，情况会变的更复杂。下面，我把标题变长了一点，然而结果并不是预期中的。我在图片中加了数字以显示标题的正确顺序。

![](../../img/ltr-mix-4.jpg)

当`dir="rtl`设置在元素上以后，标题就会变得清晰多了。句子看起来语法正确，而且顺序也是正确的。

![](../../img/ltr-mix-5.jpg)

<p class="codepen" data-height="490" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="02f4dccfb898bee7d1e1daa71f3bd6ac" style="height: 490px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test 2">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/02f4dccfb898bee7d1e1daa71f3bd6ac">
  RTL Styling - Test 2</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

## 字体处理

根据LTR和RTL布局的设计，每个方向都应该有一个特定的字体。有些字体可以用于多种语言，这很好。然而，品牌和企业倾向于为RTL使用不同的字体。

为了实现这点，我们应该为项目设置不同的字体。更多细节请参见[自动化工具](./#自动化工具)。

## Font Family

根据CSS的规则，`font-family`会在字体加载失败的时候自动回退到另一个字体。然而，如果第一个字体中没有相应的字形，它就会尝试使用第二个字体。

根据 [MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-family):
> 字体的选定不是在发现用户计算机上安装的列表中的第一个字体时停止。相反，对字体的选择是逐字进行的。也就是说即使某个字符周围都在某个字体中可以显示，但该字符在当前的字体文件中没有适合的图形，那么会继续尝试列表中靠后的字体。

[Omar Bourhaouta](https://codepen.io/bourhaouta/pen/GRgLqYL?editors=0100) 做了个demo来证明上面的说法：
<p class="codepen" data-height="316" data-theme-id="dark" data-default-tab="css,result" data-user="bourhaouta" data-slug-hash="GRgLqYL" style="height: 316px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL font fallback">
  <span>See the Pen <a href="https://codepen.io/bourhaouta/pen/GRgLqYL">
  RTL font fallback</a> by omar bourhaouta (<a href="https://codepen.io/bourhaouta">@bourhaouta</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

```css
body {
    font-family: 'Roboto','Amiri', sans-serif;
}
```

Roboto字体没有识别到阿拉伯文的字形，所以它回退到了第二个字体。

## Flexbox 布局

Flexbox 基于文档的writing mode。writing mode用于指定block在页面上的布局方式。例如，中文网站是从上到下布局的。writing mode就是为了这个目的而存在的。在flexbox中，条目根据文档的writing mode进行分配。英语和阿拉伯语的 `writing-mode` 的默认值是 `horizontal-tb`。

根据 [Mozilla Developer Network](https://developer.mozilla.org/zh-CN/docs/Web/CSS/writing-mode) (MDN), `horizontal-tb` 意思是：
> 对于左对齐（ltr）文本，内容从左到右水平流动。对于右对齐（rtl）文本，内容从右到左水平流动。下一水平行位于上一行下方。

当页面的方向切换到RTL，flexbox会相应地翻转它的项目。这是一个显著的好处！下面的插图显示了flexbox轴是如何根据文档方向翻转的。

![](../../img/flexbox-axis.jpg)

在下面的例子中，我放置了3个条目，并为每个条目编号，以显示方向更改时的不同。

```html

```html
<div class="element">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
</div>
```

```css
.element {
    display: flex;
    flex-direction: row; /* Default value, added for clarity */
}
```

![](../../img/rtl-flexbox-1.jpg)

<p class="codepen" data-height="428" data-theme-id="dark" data-default-tab="result" data-user="shadeed" data-slug-hash="76082ed22d043f1ebcdcf1037dda13f2" style="height: 428px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test 3">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/76082ed22d043f1ebcdcf1037dda13f2">
  RTL Styling - Test 3</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

## Grid 布局

和flexbox相似，grid布局取决于文档的writing mode，这为我们提供了和flexbox一样的好处。

下方的案例中，当页面方向为LTR时，侧边栏应该在左侧，`main`内容在右侧。对于RTL，它们是相反的。当我们使用grid布局时，根据页面的方向，翻转将自动完成。

```html
<div class="element">
    <div class="side">Side</div>
    <div class="main">Main</div>
</div>
```

```css
.element {
    display: grid;
    grid-template-columns: 220px 1fr;
    grid-gap: 1rem;
}
```

<p class="codepen" data-height="500" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="b15d4b4f81ce1b03ed9c1d99c560f64c" style="height: 500px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test 4">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/b15d4b4f81ce1b03ed9c1d99c560f64c">
  RTL Styling - Test 4</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

## 转换到RTL布局时的常见错误

非阿语使用者经常会犯一些容易规避的常见错误。

### 1. Letter-Spacing 字间距

在英语中为文字添加`letter-spacing`是很常见的，字体排印中也叫tracking。请看下面的英文的例子，看起来没问题。

![](../../img/letter-spacing.jpg)

然而当相同的字间距添加到阿拉伯文时，看起来就会很奇怪。看下面的真实案例。

![](../../img/letter-spacing-rtl.jpg)

注意，在增加了`letter-spacing`的内容中，每个单词的字母看起来都不相连。这是不对的。阿拉伯字母应该是连续的，而保留英语的`letter-spacing`会破坏这一点。在多语言混排中，请确保为阿拉伯字母设置`letter-spacing: 0`。

<p class="codepen" data-height="397" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="29b1428dac29ced513adc482b22e7372" style="height: 397px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test 6">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/29b1428dac29ced513adc482b22e7372">
  RTL Styling - Test 6</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

### 2. 文本透明度

为文字设置一个透明度很常见，比如为了让文字显得次要。这在英语中是可行的。然而当内容是阿拉伯文时，会导致一个奇怪的渲染问题：

![](../../img/rtl-transparency.jpg)

字母间会出现一个不同颜色的区域。在本例中，`letter-spacing`没有修改，所以这个问题不是由它引起的。解决方案很简单，只需不要让文字带有透明度即可。

<p class="codepen" data-height="395" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="d8b1d30b39933e0435e52b738b0402dd" style="height: 395px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test 7">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/d8b1d30b39933e0435e52b738b0402dd">
  RTL Styling - Test 7</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

### 3. 不同语言中单词的长度

有时候当一个网站被翻译到阿拉伯文时，元素的大小会因为翻译后的单词变大或变小而发生变化。请看下面的例子，我模拟了Smashing Magazine网站的导航栏。

![](../../img/website-header.png) 

在阿拉伯语版中，一些单词的大小与英语几乎相同，一些相同，一些更大。为了更清楚地说明这一点，下面是每个单词及其阿拉伯语翻译的对比。

![](../../img/website-header-translation.png)

你也许会想知道为什么我要谈论单词长度的差异，因为对于不同语言来说这是很正常和意料之中的。请看下面LinkedIn的例子。

![](../../img/word-length-linkedin.png) 

按钮“done”在阿拉伯语中被翻译为“تم”，这使得按钮变得太小，看起来很奇怪。最好为按钮设置一个`min-width`来考虑这种情况。我在浏览器的开发者工具中添加了这个，以显示它应该是什么样子的：
![](../../img/word-length-linkedin-2.png)

这里是Twitter的一个类似的例子：
![](../../img/word-length-twitter.png)

请注意，上面LinkedIn和Twitter的问题是在我写这篇文章的时候发现的（2019年12月13日）。

### 4. 文字溢出

我曾为一个项目处理混排文字，我遇到了一个关于文字溢出方向的问题。请看下面的例子。

```html

![](../../img/text-trun.png)

英语的溢出处理是错误的。省略号应该在元素的末尾，而不是开头。为了解决这个问题，可以在元素上设置`dir="auto"`属性，然后浏览器会自动解析内容并决定`dir`是什么。

```html
<p dir="auto">أهلاً وسهلاً بكم في المقال الذي يتحدث عن تصميم صفحات الويب للغة العربية</p>
<p dir="auto">Welcome to the article that explains how to design for RTL pages.</p>
```

![](../../img/text-trun-2.png)

<p class="codepen" data-height="240" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="aa503390e648a1738c0bb1492cbd72ae" style="height: 240px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Truncation">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/aa503390e648a1738c0bb1492cbd72ae">
  RTL Styling - Truncation</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

### 5. 选择不合适的RTL字体

设计RTL布局的界面并不意味着你可以选一个系统字体然后再也不管了。字体必须仔细挑选，以确保良好的可读性。以Twitter为例：

![](../../img/en-vs-ar.png)

从阿拉伯语使用者的视角来看，这个单词“تغريد”很难读，原因有以下几点：
- 字体不合适
- bold字重影响了可读性
- 单词的点太小了，而且距离字母太近了。

我做了一个更清晰的设计：

![](../../img/en-vs-ar-2.png)

### 6. 阿拉伯文数字混排

阿拉伯语中有两种写数字的形式：
- 印度: ٠ ١ ٢ ٣ ٤ ٥ ٦ ٧ ٨ ٩
- 阿拉伯: 0 1 2 3 4 5 6 7 8 9

英语中用到的数字是从阿拉伯数字中继承来的：“0, 1, 2, 3, 4, 5, 6, 7, 8, 9”。内容中的数字应该是一致的，要么是印度数字，要么是阿拉伯数字。

根据维基百科：
> 这些数字之所以在欧洲、美洲更常被称为“阿拉伯数字”，是因为在10世纪，来自北非的阿拉伯人引入了这些数字到欧洲，当时他们使用的数字是来自利比亚到摩洛哥的数字。

下图中的数字是印度数字和阿拉伯数字混排的。这看起来不一致，应该统一使用一种数字。
![](../../img/ar-numbers.png)

## RTL中可能不起作用的常见问题

### 1. 行高

为RTL布局设置一个不同的字体很常见。在本例中，测试一行和多行的内容。在下面的例子中，阿拉伯文的行间距比英文的小，即使它们的`line-height`都是一样的。

![](../../img/line-height-1.png)

这种情况最好的解决方案是为阿拉伯文内容设置一个更合适的`line-height`。

<p class="codepen" data-height="255" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="1cb6b25852a009d5fdaf1902bcfaa974" style="height: 255px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test 8">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/1cb6b25852a009d5fdaf1902bcfaa974">
  RTL Styling - Test 8</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

还是以Twitter为例，有一个按钮的文案被截断了，这就是因为`line-height`的值不合适。

![](../../img/ar-kasra.png)

在第一张图中，阿拉伯文的一个标点符号被截断了。这个标点符号叫做“kasra”，它对于正确阅读单词是很重要的。在下一张图中，我已经修复了行高，现在它就完整地显示出来了。

### 2. 超链接的下划线

默认的文字下划线在阿拉伯文中看起来不太好。因为这关系到阿拉伯文中字母和单词的书写方式。看下面的图：
![](../../img/rtl-underline-1.png)

我用红圈标记除了一些奇怪的地方。下划线覆盖了字母的点。还是不清楚？看下面的图：

![](../../img/rtl-underline-2.png)

红圈中的点被下划线分割。这使得文字难以阅读。解决方案是使用CSS自定义下划线。

#### 2.1. Text Decoration

~~可以通过`text-decoration-style`和`text-decoration-color`属性来改变下划线的样式和颜色。但是，这并不能保证在所有的字体和字号下都能正常工作。在写这篇文章的时候，Firefox是支持这些属性最好的浏览器。~~

**更新: 2020年1月18日**
根据 [这个](https://github.com/shadeed/rtl-styling/issues/4) Github上的issue, 原来使用`text-decoration-skip-ink`属性就可以解决点被下划线覆盖的问题。它的默认值是`skip`。

<p class="codepen" data-height="214" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="9f8c134e0d4fe1f0d58ba3c23cb96e41" style="height: 214px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Text Decoration">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/9f8c134e0d4fe1f0d58ba3c23cb96e41">
  RTL Styling - Text Decoration</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

在本文写作的时候，它在Safari中不被支持，旧版Edge中也不被支持（新版Edge支持）。下面是Safari中的效果：

![](../../img/text-deco-safari.png)

译注：现在是2022年，这个属性大胆地用吧。

#### 2.2. Box Shadow

浏览器对`box-shadow`的支持要比`text-decoration`好得多。可以检测浏览器是否支持`text-decoration`的新属性，如果不支持，就使用`box-shadow`属性。

```css

```css
.link-3 {
  color: #000;
  text-decoration-color: rgba(21, 132, 196, 0.2);
  text-decoration-style: normal;
  text-underline-offset: 4px;
  text-decoration-thickness: 2px;
  box-shadow: inset 0 -5px 0 0 rgba(#1584c4, 0.2);
}

@supports (text-decoration-color: red){
  .link-3 {
    box-shadow: none;
  }
}
```

![](../../img/text-deco-2.png)

### 3. Line Break 文字换行

如果你在CSS中使用了`word-break`属性，你需要另外测试一下，因为它可能会破坏阿拉伯语的单词。请看下面的例子：

```css

![](../../img/word-break.png)

圈出部分的阿拉伯语单词被这个属性破坏了。在阿拉伯语中，没有单词折行的概念，单词的字母是连接在一起的，所以不可能折行。

### 4. 缩写

在英语中，缩写是很常见的，比如星期，就可以用“Sat”来表示“Saturday”。

![](../../img/en-shorcuts.png)

在阿拉伯文中，这是不可能的，因为一个单词的字母是必须连接在一起的。

![](../../img/ar-shorcuts.png)

## 双向的图标

对称的图标不需要在LTR和RTL布局之间翻转。下面是一些例子：

![](../../img/general-icons.png)

对于另一些图标，则需要在RTL布局中翻转它们的方向，以便用户可以清楚地理解它们。

![](../../img/bidi-icons.png)

但也有一些例外。根据[material design](https://material.io/design/usability/bidirectionality.html#mirroring-elements)指南，如果一个图标代表一个人右手可以拿着的物体，那么它就不需要翻转。下面是一些例子：

![](../../img/bidi-icons-2.png)

### 媒体播放图标

我回想起了15年前的事情，那时我爸爸给我买了一个MP3播放器。它有一个播放按钮，它的方向指向左边。

![](../../img/mp3-player.jpeg)

一些图标是普世的，不需要我们翻转它们。原因是因为这些播放按钮代表的是磁带播放的方向，而不是时间的方向。下面是Spotify在英语和阿拉伯语中的样子：

![](../../img/spotify-icons.png)

需要注意的是，播放按钮没有被翻转，因为它们是普世的图标。

### 信息应用

在一个[有意思](https://twitter.com/AndaristRake/status/1210508742225285120)的Twitter讨论中，我被问到是否需要翻转信息应用中的发送图标。我做了一些针对Facebook Messenger，WhatsApp和Twitter的研究。

![](../../img/message-icons-1.png)

发送图标被翻转了，我个人认为这是正确的做法，因为这对我来说更加合理。另外，发送和“+”按钮的位置也应该翻转，使其更加正确。见下面的修改：

![](../../img/message-icons-1-fixed.png)

但是Facebook和Twitter没有翻转发送图标。

![](../../img/message-icons-2.png)

## 组件的翻转

在修改一些组件的时候，我需要有个快速的方法翻转它们。在Sketch应用中，我会复制一个组件，然后使用“flip”命令翻转它。同样的功能在Adobe XD和Figma中也是可用的。

![](../../img/sketch-flip.png)

为了更好地理解，下面是一个GIF，展示了我在翻转一个组件之后做了什么。

![](../../img/sketch-flip.gif)

## RTL设计中的注意事项

在本节中，我将介绍最常见的组件，并展示它们在RTL模式下应该如何显示。

### 按钮图标

在按钮中增加一个图标以展开一个菜单展示出更多操作是很常见的做法。在本例中，图标的位置应该在RTL布局中翻转。

![](../../img/button-icons.png)

### 表单输入

一些输入项在RTL布局中应该保持左对齐，例如邮箱和手机号码输入。

![](../../img/form-inputs.png)

把占位文字换成阿拉伯文没有任何意义，因为它们是从右到左的。一旦用户开始输入，文字又会变成从左到右。

![](../../img/form-inputs-2.png)

感谢[YuanHao Chiang](https://github.com/shadeed/rtl-styling/issues/6)提醒我上面的情况。

### 面包屑

面包屑中的箭头方向也应该翻转。

![](../../img/breadcrumbs.png) 

### 页头

页面头部组件包含开始和结束两个部分。在RTL布局中，这两个部分都应该翻转。

![](../../img/page-header.png)

### 表格

表格应该翻转。

![](../../img/tables.png)

### 标签页

在LTR布局中，标签页的图标应该在标签的左边。在RTL布局中，这些图标就应该在右边。

![](../../img/tabs.png)

### 卡片

对于一个水平的卡片，在RTL布局中，图片和文字的顺序应该翻转。

![](../../img/card.png)

### Toasts

你也许知道了，关闭和警告图标应该在左边。

![](../../img/toasts.png)

### 引用

代表引用的图标应该在右边，如果LTR的设计中是在左边的话。

![](../../img/blockquotes.png)

## CSS 逻辑属性

根据 [MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Logical_Properties):
> CSS 逻辑属性与值是 CSS 的一个模块，其引入的属性与值能做从逻辑角度控制布局，而不是从物理、方向或维度来控制。

我们来看一个简单的例子。假设我们需要将一串文本左对齐，添加以下内容：

```css
```css
.page-header {
    text-align: right;
}
```

针对RTL：

```css
[dir="rtl"] .nav-item {
    text-align: left;
}
```

有没有办法只添加一个`text-align`值，而不用根据文档的方向来改变值呢？这就是CSS逻辑属性的用场！

```css

```css
.page-header {
    text-align: end;
}
```

通过这种方法，`text-align`的方向会根据文档的方向来改变。[Demo](https://codepen.io/shadeed/pen/fb4e2f89ca23ab53f8b37112f027c85b?editors=1100)

为了让你更容易理解`start`和`end`的区别，我在下面的模拟图中做了标注。在LTR布局中，`start`等于左边，`end`等于右边。在RTL布局中，`start`等于右边，`end`等于左边。

![](../../img/start-end.png)

现在你已经对它的工作原理有了基本的了解，让我们来探索更多的CSS逻辑属性的例子和用例。

### 逻辑内间距 padding

![](../../img/css-logical-padding.png)

假设我们有一个搜索输入框，右边有一个搜索图标。我们应该在左右两边都添加内间距。右边的内间距要大一点，以防止文本掉到搜索图标下面。

```css

```css
.input--search {  
  padding-inline-start: 1rem;
  padding-inline-end: 2.5rem;
}
```

### 逻辑外边距 margin

![](../../img/css-logical-margin.png)

这个图标的右侧外边距需要是逻辑的，所以我们将使用`margin-inline-start`。

```css

```css
.page-header__avatar {  
  margin-inline-start: 1rem;
}
```

### 逻辑边框

![](../../img/css-logical-border.png)

很多时候你可能需要增加一个边框来表示导航元素是当前的。在上面的设计中，每个导航元素的左侧都有一个边框。我们如何让它成为逻辑的呢？

```css
.nav__item {  
  border-inline-start: 3px solid transparent;
}

.nav__item.is-active {
  border-color: #1e9ada;
}
```

### 逻辑边框半径 border-radius

![](../../img/css-logical-border-radius.png)

在上面的设计中，导航元素的背景只有右上角和右下角有边框半径。为了实现这一点，我们可以这样写：

```css
.nav__item {  
  border-start-end-radius: 30px;
  border-end-end-radius: 30px;
  background-color: transparent;
}

.nav__item.is-active {
  background-color: #ecf6fb;
}
```

### 逻辑属性对照表

当你不清楚哪个CSS属性可以用逻辑属性时，可以参考下面的对照表。请注意，这个表只包含了LTR和RTL布局中等同的属性。我是根据Adrian Roselli的[文章](https://adrianroselli.com/2019/11/css-logical-properties.html)制作的。

<p class="codepen" data-height="674" data-theme-id="dark" data-default-tab="result" data-user="shadeed" data-slug-hash="2981e62691e67452d9f282a5351d7c79" style="height: 674px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="CSS Logical Properties">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/2981e62691e67452d9f282a5351d7c79">
  CSS Logical Properties</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

除此之外，Adrian还创建了一个演示，可以很容易地理解逻辑属性和方向属性之间的区别。

<p class="codepen" data-height="635" data-theme-id="23655" data-default-tab="result" data-user="aardrian" data-slug-hash="bGGxrvM" style="height: 635px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Logical Properties Mapping">
  <span>See the Pen <a href="https://codepen.io/aardrian/pen/bGGxrvM">
  Logical Properties Mapping</a> by Adrian Roselli (<a href="https://codepen.io/aardrian">@aardrian</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

### 浏览器支持

译注：在2022年12月的时间点，上述提到的属性均已有很好的兼容性。本段略过不翻。

## CSS 命名规则

通常情况下，避免给CSS类命名时使用与元素直接相关的名称。使用可以提取为可重用组件的名称。请看：

```html

```html
<div class="c-section">
  <p><a href="#" class="see-link">See more</a></p>
</div>

<div class="c-section">
  <p><a href="#" class="see-link">Learn more</a></p>
</div>
```

在两个section中，链接是相同的，但是他们的label不同。在第二个section中，`see-link`不太合适。一个更好的名称可能是`c-link`。`c`代表组件，这是我从ITCSS框架中学到的。

现在你知道了概念，我们可以将其应用于RTL样式。下面的设计中一个section带有两个子元素。

![](../../img/css-naming.png)

与其给元素命名为`.c-page-header__left`和`.c-page-header__right`，我更倾向于使用`.c-page-header__start`和`.c-page-header__end`。这样做更加合理，因为它认定网站只能是LTR或RTL。

## 垂直滚动条

在我的认知中，CSS中容器内的垂直滚动条位置取决于页面方向。对于RTL布局，滚动条在左侧，而对于LTR，它在右侧。

请看下面的例子：

![](../../img/scroll-bar.png)

不过对于操作系统来说，浏览器的滚动条不会改变，无论操作系统的语言是什么，它都会停留在右侧。但是对于操作系统本身来说，滚动条会根据其语言而改变。

## 自动化工具

有一些很好的工具可以帮助我们更好地将设计从LTR转换为RTL。

### 1. Bi-App-Sass

Anas Nakawa的[Bi-App-Sass](https://github.com/anasnakawa/bi-app-sass）可以让你只写一次样式表，然后它会将其编译为两个不同的样式表，一个用于LTR，另一个用于RTL。

这个工具适用于大型项目。生成结果将是为每个语言适配的多个样式表。比如：
```sass
.elem {
  display: flex;
  @include margin-left(10px);
  @include border-right(2px solid #000);
}
```

转换后的CSS将是：
`app-ltr.css`
```css
.elem {
  display: flex;
  margin-left: 10px;
  border-right: 2px solid #000;
}
```

`app-rtl.css`
```css
.elem {
  display: flex;
  margin-right: 10px;
  border-left: 2px solid #000;
}
```

但是请注意，这个项目的最后一次提交是七年前（2015年11月）。

### 2. RTLCSS

Mohammad Younes的[RTLCSS](https://rtlcss.com/)是一个将LTR样式表转换为RTL样式表的框架。

这个工具的不同之处在于它只在CSS文件的构建版本上运行。例如，如果你有一个包含50多个Sass组件的项目，RTLCSS将非常有用，它可以解析编译后的CSS文件并创建一个RTL版本。

## 实际案例练习

### Website Header

我设计了一个特殊的布局，以向你展示我是如何处理和思考将其翻转为RTL布局的。

![](../../img/blog.png)

让我们先从header组件开始。为了正确地编码，我已经搭建了一个通用的结构。请注意，我已经将header分为一个主要部分和次要部分。此外，我还为各个部分添加了start和end类。

![](../../img/header-skeleton-1.png)

```css
.header__main,
.header__sub {
    display: flex;
    justify-content: space-between;
}
```

因为CSS的flexbox是根据页面的方向工作的，正如前面在本指南中解释的那样，它将自动翻转为RTL。

![](../../img/header-skeleton-2.png)

下一步是logo和导航之间的分割线。一开始，我考虑使用`border-right`。它可以工作，但不是最理想的。使用伪元素会更好，因为它将根据页面的方向翻转。

![](../../img/before-after.png)

```scss
.c-brand:after {
  content: "";
  display: inline-block;
  vertical-align: middle;
  width: 3px;
  height: 38px;
  border-radius: 5px;
  background: #e4e4e4;
  margin-inline-start: 1.25rem;
}
```

这是目前的成果：
![](../../img/header-initial.png)

接下来，我将处理主题组件（子标题中带有标签和计数器的那个）。这是LTR和RTL中主题组件的设计。注意计数器的位置是不同的。

![](../../img/topics.png)

起初这可能很容易，但LTR和RTL之间需要声明多个padding和margin。这是设计图：

![](../../img/topics-p-m.png)

```css
.topics-heading {
	margin-inline-end: 1.5rem;
}

.topics-list {
	margin-inline-end: 1rem;
}

.c-topic {
	padding-inline-start: 0.5rem;
}

.c-topic:not(:last-child) {
	margin-inline-end: 10px;
}

.c-topic__counter {
	margin-inline-start: 1rem;
}
```

如你所见，我使用了CSS的逻辑属性，而不是`left`和`right`。

下一步是“查看全部”链接。注意它末尾的箭头。以下是它的要求：
- 箭头的颜色应该在hover时变色。
- 箭头在hover的时候应该有个向右的动效。

我选择inline SVG实现。当我给箭头添加了一个`translate`动画时，我考虑了RTL。这里没有逻辑属性，我需要探索其他解决方案。我想到的一个解决方案是为margin添加动效。

```css
.c-link svg {
	margin-inline-start: 4px;
	transition: 0.15s ease-in;
}

.c-link:hover svg {
	margin-inline-start: 8px;
}
```

但是这种动销性能开销很大，尽管可以这么做。另一个解决方案是检测页面的方向，然后根据方向设置`translate`声明。

```css
.c-link:hover svg {
  transform: translateX(6px);
}

/* I’m using dir=rtl in the header for the purpose of clarity. It should be added to the root element. */
.c-header[dir="rtl"] .c-link svg {
  transform: scaleX(-1);
}

.c-header[dir="rtl"] .c-link:hover svg {
  transform: scaleX(-1) translateX(6px);
}
```

对于RTL，我增加了`scaleX(-1)`来水平翻转箭头图标。你也可以使用`rotate(180deg)`，但是scale对我来说更直观。

![](../../img/see-all.gif)

下一个时搜索输入框。有如下要求：
- 搜索图标必须出现在输入框的末尾。
- 图标的位置必须是动态的。

```css
.c-input--search {
  background-image: url("data:image/svg+xml...");
  background-position: right 6px center;
}

.c-header[dir="rtl"] .c-input--search {
  /* We replace the original icon with a flipped one. */
  background-image: url("data:image/svg+xml...");
  background-position: right 6px center;
}
```

此外，当用户输入的时候，文本不应该滑动到图标下面。为了避免这种情况，在右边或者左边添加padding。

![](../../img/input-padding.png)

```css
.c-input {
  padding-inline-end: 32px;
}
```

这是目前LTR和RTL的结果：
![](../../img/header-current-result.png)

接下来是移动端的菜单。我将使用汉堡图标来表示菜单。图标的位置将在LTR和RTL之间进行切换。动画的方向也是如此。

```css
![](../../img/header-menu-mobile.png)

在 [这里](https://codepen.io/shadeed/pen/aa0c9f6c73fe62d206b674c52dc4426e?editors=0100) 查看完整的代码。

## 致谢

特别要感谢我的妻子[Khouloud](https://twitter.com/kholoud840)，她持续不断的支持和多次审阅本指南。感谢[Adebiyi Adedotun Lukman](https://twitter.com/AdebiyiAL)和[Šime Vidas](https://twitter.com/simevidas)提供的宝贵意见。

## 参考链接

- [(Right to Left (The Mirror World](https://labs.spotify.com/2019/04/15/right-to-left-the-mirror-world/)
- [Let’s Talk About RTL](https://alfy.me/2014/07/26/lets-talk-about-rtl.html)
- [Basic Concepts of Flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)
- [Basic Concepts of Grid Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Basic_Concepts_of_Grid_Layout)
- [Right-to-Left Development: Tips and Tricks](https://steelkiwi.com/blog/right-left-development-tips-and-tricks/)
- [Arabic Numerals](https://en.wikipedia.org/wiki/Arabic_numerals)

<script async src="https://static.codepen.io/assets/embed/ei.js"></script>