---
title: مبادئ التصميم من اليمين إلى اليسار
date: 2018-05-01
layout: layouts/post-ar.njk
---
 
![](../../img/rtl-styling-intro@2x.jpg)

يتحدث العربية أكثر من 292 مليون نسمة حول العالم بوصفها لغتهم الأم. اللغة العربية هي لغتي الأم، وفي بعض الأحيان أعمل على بناء مواقع إلكترونية تحتاج لدعم الاتجاه من اليسار إلى اليمين (LTR) للغات غير العربية مثل الإنجليزية ومن اليمين إلى اليسار (RTL) للغة العربية.

## مقدمة للتصميم باتجاه اليمين إلى اليسار (RTL)
اتجاه الصفحة الافتراضي في CSS هو من اليسار إلى اليمين (LTR). لو تَحَقّقتَ من متصفحك المفضل وقمت بعمل inspect التصميم الافتراضي لعنصر `html`، ستلاحظ أن القيمة `ltr` (من اليسار إلى اليمين) هي القيمة الافتراضية للخاصية `dir` والتي تعني الاتجاه (مأخوذة من أوائل كلمة **dir**ection). أدناه أمثلة لعرض الفروقات بين التخطيطيات (layout) ذات اتجاه اليسار إلى اليمين (LTR) أو اليمين إلى اليسار (RTL).

![](../../img/rtl-intro-1.png)

لاحظ الفقرة التي تتجه من اليمين إلى اليسار (RTL)، إذ يُقرَأ النص العربي فيها من بأريحية تامة، وهو على العكس من النص الأجنبي الذي يُقرَا من اليسار إلى اليمين (LTR). لحسن الحظ، يقوم المتصفح بكل هذا العمل لهذا المثال البسيط. لتبديل اتجاه الصفحة، ستحتاج لإضافة السِمَة `dir` للعنصر الأب أو الجذر (root).

```html
<html dir="rtl">...</html>
```

عندما تتغير قيمة الخاصية `dir` لعنصر، فستتغير اتجاهات العناصر الأبناء له بالضرورة تلقائيًا: العناوين (وهي وسوم `<h1>` إلى ،`<h6>`)، وعناصر الفقرات ( `<p>`)، والروابط ( <a>)، والصور ( <img>)، وعناصر النماذج ( <form>) ...إلخ.
	
