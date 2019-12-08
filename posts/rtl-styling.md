---
title: Right-to-left Styling
date: 2018-05-01
layout: layouts/post.njk
---

![](../../img/rtl-styling-intro@2x.jpg)

There are 292+m people around the world that speak Arabic as their first language. Arabic (al-Arabiyyah) is my native language, and I sometimes build websites that need to support both LTR(Left to Right) and RTL(Right to Left) styles.

It's pronounced like that: /al ʕarabijja/, /ʕarabiː/. Play this sound to hear me pronounce it.

## Introduction to RTL styling
The default page direction in CSS is LTR. If you check a browser of your choice and inspect the default browser agent styles for the `html` element, you will notice that LTR is the default value for `direction` property. Below is a basic example to show the difference between a Left to Right (LTR) and a Right to Left (RTL) layout.

![](../../img/rtl-intro-1.png)

Notice for RTL, the text reads from Right to Left, which is the opposite for LTR text. Luckily, the browser did all the work for that simple example. To switch a document language direction, you will need to add the `dir` attribute to the root element.

```html
<html dir="rtl">...</html>
```

When the `dir` is changed, the following elements should be flipped automatically by default: Headings, Paragraphs, Links, Images, and Form Elements.

It's worth mentioning that there is a `dir="auto"` which switch the direction automatically based on the content parsed. According to the HTML spec:
> Authors are urged to only use this value as a last resort when the direction of the text is truly unknown, and no better server-side heuristic can be applied.

<p class="codepen" data-height="428" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="7662a5f048c5a6a1bbdb89905327c965" style="height: 428px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Basic Example">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/7662a5f048c5a6a1bbdb89905327c965">
  RTL Styling - Basic Example</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

In addition to setting the `dir=rtl` attribute on the HTML element, it's also possible to add `direction: rtl` as a CSS Style. 

```css
.element { direction: rtl; }
```

However, the CSSWG recommends that the direction should be defined on the root element `html` to ensure the correct bidirectional layout in the absence of CSS.

## Basic Example Of Flipping a Design
Let's take a more detailed example to explore how to flip a design from LTR to RTL.

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

Initially, I used the good old Float to align the image to the left in the LTR design, and of course, I used clearfix.

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

After adding `dir="rtl"` for the Arabic element, the result looks like the below.
![](../../img/rtl-intro-ltr-2.jpg)

Everything is flipped except the image. That's because it has `float: left` and `margin-right: 16px`. To solve that, I need to override those styles:
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

## Mixing English and Arabic Content in an LTR Layout
What would happen in case some text has a mix of English and Arabic words, while the layout is LTR? Well, the result will look weird.

![](../../img/ltr-mix-1.jpg)

The browser shows the title improperly. For an Arabic speaker, the title is confusing to read unless you're the author who wrote the title. It should read as the order in the below figure.

![](../../img/ltr-mix-2.jpg)

To avoid the above issue, it's recommended to use the appropriate language direction when possible. Once `dir="rtl"` is set on the element, it will appear as expected.

![](../../img/ltr-mix-3.jpg)

<p class="codepen" data-height="563" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="b254fb1c68ce1f8cce9c5b0917228326" style="height: 563px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/b254fb1c68ce1f8cce9c5b0917228326">
  RTL Styling - Test</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

It can be more complex if the title is longer. Here, I added a bit longer title and the result was unexpected. I added a number to show the correct order.

![](../../img/ltr-mix-4.jpg)

When `dir="rtl` is set on the element, the title is much clearer. In other words, the sentence looks grammatically correct and in the right order.

![](../../img/ltr-mix-5.jpg)

<p class="codepen" data-height="490" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="02f4dccfb898bee7d1e1daa71f3bd6ac" style="height: 490px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test 2">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/02f4dccfb898bee7d1e1daa71f3bd6ac">
  RTL Styling - Test 2</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

## Flexbox Layout Module
Flexbox is based on the writing mode of the document. The writing mode is used to specify how blocks are laid out on a page. For example, a Chinese website is laid from top to bottom. Writing mode is for that purpose. In Flexbox, items are distributed based on the writing mode of the document. The default value for `writing-mode` in English and Arabic is `horizontal-tb`

