---
id: hooks-overview
title: لمحة خاطفة عن الـ Hooks
permalink: docs/hooks-overview.html
next: hooks-state.html
prev: hooks-intro.html
---

*الخطافات* هي إضافة جديدة إلى الإصدار 16.8 في React، إذ تسمح لك باستعمال ميزة الحالة وميزات React الأخرى دون كتابة أي صنف.

الخطافات [متوافقة مع ما سبقها بشكل كامل](/docs/hooks-intro.html#no-breaking-changes). توفر هذه الصفحة نظرة عامة وسريعة حول الخطافات لمستخدمي React ذوي الخبرة. إن ازددت حيرةً في بعض المواضع أثناء قراءة هذه الصفحة، فانتقل إلى الرابط المذكور في الملاحظة "شرح أوسع" مثل:

>شرح أوسع
>
>اقرأ القسم [الحافز لإضافة الخطافات](/docs/hooks-intro.html#motivation) لمعرفة سبب إضافة الخطافات إلى React.

**↑↑↑ كل قسم يتنهي بصندوق اصفر مثل هذا.** يوجد بداخله رابط يحوي شرحًا موسعًا يمكن الرجوع اليه.

## 📌 خطاف الحالة {#state-hook}

المثال التالي يصيِّر (render) عدادًا، إذ ستزيد قيمته عند الضغط على زر محدَّد:

```js{1,4,5}
import React, { useState } from 'react';

function Example() {
  // "count" التصريح عن متغير حالة جديد ندعوه
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

في هذه الشيفرة, `useState` هو خطاف *Hook* (سنتحدث عن ما الذي يعينه هذا الأمر). نستدعي هذا الخطاف داخل مكون دالة لإضافة بعض الحالات المحلية إليه. ستحافظ React على هذه الحالة بين عمليات إعادة التصيير. يعيد  `useState` زوجًا هو: قيمة الحالة الحالية ودالة تمكنك من تحديثها. يمكنك استدعاء هذه الدالة من معالج حدث أو أي مكان آخر. هي تشبه `this.setState` في أي صنف باستثناء أنَّها لا تدمج الحالة القديمة مع الحالة الجديدة. (سنوضح الفرق بين `useState` و `this.state` عبر مثال عملي في صفحة [استعمال خطاف الحالة](/docs/hooks-state.html).)

الوسيط الوحيد الذي يمكنك تمريره إلى  `useState` هو الحالة الأولية. في المثال أعلاه، الحالة الأولية هي `0` لأنَّنا افترضنا وجوب بدء عملية العد من الصفر. لاحظ أنَّه بخلاف `this.state`, ليس إجباريًّا أن تكون الحالة هنا كائنًا رغم أنَّ تكون كذلك أن أردت أنت ذلك. وسيط الحالة الأولية يستعمل فقط في عملية التصيير الأولى.

#### التصريح عن متغيرات عديدة للحالة {#declaring-multiple-state-variables}

يمكنك استعمال خطاف الحالة (State Hook) أكثر من مرة مكون واحد بالشكل التالي:

```js
function ExampleWithManyStates() {
  // Declare multiple state variables!
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
  // ...
}
```

تمكننا صيغة [تفكيك المصفوفة](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#Array_destructuring) من إعطاء أسماء مختلفة إلى متغيرات الحالة التي صرَّحنا عنها عبر استدعاء `useState`. هذه الأسماء ليست جزءًا من الواجهة `useState` البرمجية، ولكن React تفترض أنَّك إن استدعيت `useState` عدة مرات، فإنَّك تفعل ذلك بالترتيب نفسه خلال كل عملية تصيير. سنعود لاحقًا لمناقشة كيفية عمل هذا السلوك ومتى يكون استعماله مفيدًا.

#### ولكن ما هو الخطاف؟ {#but-what-is-a-hook}

الخطافات هي دوال تمكنك من "تعليق" (hook into) حالة React وميزات دورة الحياة (lifecycle) من مكونات الدالة. لا تعمل الخطافات داخل الأصناف، إذ تمكنك من استعمال React دون الحاجة إلى الأصناف. (لا ننصح [بإعادة كتابة المكونات الحالية الخاصة بك](/docs/hooks-intro.html#gradual-adoption-strategy) بين عشية وضحاها ولكن ننصح ببدء استعمال الخطافات في المكونات الجديدة إن أردت ذلك.)

توفر React عددًا محدودًا من الخطافات المُضمَّنة منها `useState`. يمكنك أيضًا إنشاء الخطافات الخاصة بك لإعادة استعمال سلوك ذي حالة بين مكونات مختلفة. سنتطرق أولًا إلى الخطافات المُضمَّنة في React.

>شرح أوسع
>
>يمكنك تعلم المزيد حول خطاف الحالة في توثيق مخصص به هو [استعمال خطاف الحالة](/docs/hooks-state.html).

## ⚡️ خطاف التأثير {#effect-hook}

من المرجح أنَّك أجريت بعض عمليات جلب البيانات، أو الاشتراكات، أو تغير DOM يدويًا من مكونات React من قبل. نُطلِق على هذه العمليات بأنَّها عمليات تملك "تأثيرات جانبية" (side effects، أو "تأثيرات" فقط للاختصار) لأنَّها تستطيع أن تؤثر على مكونات أخرى ولا يمكن تنفيذها أثناء عملية التصيير.

خطاف التأثير (Effect Hook) - الذي هو `useEffect` يضيف القدرة على تنفيذ تأثيرات جانبية من مكون دالة. إنه يخدم الغرض ذاته الذي يفعله `componentDidMount`, `componentDidUpdate`, و `componentWillUnmount` في أصناف React، ولكن في واجهة برمجية واحدة. (سنجري عملية موازنة ونوضح الفرق بين useEffect وهذه التوابع مع أمثلة عملية في صفحة [استعمال خطاف التأثير](/docs/hooks-effect.html).)

على سبيل المثال، المكون التالي يضبط عنوان الصفحة بعد تحديث React شجرة DOM:

```js{1,6-10}
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // Similar to componentDidMount and componentDidUpdate:
  useEffect(() => {
    // Update the document title using the browser API
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

عند استدعاء `useEffect`, نخبر بذلك React بتنفيذ الدالة "`effect`" الخاصة بك بعد تطبيق التغييرات على الشجرة DOM. يُصرَّح عن التأثيرات داخل المكون، لذا يمكنها الوصول إلى خاصياته (props) وحالته (state). افتراضيًّا، تنفذ React التأثيرات بعد كل عملية تصيير بما فيها عملية التصيير الأولى. (سنتحدث بالتفصيل عن هذا السلوك مع موازنته مع سلوك دورات حياة صنف في الصفحة [استعمال خطاف التأثير](/docs/hooks-effect.html).)

قد تحدِّد التأثيرات اختياريًّا كيفية إجراء عملية "تنظيف" بعد تنفيذها عبر إعادة دالة. على سبيل المثال، يستعمل المكون التالي تأثيرًا للاشتراك بحالة اتصال صديق (friend’s online status) ثم يجري عملية تنظيف عبر إلغاء الاشتراك منها:

```js{10-16}
import React, { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);

    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

في هذا المثال، ستلغي React الاشتراك من `ChatAPI` عند فصل (unmount) المكون وقبل إعادة تنفيذ التأثير نتيجة عملية التصيير اللاحقة. (إن أردت، هنالك طريقة لإخبار React بتخطي  [عملية إعادة الاشتراك](/docs/hooks-effect.html#tip-optimizing-performance-by-skipping-effects) إن لم يتغير `props.friend.id` الذي مررناه إلى `ChatAPI`.)

بشكل مشابه للخطاف `useState`، تستطيع استعمال أكثر من تأثير في مكون:

```js{3,8}
function FriendStatusWithCounter(props) {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  const [isOnline, setIsOnline] = useState(null);
  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }
  // ...
```

تسمح لك الخطافات بتنظيم التأثيرات الجانبية في مكون بناءً على ترابط الأجزاء مع بعضها (مثل إضافة وإزالة اشتراك) عوض التقسيم الإجباري المستند إلى توابع دورة الحياة.

>شرح أوسع
>
>يمكن تعلم المزيد حول الخطاف `useEffect` في صفحة مخصصة به هي [استعمال خطاف التأثير](/docs/hooks-effect.html).

## ✌️ قواعد تخص الخطافات {#rules-of-hooks}

الخطافات هي دوال في JavaScript، ولكنها تفرض تطبيق قاعدتين إضافيتين هما:

* تُستدعَى الخطافات فقط في **المستوى الأعلى (top level)**. بناءً على ذلك، لا تستدعي الخطافات داخل حلقات تكرارية، أو شروط، أو دوال متشعبة.
* تُستدعَى الخطافات فقط **من مكونات دالة React (أي React function components)**. لا تستدعي الخطافات من دوال JavaScript العادية. (هنالك مكان آخر صالح يمكن استدعاء الخطافات منه يحدد عند بناء خطافات مخصصة خاصة بك. سنتحدث عن هذا النوع من الخطافات بعد قليل.)

نوفر [إضافةً لاكتشاف أخطاء الصياغة](https://www.npmjs.com/package/eslint-plugin-react-hooks) يمكنها أن تطبِّق هاتين القاعدتين تلقائيًّا. نتفهَّم أنَّ هاتين القاعدتين قد تبدوان لك شكلًا من أشكال التقيد لسلوك الخطافات أو قد تسببان لك القلق عند بدء استعمال الخطافات، ولكن كن على يقين أنَّهما ضروريتان لعمل الخطافات بشكل صحيح.

>شرح أوسع
>
>يمكن قراءة المزيد حول هاتين القاعدتين في صفحة [قواعد استعمال الخطافات](/docs/hooks-rules.html).

## 💡 إنشاء خطافات مخصصة خاصة بك {#building-your-own-hooks}

بعض الأحيان، نحتاج إلى إعادة استعمال بعض الشيفرات ذات الحالة (stateful logic) بين المكونات. تقليديًّا، يوجد حلان لهذه المشكلة هما: [المكونات ذات الترتيب الأعلى](/docs/higher-order-components.html) و [خاصيات التصيير](/docs/render-props.html). تمكنك الخطافات المخصصة من إنجاز هذه المهمة، ولكن دون إضافة المزيد من المكونات إلى شجرتك.

في قسم سابق من هذه الصفحة، عرَّفنا المكون `FriendStatus` الذي يستدعي الخطاف `useState` والخطاف `useEffect` للاشتراك في حالة اتصال صديق. افترض أنَّنا نريد أيضًا إعادة استعمال شيفرة هذا الاشتراك في مكون آخر فماذا نفعل؟

أولًا، سنستخرج هذا الشيفرة إلى خطاف مخصص يدعى `useFriendStatus` بالشكل التالي:

```js{3}
import React, { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```

يأخذ الوسيط `friendID`، ويعيد حالة الصديق أي إن كان متصلًا أم لا.

الآن، يمكننا استعماله من أي مكون نريد:

```js{2}
function FriendStatus(props) {
  const isOnline = useFriendStatus(props.friend.id);

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

```js{2}
function FriendListItem(props) {
  const isOnline = useFriendStatus(props.friend.id);

  return (
    <li style={{ color: isOnline ? 'green' : 'black' }}>
      {props.friend.name}
    </li>
  );
}
```

<<<<<<< HEAD
حالة هذه المكونات هي مستقلة كليًّا. الخطافات هي وسيلة لإعادة استعمال الشيفرة ذات الحالة وليس الحالة نفسها. في الحقيقة، كل استدعاء إلى خطاف يملك حالة منعزلة تمامًا، لذا يمكنك حتى استعمال نفس الخطاف المخصص مرتين في مكون واحد.
=======
The state of each component is completely independent. Hooks are a way to reuse *stateful logic*, not state itself. In fact, each *call* to a Hook has a completely isolated state -- so you can even use the same custom Hook twice in one component.
>>>>>>> 63332462bb5afa18ac7a716975b679f4c23cc8a1

الخطافات المخصصة هي أقرب للعرف من كونها ميزة. إن بدأ اسم دالة بالكلمة "`use`" واستدعت خطافات أخرى، نقول أنَّها "خطاف مخصص". التسمية `useSomething` المتعارف عليها هي التي تمكن إضافة تصحيح أخطاء الصياغة (linter plugin) من تنقيح الشيفرة التي تستعمل الخطافات.

يمكنك كتابة خطافات مخصصة تغطي مجالًا واسعًا من الحالات مثل معالجة النماذج، والتحريك، والاشتراكات التصريحية (declarative subscriptions)، والمؤقتات، وغيرها الكثير. نتطلع بشوق لرؤية الخطافات المخصصة التي سيبتكرها المجتمع.

>شرح أوسع
>
>يمكنك تعلم المزيد حول الخطافات المخصصة بالتفصيل في صفحة [بناء خطافات خاصة بك](/docs/hooks-custom.html).

## 🔌 خطافات أخرى {#other-hooks}

هنالك بعض الخطافات المضمنة غير شائعة الاستخدام يمكن أن تجد فيها فائدةً ما. على سبيل المثال، [`useContext`](/docs/hooks-reference.html#usecontext) يسمح لك بالاشتراك بسياق React دون اللجوء إلى التشعب:

```js{2,3}
function Example() {
  const locale = useContext(LocaleContext);
  const theme = useContext(ThemeContext);
  // ...
}
```

والخطاف [`useReducer`](/docs/hooks-reference.html#usereducer) يمكنك من إدارة الحالة المحلية للمكونات المعقدة مع مخفِّض (reducer):

```js{2}
function Todos() {
  const [todos, dispatch] = useReducer(todosReducer);
  // ...
```

>شرح أوسع
>
>يمكنك الاطلاع على جميع الخطافات المضمَّنة في التوثيق [مرجع إلى الواجهة البرمجية للخطافات](/docs/hooks-reference.html).

## الخطوات التالية {#next-steps}

كان هذا الشرح مختصرًا ومفيدًا، أليس كذلك؟! إن لم تعتقد ذلك أو كنت تريد تعلم المزيد وبالتفصيل، يمكنك الانتقال إلى الصفحات التالية بدءًا من توثيق  [استعمال خطاف الحالة](/docs/hooks-state.html).

يمكنك أيضًا في أي وقت الاطلاع على توثيق [مرجع إلى الواجهة البرمجية للخطافات](/docs/hooks-reference.html) وصفحة [الأسئلة الشائعة حول الخطافات](/docs/hooks-faq.html).

أخيرًا، إن لم تكن قد اطلعت على صفحة [مدخل إلى الخطافات](/docs/hooks-intro.html) فلا تدع فرصة قراءتها تفوتك، إذ تشرح تلك الصفحة سبب إضافة الخطافات وكيفية البدء باستعمالها جنبًا إلى جنب مع الأصناف دون إعادة كتابة تطبيقك.