من الجدير بالذكر أن هناك سمة `dir="auto"‎`، والتي تغيّر الاتجاه تلقائيًا وفقًا للنص المستخدم. بناء على [مواصفات HTML](https://www.w3.org/TR/2011/WD-html5-author-20110809/global-attributes.html):
> يفضل تجنب استعمال القيمة auto للخاصية `dir` إلا في الحالات التي يتعذر فيها معرفة اتجاه النص عندما لا يوجد دليل أفضل يمكن عبره كشف اللغة من جهة الخادم (server).

<p class="codepen" data-height="428" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="7662a5f048c5a6a1bbdb89905327c965" style="height: 428px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Basic Example">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/7662a5f048c5a6a1bbdb89905327c965">
  RTL Styling - Basic Example</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

بالإضافة إلى تعيين قيمة السمة `dir=rtl` على عنصر `<html>`،  قد نضيف الخاصية `direction: rtl` التي توفرها CSS لضبط الاتجاه أيضًا.

```css
.element { direction: rtl; }
```

ومع ذلك، توصي CSSWG بضرورة تعريف الاتجاه في عنصر `<html>` الجذر للتأكد من من ضبط اتجاه الصفحة مباشرةً وذلك في حالة تعذر أو تأخر تحميل ملف التنسيق CSS.


## مثال بسيط على انقلاب اتجاه التصميم
لنر مزيدًا من التفاصيل لاكتشاف كيف نقلب اتجاه التصميم  للصفحات التي تتجه من اليسار (LTR) والصفحات التي تتجه من اليمين (RTL).

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

في البداية، استخدمتُ خاصية التعويم القديمة والجميلة `float` لمحاذاة الصورة إلى اليسار في التصميم الذي تجه من اليسار (LTR)، وبالتأكيد أصلحت المشاكل الناتجة عن تطبيق التعويم على الصورة (ما يعرف باسم clearfix في مجتمع تطوير الويب).

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

بعد إضافة السمة `dir="rtl"` لتبديل الاتجاه ليناسب النص العربي (في حالة المواقع ثنائية اللغة والتي تدعم اللغة العربية)، فستكون النتيجة كالتالي:
![](../../img/rtl-intro-ltr-2.jpg)

انقلب اتجاه كل شيء عدا الصورة. هذا لأن الصورة تملك الخاصية `float: left` (طوفان من جهة اليسار) والخاصية `margin-right: 16px` (هامش من جهة اليمين). لحل هذه المشكلة، نحتاج إلى تجاوز هذه التنسيقات بإضافة التنسيقات التالية بعدها:
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
	
## نص إنجليزي وعربي في تخطيط يتجه من اليسار (LTR)
ما الذي سيحدث إذا كان بعض النص يحتوي على خليط من الكلمات الإنجليزية والعربية، في حين أن التخطيط يتجه من اليسار (RTL)؟ حسنًا، ستكون النتائج غريبة مثل:

![](../../img/ltr-mix-1.jpg)

يظهر المتصفحُ العنوان بصورة غير مقروءة، وسيكون محيّرا لمن يتحدث العربية إلا إذا كنتَ كاتبَه. يجب أن يُقرَأ العنوان في هذه الحالة بالترتيب الموضّح في الصورة أدناه.

![](../../img/ltr-mix-2.jpg)

يجب في مثل هذه الحالة ضبط الاتجاه لتجنب أي مشكلة مشابهة ويوصى عمومًا بضبط الاتجاه ما أمكن. ستُعرَض الفقرة السابقة عرضًا صحيحًا بمجرد تحديد قيمة `dir="rtl"` على العنصر.

![](../../img/ltr-mix-3.jpg)

<p class="codepen" data-height="563" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="b254fb1c68ce1f8cce9c5b0917228326" style="height: 563px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/b254fb1c68ce1f8cce9c5b0917228326">
  RTL Styling - Test</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

قد يزداد الأمر صعوبةً عندما يكون العنوان أطول، ولكن المشكلة موجودة عند خلط اللغتين سواءً كان العنوان طويلًا أم قصيرًا. جعلتُ العنوان أطول قليلًا أدناه، وكانت النتيجة غير متوقعة.

![](../../img/ltr-mix-4.jpg)

عندما يضبط الاتجاه `"dir="rtl` على العنصر، سيكون العنوان أوضح بكثير. أي أن الجملة ستبدو صحيحة نحويًا وبالترتيب الصحيح.
![](../../img/ltr-mix-5.jpg)

<p class="codepen" data-height="490" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="02f4dccfb898bee7d1e1daa71f3bd6ac" style="height: 490px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test 2">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/02f4dccfb898bee7d1e1daa71f3bd6ac">
  RTL Styling - Test 2</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

## التعامل مع الخطوط
بناء على التصميم لكل من تخطيطي الاتجاهين: من اليسار (LTR) ومن اليمين (RTL)، يجب أن يكون هناك خط مخصص لكل اتجاه. يمكن لبعض الخطوط أن تعمل جيدًا مع لغات متعددة، وهذا رائع. ومع ذلك، تميل العلامات التجارية والشركات التجارية إلى استخدام خط مختلف يتجه من اليمين (RTL).

لحساب ذلك، يجب تحديد خط مختلف في إعدادات الخط في مشروعك. انظر [أدوات الأتمتة](./#automation-tools) لمزيد من التفاصيل.

## نوع الخط
تعمل الخاصية `font-family` في CSS طريقة تجعل من السهل استعمال خط آخر في حالة عدم تحميل الخط المطلوب. ومع ذلك، اتضح أنه إذا لم يدعم أول خط محدَّد الحروف الرسومية (glyphs) للنص، فسيُستعمَل الخط المُحدَّد الذي يليه.

بحسب [شبكة مطوري موزيلا](https://developer.mozilla.org/en-US/docs/Web/CSS/font-family):
> لا يتوقف الاختيار ببساطة على أول خط مذكور في قائمة الخطوط المحددة عبر الخاصية font-family والذي يكون له عادة الأولوية، ولكن يحدد الخط بمحارف النص كلٌ على حدة، فإذا ظهر أن أول خط لا يحوي على الشكل الرسومي (glyph) لحرف موجود ضمن النص، فيُجرَّب الحرف الذي يليه وهكذا.


قدّم [عمر بوغوتة](‎‎‎https://codepen.io/bourhaouta/pen/GRgLqYL?editors=0100) العرض التوضيحي التالي الذي يثبت المفهوم أعلاه.

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

لم يتعرف خط Roboto على الحروف الرسومية العربية، لذا جرى الانتقال إلى الخط المحدَّد الذي يليه.

## وحدة تخطيط Flexbox
يعتمد تخطيط flexbox على وضع كتابة المستند (writing mode)، إذ يحدِّد وضع الكتابة كيفية تموضع الكتل في الصفحة. مثلًا، يكون تموضع الموقع الصيني من الأعلى إلى الأسفل فوضع الكتابة متوافق مع هذه اللغة. تُوزًّع العناصر في تخطيط flexbox وفقًا للوضع الكتابي للمستند. القيمة الافتراضية لوضع الكتابة `writing-mode` باللغتين الإنجليزية والعربية هي `horizontal-tb`.

بحسب [شبكة مطوري موزيلا](https://developer.mozilla.org/en-US/docs/Web/CSS/writing-mode)، يُقصد بالوضع `horizontal-tb` ما يلي:
> يتدفق المحتوى أفقيًا من اليسار إلى اليمين، وعموديًا من الأعلى إلى الأسفل. وعندما يصل المحتوى إلى نهاية السطر، ينزل المحتوى إلى السطر التالي.

عندما يتغيّر اتجاه الصفحة إلى اتجاه اليمين إلى اليسار (RTL)، فإن خاصية flexbox ستقلب اتجاه عناصرها وفقًا لذلك فهذه أكبر فائدة من استعمال هذا التخطيط! ويوضح الرسم أدناه كيفية قلب محور flexbox بناءً على الاتجاه.

![](../../img/flexbox-axis.jpg)

وضعت ثلاثة عناصر في المثال أدناه، ورقّمتُ كلًا منها لإظهار الفرق عندما يتغير الاتجاه.

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
    flex-direction: row; /* أضيفت القيمة الافتراضية للتوضيح */
}
```

![](../../img/rtl-flexbox-1.jpg)

<p class="codepen" data-height="428" data-theme-id="dark" data-default-tab="result" data-user="shadeed" data-slug-hash="76082ed22d043f1ebcdcf1037dda13f2" style="height: 428px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test 3">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/76082ed22d043f1ebcdcf1037dda13f2">
  RTL Styling - Test 3</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

## وحدة تخطيط Grid
تعتمد وحدة تخطيط grid على وضع كتابة المستند مثلها مثل وحدة تخطيط flexbox، مما يعطينا نفس الفائدة التي نحصل عليها من استخدام flexbox.

في المثال أدناه، يجب أن يكون الشريط الجانبي (sidebar) على اليسار والمحتوى الرئيسي `main` على اليمين عندما يكون الاتجاه هو من اليسار إلى اليمين (LTR). أما بالنسبة للاتجاه من اليمين إلى اليسار (RTL) فالعكس صحيح.

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

## الأخطاء الشائعة عند قلب الاتجاه إلى اتجاه اليمين إلى اليسار (RTL)
يرتكب غير الناطقين باللغة العربية بعض الأخطاء الشائعة التي يراها الناطقين بتلك اللغة رأي العين.

### 1. التباعد بين الأحرف
من الشائع إضافة تباعد بين الأحرف `letter-spacing` لضبط أحرف الكلمة في اللغة الإنجليزية، وهذا ما يُعرف أيضًا باسم التتبع (tracking) في أسلوب الطباعة. ضع في حسبانك المثال التالي للمحتوى الإنجليزي. يبدو طبيعيًا.
	
![](../../img/letter-spacing.jpg)

ومع ذلك، إذا أضيف نفس تنسيق التباعد بين الأحرف `letter-spacing` إلى المحتوى العربي، فسيظهر النص بصورة غربية أو غير طبيعية. ضع في حسبانك المثال الواقعي التالي:

![](../../img/letter-spacing-rtl.jpg)

لاحظ أن في المحتوى الذي يحتوي على تباعد بين الأحرف `letter-spacing`، تبدو أحرف كل كلمة منفصلة عن بعضها البعض، وهذا خطأ محض لأن الأحرف العربية متصلة ببعضها البعض، ويؤدي إبقاء التباعد بين الأحرف `letter-spacing` كما كان بالإنجليزية إلى ظهور أحرف الكلمة منفصلة بعض الشيء عن بعضها كما رأيت آنفًا. تأكد من تعيين `letter-spacing: 0` عند العمل على تخطيط متعدد اللغات.

<p class="codepen" data-height="397" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="29b1428dac29ced513adc482b22e7372" style="height: 397px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test 6">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/29b1428dac29ced513adc482b22e7372">
  RTL Styling - Test 6</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

## 2. شفافية النص
يشيع تغيير شفافية لون النص ليبدو لونًا ثانويًا على سبيل المثال، ويعمل هذا باللغة الإنجليزية بدون مشاكل. أما في اللغة العربية، فيبدو النص غريبًا بإضافة شفافية إليه. انظر مثلًا إلى الصورة التالية:
![](../../img/rtl-transparency.jpg)

هناك بعض المناطق لها ألوان مختلفة بين الأحرف. وبما أن التباعد بين الأحرف `letter-spacing` غير مضبوط مطلقًا في هذا المثال، فالمشكلة غير متعلقة به. الحل ببساطة هو تعيين ألوان بدون نظام ألوان RGBa أو شفافية.

<p class="codepen" data-height="395" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="d8b1d30b39933e0435e52b738b0402dd" style="height: 395px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test 7">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/d8b1d30b39933e0435e52b738b0402dd">
  RTL Styling - Test 7</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

### 3. فروقات بين أحجام الكلمات بين اللغات
لمَّا كان حجم الحرف يتغير من لغة إلى أخرى، فإن حجم كلمة في لغة ما مثل الإنجليزية، لا يماثل حجم الكلمة المقابلة بلغة أخرى مثل العربية وعليه فإن حجم العناصر يتغيّر لبعض الكلمات فتصبح أكبر أو أصغر بعد الترجمة. ضع في حسبانك هذا المثال، الذي حاكيتُ فيه شكل الترويسة العلوية لموقع Smashing Magazine وافترضت وجود قائمة عربية وكيف سيكون شكلها المفترض.

![](../../img/website-header.png) 

لاحظ أن حجم بعض الكلمات في النسخة العربية، يتقارب مع نظيراتها الإنجليزية، بينما تختلف أخرى فتارة تكون أكبر وأخرى تكون أصغر. لتوضيح الأمر، إليك موازنة بين كل كلمة وترجمتها العربية:
![](../../img/website-header-translation.png)

قد تتساءل لماذا أتحدث عن الفروقات بين أحجام الكلمات؟ لمّا كان هذا الأمر طبيعيًا ومتوقعًا، ضع في حسبانك هذا المثال الواقعي من موقع LinkedIn.

![](../../img/word-length-linkedin.png) 

تُرجم الزر “Done” (أربعة حروف) إلى "تم" (حرفان) عربيًا، ما جعل الزر أصغر من اللازم ويبدو غريبًا. كان من الأفضل وضع قيمة صغرى للعرض `min-width` للزر لتصحيح مثل هذه المشاكل، وعدم ترك الأمر إلى حجم النص. لقد زدت قليلًا في عرض العنصر (أو جعلته مساويًا لعرض العنصر في اللغة الإنجليزية) من أدوات المطوّر لترى الفرق بنفسك:

![](../../img/word-length-linkedin-2.png)

ترى الحالة نفسها في موقع تويتر في النسخة العربية منه:
	
![](../../img/word-length-twitter.png)

لوحظت المشكلة السابقة من موقع LinkedIn وموقع تويتر في النسخة العربية بتاريخ (13 ديسمبر 2019).

### 4. بتر النص
عملت مرّة في مشروع ذا محتوى مختلط، وواجهتُ مشكلة مرتبطة ببتر النص في الاتجاه الخطأ. ضع في حسبانك المثال التالي:

![](../../img/text-trun.png)

بُتِر النص المكتوب باللغة الإنجليزية من الاتجاه الخطأ، وكان يجب أن يُبتَر من الاتجاه المقابل في نهاية النص وليس من بدايته. حل هذه المشكلة يكمن في ضبط السمة `dir="auto"‎‏` في العنصر نفسه، وسيتعرف بعدها المتصفح تلقائيًا على الاتجاه `dir` المناسب لكل لغة ويعرض النص عرضًا صحيحًا.
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

### 5. اختيار خط سيء لا يتناسب مع لغة تتجه من اليمين (RTL)
لا يمكنك اختيار خط نظام التشغيل الافتراضي واستعماله مباشرة بمجرد وجود نسخة تصميم تتجه من اليمين (RTL). يجب اختيار الخط بعناية للتأكد من المقروئية الجيّدة. إليك المثال التالي من موقع تويتر:

![](../../img/en-vs-ar.png)

يرى أي ناطق باللغة العربية (وأنا أولهم) أن كلمة “تغريد” صعبة القراءة لعدد من الأسباب:
- الخط ليس جيّدًا.
- ثخن الخط يعيق المقروئية.
- نقاط الكلمات صغيرة وتكاد تلتصق بالحروف.

لقد حاكيت التصميم وجعلته أوضح وإليك الموازنة:

![](../../img/en-vs-ar-2.png)

## 6. خلط الأرقام الهندية والعربية
هناك طريقتان في اللغة العربية لكتابة الأرقام:
- الطريقة الهندية:  ٠ ١ ٢ ٣ ٤ ٥ ٦ ٧ ٨ ٩
- الطريقة العربية: 0 1 2 3 4 5 6 7 8 9 

الأرقام المستخدمة في اللغة الإنجليزية موروثة من الأرقام العربية: “0، 1, 2, 3, 4, 5, 6, 7, 8, 9”، لذا يجب أن تكون الأرقام في المحتوى متناسقة فلا تُكتَب مرة بالنمط الهندي ومرة أخرى بالنمط العربي بل اكتب بنمط واحد فقط.
	
بحسب ويكيبيديا:
> سبب شهرة تسمية "الأرقام العربية" في أوروبا والأمريكيتين أن ناطقين بالعربية قد نقلوها من المغرب، حيث كانت تُستَخدَم آنذاك، إلى أوروبا في القرن العاشر الميلادي.

المثال التالي هو محاكاة لنص يحوي خليطًا من الأرقام العربية والهندية. لاحظ عدم الاتساق في النص وضرورة توحيد نمط الأرقام.
![](../../img/ar-numbers.png)

## أمور شائعة قد لا تعمل في الاتجاه من اليمين إلى اليسار

### 1. ارتفاع الخط

رأينا أنه من الضروري تعيين خط خاص متوافق مع التخطيط الذي يدعم لغة تتجه من اليمين إلى اليسار (RTL)، ويجب أيضًا في ذلك التخطيط اختبار كيفية ظهور المحتوى على سطر واحد أو عدة أسطر. في المثال التالي، المسافة بين الأسطر بالنسبة لنصوص اللغة العربية أقل من النصوص الإنجليزية، على الرغم من أن كلا اللغتين لديهما نفس قيمة `line-height`.

![](../../img/line-height-1.png)

من المهم حساب هذا الأمر وتقديم ارتفاع سطر `line-height` مناسب للمحتوى العربي والإنجليزي على حدة.

<p class="codepen" data-height="255" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="1cb6b25852a009d5fdaf1902bcfaa974" style="height: 255px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Test 8">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/1cb6b25852a009d5fdaf1902bcfaa974">
  RTL Styling - Test 8</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

مشكلة أخرى تظهر في سياق ارتفاع السطر متعلقة بسياق ارتفاع الخط موضحة في المثال التالي المأخوذ من تويتر، إذ هناك محتوى مبتور في الزر ناجم عن قيمة غير مناسبة لارتفاع السطر `line-height`:

![](../../img/ar-kasra.png)

لاحظ الصورة الأولى، الكسرة مبتورة. في الصورة المحاذية، أصلحتُ ارتفاع السطر، وتبدو الآن الحركة كاملة بدون أي نقصان.

### 2. الروابط المسطّرة
التسطير الافتراضي للنصوص يبدو سيئًا في الكلمات العربية، إذ هذا مرتبط بكيفية كتابة الكلمات والأحرف في اللغة العربية. انظر إلى الشكل التالي:

![](../../img/rtl-underline-1.png)

لاحظ أيها القارئ كيف يحجب الخط السفلي نقاط الحروف نوعًا ما. أما زالت غير واضحة؟ هنا تكبير للشكل.

![](../../img/rtl-underline-2.png)

النقاط البارزة باللون الأزرق تتداخل مع الخط السفلي. هذا ليس جيدًا، ويجعل النص صعب القراءة. الحل لهذه المشكلة هو استخدام تسطير مخصص باستخدام CSS أو إزالة التسطير إن لم يكن ضروريًا.

#### 2.1 تجميل النص
~~يمكن تغيير تنسيق التسطير واللون بخاصيتين جديدتين هما `text-decoration-style` و`text-decoration-color`، ومع ذلك ليس مضمونًا أن تعمل مع جميع الخطوط والأحجام. إلى وقت الكتابة، متصفح Firefox هو المتصفح صاحب أفضل دعم لهذه الخصائص.~~

**تحديث بتاريخ: 18 يناير 2020**
بحسب [هذا](https://github.com/shadeed/rtl-styling/issues/4) الاعتراض على موقع GitHub، اتضح أن استخدام خاصية `text-decoration-skip-ink` يمكن أن تحل مشكلة تداخل نقاط الحروف مع الخط السفلي. القيمة الافتراضية هي `skip`. 

<p class="codepen" data-height="214" data-theme-id="light" data-default-tab="result" data-user="shadeed" data-slug-hash="9f8c134e0d4fe1f0d58ba3c23cb96e41" style="height: 214px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="RTL Styling - Text Decoration">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/9f8c134e0d4fe1f0d58ba3c23cb96e41">
  RTL Styling - Text Decoration</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

في وقت كتابة هذا الدليل، هذه الخاصية غير مدعومة في متصفح Safari، ومتصفح Edge القديم (أما متصفح Edge المبني على chromium فيدعمها). إليك كيف تظهر في متصفح Safari:

![](../../img/text-deco-safari.png)

#### 2.2 الظل
أصبح دعم المتصفحات لخاصية `box-shadow` أفضل بكثير من خاصية `text-decoration`، فعندما لا تكون الخاصية `text-decoration` مدعومة في المتصفح، فستستعمل الخاصية `box-shadow` بدلًا عنها.

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

### 3. انقطاع الخط
لو حوى ملف CSS خاصية `word-break`، فسوف تحتاج لاختبارها لأنها قد تقطع الكلمات العربية. ضع في حسبانك التالي:
	
![](../../img/word-break.png)

لاحظ اقتطاع أحرف من الكلمات الموجودة في نهاية السطر بسبب تأثير خاصية `word-break` إذ حروف الكلمة العربية مرتبطة ببعضها البعض، لذلك لا يمكن أن تقطع الكلمة على عكس اللغة الأجنبية التي يمكن قطع أحرف منها عندما تكون في نهاية السطر وإرسالها إلى بداية السطر التالي.

### 4. اختصارات الكلمات
من الشائع استخدام اختصارات الكلمات في اللغة الإنجليزية، مثل أيام الأسبوع. لذلك يُختصَر يوم السبت “Saturday” إلى “Sat”.

![](../../img/en-shorcuts.png)

أما في اللغة العربية فلا يمكن ذلك لأن حروف الكلمة ملتصقة ببعضها.

![](../../img/ar-shorcuts.png)

## الأيقونات ثنائية الاتجاه
الأيقونات المتناظرة (ليس لها اتجاه معيّن) لا تحتاج أن تُقلب اتجاهاتها بين تخطيطي اليسار إلى اليمين (LTR) واليمين إلى اليسار (RTL) مثل الأيقونات التالية:

![](../../img/general-icons.png)

أما الأيقونات غير المتناظرة؛ أي التي لها اتجاه متناسب مع اللغة المتجهة من الشِّمال، فمن المهم قلب اتجاهاتها في تخطيط اليمين إلى اليسار (RTL)، وذلك حتى تكون مفهومة تمامًا من المستخدم.

![](../../img/bidi-icons.png)

على الرغم من ذلك، هناك دائمًا استثناءات، فبحسب توجيهات التصميم المادي [material design](https://material.io/design/usability/bidirectionality.html#mirroring-elements)، إذا كانت الأيقونة تمثّل كائنًا يمكن حمله باليد اليُمنى، فلا داعي لقلب الاتجاه. هنا بعض الأمثلة:

![](../../img/bidi-icons-2.png)

### أيقونات مشغّل الوسائط
رجعتُ بالزمن خمسة عشر عامًا عندما أعطاني والدي مشغل MP3 فيه زر تشغيل يتجه إلى اليسار.

![](../../img/mp3-player.jpeg)

بعض الأيقونات عالمية، وليس مطلوبًا منا قلب اتجاهها. سبب ذلك أن أزرار التشغيل هذه تمثّل اتجاه الشريط الذي يعمل، وليس اتجاه الوقت. هنا يظهر كيف يبدو تطبيق Spotify في اللغة الإنجليزية والعربية:

![](../../img/spotify-icons.png)

لاحظ أن أزرار التشغيل لم تقلب اتجاهاتها لأنها أيقونات عالمية.

### تطبيقات المحادثة
في نقاش [مثير](https://twitter.com/AndaristRake/status/1210508742225285120) على تويتر، سُئلتُ ماذا إذا كان الصحيح قلب اتجاه الإرسال في تطبيق المراسلة من عدمه. بحثت عن ذلك في مواقع Facebook Messenger و WhatsApp وتويتر.

![](../../img/message-icons-1.png)

كان اتجاه زر الإرسال مقلوبًا، وفي رأيي الشخصي، أن هذا هو الصحيح لأنه يشعرك أنه أكثر منطقي بالنسبة لي. إضافة لذلك، يجب أن يبدَّل بين زرَّي الإرسال و”+” ليكونا أصح. انظر المحاكاة أدناه:
![](../../img/message-icons-1-fixed.png)

ومع ذلك، لا فيس بوك ولا تويتر قلبا اتجاه زر الإرسال.

![](../../img/message-icons-2.png)

## قلب اتجاه عناصر واجهة الاستخدام
بينما أعمل على بعض عناصر واجهة الاستخدام، أحتاج إلى طريقة لقلب اتجاهها. فمثلًا في برنامج Sketch، سأنسخ العنصر وأقلب اتجاهه بواسطة أمر قلب الاتجاه “flip”. ونفس العملية متاحة في برنامجي Adobe XD و Figma.

![](../../img/sketch-flip.png)

لرؤية ما أعنيه، هذه صورة متحركة تبيّن ما فعلت بعد قلب اتجاه العنصر.

![](../../img/sketch-flip.gif)

## أمور تتطلب المراعاة في التصميم لاتجاه اليمين إلى اليسار
في هذا القسم، سأمرّ على أهم عناصر واجهة الاستخدام وأبيّن كيف يجب أن تظهر في وضع اليمين إلى اليسار (RTL).

### أيقونات الأزرار
من الشائع أن يكون لديك زر به أيقونة يفتح قائمة لمزيد من الإجراءات. في هذه الحالة، يجب قلب موضع الأيقونة في تخطيط الاتجاه من اليمين إلى اليسار (RTL).

![](../../img/button-icons.png)

## مدخلات النموذج (Form)
يجب أن تبقى بعض مدخلات النموذج محاذية لليسار في الاتجاه من اليمين (RTL) مثل مدخلات البريد الإلكتروني ورقم الجوال بينما تقلب الأيقونات الأخرى مثل أيقونة الاسم.

![](../../img/form-inputs.png)

تجدر الإشارة إلى أنه إذا كان محتوى العنصر النائب (placeholder) باللغة العربية أو أي لغة أخرى ذات اتجاه من اليمين إلى اليسار (RTL)، فيجب محاذاة العنصر النائب إلى اليمين ولكن بمجرد التركيز على عنصر الإدخال وما أن يبدأ المستخدم في الكتابة، سيتم قلب المحاذاة إلى اليسار.

![](../../img/form-inputs-2.png)

شكرًا ل [YuanHao Chiang‏](https://github.com/shadeed/rtl-styling/issues/6) لإعلامي بهذه الحالة أعلاه.
	
### قوائم التنقل التفصيلية (breadcrumbs)
يجب قلب اتجاه الأسهم الموجودة في قوائم التنقّل التفصيلية كذلك.

![](../../img/breadcrumbs.png) 

## الترويسة العلوية للصفحة
تحتوي الترويسة العلوية للصفحة على قسمي البداية والنهاية. كل قسم منهما يجب أن يُقلب اتجاهه في وضع اتجاه اليمين إلى اليسار (RTL).

![](../../img/page-header.png)

### الجداول
على الجدول أن يقلب اتجاهه كذلك.

![](../../img/tables.png)	

### التبويبات
بالنسبة لمكون التبويبات في وضع اليسار إلى اليمين (LTR)، ستكون الأيقونات على شِمال الاسم التعريفي (label). أما في اتجاه اليمين إلى اليسار (RTL)، فيجب قلب اتجاهه.

![](../../img/tabs.png)

### البطاقة
بالنسبة للبطاقة الأفقية، يجب قلب ترتيب الصورة والنص في اتجاه اليمين إلى اليسار (RTL).

![](../../img/card.png)

## الرتوش (يُقصد المكونات البسيطة الخفيفة)
كما تتوقع، يجب قلب اتجاه أيقونات (الإغلاق) والتحذير.

![](../../img/toasts.png)

### كتل الاقتباسات
يجب قلب اتجاه الأيقونة كما هو موضح في النموذج أدناه.

![](../../img/blockquotes.png)

## خصائص CSS المنطقية
بحسب [شبكة مطوري موزيلا](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Logical_Properties):
> الخصائص والقيم المنطقية لـ CSS هي عبارة عن وحدة من CSS تقدم خصائص وقيم منطقية توفر القدرة على التحكم في التخطيط من خلال تعيينات الاتجاه والأبعاد المنطقية، وليس المادية.

لنتحدث عن مثال بسيط. لنفترض أننا نحتاج إلى محاذاة نص إلى اليسار، لذلك أضفنا الأكواد التالية:

```css
.page-header {
    text-align: right;
}
```

وللاتجاه من اليمين إلى الشِمّال (RTL)
	
```css
[dir="rtl"] .nav-item {
    text-align: left;
}
```

ماذا لو كان هناك طريقة لإضافة قيمة المحاذاة `text-align` التي تغيّر الاتجاه بناء على اتجاه الصفحة؟ أتت خصائص CSS المنطقية لإنقاذنا في هذه المهمة!

```css
.page-header {
    text-align: end;
}
```

باستعمال هذه الخاصيات، سيعتمد اتجاه محاذاة النص `text-align` بناء على اتجاه الصفحة. إليك [هذه التجربة الحية](https://codepen.io/shadeed/pen/fb4e2f89ca23ab53f8b37112f027c85b?editors=1100).

لتسهيل رؤية الفرق بين قيمة البداية `start` وقيمة النهاية `end` للخاصية `text-align`، فقد صنعت النموذج المحاكي أدناه. قيمة البدء `start` تساوي اليسار في اتجاه اليسار إلى اليمين (LTR)، وقيمة النهاية `end` تساوي اليمين في اتجاه اليمين إلى اليسار (RTL).

![](../../img/start-end.png)

الآن بعد أن أصبحت لديك فكرة أساسية عن كيفية عملها، دعنا نكتشف المزيد من الأمثلة وحالات الاستخدام لخاصيات CSS المنطقية.

### الحاشية الداخلية المنطقية
![](../../img/css-logical-padding.png)

لنفترض أن لدينا خانة بحث لها أيقونة بحث على اليمين. يجب علينا أن نضيف حاشية (padding) في اليمين واليسار. ستكون الحاشية على اليمين أكبر قليلًا لمنع النص من التداخل مع أيقونة البحث.

```css
.input--search {  
  padding-inline-start: 1rem;
  padding-inline-end: 2.5rem;
}
```

### الهوامش الخارجية المنطقية
![](../../img/css-logical-margin.png)

يجب أن تكون الهوامش الخارجية على الجانب الأيمن منطقية، لذلك سنستخدم `margin-inline-start` لذلك الغرض.

```css
.page-header__avatar {  
  margin-inline-start: 1rem;
}
```

### الحدود المنطقية
![](../../img/css-logical-border.png)


قد تحتاج في كثير من الأحيان إلى إضافة أحد الحدود للإشارة إلى أن عنصر التنقّل نشِط. في التصميم أعلاه، يوجد حد على الجانب الأيسر لكل عنصر تنقّل. كيف نجعلها منطقية؟ إليك الطريقة:

```css
.nav__item {  
  border-inline-start: 3px solid transparent;
}

.nav__item.is-active {
  border-color: #1e9ada;
}
```

### الحدود الناعمة (المدوّرة) المنطقية
![](../../img/css-logical-border-radius.png)

في التصميم أعلاه، تحتوي خلفية عنصر التنقل على حدود مدوّرة (border radius) فقط للزوايا العلوية اليمنى والسفلية اليمنى. للقيام بذلك منطقيًا، نستخدم ما يلي:
	
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

### ورقة مرجعية (cheat sheet) للخصائص المنطقية

إن كنت في شك من المكافئ المنطقي لخاصية CSS اتجاهية، استخدم الورقة المرجعية (cheat sheet) أدناه. يرجى ملاحظة أن الخصائص المضمّنة تقتصر على ما هو مفيد لـخصائص الاتجاه من اليسار إلى اليمين (LTR) ومن اليمين إلى اليسار (RTL). لقد كتبته بناء على المقال [العظيم](https://adrianroselli.com/2019/11/css-logical-properties.html) الذي كتبته Adrian Roselli.

<p class="codepen" data-height="674" data-theme-id="dark" data-default-tab="result" data-user="shadeed" data-slug-hash="2981e62691e67452d9f282a5351d7c79" style="height: 674px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="CSS Logical Properties">
  <span>See the Pen <a href="https://codepen.io/shadeed/pen/2981e62691e67452d9f282a5351d7c79">
  CSS Logical Properties</a> by Ahmad Shadeed (<a href="https://codepen.io/shadeed">@shadeed</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

بالإضافة إلى ذلك، أنشأ Adrian عرضًا توضيحيًا يسهّل فهم الفرق بين خاصية CSS المنطقية والاتجاهية.

<p class="codepen" data-height="635" data-theme-id="23655" data-default-tab="result" data-user="aardrian" data-slug-hash="bGGxrvM" style="height: 635px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Logical Properties Mapping">
  <span>See the Pen <a href="https://codepen.io/aardrian/pen/bGGxrvM">
  Logical Properties Mapping</a> by Adrian Roselli (<a href="https://codepen.io/aardrian">@aardrian</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

### دعم المتصفح
إن دعم المتصفح جيد جدًا للحاشية الداخلية `padding` والهامش `margin` ومحاذاة النص `text-align`. ومع ذلك، فالدعم ليس جيدًا لخصائص تدوير الحدود (border-radius). فيما يلي جداول الدعم من موقع ‏[Can I Use] ‏(/https://caniuse.com):

‎‏![Support for CSS logical properties from Can I Use website](../../img/caniuse-css-logical.png)‎

![Support for CSS logical properties from Can I U

se website](../../img/caniuse-css-logical-2.png)

على الرغم من أن الدعم ليس مثاليًا (ولن يكون مثاليًا على الإطلاق)، أنصحك باستخدام خصائص CSS المنطقية مع احتياطات تمكّنه من الرجوع (لقيم احتياطية في حالة انعدام الدعم). فمثلا:

```css
.input--search {  
  padding-left: 1rem;
  padding-right: 2.5rem;
  padding-inline-start: 1rem;
  padding-inline-end: 2.5rem;
}
```

يمكنك كذلك استخدام المكوّن الإضافي [PostCSS Logical] ‏(https://github.com/csstools/postcss-logical)، والذي يضيف قيمة مرجعية يُرجَع إليها في حال عدم توفر دعم للخاصية المنطقية المقابلة في المتصفح.

## اصطلاحات تسمية CSS
عمومًا، تجنّب تسمية أصناف CSS تسمية مشابهة لاسم محتوى العنصر إذ سترتبط التسمية آنذاك بذلك العنصر فقط ولن تتمكن من استعمال ذاك الصنف مع عناصر أخرى مشابهة بالوظيفة ومختلفة بالتسمية، فمثلًا إذا كان لديك رابطًا باسم See more، فتجنب استعمال الصنف see-more معه فقد يتواجد رابط آخر مشابه باسم learn more وستضطر إلى إنشاء صنف جديد باسم learn-more لذا استخدم الأسماء التي يمكن اعادة استخدامها مع عناصر أخرى في الواجهة. ضع في حسبانك ما يلي:
	
```html
<div class="c-section">
  <p><a href="#" class="see-link">See more</a></p>
</div>

<div class="c-section">
  <p><a href="#" class="see-link">Learn more</a></p>
</div>
```

في كلا القسمين، الروابط هي نفسها ولكن تسمياتها مختلفة. في القسم الثاني see-link` ليس لها معنى. قد يكون الاسم الجيد هو `c-link`. يشير `c` إلى المكوّن، والذي تعلمته من إطار عمل ITCSS لتسميات CSS.

الآن بعد أن حصلت على الفكرة، يمكننا تطبيقها على تنسيق اليمين إلى اليسار (RTL) كذلك. يحتوي نموذج التصميم أدناه على قسم به مكونيَن فرعييَن.

![](../../img/css-naming.png)


بدلاً من إعطاء أسماء العروض التقديمية للعناصر، مثل `.c-page-header__left` و` .c-page-header__right` ، سمّيتُها `.c-page-header__start` و `.c-page-header__end`. هذا تحوّط أكثر للمستقبل ولا يفترض موقع الويب أن المحتوى سيكون حصرًا ذا اتجاه من اليسار (LTR) أو من اليمين (RTL) بل سيكون مرنًا لتبديله بكلا الاتجاهين.

## أشرطة تمرير (scrollbars) عمودية ثنائية الاتجاه
على حد علمي، يتغير اتجاه شريط التمرير (scrollbars) العمودي داخل حاوية في CSS بناءً على اتجاه الصفحة. بالنسبة لتخطيط اليمين إلى اليسار (RTL) يكون اتجاه شريط التمرير على اليسار، وبالنسبة إلى تخطيط اليسار إلى اليمين (LTR)، يكون على اليمين.

انظر في الشكل أدناه.

![](../../img/scroll-bar.png)

ومع ذلك، بالنسبة لأنظمة التشغيل، لا يتغير شريط التمرير (scrollbar) الخاص بالمتصفح ويظل على الجانب الأيمن بغض النظر عن لغة نظام التشغيل. ولكن بالنسبة لنظام التشغيل نفسه، يتغير شريط التمرير اعتمادًا على لغته.

## أدوات أتمتة
توجد أدوات رائعة لتسهيل عملنا عندما نحتاج إلى قلب اتجاه التصميم من اليسار إلى اليمين (LTR) إلى اتجاه اليمين إلى اليسار (RTL).

### 1. أداة Bi-App-Sass
تتيح لك أداة [Bi-App-Sass]‏(https://github.com/anasnakawa/bi-app-sass)‏‏ بواسطة Anas Nacho كتابة صفحات تنسيق لمرة واحدة، ثم تعالجها لتخرجها في صفحتي تنسيق مختلفتين، واحدة لاتجاه اليسار إلى اليمين (LTR) والأخرى لاتجاه اليمين إلى اليسار (RTL).

هذه الأداة ستكون مفيدة لمشروع كبير. ستكون النتيجة صفحات تنسيق متعددة لكل اتجاه لغة. ضع في حسبانك ما يلي:
	
```sass
.elem {
  display: flex;
  @include margin-left(10px);
  @include border-right(2px solid #000);
}
```

ستكون النتيجة في CSS كما يلي:
	
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

لاحظ مع ذلك، أن آخر تغيير محفوظ للكود في مستودع GitHub كان قبل أربع سنوات (نوفمبر 2015).

### 2. أداة RTLCSS
أداة [RTLCSS‏] (/https://rtlcss.com) بواسطة محمد يونس هي إطار عمل لتحويل صفحات التنسيق من اتجاه اليسار إلى اليمين (LTR) إلى اتجاه اليمين إلى اليسار (RTL).

يتمثل الاختلاف في هذه الأداة في أنها تعمل فقط على الإصدار المبني النهائي من ملف CSS. على سبيل المثال، إذا كان لديك مشروع يحتوي على أكثر من 50 مكونًا من مكونات Sass، فسيكون RTLCSS مفيدًا لتحليل ملف CSS المبني بعد معالجته وإنشاء نسخة لاتجاه اليمين إلى اليسار (RTL) منه.

## أمثلة عملية
### الترويسة العلوية للموقع
لقد صممت تخطيطًا خصيصًا لأوضح لك كيف سأقارب وأفكّر في قلب اتجاهه إلى تنسيق اليمين إلى اليسار (RTL).

![](../../img/blog.png)

لنبدأ بمكوّن التروسية العلوية. لكتابة الكود كتابة صحيحة، حددت الهيكل العام. لاحظ أنني قسّمت العنوان إلى قسم رئيسي وأقسام فرعية. لقد أضفت أيضًا أصناف البداية والنهاية للأقسام.

![](../../img/header-skeleton-1.png)

```css
.header__main,
.header__sub {
    display: flex;
    justify-content: space-between;
}
```

ونظرًا لأن خاصية CSS flexbox تعمل بناءً على اتجاه الصفحة، كما هو موضّح سابقًا في هذا الدليل، فإنها ستقلب اتجاهها تلقائيًا لاتجاه اليمين إلى اليسار (RTL).

![](../../img/header-skeleton-2.png)

الشيء التالي هو الخط الفاصل بين الشعار وعنصر التنقّل. في البداية، فكرتُ في استخدام الحد الأيمن `border-right` إذ إنه يعمل ولكنه ليس الحل الأمثل. سيكون استخدام عنصر زائف (pseudo-element) أفضل لأنه سيقلب اتجاهه بناءً على اتجاه الصفحة.

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

ها هي النتيجة حتى الآن:
	
![](../../img/header-initial.png)

بعد ذلك، سأعمل على مكوّن الموضوعات (المكوّن الموجود في العنوان الفرعي مع التسميات والعدادات). فيما يلي نموذج بالحجم الطبيعي لكيفية ظهور مكون الموضوعات في اتجاه اليسار إلى اليمين (LTR) واتجاه اليمين إلى اليسار (RTL). لاحظ أن تموضع العدادات مختلف.

![](../../img/topics.png)

قد يبدو الأمر بسيطًا للوهلة الأولى، ولكن يجب معالجة العديد من قيم الحاشية (padding) والهامش (margin) بين اليسار واليمين. هنا نموذج محاكٍ يوضح ذلك:

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

كما ترى، لقد استخدمت خاصيات CSS المنطقية، بدلاً من `left` و `right`.

الخطوة التالية هي رابط مشاهدة الكل “See All”. لاحظ السهم في نهايته. فيما يلي متطلباته:
- يجب أن يتغير لون السهم عند التحويم (hover).
- يجب أن يتحرك السهم جهة اليمين عند التحويم (hover).

اخترت استخدام الرسومات المتجهة SVG المضمنة لهذا الغرض. عندما أضفت الرسم المتحرك `translate` إلى السهم، فكّرت في اتجاه اليمين إلى اليسار (RTL). لا توجد خاصية منطقية لهذا، وكنت بحاجة لاستكشاف حلول أخرى. كان أحد الحلول التي توصلت إليها هو تحريك الهوامش (margins).

```css
.c-link svg {
	margin-inline-start: 4px;
	transition: 0.15s ease-in;
}

.c-link:hover svg {
	margin-inline-start: 8px;
}
```

لكن تحريك الهوامش ليس جيدًا للأداء على الرغم من أنه يعمل. الحل الآخر هو اكتشاف اتجاه الصفحة، وتعيين `translate` بناءً على ذلك.
```css
.c-link:hover svg {
  transform: translateX(6px);
}


/ * في الترويسة العلوية بغرض التوضيح. يجب إضافته إلى العنصر الجذر dir=rtl أستخدم * /‎

.c-header[dir="rtl"] .c-link svg {
  transform: scaleX(-1);
}

.c-header[dir="rtl"] .c-link:hover svg {
  transform: scaleX(-1) translateX(6px);
}
```

لاحظ أنه بالنسبة إلى اتجاه اليمين إلى اليسار (RTL)، أضفت `scaleX(-1)‎` لقلب اتجاه أيقونة السهم أفقيًا. يمكنك استخدام خاصية التدوير لمائة وثمانين درجة `rotate(180deg)‎` بدلاً من ذلك، لكن هذا المقياس أكثر وضوحًا بالنسبة لي.

![](../../img/see-all.gif)

التالي هو مدخل البحث وهذه هي المتطلبات التي يجب تحقيقها:
- يجب أن تظهر أيقونة البحث في نهاية عنصر الإدخال.
- يجب أن يكون موضع أيقونة البحث ديناميكيًا.

```css
.c-input--search {
  background-image: url("data:image/svg+xml...");
  background-position: right 6px center;
}

.c-header[dir="rtl"] .c-input--search {
  /* We replace the original icon with a flipped one. */
/ * .استبدلنا الأيقونة الأصلية بأيقونة مقلوبة الاتجاه * /
  background-image: url("data:image/svg+xml...");
  background-position: right 6px center;
}
```

أيضًا، عندما يكتب المستخدم في مربع البحث، يجب ألا ينزلق النص أسفل الأيقونة. لتجنب ذلك، أضِف الحاشية الداخلية (padding) على الجانب الأيمن أو الأيسر.

![](../../img/input-padding.png)

```css
.c-input {
  padding-inline-end: 32px;
}
```

ها هي النتيجة حتى الآن لكل من اتجاه اليسار إلى اليمين (LTR) واتجاه اليمين إلى اليسار (RTL):

![](../../img/header-current-result.png)

تاليًا، هو قائمة الجوال. سأستخدم أيقونة الهامبرجر (ثلاثة خطوط أفقية) للإشارة إلى القائمة. سيتغير موضع الأيقونة بين اتجاه اليسار إلى اليمين (LTR) واتجاه اليمين إلى اليسار (RTL). ينطبق الأمر نفسه على اتجاه حركة `translate`.

![](../../img/header-menu-mobile.png)

تحقق من [العرض التوضيحي] (https://codepen.io/shadeed/pen/aa0c9f6c73fe62d206b674c52dc4426e؟editors=0100) على موقع CodePen.

## شكر
شكر خاص لزوجتي [خلود] (https://twitter.com/kholoud840) على دعمها المستمر وقراءتها الدليل عدة مرات. شكرًا لكل من [Adebiyi Adedotun Lukman]‏(https://twitter.com/AdebiyiAL)‏ و [Šime Vidas]‏ (https://twitter.com/simevidas) على تعليقاتهما الرائعة.

## مصادر ومقالات ذات صلة
- [Right to Left (The Mirror World)](https://labs.spotify.com/2019/04/15/right-to-left-the-mirror-world/)
- [Let’s Talk About RTL](https://alfy.me/2014/07/26/lets-talk-about-rtl.html)
- [Basic Concepts of Flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)
- [Basic Concepts of Grid Layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Basic_Concepts_of_Grid_Layout)
- [Right-to-Left Development: Tips and Tricks](https://steelkiwi.com/blog/right-left-development-tips-and-tricks/)
- [Arabic Numerals](https://en.wikipedia.org/wiki/Arabic_numerals)

<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