According to MDN, `horizontal-tb` means the following:
> Content flows horizontally from left to right, vertically from top to bottom. The next horizontal line is positioned below the previous line.

When the page direction is changed to RTL, Flexbox will flip its items accordingly. That's a huge benefit! Below is an illustration that shows how the Flexbox axis is flipped based on the direction.

![](../../img/flexbox-axis.jpg)

In the below example, I laid out three items and numbered each of them to see the difference when the direction change.

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
    flex-direction: row; /* Default value, added for explanation purposes */
}
```

![](../../img/rtl-flexbox-1.jpg)

<p class="codepen" data-height="561" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="02f4dccfb898bee7d1e1daa71f3bd6ac" style="height: 561px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test 2">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/02f4dccfb898bee7d1e1daa71f3bd6ac">
  RTL Styling - Test 2</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

## Grid Layout Module
Same as Flexbox, the grid layout module depends on the writing mode of the document, which gives us the same benefit that we get from using Flexbox.

In the below example, the sidebar should be on the left and the main on the right when the direction ins LTR. For RTL, it's vice versa. By using CSS Grid, the flipping will be done automatically as per the page direction.

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

![](../../img/ltr-rtl-grid.jpg)

<p class="codepen" data-height="500" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="b15d4b4f81ce1b03ed9c1d99c560f64c" style="height: 500px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test 4">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/b15d4b4f81ce1b03ed9c1d99c560f64c">
  RTL Styling - Test 4</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

## Common Mistakes When Flipping to RTL
There are some common mistakes that Non-Arabic speakers made and they are easy to spot.

### 1) Letter Spacing
In English, it's common to add `letter-spacing` between letters of a word. It's also known as Tracking in typography. Consider the following example for English content. It sounds normal.

![](../../img/letter-spacing.jpg)

However, if the same `letter-spacing` were added to Arabic content, it will look weird. Consider the following real-life example.

![](../../img/letter-spacing-rtl.jpg)

Notice that in the content with `letter-spacing`, the word's letters look **disconnected**. That's wrong. Arabic letters are supposed to look connected and keeping the spacing will be against that. Make sure to do `letter-spacing: 0` when working on a multilingual layout.

<p class="codepen" data-height="397" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="29b1428dac29ced513adc482b22e7372" style="height: 397px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test 6">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/29b1428dac29ced513adc482b22e7372">
  RTL Styling - Test 6</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

### 2) Text Transparency
It's common to change the transparency of text color to make it look secondary for example. That works for English. However, when the content is Arabic, that will cause a weird text rendering issue.

![](../../img/rtl-transparency.jpg)

There are some areas with a different color between each letter. In this example, `letter-spacing` hasn't been changed so the issue is not related to that. The solution is simply to use color without RGBA or opacity.

<p class="codepen" data-height="395" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="d8b1d30b39933e0435e52b738b0402dd" style="height: 395px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test 7">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/d8b1d30b39933e0435e52b738b0402dd">
  RTL Styling - Test 7</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

### 3) Differences in Words Size Between Languages
Sometimes, when a website is translated into Arabic, the sizing of elements change due to some words become bigger or smaller after translation. Consider the following example where I mocked the navigation of Smashing Magazine website.

![](../../img/website-header.png) 

In the Arabic Version, some of the words are almost the same size as its English counterpart, some are the same, and some are bigger. To make it more clear, here is a comparison between each word and its Arabic translation.

![](../../img/website-header-translation.png)

You might be thinking about why I'm talking about differences between word size since this is normal and expected. Consider the following real-life example from Linkedin.

![](../../img/word-length-linkedin.png) 

The button "Done" is translated to "تم" in Arabic which makes the button too small and weird. It's better to have a `min-width` for the button to account for such cases. I added that in the browser DevTools to show you how it's expected to look:
![](../../img/word-length-linkedin-2.png)

And here is a very similar example from Twitter:
![](../../img/word-length-twitter.png)

### 4) Text Truncation
In the past, I worked on a project with mixed content and I faced an issue related to truncated in the wrong direction. Consider the following example.

![](../../img/text-trun.png)

The truncation for the English text is incorrect. It should be at the end of the element, not the start of it. To solve that, set the attribute `dir="auto"` on the element itself and it will automatically parse the content and decide which `dir` it is.

```html
<p dir="auto">أهلاً وسهلاً بكم في المقال الذي يتحدث عن تصميم صفحات الويب للغة العربية</p>
<p dir="auto">Welcome to the article that explains about how to design web for RTL pages</p>
```

![](../../img/text-trun-2.png)

<p class="codepen" data-height="240" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="aa503390e648a1738c0bb1492cbd72ae" style="height: 240px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Truncation">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/aa503390e648a1738c0bb1492cbd72ae">
  RTL Styling - Truncation</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

### 5) Picking a Bad RTL Font
Having an RTL version of a design doesn't mean picking the default system font and calling it a day. It had to be picked carefully to ensure good readability. An example of that is Twitter:

![](../../img/en-vs-ar.png)

From an Arabic speaker point of view, the word "تغريد" is hard to read due to:
1) The font is not good
2) Bold style
3) The word dots are so small and really close to the letters

I mocked up a design that looks more clear.

![](../../img/en-vs-ar-2.png)

### 6) Mixing Hindi and Arabic Numerals
In Arabic, there are two ways of using numbers:
- Hindi: ٠ ١ ٢ ٣ ٤ ٥ ٦ ٧ ٨ ٩
- Arabic: 0 1 2 3 4 5 6 7 8 9

The numbers used in English are inherited from the Arabic ones "0, 1, 2, 3, 4, 5, 6, 7, 8, 9". When there is a content that has numbers, it should be consistent. Either it use Hindi or Arabic numerals.

According to Wikipedia:
> The reason the digits are more commonly known as "Arabic numerals" in Europe and the Americas is that they were introduced to Europe in the 10th century by Arabic-speakers of North Africa, who were then using the digits from Libya to Morocco.

In the following mockup, there is a mix of Hindi and Arabic numbers. This looks incosistent and it should unified by using one type of the numerals.
![](../../img/ar-numbers.png)

## Common Things That Might Not Work for RTL

### 1) Line Height

It's common to have a different typeface that will be served for the RTL layout. In that case, you should test how the content looks in one and multiple lines. In the following example, the spacing between the lines for the Arabic text is less than the English one. Even though both of them have the same `line-height`.

![](../../img/line-height-1.png)

It's important to account for that and to provide a suitable `line-height` for the Arabic content.

<p class="codepen" data-height="255" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="1cb6b25852a009d5fdaf1902bcfaa974" style="height: 255px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test 8">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/1cb6b25852a009d5fdaf1902bcfaa974">
  RTL Styling - Test 8</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

In Twitter, for example, there is a button with a cut-off content due to an unsuitable value of line-height.

![](../../img/ar-kasra.png)

Notice that in the first image, there is an Arabic diacritic cut-off. It's called "Kasra" and it's vital for reading the word correctly. In the other image, I fixed the line-height and now it appears fully without being cut-off.

### 2) Links Underline

The default text underline looks bad when used with Arabic words. It's related to how words and letters are written in Arabic. See the following illustration:
![](../../img/rtl-underline-1.png)

I highlighted the weird areas with the red circle. The underline is kind of covering the dots of the letters. It's still not clear? Here is a close up look.

![](../../img/rtl-underline-2.png)

The dots highlighted in blue are overlapping with the underline. This is not good and it makes the text hard to read. The solution is to use a custom underline with CSS.

#### 2.1) Text Decoration

It's possible to change the underline color and style with the new `text-decoration-style` and `text-decoration-color` properties. However, it might not be guaranteed to work with different typefaces and font sizes. At the time of writing, Firefox is the browser that has the best support for those properties.

```css
.link-2 {
  text-decoration-color: rgba(21, 132, 196, 0.2);
  text-decoration-style: normal;
  text-underline-offset: 4px;
  text-decoration-thickness: 2px;
}
```

![](../../img/text-deco-1.png)

#### 2.2) Box Shadow

The browser support is much better than `text-decoration` and actually, it's possible to detect the support for one of the new `text-decoration` properties and if not supported, the Box Shadow solution will be used.

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

### 3) Line Break

If the CSS has `word-break`, you need to test that since it might *break* the Arabic words. Consider the following:

![](../../img/word-break.png)

The areas with a circle around are broken Arabic words due to the effect of `word-break`. In Arabic, there no such thing as breaking words. The letters of a word are connected with each other so it's not possible to break a word.

### 4) Words Shortcuts

In English, it's common to have shortcuts for the week days. For example, "Saturday" becomes "Sat".

![](../../img/en-shorcuts.png)

While in Arabic, this not possible at all since a word's letters are meant to be connected.

![](../../img/ar-shorcuts.png)

## Bidirectional Icons

There are symmetric icons that don't need to be flipped between LTR and RTL layouts. Here are some examples:

![](../../img/general-icons.png)

For some icons, it's important to flip the direction of it so it can be clearly understood by the user. That's because the direction of the page is from right to left.

![](../../img/bidi-icons.png)

## Flipping a Component
While working on some components, I need a way to quickly flip a component. In the Sketch App, I started copying each component and then flip it with a flip command. The same functionality is available in Adobe XD and Figma.

![](../../img/sketch-flip.png)

To see what I mean in action here is a GIF image that shows what I did after flipping the component.

![](../../img/sketch-flip.gif) 

## RTL Design Considerations
In this section, I'll go through the most commonly used components and show how it should look in RTL mode.

### Button Icons
It's common to have a button that opens a menu for more actions. In that case, the icon place should be flipped.

![](../../img/button-icons.png)

### Form Inputs
Some form inputs should remain left-aligned in RTL. For example, email and mobile number inputs.

![](../../img/form-inputs.png)

### Breadcrumbs
The arrows in the breadcrumbs pattern should be flipped, too.

![](../../img/breadcrumbs.png) 

### Page Header
A page header component contains a start and end sections. Each one of them will be flipped in RTL.

![](../../img/page-header.png)

### Tabs
For a tabs component, the icons are on the left of the label in LTR. In RTL, this should be flipped.

![](../../img/tabs.png)

### Card
In a horizontal card, the order of the image and content is flipped in RTL.

![](../../img/card.png)

### Toast
As you might expect, close and warning icons are flipped.

![](../../img/toasts.png)

## CSS Logical Properties
According to MDN:
> CSS Logical Properties and Values is a module of CSS introducing logical properties and values that provide the ability to control layout through logical, rather than physical, direction and dimension mappings.

Whats I'm interested to shed light on is the margin, padding and borders properties. I won't dig deep into that since it's out of the scope of this article.

Let's take a very simple example. I need to have a space between navigation links in a header, so I added the following.

```css
.nav-item {
    margin-left: 16px;
}
```

And for RTL:
```css
[dir="rtl"] .nav-item {
    margin-right: 16px;
}
```

What if there is a one-line that will change the margin direction based on the language? There you go with CSS Logical Properties!

```css
.nav-item {
    margin-inline-end: 16px;
}
```

By having that, the margin will change automatically based on the direction of the page. If you want to dig more into that, here is a great [article](https://adrianroselli.com/2019/11/css-logical-properties.html) by Adrian Roselli.

## CSS Naming Convention
In general, avoid naming CSS classes with names that are too attached to the element. Use a name that can be extracted to a reusable component. Consider the following:

```html
<div class="c-section">
  <p><a href="#" class="see-link">See more</a></p>
