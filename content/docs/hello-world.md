---
id: hello-world
title: مثال «أهلًا بالعالم»
permalink: docs/hello-world.html
prev: cdn-links.html
next: introducing-jsx.html
---

يبدو أصغر مثال في React كما يلي:


```js
ReactDOM.render(
  <h1>أهلًا بالعالم!</h1>,
  document.getElementById('root')
);
```

يعرض هذا المثال ترويسةً تقول "أهلًا بالعالم!" في الصّفحة. 

[](codepen://hello-world)

اضغط الرابط أعلاه لفتح مُحرِّر فوري "online". لا تتردد وقم بالتعديل هذا المثال كما يحلو لك وراقب كيف تؤثر تعديلاتك على المُخرجات. أغلب الصفحات في هذا الدليل ستحتوي على أمثلة قابلة للتعديل مثل هذا المثال.```

## كيف تقرأ هذا الدليل {#how-to-read-this-guide}

ستُمهِّد لك الأقسام القادمة تدريجيًّا كيفيّة استخدام React، وسنتعامل مع الكتل التي يتكوّن منها تطبيق React وهي العناصر (elements) والمُكوِّنات (Components). حالما تتقنها سيصبح بمقدورك إنشاء تطبيقات مُعقَّدة من قطع صغيرة قابلة لإعادة الاستخدام.

>ملاحظة
>
>هذا الدليل صمِّم من أجل الأشخاص الذين يفضلون **تعلم المفاهيم النظرية خطوةً بخطوة**. إن كنت تفضل التعلم بالممارسة، انتقل إلى [الدليل التطبيقي](/tutorial/tutorial.html). ستجد أنَّ هذا الدليل والدليل التطبيقي يكمِّل أحدهما الأخر.

هذا هو الفصل الأول في دليل خطوة بخطوة حول مفاهيم React الرئيسية. يُمكنك العثور على قائمة بجميع فصولها في شريط التَنقل الجانبي. إذا كنت تقرأ هذا من جهاز محمول ، يمكنك الوصول إلى التنقل عن طريق الضغط على الزر في الركن الأيمن السفلي من الشاشة.

كل فصل في هذا الدليل، يبني على المعرفة التي تعلمتها في الفصل السابق. **يمكنك معرفة معظم React من خلال قراءة “المفاهيم الرئيسية”  بالترتيب الذي تظهر به في الشريط الجانبي.** على سبيل المثال, الفصل التالي بعد هذا الفصل هو [“مقدمة إلى JSX”](/docs/introducing-jsx.html) 

## درجة المعرفة المفترضة {#knowledge-level-assumptions}

بما أنّ React هي مكتبة JavaScript فسنفترض أنّك تملك معرفة أساسيّة بلغة JavaScript. **إن لم تكن واثقًا من إمكانياتك فننصحك بأن تذهب إلى [ درس JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript) للتحقّق من مستواك** والتمكّن من متابعة هذا الدليل دون تَخبُّط. سيستغرق منك حوالي نصف ساعة إلى ساعة، ولكنّك بعد المرور عليه لن تشعر بأنّك تتعلّم React و JavaScript معًا.

>ملاحظة
>
>يعتمد هذا الدليل أيضًا على بعض من صياغة JavaScript الجديدة في الأمثلة، فإن لم تكن قد تعاملت مع JavaScript في السنوات القليلة الماضية، [هذه النقاط الثلاث](https://gist.github.com/gaearon/683e676101005de0add59e8bb345340c) ستمهد لك الطريق.

## دعنا نبدأ! {#lets-get-started}

ستجد في كل فصل رابطًا يشير إلى [ الفصل التالي ](/docs/introducing-jsx.html) من هذا الدليل. ستجد في قسم "انظر أيضًا" روابط جميع فصول هذا الدليل لتسهيل التنقل بينها.