</div>

<div class="c-section">
  <p><a href="#" class="see-link">Learn more</a></p>
</div>
```

In both sections, the link is the same but its label is different. In the second section, `see-link` doesn't make sense to be used. A good name could be `c-link`. The `c` stands for the component which I learned from the ITCSS framework.

Now that you got the idea, it applies to RTL styling as well. In the below design mockup, there is a section with two children.

![](../../img/css-naming.png)

Instead of naming the elements with a presentational names like `.c-page-header__left` and `.c-page-header__right`. I named them `.c-page-header__start` and `.c-page-header__end`. This is more future proof and doesn't assume that the website is in LTR or RTL only.

## Automation Tools
There are great tools that make our job easier when we need a way to flip a design from LTR to RTL.

### 1) bi-app-sass
> [bi-app](https://github.com/anasnakawa/bi-app-sass) lets you write your stylesheets once, and have them compiled into 2 different stylesheets one for left-to-right layout, and the other for right-to-left layouts

This tool is useful for a large project. The result will be multiple stylesheets for each direction (LTR, RTL). Consider the following:
```sass
.elem {
  display: flex;
  @include margin-left(10px);
  @include border-right(2px solid #000);
}
```

The resulted CSS will be as below:
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

Though the last commit in the Github repo was 4 years ago (Nov 2015).

### 2) RTLCSS
> [RTLCSS](https://rtlcss.com/) is a Framework for converting Left-To-Right (LTR) Cascading Style Sheets(CSS) to Right-To-Left (RTL)

This tool is automated and converts things automatically. I haven't used it but it looks good.

## Practical Examples (WIP)
### Example 1
I designed a layout specially for the goal of showing you how I would approach and think about flipping it to a Right-to-left layout.

![](../../img/blog.png)

Let's start with the header component. To code it properly, I outlined a general skeleton for the header. Notice that I divided the header into main and subsections. Also, I added start and end classes for the sections.

![](../../img/header-skeleton-1.png)

```css
.header__main,
.header__sub {
    display: flex;
    justify-content: space-between;
}
```

And since CSS Flexbox works based on the direction of the page as explained previously in this guide, it will flip automatically for RTL.

![](../../img/header-skeleton-2.png)

Next thing is the divider line between the logo and navigation. At first glance, I thought about using `border-right`. It work, but not ideal. Using pseudo elements is better since they can flip based on the page direction.

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

Here is the current result:
![](../../img/header-initial.png)

Next, I'll work on the topic component (The one in the sub header with a label and a counter). Here is a design mockup of how the topic component should look in LTR and RTL. Notice that the counter placement is different.

![](../../img/topics.png)

It might seems simple at first, but there are multiple padding and margins that needs to be handled between LTR and RTL. Here is a mockup illustrating that:

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

As you see, I used CSS Logical properties instead of `left` and `right`. Next step is the "See All" link. Notice that there is an arrow at the end of it. Below are the requirements for it:
- The arrow color should be changed on hover.
- The arrow should be translated to the right on hover.

I chose to use inline SVG for that purpose. When I tried to add a translate animation to the arrow, I thought about RTL. There is no logical property for it and I need to explore other solutions. The one that I got is animating margins.

```css
.c-link svg {
	margin-inline-start: 4px;
	transition: 0.15s ease-in;
}

.c-link:hover svg {
	margin-inline-start: 8px;
}
```

But animating margins is not good for performance. Though, it works. The other solution is to detect the page direction and use `translate` based on that.

```css
.c-link:hover svg {
  transform: translateX(6px);
}

/* I'm using dir=rtl on the header for explaining purposes. It should be added to the root element */
.c-header[dir="rtl"] .c-link svg {
  transform: scaleX(-1);
}

.c-header[dir="rtl"] .c-link:hover svg {
  transform: scaleX(-1) translateX(6px);
}
```

![](../../img/see-all.gif)

Next is the search input. Here are the requirements of it:
- An icon placed at the end of the input.
- The placement of the search icon is dynamic.

```css
.c-input--search {
  background-image: url("data:image/svg+xml...");
  background-position: right 6px center;
}

.c-header[dir="rtl"] .c-input--search {
  /* I replaced the original icon with a flipped one */
  background-image: url("data:image/svg+xml...");
  background-position: right 6px center;
}
```

Also, when typing into the search box, the text shouldn't go under the icon. To avoid that, padding should be added either on the right or left sides.

![](../../img/input-padding.png)

```css
.c-input {
  padding-inline-end: 32px;
}
```

Here is the current coding result for both LTR and RTL:
![](../../img/header-current-result.png)

## Resources and Related Articles
- [(Right to Left (The Mirror World](https://labs.spotify.com/2019/04/15/right-to-left-the-mirror-world/)
- [Let's Talk About RTL](https://alfy.me/2014/07/26/lets-talk-about-rtl.html)
- [Basic concepts of flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)
- [Basic Concepts of grid layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Basic_Concepts_of_Grid_Layout)
- [Right-to-Left Development: Tips and Tricks](https://steelkiwi.com/blog/right-left-development-tips-and-tricks/)
- [Arabic numerals](https://en.wikipedia.org/wiki/Arabic_numerals)

<script async src="https://static.codepen.io/assets/embed/ei.js"></script>