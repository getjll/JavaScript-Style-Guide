> 用于本人提高代码风格、学习在写代码中的一些坑。
>
> 同时提高自己的英文文档阅读能力！！！！
>
> 强烈建议看原版 => [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)

# Airbnb JavaScript 风格指南() {

*更合理的书写 JavaScript*

[![Downloads](https://img.shields.io/npm/dm/eslint-config-airbnb.svg)](https://www.npmjs.com/package/eslint-config-airbnb)
[![Downloads](https://img.shields.io/npm/dm/eslint-config-airbnb-base.svg)](https://www.npmjs.com/package/eslint-config-airbnb-base)
[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/airbnb/javascript?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

其他风格指南

 - [ES5 (已废弃)](https://github.com/airbnb/javascript/tree/es5-deprecated/es5)
 - [React](react/)
 - [CSS-in-JavaScript](css-in-javascript/)
 - [CSS & Sass](https://github.com/airbnb/css)
 - [Ruby](https://github.com/airbnb/ruby)

<a name="table-of-contents"></a>
## 目录

  1. [类型](#types)
  1. [引用](#references)
  1. [对象](#objects)
  1. [数组](#arrays)
  1. [解构](#destructuring)
  1. [字符串](#strings)
  1. [函数](#functions)
  1. [箭头函数](#arrow-functions)
  1. [类和构造函数](#classes--constructors)
  1. [模块](#modules)
  1. [迭代器和生成器](#iterators-and-generators)
  1. [属性](#properties)
  1. [变量](#variables)
  1. [变量提升](#hoisting)
  1. [比较运算符 & 相等](#comparison-operators--equality)
  1. [代码块](#blocks)
  1. [控制语句](#control-statements)
  1. [注释](#comments)
  1. [空白](#whitespace)
  1. [逗号](#commas)
  1. [分号](#semicolons)
  1. [类型转换](#type-casting--coercion)
  1. [命名约定](#naming-conventions)
  1. [访问器](#accessors)
  1. [事件](#events)
  1. [jQuery](#jquery)
  1. [ECMAScript 5 兼容性](#ecmascript-5-compatibility)
  1. [ECMAScript 6+ (ES 2015+) 风格](#ecmascript-6-es-2015-styles)
  1. [测试](#testing)
  1. [性能](#performance)
  1. [相关资源](#resources)
  1. [谁使用了](#in-the-wild)
  1. [翻译](#translation)
  1. [JavaScript 风格指南说明](#the-javascript-style-guide-guide)
  1. [一起来讨论 JavaScript](#chat-with-us-about-javascript)
  1. [贡献者](#contributors)
  1. [许可证](#license)

## 类型

  <a name="types--primitives"></a><a name="1.1"></a>
  
  - [1.1](#types--primitives) **基本类型**: 使用基本类型时实际上是访问了值。

    + `string`
    + `number`
    + `boolean`
    + `null`
    + `undefined`

    ```javascript
    const foo = 1;
    let bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```

  <a name="types--complex"></a><a name="1.2"></a>
  - [1.2](#types--complex)  **复杂类型**: 使用复杂类型时实际上是访问了一个引用。

    + `object`
    + `array`
    + `function`

    ```javascript
    const foo = [1, 2];
    const bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```

**[⬆ 回到顶部](#table-of-contents)**

## 引用

  <a name="references--prefer-const"></a><a name="2.1"></a>
  
  - [2.1](#references--prefer-const) 总是使用 `const` 声明引用; 避免 `var`。 eslint: [`prefer-const`](http://eslint.org/docs/rules/prefer-const.html), [`no-const-assign`](http://eslint.org/docs/rules/no-const-assign.html)

    > 为什么? 这将确保你不能重新分配你的引用，从而导致错误和难以理解的代码.

    ```javascript
    // 坏
    var a = 1;
    var b = 2;

    // 好
    const a = 1;
    const b = 2;
    ```

  <a name="references--disallow-var"></a><a name="2.2"></a>
  
  - [2.2](#references--disallow-var) 如果必须重新赋值声明，请使用 `let ` 代替 ` var `。 eslint: [`no-var`](http://eslint.org/docs/rules/no-var.html) jscs: [`disallowVar`](http://jscs.info/rule/disallowVar)

    > 为什么? 因为 `let` 是块级作用域，而 `var` 是函数作用域。

    ```javascript
    // 坏
    var count = 1;
    if (true) {
      count += 1;
    }

    // 使用 let 更好.
    let count = 1;
    if (true) {
      count += 1;
    }
    ```

  <a name="references--block-scope"></a><a name="2.3"></a>
  
  - [2.3](#references--block-scope) 需要注意 `let` 和 `const` 都是块级作用域。

    ```javascript
    // const 和 let 仅生效于定义的代码块内.
    {
      let a = 1;
      const b = 1;
    }
    console.log(a); // ReferenceError
    console.log(b); // ReferenceError
    ```

**[⬆ 回到顶部](#table-of-contents)**

## 对象

  <a name="objects--no-new"></a><a name="3.1"></a>
  
  - [3.1](#objects--no-new) 使用字面语法创建对象。 eslint: [`no-new-object`](http://eslint.org/docs/rules/no-new-object.html)

    ```javascript
    // 坏
    const item = new Object();

    // 好
    const item = {};
    ```

  <a name="es6-computed-properties"></a><a name="3.4"></a>
  
  - [3.2](#es6-computed-properties) 在创建具有动态属性名称的对象时使用计算属性名称。

    > 为什么? 它们允许你在一个地方定义所有属性
    
    ```javascript

    function getKey(k) {
      return `a key named ${k}`;
    }

    // 坏
    const obj = {
      id: 5,
      name: 'San Francisco',
    };
    obj[getKey('enabled')] = true;

    // 好
    const obj = {
      id: 5,
      name: 'San Francisco',
      [getKey('enabled')]: true,
    };
    ```

  <a name="es6-object-shorthand"></a><a name="3.5"></a>
  
  - [3.3](#es6-object-shorthand) 简写对象方法。 eslint: [`object-shorthand`](http://eslint.org/docs/rules/object-shorthand.html) jscs: [`requireEnhancedObjectLiterals`](http://jscs.info/rule/requireEnhancedObjectLiterals)

    ```javascript
    // 坏
    const atom = {
      value: 1,

      addValue: function (value) {
        return atom.value + value;
      },
    };

    // 好
    const atom = {
      value: 1,

      addValue(value) {
        return atom.value + value;
      },
    };
    ```

  <a name="es6-object-concise"></a><a name="3.6"></a>
  
  - [3.4](#es6-object-concise) 属性简写 eslint: [`object-shorthand`](http://eslint.org/docs/rules/object-shorthand.html) jscs: [`requireEnhancedObjectLiterals`](http://jscs.info/rule/requireEnhancedObjectLiterals)

    > 为什么? 书写和描述简洁。

    ```javascript
    const lukeSkywalker = 'Luke Skywalker';

    // 坏
    const obj = {
      lukeSkywalker: lukeSkywalker,
    };

    // 好
    const obj = {
      lukeSkywalker,
    };
    ```

  <a name="objects--grouped-shorthand"></a><a name="3.7"></a>
  
  - [3.5](#objects--grouped-shorthand) 简写属性一起写在对象声明头部

    > 为什么? 可以清晰知道定义哪些简写属性

    ```javascript
    const anakinSkywalker = 'Anakin Skywalker';
    const lukeSkywalker = 'Luke Skywalker';

    // 坏
    const obj = {
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      lukeSkywalker,
      episodeThree: 3,
      mayTheFourth: 4,
      anakinSkywalker,
    };

    // 好
    const obj = {
      lukeSkywalker,
      anakinSkywalker,
      episodeOne: 1,
      twoJediWalkIntoACantina: 2,
      episodeThree: 3,
      mayTheFourth: 4,
    };
    ```

  <a name="objects--quoted-props"></a><a name="3.8"></a>
  
  - [3.6](#objects--quoted-props) 非法属性才使用引号包裹 eslint: [`quote-props`](http://eslint.org/docs/rules/quote-props.html) jscs: [`disallowQuotedKeysInObjects`](http://jscs.info/rule/disallowQuotedKeysInObjects)

    > 为什么? 一般来说，我们认为它主观容易阅读。它提高了语法高亮显示，也更容易地优化了许多JS引擎。

    ```javascript
    // 坏
    const bad = {
      'foo': 3,
      'bar': 4,
      'data-blah': 5,
    };

    // 好
    const good = {
      foo: 3,
      bar: 4,
      'data-blah': 5,
    };
    ```

  <a name="objects--prototype-builtins"></a>
  
  - [3.7](#objects--prototype-builtins) 不要直接调用 `Object.prototype` 方法, 例如 `hasOwnProperty`, `propertyIsEnumerable`, 和 `isPrototypeOf`。

    > 为什么? 这些方法可能被对象的属性所遮蔽 - 考虑 `{ hasOwnProperty: false }` - 或, 对象可以是空对象 (`Object.create(null)`).

    ```javascript
    // 糟糕
    console.log(object.hasOwnProperty(key));

    // 好
    console.log(Object.prototype.hasOwnProperty.call(object, key));

    // 更好
    const has = Object.prototype.hasOwnProperty; // 在模块范围内缓存一次查找
    /* or */
    import has from 'has';
    // ...
    console.log(has.call(object, key));
    ```

  <a name="objects--rest-spread"></a>
  
  - [3.8](#objects--rest-spread) 浅拷贝对象时，使用对象展开符代替[`Object.assign`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)。使用对象解构操作符赋值属性。

    ```javascript
    // 太糟糕了
    const original = { a: 1, b: 2 };
    const copy = Object.assign(original, { c: 3 }); // 因为`original`被修改 ಠ_ಠ
    delete copy.a; // 所以这里要这么干

    // 糟糕
    const original = { a: 1, b: 2 };
    const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

    // 好的
    const original = { a: 1, b: 2 };
    const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

    const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
    ```

**[⬆ 回到顶部](#table-of-contents)**

## 数组

  <a name="arrays--literals"></a><a name="4.1"></a>
  
  - [4.1](#arrays--literals) 使用字面量语法创建数组。 eslint: [`no-array-constructor`](http://eslint.org/docs/rules/no-array-constructor.html)

    ```javascript
    // 糟糕的
    const items = new Array();

    // 好的
    const items = [];
    ```

  <a name="arrays--push"></a><a name="4.2"></a>
  
  - [4.2](#arrays--push) 使用 [Array#push](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/push) 而不是直接向数组追加项。

    ```javascript
    const someStack = [];

    // 糟糕的
    someStack[someStack.length] = 'abracadabra';

    // 好的
    someStack.push('abracadabra');
    ```

  <a name="es6-array-spreads"></a><a name="4.3"></a>
  
  - [4.3](#es6-array-spreads) 使用数组解构 `...` 进行拷贝.

    ```javascript
    // 糟糕的
    const len = items.length;
    const itemsCopy = [];
    let i;

    for (i = 0; i < len; i += 1) {
      itemsCopy[i] = items[i];
    }

    // 好的
    const itemsCopy = [...items];
    ```

  <a name="arrays--from"></a><a name="4.4"></a>
  
  - [4.4](#arrays--from) 转换类数组时, 使用 [Array.from](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/from).

    ```javascript
    const foo = document.querySelectorAll('.foo');
    const nodes = Array.from(foo);
    ```

  <a name="arrays--callback-return"></a><a name="4.5"></a>
  
  - [4.5](#arrays--callback-return) 数组方法始终显示声明返回。 如果你的函数体项[8.2](#arrows--implicit-return)一样简单，则可以省略。 eslint: [`array-callback-return`](http://eslint.org/docs/rules/array-callback-return)
	
    ```javascript
    // 好的
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });

    // 好的
    [1, 2, 3].map(x => x + 1);

    // 糟糕的
    const flat = {};
    [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
      const flatten = memo.concat(item);
      flat[index] = flatten;
    });

    // 好的
    const flat = {};
    [[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
      const flatten = memo.concat(item);
      flat[index] = flatten;
      return flatten;
    });

    // 糟糕的
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      } else {
        return false;
      }
    });

    // 好的
    inbox.filter((msg) => {
      const { subject, author } = msg;
      if (subject === 'Mockingbird') {
        return author === 'Harper Lee';
      }

      return false;
    });
    ```

  <a name="arrays--bracket-newline"></a>

  - [4.6](#arrays--bracket-newline) 如果数组有多行，请在打开数组后和关闭数组括号之前使用换行符。

  ```javascript
  // 糟糕的
  const arr = [
    [0, 1], [2, 3], [4, 5],
  ];

  const objectInArray = [{
    id: 1,
  }, {
    id: 2,
  }];

  const numberInArray = [
    1, 2,
  ];

  // good
  const arr = [[0, 1], [2, 3], [4, 5]];

  const objectInArray = [
    {
      id: 1,
    },
    {
      id: 2,
    },
  ];

  const numberInArray = [
    1,
    2,
  ];
  ```

**[⬆ 回到顶部](#table-of-contents)**

## 解构

  <a name="destructuring--object"></a><a name="5.1"></a>
  
  - [5.1](#destructuring--object) 当你访问或使用一个对象的多个属性时，使用对象解构。 jscs: [`requireObjectDestructuring`](http://jscs.info/rule/requireObjectDestructuring)

    > 为什么? 解构可以节省创建临时变量的性能。

    ```javascript
    // 糟糕的
    function getFullName(user) {
      const firstName = user.firstName;
      const lastName = user.lastName;

      return `${firstName} ${lastName}`;
    }

    // 好的
    function getFullName(user) {
      const { firstName, lastName } = user;
      return `${firstName} ${lastName}`;
    }

    // 更好的
    function getFullName({ firstName, lastName }) {
      return `${firstName} ${lastName}`;
    }
    ```

  <a name="destructuring--array"></a><a name="5.2"></a>
  
  - [5.2](#destructuring--array) 对数组使用解构。 jscs: [`requireArrayDestructuring`](http://jscs.info/rule/requireArrayDestructuring)

    ```javascript
    const arr = [1, 2, 3, 4];

    // 糟糕的
    const first = arr[0];
    const second = arr[1];

    // 好的
    const [first, second] = arr;
    ```

  <a name="destructuring--object-over-array"></a><a name="5.3"></a>
  
  - [5.3](#destructuring--object-over-array) 使用对象而非数组解构处理多个返回值。jscs: [`disallowArrayDestructuringReturn`](http://jscs.info/rule/disallowArrayDestructuringReturn)
  使用对象而非数组解构处理多个返回值。

    > 为什么? 在你添加先的属性时，不改变原有顺序。

    ```javascript
    // 糟糕的
    function processInput(input) {
      // 见证奇迹的时刻
      return [left, right, top, bottom];
    }

    // 调用方需要考虑返回的顺序
    const [left, __, top] = processInput(input);

    // good
    function processInput(input) {
      // 见证奇迹的时刻
      return { left, right, top, bottom };
    }

    // 不需要关心顺序
    const { left, top } = processInput(input);
    ```


**[⬆ 回到顶部](#table-of-contents)**

## 字符串

  <a name="strings--quotes"></a><a name="6.1"></a>
  
  - [6.1](#strings--quotes) 字符串使用单引号 `''`。 eslint: [`quotes`](http://eslint.org/docs/rules/quotes.html) jscs: [`validateQuoteMarks`](http://jscs.info/rule/validateQuoteMarks)

    ```javascript
    // 糟糕的
    const name = "Capt. Janeway";

    // 同样糟糕的 - 模板文字应包含插值或换行符
    const name = `Capt. Janeway`;

    // 好的
    const name = 'Capt. Janeway';
    ```

  <a name="strings--line-length"></a><a name="6.2"></a>
  
  - [6.2](#strings--line-length) 导致字符串超过100个字符的字符串不应该使用字符串连接在多行上写入。

    > 为什么? 断字符串是痛苦的工作，使代码少搜索。

    ```javascript
    // 糟糕的
    const errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // 同样糟糕的
    const errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';

    // 好的
    const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
    ```

  <a name="es6-template-literals"></a><a name="6.4"></a>
  
  - [6.3](#es6-template-literals) 当拼接建立字符串时，使用模板字符串而不是连接。 eslint: [`prefer-template`](http://eslint.org/docs/rules/prefer-template.html) [`template-curly-spacing`](http://eslint.org/docs/rules/template-curly-spacing) jscs: [`requireTemplateStrings`](http://jscs.info/rule/requireTemplateStrings)

    > 为什么? 模板字符串给你一个可读的，简明的语法正确的换行和字符串插值功能。

    ```javascript
    // 糟糕的
    function sayHi(name) {
      return 'How are you, ' + name + '?';
    }

    // 同样糟糕的
    function sayHi(name) {
      return ['How are you, ', name, '?'].join();
    }

    // 糟糕的
    function sayHi(name) {
      return `How are you, ${ name }?`;
    }

    // 优雅的
    function sayHi(name) {
      return `How are you, ${name}?`;
    }
    ```

  <a name="strings--eval"></a><a name="6.5"></a>
  
  - [6.4](#strings--eval) 永远不要将字符串传递给 `eval()` ，它是许多漏洞的根源。
 

  <a name="strings--escaping"></a>
  
  - [6.5](#strings--escaping) 不要转义字符串中没必要转义的字符。 eslint: [`no-useless-escape`](http://eslint.org/docs/rules/no-useless-escape)

    > 为什么? 反斜杠破坏了可读性，因此它们只能出现在必要的时候。

    ```javascript
    // 糟糕的
    const foo = '\'this\' \i\s \"quoted\"';

    // 好的
    const foo = '\'this\' is "quoted"';
    const foo = `my name is '${name}'`;
    ```

**[⬆ 回到顶部](#table-of-contents)**


## 函数

  <a name="functions--declarations"></a><a name="7.1"></a>
  
  - [7.1](#functions--declarations) 使用命名函数表达式代替函数声明。 eslint: [`func-style`](http://eslint.org/docs/rules/func-style) jscs: [`disallowFunctionDeclarations`](http://jscs.info/rule/disallowFunctionDeclarations)

    > 为什么? 函数声明被挂起，这意味着它很容易-太容易-在文件中定义函数之前引用它。这损害可读性和可维护性。如果你发现一个函数的定义是大的或足够复杂的，它会干扰理解文件的其余部分，那么也许是时候把它提取到自己的模块了！不要忘记给表达式命名--匿名函数会使得在错误调用堆栈中查找问题变得更加困难。 ([Discussion](https://github.com/airbnb/javascript/issues/794))

    ```javascript
    // 糟糕的
    function foo() {
      // ...
    }

    // 同样糟糕的
    const foo = function () {
      // ...
    };

    // 好的
    const foo = function bar() {
      // ...
    };
    ```

  <a name="functions--iife"></a><a name="7.2"></a>
  
  - [7.2](#functions--iife) Wrap immediately invoked function expressions in parentheses. eslint: [`wrap-iife`](http://eslint.org/docs/rules/wrap-iife.html) jscs: [`requireParenthesesAroundIIFE`](http://jscs.info/rule/requireParenthesesAroundIIFE)

    > 为什么? 一个立即调用函数表达式是一个单独的单元包装它，和它的调用括号，在括号里，干净的表达。值得注意的是，在这个世界上，模块无处不在，你几乎从不需要IIFE。

    ```javascript
    // 立即调用函数表达式 (IIFE)
    (function () {
      console.log('Welcome to the Internet. Please follow me.');
    }());
    ```

  <a name="functions--in-blocks"></a><a name="7.3"></a>
  
  - [7.3](#functions--in-blocks) 不要在非函数块中声明函数（`if`，`while`，etc）。将函数赋给变量。浏览器会允许你这样做，但不幸的是它们的解析表现不一致。 eslint: [`no-loop-func`](http://eslint.org/docs/rules/no-loop-func.html)

  <a name="functions--note-on-blocks"></a><a name="7.4"></a>
  
  - [7.4](#functions--note-on-blocks) **注意:** ECMA-262 定义 `block` 一组语句。函数声明不是语句 [查看ECMA-262的说明](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97).

    ```javascript
    // 糟糕的
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // 好的
    let test;
    if (currentUser) {
      test = () => {
        console.log('Yup.');
      };
    }
    ```

  <a name="functions--arguments-shadow"></a><a name="7.5"></a>
  
  - [7.5](#functions--arguments-shadow) 永远不要将一个参数命名为`arguments`。否则这个参数的优先级将高于原有函数作用域内的`arguments`对象。

    ```javascript
    // 糟糕的
    function foo(name, options, arguments) {
      // ...
    }

    // 好的
    function foo(name, options, args) {
      // ...
    }
    ```

  <a name="es6-rest"></a><a name="7.6"></a>
  
  - [7.6](#es6-rest) 不要使用 `arguments`, 选择 rest 语法 `...` 代替. eslint: [`prefer-rest-params`](http://eslint.org/docs/rules/prefer-rest-params)

    > 为什么? 使用 `...` 能明确你要传入的参数。另外 rest 参数是一个真正的数组，而 `arguments` 是一个类数组。

    ```javascript
    // 糟糕的
    function concatenateAll() {
      const args = Array.prototype.slice.call(arguments);
      return args.join('');
    }

    // 好的
    function concatenateAll(...args) {
      return args.join('');
    }
    ```

  <a name="es6-default-parameters"></a><a name="7.7"></a>
  
  - [7.7](#es6-default-parameters) 使用默认参数语法，而不是重写函数参数。

    ```javascript
    // 实在有点糟糕
    function handleThings(opts) {
      // 不好! 我们不应该重写函数参数。
      // 更糟糕: 如果 opts 是 falsy 将会将参数设置为一个对象
      // 是你想要的，但它可以引入微妙的错误。
      opts = opts || {};
      // ...
    }

    // 同样糟糕
    function handleThings(opts) {
      if (opts === void 0) {
        opts = {};
      }
      // ...
    }

    // 好的
    function handleThings(opts = {}) {
      // ...
    }
    ```

  <a name="functions--default-side-effects"></a><a name="7.8"></a>
  
  - [7.8](#functions--default-side-effects) 避免有副作用的默认参数
    > 为什么? 它将使人困惑。

    ```javascript
    var b = 1;
    // 糟糕的
    function count(a = b++) {
      console.log(a);
    }
    count();  // 1
    count();  // 2
    count(3); // 3
    count();  // 3
    ```

  <a name="functions--defaults-last"></a><a name="7.9"></a>
  
  - [7.9](#functions--defaults-last) 总是将默认参数放在最后。

    ```javascript
    // 不好的
    function handleThings(opts = {}, name) {
      // ...
    }

    // 好的
    function handleThings(name, opts = {}) {
      // ...
    }
    ```

  <a name="functions--constructor"></a><a name="7.10"></a>
  
  - [7.10](#functions--constructor) 不要使用 Function 构造函数创建新函数。 eslint: [`no-new-func`](http://eslint.org/docs/rules/no-new-func)

    > 为什么? 这样创建的函数类似 eval(), 存在漏洞。

    ```javascript
    // 糟糕的
    var add = new Function('a', 'b', 'return a + b');

    // 同样糟糕的
    var subtract = Function('a', 'b', 'return a - b');
    ```

  <a name="functions--signature-spacing"></a><a name="7.11"></a>
  
  - [7.11](#functions--signature-spacing) 保持function关键字的间距。 eslint: [`space-before-function-paren`](http://eslint.org/docs/rules/space-before-function-paren) [`space-before-blocks`](http://eslint.org/docs/rules/space-before-blocks)

    > 为什么? 良好的一致性, 当你添加或移除名字时，不需要添加额外的空格。

    ```javascript
    // 不好的
    const f = function(){};
    const g = function (){};
    const h = function() {};

    // 好的
    const x = function () {};
    const y = function a() {};
    ```

  <a name="functions--mutate-params"></a><a name="7.12"></a>
  
  - [7.12](#functions--mutate-params) 永远不要重写参数。 eslint: [`no-param-reassign`](http://eslint.org/docs/rules/no-param-reassign.html)

    > 为什么? 操纵传入的参数可能会导致对调用者不必要的变量副作用。

    ```javascript
    // 糟糕的
    function f1(obj) {
      obj.key = 1;
    }

    // 好的
    function f2(obj) {
      const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
    }
    ```

  <a name="functions--reassign-params"></a><a name="7.13"></a>
  
  - [7.13](#functions--reassign-params) 不要重现赋值参数。 eslint: [`no-param-reassign`](http://eslint.org/docs/rules/no-param-reassign.html)

    > 为什么? 将参数会导致意外的行为，特别是当访问 `arguments` 对象。它也可以导致优化问题，特别是在V8。

    ```javascript
    // 糟糕的
    function f1(a) {
      a = 1;
      // ...
    }

    function f2(a) {
      if (!a) { a = 1; }
      // ...
    }

    // 好的
    function f3(a) {
      const b = a || 1;
      // ...
    }

    function f4(a = 1) {
      // ...
    }
    ```

  <a name="functions--spread-vs-apply"></a><a name="7.14"></a>
  
  - [7.14](#functions--spread-vs-apply) 可变参函数调用，使用拓展操作符 `...`。 eslint: [`prefer-spread`](http://eslint.org/docs/rules/prefer-spread)
  
    > 为什么? 更简洁, 不需要上下文，同时你不能轻易组合具有 `apply` 的 `new` 调用。

    ```javascript
    // 糟糕的
    const x = [1, 2, 3, 4, 5];
    console.log.apply(console, x);

    // 好的
    const x = [1, 2, 3, 4, 5];
    console.log(...x);

    // 糟糕的
    new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));

    // 好的
    new Date(...[2016, 8, 5]);
    ```

  <a name="functions--signature-invocation-indentation"></a>
  
  - [7.15](#functions--signature-invocation-indentation) 多参数的函数定义和调用，应该像其他多行列表一样缩进的风格：每行只包含一项，同时最后一项尾随一个逗号。

    ```javascript
    // 糟糕的
    function foo(bar,
                 baz,
                 quux) {
      // ...
    }

    // 好的
    function foo(
      bar,
      baz,
      quux,
    ) {
      // ...
    }

    // 糟糕的
    console.log(foo,
      bar,
      baz);

    // 好的
    console.log(
      foo,
      bar,
      baz,
    );
    ```

**[⬆ 回到顶部](#table-of-contents)**

## 箭头函数

  <a name="arrows--use-them"></a><a name="8.1"></a>
  
  - [8.1](#arrows--use-them) 当您必须使用函数表达式（如传递匿名函数时），请使用箭头函数符号。 eslint: [`prefer-arrow-callback`](http://eslint.org/docs/rules/prefer-arrow-callback.html), [`arrow-spacing`](http://eslint.org/docs/rules/arrow-spacing.html) jscs: [`requireArrowFunctions`](http://jscs.info/rule/requireArrowFunctions)

    > 为什么? 因为箭头函数创建新`this`的执行上下文， 这通常是你想要的， 同时这是更简洁的语法。

    > 为什么不? 如果你有一个相当复杂的函数，你可以把这个逻辑输出到它自己的函数声明中。

    ```javascript
    // 不好
    [1, 2, 3].map(function (x) {
      const y = x + 1;
      return x * y;
    });

    // 好的
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--implicit-return"></a><a name="8.2"></a>
  - [8.2](#arrows--implicit-return) 如果函数体是一个简单的表达式，省略大括号，使用隐形返回。否则，保持大括号显式 `return` 返回值 eslint: [`arrow-parens`](http://eslint.org/docs/rules/arrow-parens.html), [`arrow-body-style`](http://eslint.org/docs/rules/arrow-body-style.html) jscs:  [`disallowParenthesesAroundArrowParam`](http://jscs.info/rule/disallowParenthesesAroundArrowParam), [`requireShorthandArrowFunctions`](http://jscs.info/rule/requireShorthandArrowFunctions)
 

    > 为什么? 语法糖。 多个函数链接时，可读性较好。

    ```javascript
    // 不太好
    [1, 2, 3].map(number => {
      const nextNumber = number + 1;
      `A string containing the ${nextNumber}.`;
    });

    // 这样更好
    [1, 2, 3].map(number => `A string containing the ${number}.`);

    // 同样好的
    [1, 2, 3].map((number) => {
      const nextNumber = number + 1;
      return `A string containing the ${nextNumber}.`;
    });

    // 更漂亮的
    [1, 2, 3].map((number, index) => ({
      [index]: number,
    }));
    ```

  <a name="arrows--paren-wrap"></a><a name="8.3"></a>
  
  - [8.3](#arrows--paren-wrap) 如果表达式跨越多行，请将其包在括号中以获得更好的可读性。

    > 为什么? 这样你可以清晰的知道一个函数的开始和结束。

    ```javascript
    // 糟糕的
    ['get', 'post', 'put'].map(httpMethod => Object.prototype.hasOwnProperty.call(
        httpMagicObjectWithAVeryLongName,
        httpMethod,
      )
    );

    // 好的
    ['get', 'post', 'put'].map(httpMethod => (
      Object.prototype.hasOwnProperty.call(
        httpMagicObjectWithAVeryLongName,
        httpMethod,
      )
    ));
    ```

  <a name="arrows--one-arg-parens"></a><a name="8.4"></a>
  
  - [8.4](#arrows--one-arg-parens) 如果函数只有一个参数，不使用括号，省略括号。 否者，为了清晰和一致性总是用圆括号包裹参数。 注意: 使用圆括号也是可以接受的，在这种情况下，使用ESLint["always" option](http://eslint.org/docs/rules/arrow-parens#always)选项或则不引入 jscs的 [`disallowParenthesesAroundArrowParam`](http://jscs.info/rule/disallowParenthesesAroundArrowParam) 选项。 eslint: [`arrow-parens`](http://eslint.org/docs/rules/arrow-parens.html) jscs:  [`disallowParenthesesAroundArrowParam`](http://jscs.info/rule/disallowParenthesesAroundArrowParam)

    > 为什么? 减少视觉混乱。

    ```javascript
    // 糟糕的
    [1, 2, 3].map((x) => x * x);

    // 好的
    [1, 2, 3].map(x => x * x);

    // 好的
    [1, 2, 3].map(number => (
      `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
    ));

    // 不好的
    [1, 2, 3].map(x => {
      const y = x + 1;
      return x * y;
    });

    // 好的
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

  <a name="arrows--confusing"></a><a name="8.5"></a>
  
  - [8.5](#arrows--confusing) 避免与比较运算符(`<=`, `>=`)混淆箭头函数(`=>`)。 eslint: [`no-confusing-arrow`](http://eslint.org/docs/rules/no-confusing-arrow)

    ```javascript
    // 糟糕
    const itemHeight = item => item.height > 256 ? item.largeSize : item.smallSize;

    // 糟糕
    const itemHeight = (item) => item.height > 256 ? item.largeSize : item.smallSize;

    // 好的
    const itemHeight = item => (item.height > 256 ? item.largeSize : item.smallSize);

    // 好的
    const itemHeight = (item) => {
      const { height, largeSize, smallSize } = item;
      return height > 256 ? largeSize : smallSize;
    };
    ```

**[⬆ 回到顶部](#table-of-contents)**


## 类和构造函数

  <a name="constructors--use-class"></a><a name="9.1"></a>
  
  - [9.1](#constructors--use-class) 总是使用 `class`。 避免直接操作 `prototype`。

    > 为什么? `class` 更简洁，更容易推理。

    ```javascript
    // 糟糕的
    function Queue(contents = []) {
      this.queue = [...contents];
    }
    Queue.prototype.pop = function () {
      const value = this.queue[0];
      this.queue.splice(0, 1);
      return value;
    };


    // 好的
    class Queue {
      constructor(contents = []) {
        this.queue = [...contents];
      }
      pop() {
        const value = this.queue[0];
        this.queue.splice(0, 1);
        return value;
      }
    }
    ```

  <a name="constructors--extends"></a><a name="9.2"></a>
  
  - [9.2](#constructors--extends) 使用 `extends` 进行。

    > 为什么? 它是一个内置的方式来继承原型的功能而不破坏 `instanceof`.

    ```javascript
    // 糟糕的
    const inherits = require('inherits');
    function PeekableQueue(contents) {
      Queue.apply(this, contents);
    }
    inherits(PeekableQueue, Queue);
    PeekableQueue.prototype.peek = function () {
      return this.queue[0];
    };

    // 好的
    class PeekableQueue extends Queue {
      peek() {
        return this.queue[0];
      }
    }
    ```

  <a name="constructors--chaining"></a><a name="9.3"></a>
  
  - [9.3](#constructors--chaining) 方法可以返回 `this` 以帮助方法链接。

    ```javascript
    // 不太好
    Jedi.prototype.jump = function () {
      this.jumping = true;
      return true;
    };

    Jedi.prototype.setHeight = function (height) {
      this.height = height;
    };

    const luke = new Jedi();
    luke.jump(); // => true
    luke.setHeight(20); // => undefined

    // 好的
    class Jedi {
      jump() {
        this.jumping = true;
        return this;
      }

      setHeight(height) {
        this.height = height;
        return this;
      }
    }

    const luke = new Jedi();

    luke.jump()
      .setHeight(20);
    ```


  <a name="constructors--tostring"></a><a name="9.4"></a>
  
  - [9.4](#constructors--tostring) 这样写也是可以的，只要你能确保它正常运行。
    ```javascript
    class Jedi {
      constructor(options = {}) {
        this.name = options.name || 'no name';
      }

      getName() {
        return this.name;
      }

      toString() {
        return `Jedi - ${this.getName()}`;
      }
    }
    ```

  <a name="constructors--no-useless"></a><a name="9.5"></a>
  
  - [9.5](#constructors--no-useless) 类有默认构造函数。一个空构造函数函数或一个只向父类委托的函数是不必要的。 eslint: [`no-useless-constructor`](http://eslint.org/docs/rules/no-useless-constructor)

    ```javascript
    // 糟糕的
    class Jedi {
      constructor() {}

      getName() {
        return this.name;
      }
    }

    // 同样糟糕
    class Rey extends Jedi {
      constructor(...args) {
        super(...args);
      }
    }

    // 好的
    class Rey extends Jedi {
      constructor(...args) {
        super(...args);
        this.name = 'Rey';
      }
    }
    ```

  <a name="classes--no-duplicate-members"></a>
  
  - [9.6](#classes--no-duplicate-members) 避免重复定义类成员。 eslint: [`no-dupe-class-members`](http://eslint.org/docs/rules/no-dupe-class-members)

    > 为什么? 重复定义的类成员默认使用最后一个 - 有重复基本肯定是一个bug。

    ```javascript
    // 糟糕
    class Foo {
      bar() { return 1; }
      bar() { return 2; }
    }

    // 好的
    class Foo {
      bar() { return 1; }
    }

    // 好的
    class Foo {
      bar() { return 2; }
    }
    ```


**[⬆ 回到顶部](#table-of-contents)**


## 模块

  <a name="modules--use-them"></a><a name="10.1"></a>
  
  - [10.1](#modules--use-them) 总是在非标准模块系统上使用模块 (`import`/`export`)。 你可以编译为你喜欢的模块系统。

    > 为什么? 模块是未来趋势， 让我们现在就拥抱它。

    ```javascript
    // 不好的
    const AirbnbStyleGuide = require('./AirbnbStyleGuide');
    module.exports = AirbnbStyleGuide.es6;

    // 好可以
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    export default AirbnbStyleGuide.es6;

    // 更好的方式
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  <a name="modules--no-wildcard"></a><a name="10.2"></a>
  
  - [10.2](#modules--no-wildcard) 不要使用通配符导出。

    > 为什么? 这将确保你有一个默认的导出。

    ```javascript
    // 糟糕的
    import * as AirbnbStyleGuide from './AirbnbStyleGuide';

    // 好的
    import AirbnbStyleGuide from './AirbnbStyleGuide';
    ```

  <a name="modules--no-export-from-import"></a><a name="10.3"></a>
  
  - [10.3](#modules--no-export-from-import) 不要直接在 `export` 上进行导出。

    > 为什么? 虽然同行更加简洁，但是有一个明确的 `import` 和 `export` 更加一致。

    ```javascript
    // 这样不太好
    // filename es6.js
    export { es6 as default } from './AirbnbStyleGuide';

    // 这样比较好
    // filename es6.js
    import { es6 } from './AirbnbStyleGuide';
    export default es6;
    ```

  <a name="modules--no-duplicate-imports"></a>
  
  - [10.4](#modules--no-duplicate-imports) 只在一个地方使用 `import` 导出。 eslint: [`no-duplicate-imports`](http://eslint.org/docs/rules/no-duplicate-imports)
    > 为什么? 同一模块多行导出更难维护。

    ```javascript
    // 不太好
    import foo from 'foo';
    // … 同时导出额外的 … //
    import { named1, named2 } from 'foo';

    // 好
    import foo, { named1, named2 } from 'foo';

    // 好
    import foo, {
      named1,
      named2,
    } from 'foo';
    ```

  <a name="modules--no-mutable-exports"></a>
  
  - [10.5](#modules--no-mutable-exports) 不导出可变绑定。
 eslint: [`import/no-mutable-exports`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-mutable-exports.md)
    > 为什么? 可变一般应避免，但特别是当导出可变绑定时。虽然这种技术可能需要一些特殊的情况下，一般来说，只有常量引用可以导出。

    ```javascript
    // 糟糕的
    let foo = 3;
    export { foo };

    // 好的
    const foo = 3;
    export { foo };
    ```

  <a name="modules--prefer-default-export"></a>
  
  - [10.6](#modules--prefer-default-export) 在单出口的模块中，默认出口多于指定的出口。
 eslint: [`import/prefer-default-export`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/prefer-default-export.md)

    ```javascript
    // 不太好
    export function foo() {}

    // 这样可以
    export default function foo() {}
    ```

  <a name="modules--imports-first"></a>
  
  - [10.7](#modules--imports-first)将所有的 `import` 定义在头部。
 eslint: [`import/first`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/first.md)
    > 为什么? 保持他们在顶部防止令人惊讶的行为。
    ```javascript
    // 不太好
    import foo from 'foo';
    foo.init();

    import bar from 'bar';

    // 好的
    import foo from 'foo';
    import bar from 'bar';

    foo.init();
    ```

  <a name="modules--multiline-imports-over-newlines"></a>
  
  - [10.8](#modules--multiline-imports-over-newlines) 多个出口应该像数组和对象一样换行缩进。

    > 为什么? 在样式指南中，滚动括号和其他滚动括号一样遵循缩进规则，后面的逗号也一样

    ```javascript
    // 不好的
    import {longNameA, longNameB, longNameC, longNameD, longNameE} from 'path';

    // 好的
    import {
      longNameA,
      longNameB,
      longNameC,
      longNameD,
      longNameE,
    } from 'path';
    ```

  <a name="modules--no-webpack-loader-syntax"></a>
  
  - [10.9](#modules--no-webpack-loader-syntax) 禁止模块`import`声明中使用Webpack loader语法。
 eslint: [`import/no-webpack-loader-syntax`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-webpack-loader-syntax.md)
    > 为什么? 由于Webpack语法是模块构建工具的语法糖，偏向于在`webpack.config.js`中使用。 

    ```javascript
    // 糟糕
    import fooSass from 'css!sass!foo.scss';
    import barCss from 'style!css!bar.css';

    // 好的
    import fooSass from 'foo.scss';
    import barCss from 'bar.css';
    ```

**[⬆ 回到顶部](#table-of-contents)**

## 迭代器和生成器

  <a name="iterators--nope"></a><a name="11.1"></a>
  
  - [11.1](#iterators--nope) 不要使用迭代器。更喜欢JavaScript的高阶函数，而不是`for-in` 或 `for-of`。 eslint: [`no-iterator`](http://eslint.org/docs/rules/no-iterator.html) [`no-restricted-syntax`](http://eslint.org/docs/rules/no-restricted-syntax)

    > 为什么? 强制执行我们的不可变规则。处理返回值的纯函数比副作用更容易解释。

    > 使用 `map()` / `every()` / `filter()` / `find()` / `findIndex()` / `reduce()` / `some()` / ... 遍历数组； `Object.keys()` / `Object.values()` / `Object.entries()` 生成数组，以便可以遍历对象。

    ```javascript
    const numbers = [1, 2, 3, 4, 5];

    // 不好
    let sum = 0;
    for (let num of numbers) {
      sum += num;
    }
    sum === 15;

    // 好
    let sum = 0;
    numbers.forEach(num => sum += num);
    sum === 15;

    // 更好 (使用函数功能)
    const sum = numbers.reduce((total, num) => total + num, 0);
    sum === 15;

    // 不好
    const increasedByOne = [];
    for (let i = 0; i < numbers.length; i++) {
      increasedByOne.push(numbers[i] + 1);
    }

    // 好的
    const increasedByOne = [];
    numbers.forEach(num => increasedByOne.push(num + 1));

    // 更好 (保持它的功能)
    const increasedByOne = numbers.map(num => num + 1);
    ```

  <a name="generators--nope"></a><a name="11.2"></a>
  
  - [11.2](#generators--nope) 目前不要使用generators。

    > 为什么? 不能编译为ES5。

  <a name="generators--spacing"></a>
  
  - [11.3](#generators--spacing) 如果你必须使用 generators 或者无视我们的[劝告](#generators--nope)， 请确保它们的标识间隔正确。 eslint: [`generator-star-spacing`](http://eslint.org/docs/rules/generator-star-spacing)

    > 为什么? `function` 和 `*` 是同一概念关键字的一部分 - `*` 不是 `function` 的修饰符， `function*` 是一个独特的结构，不同于 `function`。

    ```javascript
    // 糟糕
    function * foo() {
      // ...
    }

    // 糟糕
    const bar = function * () {
      // ...
    };

    // 糟糕
    const baz = function *() {
      // ...
    };

    // 糟糕
    const quux = function*() {
      // ...
    };

    // 糟糕
    function*foo() {
      // ...
    }

    // 糟糕
    function *foo() {
      // ...
    }

    // 非常糟糕
    function
    *
    foo() {
      // ...
    }

    // 非常糟糕
    const wat = function
    *
    () {
      // ...
    };

    // 好的
    function* foo() {
      // ...
    }

    // 好
    const foo = function* () {
      // ...
    };
    ```

**[⬆ 回到顶部](#table-of-contents)**


## 属性

  <a name="properties--dot"></a><a name="12.1"></a>
  
  - [12.1](#properties--dot) 使用点语法访问属性。 eslint: [`dot-notation`](http://eslint.org/docs/rules/dot-notation.html) jscs: [`requireDotNotation`](http://jscs.info/rule/requireDotNotation)

    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    // 不好
    const isJedi = luke['jedi'];

    // 好
    const isJedi = luke.jedi;
    ```

  <a name="properties--bracket"></a><a name="12.2"></a>
  
  - [12.2](#properties--bracket) 访问属性是一个变量时使用括号 `[]`。
    ```javascript
    const luke = {
      jedi: true,
      age: 28,
    };

    function getProp(prop) {
      return luke[prop];
    }

    const isJedi = getProp('jedi');
    ```

**[⬆ 回到顶部](#table-of-contents)**


## 变量

  <a name="variables--const"></a><a name="13.1"></a>
  
  - [13.1](#variables--const) 总是使用 `const` 或 `let` 定义变量。 不这样做会导致全局变量。 我们要避免污染全局命名空间。 Captain Planet warned us of that. eslint: [`no-undef`](http://eslint.org/docs/rules/no-undef) [`prefer-const`](http://eslint.org/docs/rules/prefer-const)

    ```javascript
    // 糟糕
    superPower = new SuperPower();

    // 好的
    const superPower = new SuperPower();
    ```

  <a name="variables--one-const"></a><a name="13.2"></a>
  
  - [13.2](#variables--one-const) 使用 `const` 或 `let` 定义每一个变量。 eslint: [`one-var`](http://eslint.org/docs/rules/one-var.html) jscs: [`disallowMultipleVarDecl`](http://jscs.info/rule/disallowMultipleVarDecl)

    > 为什么? 这样可以更容易定义一个新变量， 同时你永远不用担心切换`;`还是`,`。 还可以使用调试器单步执行每个声明，而不是跳过所有的声明。

    ```javascript
    // 糟糕
    const items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';

    // 糟糕
    // (compare to above, and try to spot the mistake)
    const items = getItems(),
        goSportsTeam = true;
        dragonball = 'z';

    // 好的
    const items = getItems();
    const goSportsTeam = true;
    const dragonball = 'z';
    ```

  <a name="variables--const-let-group"></a><a name="13.3"></a>
  
  - [13.3](#variables--const-let-group) 全部`const`一组，全部`let`一组。
    > 为什么? 当您稍后需要根据先前分配的变量分配一个变量时，这将很有帮助。

    ```javascript
    // 糟糕
    let i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // 不好
    let i;
    const items = getItems();
    let dragonball;
    const goSportsTeam = true;
    let len;

    // 好的
    const goSportsTeam = true;
    const items = getItems();
    let dragonball;
    let i;
    let length;
    ```

  <a name="variables--define-where-used"></a><a name="13.4"></a>
  
  - [13.4](#variables--define-where-used) 就近定义相关的变量

    > 为什么? `let` 和 `const` 是块级作用域而不是函数作用域。

    ```javascript
    // 糟糕 - 不必要的函数调用
    function checkName(hasName) {
      const name = getName();

      if (hasName === 'test') {
        return false;
      }

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }

    // 好的
    function checkName(hasName) {
      if (hasName === 'test') {
        return false;
      }

      const name = getName();

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }
    ```
  <a name="variables--no-chain-assignment"></a><a name="13.5"></a>
  
  - [13.5](#variables--no-chain-assignment) 不要链式定义变量

    > 为什么? 链式定义变量会隐性创造全局变量。
    
    ```javascript
    // 不好的
    (function example() {
      // JavaScript 是这样解析的：
      // let a = ( b = ( c = 1 ) );
      // 关键词 `let` 只作用于变量 a; 变量 b 和 c 成为了全局变量
      let a = b = c = 1;
    }());

    console.log(a); // undefined
    console.log(b); // 1
    console.log(c); // 1

    // 好的
    (function example() {
      let a = 1;
      let b = a;
      let c = a;
    }());

    console.log(a); // undefined
    console.log(b); // undefined
    console.log(c); // undefined

    // `const`也是同样的
    ```

  <a name="variables--unary-increment-decrement"></a><a name="13.6"></a>
  
  - [13.6](#variables--unary-increment-decrement) 避免使用一元操作符递增和递减 (++, --)。 eslint [`no-plusplus`](http://eslint.org/docs/rules/no-plusplus)

    > 为什么? Per the eslint documentation, 一元递增和递减陈述受自动分号的插入，导致递增或递减的值在应用沉默的错误。 更直观说明的代码含义如 `num += 1`，而不是 `num++` 和 `num--`。不允许一元递增和递减的陈述也防止您递增/递减值预前无意中也可使你的程序的意外行为。
    
    ```javascript
    // 糟糕

    const array = [1, 2, 3];
    let num = 1;
    num++;
    --num;

    let sum = 0;
    let truthyCount = 0;
    for (let i = 0; i < array.length; i++) {
      let value = array[i];
      sum += value;
      if (value) {
        truthyCount++;
      }
    }

    // 好的

    const array = [1, 2, 3];
    let num = 1;
    num += 1;
    num -= 1;

    const sum = array.reduce((a, b) => a + b, 0);
    const truthyCount = array.filter(Boolean).length;
    ```

**[⬆ 回到顶部](#table-of-contents)**


## 变量提升

  <a name="hoisting--about"></a><a name="14.1"></a>
  
  - [14.1](#hoisting--about) `var` 声明会被提升至声明时作用域的顶部。`const` 和 `let` 有一种新的概念 [暂时性死区(TDZ)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let#Temporal_dead_zone_and_errors_with_let)所以不会。这对理解[typeof 不安全](http://es-discourse.com/t/why-typeof-is-no-longer-safe/15)很重要。
    ```javascript
    // 我们知道这是无法工作的 (假设没有定义全局变量notDefined)
    function example() {
      console.log(notDefined); // => throws a ReferenceError
    }

    // 创建变量声明后
    // 由于变量提升参考变量可以工作
    // 注意: 赋值 `true` 不提升。
    function example() {
      console.log(declaredButNotAssigned); // => undefined
      var declaredButNotAssigned = true;
    }

    // 解释器正在提升变量
    // 声明到范围的顶部，
    // 这意味着我们的例子可以改写为:
    function example() {
      let declaredButNotAssigned;
      console.log(declaredButNotAssigned); // => undefined
      declaredButNotAssigned = true;
    }

    // 使用 const 和 let
    function example() {
      console.log(declaredButNotAssigned); // => throws a ReferenceError
      console.log(typeof declaredButNotAssigned); // => throws a ReferenceError
      const declaredButNotAssigned = true;
    }
    ```

  <a name="hoisting--anon-expressions"></a><a name="14.2"></a>
  
  - [14.2](#hoisting--anon-expressions) 匿名函数表达式的变量名提升，但不是函数赋值。

    ```javascript
    function example() {
      console.log(anonymous); // => undefined

      anonymous(); // => TypeError anonymous is not a function

      var anonymous = function () {
        console.log('anonymous function expression');
      };
    }
    ```

  <a name="hoisting--named-expresions"></a><a name="14.3"></a>
  
  - [14.3](#hoisting--named-expresions) 具名函数表达式的变量名提升， 而函数名和函数体不提升。

    ```javascript
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      superPower(); // => ReferenceError superPower is not defined

      var named = function superPower() {
        console.log('Flying');
      };
    }

    // 当函数名与变量名相同时也一样。
    function example() {
      console.log(named); // => undefined

      named(); // => TypeError named is not a function

      var named = function named() {
        console.log('named');
      };
    }
    ```

  <a name="hoisting--declarations"></a><a name="14.4"></a>
  
  - [14.4](#hoisting--declarations) 函数声明将提升函数名和函数体。

    ```javascript
    function example() {
      superPower(); // => Flying

      function superPower() {
        console.log('Flying');
      }
    }
    ```

  - 更多信息参考[Ben Cherry](http://www.adequatelygood.com/)的[JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting/)。

**[⬆ 回到顶部](#table-of-contents)**


## 比较运算符 & 相等

  <a name="comparison--eqeqeq"></a><a name="15.1"></a>
  
  - [15.1](#comparison--eqeqeq) 使用 `===` 和 `!==` ； `==` 和 `!=`. eslint: [`eqeqeq`](http://eslint.org/docs/rules/eqeqeq.html)

  <a name="comparison--if"></a><a name="15.2"></a>
  
  - [15.2](#comparison--if) 条件语法，如 `if` 通过默认方式 `ToBoolean` 计算表达式，并且总时遵循一下规则：

    + **Objects** 转换为 **true**
    + **Undefined** 转换为 **false**
    + **Null** 转换为 **false**
    + **Booleans** 转换为 **the value of the boolean**
    + **Numbers** 如果 **+0, -0, or NaN** 转换为 **false**，否则 **true**
    + **Strings** 空字符串`''`转换为 **false**，否则 **true**

    ```javascript
    if ([0] && []) {
      // true
      // 数组 (即使是空的) 也是一个对象, 对象将被转换为 true
    }
    ```

  <a name="comparison--shortcuts"></a><a name="15.3"></a>
  
  - [15.3](#comparison--shortcuts) 使用表达式转换， 但是明确比较字符串和数字。

    ```javascript
    // 不好
    if (isValid === true) {
      // ...
    }

    // 好
    if (isValid) {
      // ...
    }

    // 不好
    if (name) {
      // ...
    }

    // 好
    if (name !== '') {
      // ...
    }

    // 不好
    if (collection.length) {
      // ...
    }

    // 好
    if (collection.length > 0) {
      // ...
    }
    ```

  <a name="comparison--moreinfo"></a><a name="15.4"></a>
  
  - [15.4](#comparison--moreinfo) 更多信息参考 Angus Croll 的 [Truth Equality and JavaScript](https://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) 。

  <a name="comparison--switch-blocks"></a><a name="15.5"></a>
  
  - [15.5](#comparison--switch-blocks) `case` 和 `default` 使用花括号创建包含词法声明（例如：`let`， `const`， `function`， 和 `class`）的代码块。

    > 为什么? 在整个 `switch` 块中词法声明是可见的，但是只在匹配 `case` 初始化后才赋值。 当多个 `case` 定义相同的声明，就会出现问题。

    eslint rules: [`no-case-declarations`](http://eslint.org/docs/rules/no-case-declarations.html).

    ```javascript
    // 不好
    switch (foo) {
      case 1:
        let x = 1;
        break;
      case 2:
        const y = 2;
        break;
      case 3:
        function f() {
          // ...
        }
        break;
      default:
        class C {}
    }

    // 好的
    switch (foo) {
      case 1: {
        let x = 1;
        break;
      }
      case 2: {
        const y = 2;
        break;
      }
      case 3: {
        function f() {
          // ...
        }
        break;
      }
      case 4:
        bar();
        break;
      default: {
        class C {}
      }
    }
    ```

  <a name="comparison--nested-ternaries"></a><a name="15.6"></a>
  
  - [15.6](#comparison--nested-ternaries) 三元表达式不要嵌套并且一般写成单行。
    eslint rules: [`no-nested-ternary`](http://eslint.org/docs/rules/no-nested-ternary.html).

    ```javascript
    // 不好
    const foo = maybe1 > maybe2
      ? "bar"
      : value1 > value2 ? "baz" : null;

    // 稍微好点
    const maybeNull = value1 > value2 ? 'baz' : null;

    const foo = maybe1 > maybe2
      ? 'bar'
      : maybeNull;

    // 更好的选择
    const maybeNull = value1 > value2 ? 'baz' : null;

    const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
    ```

  <a name="comparison--unneeded-ternary"></a><a name="15.7"></a>
  
  - [15.7](#comparison--unneeded-ternary) 避免不必要的三元表达式。

    eslint rules: [`no-unneeded-ternary`](http://eslint.org/docs/rules/no-unneeded-ternary.html).

    ```javascript
    // 不太好
    const foo = a ? a : b;
    const bar = c ? true : false;
    const baz = c ? false : true;

    // 好的
    const foo = a || b;
    const bar = !!c;
    const baz = !c;
    ```

**[⬆ 回到顶部](#table-of-contents)**


## 代码块

  <a name="blocks--braces"></a><a name="16.1"></a>
  
  - [16.1](#blocks--braces) 在所有的多行代码块使用括号。

    ```javascript
    // 不好
    if (test)
      return false;

    // 好的
    if (test) return false;

    // 好的
    if (test) {
      return false;
    }

    // 坏
    function foo() { return false; }

    // 好
    function bar() {
      return false;
    }
    ```

  <a name="blocks--cuddled-elses"></a><a name="16.2"></a>
  
  - [16.2](#blocks--cuddled-elses) 如果你用到多行代码块 `if` 和 `esle` ，请将`else`放在 `if` 闭合括号的同一行。 eslint: [`brace-style`](http://eslint.org/docs/rules/brace-style.html) jscs:  [`disallowNewlineBeforeBlockStatements`](http://jscs.info/rule/disallowNewlineBeforeBlockStatements)

    ```javascript
    // 坏
    if (test) {
      thing1();
      thing2();
    }
    else {
      thing3();
    }

    // 好
    if (test) {
      thing1();
      thing2();
    } else {
      thing3();
    }
    ```


**[⬆ 回到顶部](#table-of-contents)**


## 控制语句

  <a name="control-statements"></a>
  
  - [17.1](#control-statements) 如果你的控制语句（`if`，`while`等。）太长或者超过单行最大长度，每个分组条件都应该单独一行。逻辑运算符是否应该开始或结束行取决于你。

    ```javascript
    // 不好
    if ((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
      thing1();
    }

    // 不好
    if (foo === 123 &&
      bar === 'abc') {
      thing1();
    }

    // 不好
    if (foo === 123
      && bar === 'abc') {
      thing1();
    }

    // 好
    if (
      (foo === 123 || bar === "abc") &&
      doesItLookGoodWhenItBecomesThatLong() &&
      isThisReallyHappening()
    ) {
      thing1();
    }

    // 好
    if (foo === 123 && bar === 'abc') {
      thing1();
    }

    // 好
    if (
      foo === 123 &&
      bar === 'abc'
    ) {
      thing1();
    }

    // 好
    if (
      foo === 123
      && bar === 'abc'
    ) {
      thing1();
    }
    ```


**[⬆ 回到顶部](#table-of-contents)**


## 注释

  <a name="comments--multiline"></a><a name="17.1"></a>
  
  - [18.1](#comments--multiline) 对行注释使用 `/** ... */`。

    ```javascript
    // 不好
    // make() returns a new element
    // based on the passed in tag name
    //
    // @param {String} tag
    // @return {Element} element
    function make(tag) {

      // ...

      return element;
    }

    // 好的
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }
    ```

  <a name="comments--singleline"></a><a name="17.2"></a>
  
  - [18.2](#comments--singleline) 单行注释使用 `//` 。将单行注释放在上方。 注释行上方添加一个空白行，除非是在代码块的第一行。

    ```javascript
    // 坏
    const active = true;  // is current tab

    // 好
    // is current tab
    const active = true;

    // 坏
    function getType() {
      console.log('fetching type...');
      // set the default type to 'no type'
      const type = this.type || 'no type';

      return type;
    }

    // 好
    function getType() {
      console.log('fetching type...');

      // type的默认值为'no type'
      const type = this.type || 'no type';

      return type;
    }

    // 同样好的
    function getType() {
      // type的默认值为'no type'
      const type = this.type || 'no type';

      return type;
    }
    ```

  - [18.3](#comments--spaces) 注释文字开始前的添加空格可以提高可读性。 eslint: [`spaced-comment`](http://eslint.org/docs/rules/spaced-comment)

    ```javascript
    // 坏
    //is current tab
    const active = true;

    // 好
    // is current tab
    const active = true;

    // 坏
    /**
     *make() returns a new element
     *based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }

    // 好
    /**
     * make() returns a new element
     * based on the passed-in tag name
     */
    function make(tag) {

      // ...

      return element;
    }
    ```

  <a name="comments--actionitems"></a><a name="17.3"></a>
  
  - [18.4](#comments--actionitems) 如果你指出一个需要重新审视的问题，添加 `FIXME` 前缀 帮助其他的开发者快速理解。如果这一个需要解决方案的问题，添加 `TODO` 前缀。 这些不同于常规评论，因为它们是可操作的。 使用 `FIXME: -- 需要解决` or `TODO: -- 需要实现`.

  <a name="comments--fixme"></a><a name="17.4"></a>
  
  - [18.5](#comments--fixme) 使用 `// FIXME:` 注释一个问题。

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // FIXME: 不应该使用全局变量
        total = 0;
      }
    }
    ```

  <a name="comments--todo"></a><a name="17.5"></a>
  
  - [18.6](#comments--todo) 使用 `// TODO:` 注释一个待解决问题。

    ```javascript
    class Calculator extends Abacus {
      constructor() {
        super();

        // TODO: total 需要变成一个可配置的选项参数
        this.total = 0;
      }
    }
    ```

**[⬆ 回到顶部](#table-of-contents)**


## 空白

  <a name="whitespace--spaces"></a><a name="18.1"></a>
  
  - [19.1](#whitespace--spaces) 使用2个空格的soft tabs (空格字符)。 eslint: [`indent`](http://eslint.org/docs/rules/indent.html) jscs: [`validateIndentation`](http://jscs.info/rule/validateIndentation)

    ```javascript
    // 不好的
    function foo() {
    ∙∙∙∙let name;
    }

    // 不好的
    function bar() {
    ∙let name;
    }

    // 好的
    function baz() {
    ∙∙let name;
    }
    ```

  <a name="whitespace--before-blocks"></a><a name="18.2"></a>
  
  - [19.2](#whitespace--before-blocks) 在开始括号的前面添加一个空格。 eslint: [`space-before-blocks`](http://eslint.org/docs/rules/space-before-blocks.html) jscs: [`requireSpaceBeforeBlockStatements`](http://jscs.info/rule/requireSpaceBeforeBlockStatements)

    ```javascript
    // 不好的
    function test(){
      console.log('test');
    }

    // 好的
    function test() {
      console.log('test');
    }

    // 不好
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });

    // 好
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });
    ```

  <a name="whitespace--around-keywords"></a><a name="18.3"></a>
  
  - [19.3](#whitespace--around-keywords) 在控制语句的前括号中放置1个空格 (`if`, `while`等。)。在函数调用和声明之间没有参数列表和函数名之间的空格。 eslint: [`keyword-spacing`](http://eslint.org/docs/rules/keyword-spacing.html) jscs: [`requireSpaceAfterKeywords`](http://jscs.info/rule/requireSpaceAfterKeywords)

    ```javascript
    // 不好
    if(isJedi) {
      fight ();
    }

    // 好
    if (isJedi) {
      fight();
    }

    // 不好
    function fight () {
      console.log ('Swooosh!');
    }

    // 好
    function fight() {
      console.log('Swooosh!');
    }
    ```

  <a name="whitespace--infix-ops"></a><a name="18.4"></a>
  
  - [19.4](#whitespace--infix-ops) 运算符添加空格。 eslint: [`space-infix-ops`](http://eslint.org/docs/rules/space-infix-ops.html) jscs: [`requireSpaceBeforeBinaryOperators`](http://jscs.info/rule/requireSpaceBeforeBinaryOperators), [`requireSpaceAfterBinaryOperators`](http://jscs.info/rule/requireSpaceAfterBinaryOperators)

    ```javascript
    // 不好
    const x=y+5;

    // 好的
    const x = y + 5;
    ```

  <a name="whitespace--newline-at-end"></a><a name="18.5"></a>
  
  - [19.5](#whitespace--newline-at-end) 文件结尾添加一个换行符。 eslint: [`eol-last`](https://github.com/eslint/eslint/blob/master/docs/rules/eol-last.md)

    ```javascript
    // 不好
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;
    ```

    ```javascript
    // 不好
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;↵
    ↵
    ```

    ```javascript
    // 好
    import { es6 } from './AirbnbStyleGuide';
      // ...
    export default es6;↵
    ```

  <a name="whitespace--chains"></a><a name="18.6"></a>
  
  - [19.6](#whitespace--chains)在使用长方法链时使用缩进（超过2个方法链）。 点前置， 它强调该行是方法调用，而不是新语句。 eslint: [`newline-per-chained-call`](http://eslint.org/docs/rules/newline-per-chained-call) [`no-whitespace-before-property`](http://eslint.org/docs/rules/no-whitespace-before-property)

    ```javascript
    // 糟糕
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // 糟糕
    $('#items').
      find('.selected').
        highlight().
        end().
      find('.open').
        updateCount();

    // 好
    $('#items')
      .find('.selected')
        .highlight()
        .end()
      .find('.open')
        .updateCount();

    // 糟糕
    const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
        .attr('width', (radius + margin) * 2).append('svg:g')
        .attr('transform', `translate(${radius + margin},${radius + margin})`)
        .call(tron.led);

    // 好
    const leds = stage.selectAll('.led')
        .data(data)
      .enter().append('svg:svg')
        .classed('led', true)
        .attr('width', (radius + margin) * 2)
      .append('svg:g')
        .attr('transform', `translate(${radius + margin},${radius + margin})`)
        .call(tron.led);

    // 好
    const leds = stage.selectAll('.led').data(data);
    ```

  <a name="whitespace--after-blocks"></a><a name="18.7"></a>
  
  - [19.7](#whitespace--after-blocks) 在空白块和下一个语句之前留下空白行。 jscs: [`requirePaddingNewLinesAfterBlocks`](http://jscs.info/rule/requirePaddingNewLinesAfterBlocks)

    ```javascript
    // 不好
    if (foo) {
      return bar;
    }
    return baz;

    // 好
    if (foo) {
      return bar;
    }

    return baz;

    // 不好
    const obj = {
      foo() {
      },
      bar() {
      },
    };
    return obj;

    // 好
    const obj = {
      foo() {
      },

      bar() {
      },
    };

    return obj;

    // 不好
    const arr = [
      function foo() {
      },
      function bar() {
      },
    ];
    return arr;

    // 好
    const arr = [
      function foo() {
      },

      function bar() {
      },
    ];

    return arr;
    ```

  <a name="whitespace--padded-blocks"></a><a name="18.8"></a>
  
  - [19.8](#whitespace--padded-blocks) 不要在代码块头部添加空白行。 eslint: [`padded-blocks`](http://eslint.org/docs/rules/padded-blocks.html) jscs:  [`disallowPaddingNewlinesInBlocks`](http://jscs.info/rule/disallowPaddingNewlinesInBlocks)

    ```javascript
    // 不好
    function bar() {

      console.log(foo);

    }

    // 同样不好
    if (baz) {

      console.log(qux);
    } else {
      console.log(foo);

    }

    // 好的
    function bar() {
      console.log(foo);
    }

    // 好的
    if (baz) {
      console.log(qux);
    } else {
      console.log(foo);
    }
    ```

  <a name="whitespace--in-parens"></a><a name="18.9"></a>
  
  - [19.9](#whitespace--in-parens) 在圆括号内边添加空格。 eslint: [`space-in-parens`](http://eslint.org/docs/rules/space-in-parens.html) jscs: [`disallowSpacesInsideParentheses`](http://jscs.info/rule/disallowSpacesInsideParentheses)

    ```javascript
    // 坏
    function bar( foo ) {
      return foo;
    }

    // 好
    function bar(foo) {
      return foo;
    }

    // 坏
    if ( foo ) {
      console.log(foo);
    }

    // 好
    if (foo) {
      console.log(foo);
    }
    ```

  <a name="whitespace--in-brackets"></a><a name="18.10"></a>
  
  - [19.10](#whitespace--in-brackets) 在括号内边添加空格。 eslint: [`array-bracket-spacing`](http://eslint.org/docs/rules/array-bracket-spacing.html) jscs: [`disallowSpacesInsideArrayBrackets`](http://jscs.info/rule/disallowSpacesInsideArrayBrackets)

    ```javascript
    // 坏
    const foo = [ 1, 2, 3 ];
    console.log(foo[ 0 ]);

    // 好
    const foo = [1, 2, 3];
    console.log(foo[0]);
    ```

  <a name="whitespace--in-braces"></a><a name="18.11"></a>
  
  - [19.11](#whitespace--in-braces) 大括号内边添加空格。eslint: [`object-curly-spacing`](http://eslint.org/docs/rules/object-curly-spacing.html) jscs: [`requireSpacesInsideObjectBrackets`](http://jscs.info/rule/requireSpacesInsideObjectBrackets)

    ```javascript
    // 坏
    const foo = {clark: 'kent'};

    // 好
    const foo = { clark: 'kent' };
    ```

  <a name="whitespace--max-len"></a><a name="18.12"></a>
  
  - [19.12](#whitespace--max-len) 避免一行过长超过100个字符（包括空格）。 注意: 长字符串免除当前规则，不能打破字符串的[规则](#strings--line-length) eslint: [`max-len`](http://eslint.org/docs/rules/max-len.html) jscs: [`maximumLineLength`](http://jscs.info/rule/maximumLineLength)

    > 为什么? 保证可读性和可维护性。

    ```javascript
    // 坏
    const foo = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

    // 坏
    $.ajax({ method: 'POST', url: 'https://airbnb.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));

    // 好
    const foo = jsonData
      && jsonData.foo
      && jsonData.foo.bar
      && jsonData.foo.bar.baz
      && jsonData.foo.bar.baz.quux
      && jsonData.foo.bar.baz.quux.xyzzy;

    // 好
    $.ajax({
      method: 'POST',
      url: 'https://airbnb.com/',
      data: { name: 'John' },
    })
      .done(() => console.log('Congratulations!'))
      .fail(() => console.log('You have failed this city.'));
    ```

**[⬆ 回到顶部](#table-of-contents)**

## 逗号

<a name="commas--leading-trailing"></a><a name="19.1"></a>

  - [20.1](#commas--leading-trailing) 逗号前置？ **不。** eslint: [`comma-style`](http://eslint.org/docs/rules/comma-style.html) jscs: [`requireCommaBeforeLineBreak`](http://jscs.info/rule/requireCommaBeforeLineBreak)

    ```javascript
    // 不好
    const story = [
        once
      , upon
      , aTime
    ];

    // 好
    const story = [
      once,
      upon,
      aTime,
    ];

    // 不好
    const hero = {
        firstName: 'Ada'
      , lastName: 'Lovelace'
      , birthYear: 1815
      , superPower: 'computers'
    };

    // 好
    const hero = {
      firstName: 'Ada',
      lastName: 'Lovelace',
      birthYear: 1815,
      superPower: 'computers',
    };
    ```

  <a name="commas--dangling"></a><a name="19.2"></a>
  
  - [20.2](#commas--dangling) 最后也添加都好？ **是的。** eslint: [`comma-dangle`](http://eslint.org/docs/rules/comma-dangle.html) jscs: [`requireTrailingComma`](http://jscs.info/rule/requireTrailingComma)

    > 为什么? git的diff记录更清爽。 同时，你不必担心后面的[逗号的问题](https://github.com/airbnb/javascript/blob/es5-deprecated/es5/README.md#commas)在传统的浏览器，因为类似Babel这样的转译器将会在转译的同时删除多余的逗号。

    ```diff
    // 不好的 - git diff 没有尾随逗号
    const hero = {
         firstName: 'Florence',
    -    lastName: 'Nightingale'
    +    lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing']
    };

    // good - git diff 有尾随逗号
    const hero = {
         firstName: 'Florence',
         lastName: 'Nightingale',
    +    inventorOf: ['coxcomb chart', 'modern nursing'],
    };
    ```

    ```javascript
    // 不好
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully'
    };

    const heroes = [
      'Batman',
      'Superman'
    ];

    // 好
    const hero = {
      firstName: 'Dana',
      lastName: 'Scully',
    };

    const heroes = [
      'Batman',
      'Superman',
    ];

    // 不好
    function createHero(
      firstName,
      lastName,
      inventorOf
    ) {
      // does nothing
    }

    // 好
    function createHero(
      firstName,
      lastName,
      inventorOf,
    ) {
      // does nothing
    }

    // 好 (注意：在展开对象后面不能出现逗号)
    function createHero(
      firstName,
      lastName,
      inventorOf,
      ...heroArgs
    ) {
      // does nothing
    }

    // 不好
    createHero(
      firstName,
      lastName,
      inventorOf
    );

    // 好
    createHero(
      firstName,
      lastName,
      inventorOf,
    );

    // 好 (注意：在展开对象后面不能出现逗号)
    createHero(
      firstName,
      lastName,
      inventorOf,
      ...heroArgs
    );
    ```

**[⬆ 回到顶部](#table-of-contents)**


## 分号

  <a name="semicolons--required"></a><a name="20.1"></a>
  
  - [21.1](#semicolons--required) **需要。** eslint: [`semi`](http://eslint.org/docs/rules/semi.html) jscs: [`requireSemicolons`](http://jscs.info/rule/requireSemicolons)

    ```javascript
    // 不好
    (function () {
      const name = 'Skywalker'
      return name
    })()

    // 好
    (function () {
      const name = 'Skywalker';
      return name;
    }());

    // 好, but legacy (防止两个立即调用的函数表达式合并时被当成参数)
    ;((() => {
      const name = 'Skywalker';
      return name;
    })());
    ```

    [查看更多](https://stackoverflow.com/questions/7365172/semicolon-before-self-invoking-function/7365214%237365214).

**[⬆ 回到顶部](#table-of-contents)**


## 类型转换

  <a name="coercion--explicit"></a><a name="21.1"></a>
  
  - [22.1](#coercion--explicit) 在语句开始时执行类型转换

  <a name="coercion--strings"></a><a name="21.2"></a>
  
  - [22.2](#coercion--strings)  字符类型:

    ```javascript
    // => this.reviewScore = 9;

    // 不好
    const totalScore = this.reviewScore + ''; // 调用 this.reviewScore.valueOf()

    // 不好
    const totalScore = this.reviewScore.toString(); // 不一定返回字符串

    // 好
    const totalScore = String(this.reviewScore);
    ```

  <a name="coercion--numbers"></a><a name="21.3"></a>
  
  - [22.3](#coercion--numbers) 数字类型: 使用 `Number` 和 总是带上转换基数的 `parseInt`。eslint: [`radix`](http://eslint.org/docs/rules/radix)

    ```javascript
    const inputValue = '4';

    // 不好
    const val = new Number(inputValue);

    // 不好
    const val = +inputValue;

    // 不好
    const val = inputValue >> 0;

    // 不好
    const val = parseInt(inputValue);

    // 好
    const val = Number(inputValue);

    // 好
    const val = parseInt(inputValue, 10);
    ```

  <a name="coercion--comment-deviations"></a><a name="21.4"></a>
  
  - [22.4](#coercion--comment-deviations) 如果因为 `parseInt` 的 [性能问题](https://jsperf.com/coercion-vs-casting/3)不能满足你的需求，请留下注释说明原因。

    ```javascript
    // 好
    /**
     * parseInt was the reason my code was slow.
     * Bitshifting the String to coerce it to a
     * Number made it a lot faster.
     */
    const val = inputValue >> 0;
    ```

  <a name="coercion--bitwise"></a><a name="21.5"></a>
  
  - [22.5](#coercion--bitwise) **Note:** 小心位操作。数字会被当成 [64-bit values](https://es5.github.io/#x4.3.19)， 但是位操作运算符总是返回 32 位的整数 ([source](https://es5.github.io/#x11.7))。位操作处理大于 32 位的整数值时还会导致意料之外的行为。 [Discussion](https://github.com/airbnb/javascript/issues/109). 最大的32位整数是 2,147,483,647:

    ```javascript
    2147483647 >> 0; // => 2147483647
    2147483648 >> 0; // => -2147483648
    2147483649 >> 0; // => -2147483647
    ```

  <a name="coercion--booleans"></a><a name="21.6"></a>
  
  - [22.6](#coercion--booleans) 布尔类型:

    ```javascript
    const age = 0;

    // 不好
    const hasAge = new Boolean(age);

    // 好
    const hasAge = Boolean(age);

    // 更好
    const hasAge = !!age;
    ```

**[⬆ 回到顶部](#table-of-contents)**


## 命名规则

  <a name="naming--descriptive"></a><a name="22.1"></a>
  
  - [23.1](#naming--descriptive) 避免单字母名。描述你的命名。eslint: [`id-length`](http://eslint.org/docs/rules/id-length)

    ```javascript
    // 不好
    function q() {
      // ...
    }

    // 好
    function query() {
      // ...
    }
    ```

  <a name="naming--camelCase"></a><a name="22.2"></a>
  
  - [23.2](#naming--camelCase) 使用驼峰命名法命名对象、函数、实例。 eslint: [`camelcase`](http://eslint.org/docs/rules/camelcase.html) jscs: [`requireCamelCaseOrUpperCaseIdentifiers`](http://jscs.info/rule/requireCamelCaseOrUpperCaseIdentifiers)

    ```javascript
    // 不好
    const OBJEcttsssss = {};
    const this_is_my_object = {};
    function c() {}

    // 好的
    const thisIsMyObject = {};
    function thisIsMyFunction() {}
    ```

  <a name="naming--PascalCase"></a><a name="22.3"></a>

  - [23.3](#naming--PascalCase) 命名构造函数或类只使用帕斯卡拼写法。 eslint: [`new-cap`](http://eslint.org/docs/rules/new-cap.html) jscs: [`requireCapitalizedConstructors`](http://jscs.info/rule/requireCapitalizedConstructors)

    ```javascript
    // 坏
    function user(options) {
      this.name = options.name;
    }

    const bad = new user({
      name: 'nope',
    });

    // 好
    class User {
      constructor(options) {
        this.name = options.name;
      }
    }

    const good = new User({
      name: 'yup',
    });
    ```

  <a name="naming--leading-underscore"></a><a name="22.4"></a>
  
  - [23.4](#naming--leading-underscore) 前后不适用下划线。 eslint: [`no-underscore-dangle`](http://eslint.org/docs/rules/no-underscore-dangle.html) jscs: [`disallowDanglingUnderscores`](http://jscs.info/rule/disallowDanglingUnderscores)

    > 为什么? 虽然大家约定下划线代表“私有”，但事实上它们仍然是公有的属性和方法。这个约定导致开发人员错误的理解是不会改变的，并且测试不是必需的。tl;dr: 如果你想要一个“私有”，它必须是不能显著存在的。

    ```javascript
    // 不好
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';
    this._firstName = 'Panda';

    // 好
    this.firstName = 'Panda';
    ```

  <a name="naming--self-this"></a><a name="22.5"></a>
  
  - [23.5](#naming--self-this) 不用缓存 `this`。使用箭头函数或[Function#bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)。 jscs: [`disallowNodeTypes`](http://jscs.info/rule/disallowNodeTypes)

    ```javascript
    // 坏
    function foo() {
      const self = this;
      return function () {
        console.log(self);
      };
    }

    // 坏
    function foo() {
      const that = this;
      return function () {
        console.log(that);
      };
    }

    // 好
    function foo() {
      return () => {
        console.log(this);
      };
    }
    ```

  <a name="naming--filename-matches-export"></a><a name="22.6"></a>
  
  - [23.6](#naming--filename-matches-export) 文件名应与其默认导出名称完全匹配。

    ```javascript
    // 文件 1 内容
    class CheckBox {
      // ...
    }
    export default CheckBox;

    // 文件 2 内容
    export default function fortyTwo() { return 42; }

    // 文件 3 内容
    export default function insideDirectory() {}

    // 在其他文件中
    // 坏
    import CheckBox from './checkBox'; // PascalCase import/export, camelCase filename
    import FortyTwo from './FortyTwo'; // PascalCase import/filename, camelCase export
    import InsideDirectory from './InsideDirectory'; // PascalCase import/filename, camelCase export

    // 坏
    import CheckBox from './check_box'; // PascalCase import/export, snake_case filename
    import forty_two from './forty_two'; // snake_case import/filename, camelCase export
    import inside_directory from './inside_directory'; // snake_case import, camelCase export
    import index from './inside_directory/index'; // requiring the index file explicitly
    import insideDirectory from './insideDirectory/index'; // requiring the index file explicitly

    // 好
    import CheckBox from './CheckBox'; // PascalCase export/import/filename
    import fortyTwo from './fortyTwo'; // camelCase export/import/filename
    import insideDirectory from './insideDirectory'; // camelCase export/import/directory name/implicit "index"
    // ^ supports both insideDirectory.js and insideDirectory/index.js
    ```

  <a name="naming--camelCase-default-export"></a><a name="22.7"></a>
  
  - [23.7](#naming--camelCase-default-export) 模块默认导出函数时使用驼峰命名法，并且模块名字相同。

    ```javascript
    function makeStyleGuide() {
      // ...
    }

    export default makeStyleGuide;
    ```

  <a name="naming--PascalCase-singleton"></a><a name="22.8"></a>
  
  - [23.8](#naming--PascalCase-singleton) 模块导出a constructor / class / singleton / function library / bare object使用帕斯卡拼写法。

    ```javascript
    const AirbnbStyleGuide = {
      es6: {
      },
    };

    export default AirbnbStyleGuide;
    ```

  <a name="naming--Acronyms-and-Initialisms"></a>
  
  - [23.9](#naming--Acronyms-and-Initialisms) 缩略词应全部大写或小写。

    > 为什么? 名字是为了可读性，不是为了安抚电脑算法。

    ```javascript
    // 坏
    import SmsContainer from './containers/SmsContainer';

    // 坏
    const HttpRequests = [
      // ...
    ];

    // 好
    import SMSContainer from './containers/SMSContainer';

    // 好
    const HTTPRequests = [
      // ...
    ];

    // 更好
    import TextMessageContainer from './containers/TextMessageContainer';

    // 更好
    const Requests = [
      // ...
    ];
    ```

**[⬆ 返回顶部](#table-of-contents)**


## 访问器

  <a name="accessors--not-required"></a><a name="23.1"></a>
  
  - [24.1](#accessors--not-required) 属性的访问器函数不是必须的。

  <a name="accessors--no-getters-setters"></a><a name="23.2"></a>
  
  - [24.2](#accessors--no-getters-setters) JavaScript不使用相同的getter和setter，这会引起意想不到的副作用，很难测试、维护等的原因。相反的， 如果你需要定义访问器函数，请使用 getVal() 和 setVal('hello').

    ```javascript
    // 坏
    class Dragon {
      get age() {
        // ...
      }

      set age(value) {
        // ...
      }
    }

    // 好
    class Dragon {
      getAge() {
        // ...
      }

      setAge(value) {
        // ...
      }
    }
    ```

  <a name="accessors--boolean-prefix"></a><a name="23.3"></a>
  
  - [24.3](#accessors--boolean-prefix) 如果属性／方法的结果是布尔值，使用 `isVal()` 或 `hasVal()`.

    ```javascript
    // 坏
    if (!dragon.age()) {
      return false;
    }

    // 好
    if (!dragon.hasAge()) {
      return false;
    }
    ```

  <a name="accessors--consistent"></a><a name="23.4"></a>
  
  - [24.4](#accessors--consistent) 创建 get() 和 set() 函数是可以的，但要保持一致。

    ```javascript
    class Jedi {
      constructor(options = {}) {
        const lightsaber = options.lightsaber || 'blue';
        this.set('lightsaber', lightsaber);
      }

      set(key, val) {
        this[key] = val;
      }

      get(key) {
        return this[key];
      }
    }
    ```

**[⬆ 回到顶部](#table-of-contents)**


## 事件

  <a name="events--hash"></a><a name="24.1"></a>
  
  - [25.1](#events--hash) 当事件需要传递额外数据时，(无论是 DOM 事件还是私有事件)， 传递一个散列而不是原始值。 这允许后面的开发者添加更多参数的同时，不需要更新事件的每一个回调函数。 举个例子, 不好的:

    ```javascript
    // bad
    $(this).trigger('listingUpdated', listing.id);

    // ...

    $(this).on('listingUpdated', (e, listingId) => {
      // do something with listingId
    });
    ```

    好的:

    ```javascript
    // good
    $(this).trigger('listingUpdated', { listingId: listing.id });

    // ...

    $(this).on('listingUpdated', (e, data) => {
      // do something with data.listingId
    });
    ```

  **[⬆ 回到顶部](#table-of-contents)**


## jQuery

  <a name="jquery--dollar-prefix"></a><a name="25.1"></a>
  - [26.1](#jquery--dollar-prefix) Prefix jQuery object variables with a `$`. jscs: [`requireDollarBeforejQueryAssignment`](http://jscs.info/rule/requireDollarBeforejQueryAssignment)

    ```javascript
    // bad
    const sidebar = $('.sidebar');

    // good
    const $sidebar = $('.sidebar');

    // good
    const $sidebarBtn = $('.sidebar-btn');
    ```

  <a name="jquery--cache"></a><a name="25.2"></a>
  - [26.2](#jquery--cache) Cache jQuery lookups.

    ```javascript
    // bad
    function setSidebar() {
      $('.sidebar').hide();

      // ...

      $('.sidebar').css({
        'background-color': 'pink',
      });
    }

    // good
    function setSidebar() {
      const $sidebar = $('.sidebar');
      $sidebar.hide();

      // ...

      $sidebar.css({
        'background-color': 'pink',
      });
    }
    ```

  <a name="jquery--queries"></a><a name="25.3"></a>
  - [26.3](#jquery--queries) For DOM queries use Cascading `$('.sidebar ul')` or parent > child `$('.sidebar > ul')`. [jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)

  <a name="jquery--find"></a><a name="25.4"></a>
  - [26.4](#jquery--find) Use `find` with scoped jQuery object queries.

    ```javascript
    // bad
    $('ul', '.sidebar').hide();

    // bad
    $('.sidebar').find('ul').hide();

    // good
    $('.sidebar ul').hide();

    // good
    $('.sidebar > ul').hide();

    // good
    $sidebar.find('ul').hide();
    ```

**[⬆ back to top](#table-of-contents)**


## ECMAScript 5 Compatibility

  <a name="es5-compat--kangax"></a><a name="26.1"></a>
  - [27.1](#es5-compat--kangax) Refer to [Kangax](https://twitter.com/kangax/)'s ES5 [compatibility table](https://kangax.github.io/es5-compat-table/).

**[⬆ back to top](#table-of-contents)**

<a name="ecmascript-6-styles"></a>
## ECMAScript 6+ (ES 2015+) Styles

  <a name="es6-styles"></a><a name="27.1"></a>
  - [28.1](#es6-styles) This is a collection of links to the various ES6 features.

1. [Arrow Functions](#arrow-functions)
1. [Classes](#classes--constructors)
1. [Object Shorthand](#es6-object-shorthand)
1. [Object Concise](#es6-object-concise)
1. [Object Computed Properties](#es6-computed-properties)
1. [Template Strings](#es6-template-literals)
1. [Destructuring](#destructuring)
1. [Default Parameters](#es6-default-parameters)
1. [Rest](#es6-rest)
1. [Array Spreads](#es6-array-spreads)
1. [Let and Const](#references)
1. [Iterators and Generators](#iterators-and-generators)
1. [Modules](#modules)

  <a name="tc39-proposals"></a>
  - [28.2](#tc39-proposals) Do not use [TC39 proposals](https://github.com/tc39/proposals) that have not reached stage 3.

    > Why? [They are not finalized](https://tc39.github.io/process-document/), and they are subject to change or to be withdrawn entirely. We want to use JavaScript, and proposals are not JavaScript yet.

**[⬆ back to top](#table-of-contents)**

## Testing

  <a name="testing--yup"></a><a name="28.1"></a>
  - [29.1](#testing--yup) **Yup.**

    ```javascript
    function foo() {
      return true;
    }
    ```

  <a name="testing--for-real"></a><a name="28.2"></a>
  - [29.2](#testing--for-real) **No, but seriously**:
   - Whichever testing framework you use, you should be writing tests!
   - Strive to write many small pure functions, and minimize where mutations occur.
   - Be cautious about stubs and mocks - they can make your tests more brittle.
   - We primarily use [`mocha`](https://www.npmjs.com/package/mocha) at Airbnb. [`tape`](https://www.npmjs.com/package/tape) is also used occasionally for small, separate modules.
   - 100% test coverage is a good goal to strive for, even if it's not always practical to reach it.
   - Whenever you fix a bug, _write a regression test_. A bug fixed without a regression test is almost certainly going to break again in the future.

**[⬆ back to top](#table-of-contents)**


## Performance

  - [On Layout & Web Performance](https://www.kellegous.com/j/2013/01/26/layout-performance/)
  - [String vs Array Concat](https://jsperf.com/string-vs-array-concat/2)
  - [Try/Catch Cost In a Loop](https://jsperf.com/try-catch-in-loop-cost)
  - [Bang Function](https://jsperf.com/bang-function)
  - [jQuery Find vs Context, Selector](https://jsperf.com/jquery-find-vs-context-sel/13)
  - [innerHTML vs textContent for script text](https://jsperf.com/innerhtml-vs-textcontent-for-script-text)
  - [Long String Concatenation](https://jsperf.com/ya-string-concat)
  - [Are Javascript functions like `map()`, `reduce()`, and `filter()` optimized for traversing arrays?](https://www.quora.com/JavaScript-programming-language-Are-Javascript-functions-like-map-reduce-and-filter-already-optimized-for-traversing-array/answer/Quildreen-Motta)
  - Loading...

**[⬆ back to top](#table-of-contents)**


## Resources

**Learning ES6**

  - [Draft ECMA 2015 (ES6) Spec](https://people.mozilla.org/~jorendorff/es6-draft.html)
  - [ExploringJS](http://exploringjs.com/)
  - [ES6 Compatibility Table](https://kangax.github.io/compat-table/es6/)
  - [Comprehensive Overview of ES6 Features](http://es6-features.org/)

**Read This**

  - [Standard ECMA-262](http://www.ecma-international.org/ecma-262/6.0/index.html)

**Tools**

  - Code Style Linters
    + [ESlint](http://eslint.org/) - [Airbnb Style .eslintrc](https://github.com/airbnb/javascript/blob/master/linters/.eslintrc)
    + [JSHint](http://jshint.com/) - [Airbnb Style .jshintrc](https://github.com/airbnb/javascript/blob/master/linters/.jshintrc)
    + [JSCS](https://github.com/jscs-dev/node-jscs) - [Airbnb Style Preset](https://github.com/jscs-dev/node-jscs/blob/master/presets/airbnb.json) (Deprecated, please use [ESlint](https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb-base))
  - Neutrino preset - [neutrino-preset-airbnb-base](https://neutrino.js.org/presets/neutrino-preset-airbnb-base/)

**Other Style Guides**

  - [Google JavaScript Style Guide](https://google.github.io/styleguide/javascriptguide.xml)
  - [jQuery Core Style Guidelines](https://contribute.jquery.org/style-guide/js/)
  - [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwaldron/idiomatic.js)

**Other Styles**

  - [Naming this in nested functions](https://gist.github.com/cjohansen/4135065) - Christian Johansen
  - [Conditional Callbacks](https://github.com/airbnb/javascript/issues/52) - Ross Allen
  - [Popular JavaScript Coding Conventions on GitHub](http://sideeffect.kr/popularconvention/#javascript) - JeongHoon Byun
  - [Multiple var statements in JavaScript, not superfluous](http://benalman.com/news/2012/05/multiple-var-statements-javascript/) - Ben Alman

**Further Reading**

  - [Understanding JavaScript Closures](https://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/) - Angus Croll
  - [Basic JavaScript for the impatient programmer](http://www.2ality.com/2013/06/basic-javascript.html) - Dr. Axel Rauschmayer
  - [You Might Not Need jQuery](http://youmightnotneedjquery.com/) - Zack Bloom & Adam Schwartz
  - [ES6 Features](https://github.com/lukehoban/es6features) - Luke Hoban
  - [Frontend Guidelines](https://github.com/bendc/frontend-guidelines) - Benjamin De Cock

**Books**

  - [JavaScript: The Good Parts](https://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742) - Douglas Crockford
  - [JavaScript Patterns](https://www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752) - Stoyan Stefanov
  - [Pro JavaScript Design Patterns](https://www.amazon.com/JavaScript-Design-Patterns-Recipes-Problem-Solution/dp/159059908X)  - Ross Harmes and Dustin Diaz
  - [High Performance Web Sites: Essential Knowledge for Front-End Engineers](https://www.amazon.com/High-Performance-Web-Sites-Essential/dp/0596529309) - Steve Souders
  - [Maintainable JavaScript](https://www.amazon.com/Maintainable-JavaScript-Nicholas-C-Zakas/dp/1449327680) - Nicholas C. Zakas
  - [JavaScript Web Applications](https://www.amazon.com/JavaScript-Web-Applications-Alex-MacCaw/dp/144930351X) - Alex MacCaw
  - [Pro JavaScript Techniques](https://www.amazon.com/Pro-JavaScript-Techniques-John-Resig/dp/1590597273) - John Resig
  - [Smashing Node.js: JavaScript Everywhere](https://www.amazon.com/Smashing-Node-js-JavaScript-Everywhere-Magazine/dp/1119962595) - Guillermo Rauch
  - [Secrets of the JavaScript Ninja](https://www.amazon.com/Secrets-JavaScript-Ninja-John-Resig/dp/193398869X) - John Resig and Bear Bibeault
  - [Human JavaScript](http://humanjavascript.com/) - Henrik Joreteg
  - [Superhero.js](http://superherojs.com/) - Kim Joar Bekkelund, Mads Mobæk, & Olav Bjorkoy
  - [JSBooks](http://jsbooks.revolunet.com/) - Julien Bouquillon
  - [Third Party JavaScript](https://www.manning.com/books/third-party-javascript) - Ben Vinegar and Anton Kovalyov
  - [Effective JavaScript: 68 Specific Ways to Harness the Power of JavaScript](http://amzn.com/0321812182) - David Herman
  - [Eloquent JavaScript](http://eloquentjavascript.net/) - Marijn Haverbeke
  - [You Don't Know JS: ES6 & Beyond](http://shop.oreilly.com/product/0636920033769.do) - Kyle Simpson

**Blogs**

  - [JavaScript Weekly](http://javascriptweekly.com/)
  - [JavaScript, JavaScript...](https://javascriptweblog.wordpress.com/)
  - [Bocoup Weblog](https://bocoup.com/weblog)
  - [Adequately Good](http://www.adequatelygood.com/)
  - [NCZOnline](https://www.nczonline.net/)
  - [Perfection Kills](http://perfectionkills.com/)
  - [Ben Alman](http://benalman.com/)
  - [Dmitry Baranovskiy](http://dmitry.baranovskiy.com/)
  - [Dustin Diaz](http://dustindiaz.com/)
  - [nettuts](http://code.tutsplus.com/?s=javascript)

**Podcasts**

  - [JavaScript Air](https://javascriptair.com/)
  - [JavaScript Jabber](https://devchat.tv/js-jabber/)


**[⬆ back to top](#table-of-contents)**

## In the Wild

  This is a list of organizations that are using this style guide. Send us a pull request and we'll add you to the list.

  - **3blades**: [3Blades/javascript](https://github.com/3blades/javascript)
  - **4Catalyzer**: [4Catalyzer/javascript](https://github.com/4Catalyzer/javascript)
  - **Aan Zee**: [AanZee/javascript](https://github.com/AanZee/javascript)
  - **Adult Swim**: [adult-swim/javascript](https://github.com/adult-swim/javascript)
  - **Airbnb**: [airbnb/javascript](https://github.com/airbnb/javascript)
  - **AltSchool**: [AltSchool/javascript](https://github.com/AltSchool/javascript)
  - **Apartmint**: [apartmint/javascript](https://github.com/apartmint/javascript)
  - **Ascribe**: [ascribe/javascript](https://github.com/ascribe/javascript)
  - **Avalara**: [avalara/javascript](https://github.com/avalara/javascript)
  - **Avant**: [avantcredit/javascript](https://github.com/avantcredit/javascript)
  - **Axept**: [axept/javascript](https://github.com/axept/javascript)
  - **BashPros**: [BashPros/javascript](https://github.com/BashPros/javascript)
  - **Billabong**: [billabong/javascript](https://github.com/billabong/javascript)
  - **Bisk**: [bisk/javascript](https://github.com/Bisk/javascript/)
  - **Bonhomme**: [bonhommeparis/javascript](https://github.com/bonhommeparis/javascript)
  - **Brainshark**: [brainshark/javascript](https://github.com/brainshark/javascript)
  - **CaseNine**: [CaseNine/javascript](https://github.com/CaseNine/javascript)
  - **Chartboost**: [ChartBoost/javascript-style-guide](https://github.com/ChartBoost/javascript-style-guide)
  - **ComparaOnline**: [comparaonline/javascript](https://github.com/comparaonline/javascript-style-guide)
  - **Compass Learning**: [compasslearning/javascript-style-guide](https://github.com/compasslearning/javascript-style-guide)
  - **DailyMotion**: [dailymotion/javascript](https://github.com/dailymotion/javascript)
  - **DoSomething**: [DoSomething/eslint-config](https://github.com/DoSomething/eslint-config)
  - **Digitpaint** [digitpaint/javascript](https://github.com/digitpaint/javascript)
  - **Ecosia**: [ecosia/javascript](https://github.com/ecosia/javascript)
  - **Evernote**: [evernote/javascript-style-guide](https://github.com/evernote/javascript-style-guide)
  - **Evolution Gaming**: [evolution-gaming/javascript](https://github.com/evolution-gaming/javascript)
  - **EvozonJs**: [evozonjs/javascript](https://github.com/evozonjs/javascript)
  - **ExactTarget**: [ExactTarget/javascript](https://github.com/ExactTarget/javascript)
  - **Expensify** [Expensify/Style-Guide](https://github.com/Expensify/Style-Guide/blob/master/javascript.md)
  - **Flexberry**: [Flexberry/javascript-style-guide](https://github.com/Flexberry/javascript-style-guide)
  - **Gawker Media**: [gawkermedia/javascript](https://github.com/gawkermedia/javascript)
  - **General Electric**: [GeneralElectric/javascript](https://github.com/GeneralElectric/javascript)
  - **Generation Tux**: [GenerationTux/javascript](https://github.com/generationtux/styleguide)
  - **GoodData**: [gooddata/gdc-js-style](https://github.com/gooddata/gdc-js-style)
  - **Grooveshark**: [grooveshark/javascript](https://github.com/grooveshark/javascript)
  - **Honey**: [honeyscience/javascript](https://github.com/honeyscience/javascript)
  - **How About We**: [howaboutwe/javascript](https://github.com/howaboutwe/javascript-style-guide)
  - **Huballin**: [huballin/javascript](https://github.com/huballin/javascript)
  - **HubSpot**: [HubSpot/javascript](https://github.com/HubSpot/javascript)
  - **Hyper**: [hyperoslo/javascript-playbook](https://github.com/hyperoslo/javascript-playbook/blob/master/style.md)
  - **InterCity Group**: [intercitygroup/javascript-style-guide](https://github.com/intercitygroup/javascript-style-guide)
  - **Jam3**: [Jam3/Javascript-Code-Conventions](https://github.com/Jam3/Javascript-Code-Conventions)
  - **JeopardyBot**: [kesne/jeopardy-bot](https://github.com/kesne/jeopardy-bot/blob/master/STYLEGUIDE.md)
  - **JSSolutions**: [JSSolutions/javascript](https://github.com/JSSolutions/javascript)
  - **KickorStick**: [kickorstick/javascript](https://github.com/kickorstick/javascript)
  - **Kinetica Solutions**: [kinetica/javascript](https://github.com/kinetica/Javascript-style-guide)
  - **Lonely Planet**: [lonelyplanet/javascript](https://github.com/lonelyplanet/javascript)
  - **M2GEN**: [M2GEN/javascript](https://github.com/M2GEN/javascript)
  - **Mighty Spring**: [mightyspring/javascript](https://github.com/mightyspring/javascript)
  - **MinnPost**: [MinnPost/javascript](https://github.com/MinnPost/javascript)
  - **MitocGroup**: [MitocGroup/javascript](https://github.com/MitocGroup/javascript)
  - **ModCloth**: [modcloth/javascript](https://github.com/modcloth/javascript)
  - **Money Advice Service**: [moneyadviceservice/javascript](https://github.com/moneyadviceservice/javascript)
  - **Muber**: [muber/javascript](https://github.com/muber/javascript)
  - **National Geographic**: [natgeo/javascript](https://github.com/natgeo/javascript)
  - **Nimbl3**: [nimbl3/javascript](https://github.com/nimbl3/javascript)
  - **Nulogy**: [nulogy/javascript](https://github.com/nulogy/javascript)
  - **Orange Hill Development**: [orangehill/javascript](https://github.com/orangehill/javascript)
  - **Orion Health**: [orionhealth/javascript](https://github.com/orionhealth/javascript)
  - **OutBoxSoft**: [OutBoxSoft/javascript](https://github.com/OutBoxSoft/javascript)
  - **Peerby**: [Peerby/javascript](https://github.com/Peerby/javascript)
  - **Razorfish**: [razorfish/javascript-style-guide](https://github.com/razorfish/javascript-style-guide)
  - **reddit**: [reddit/styleguide/javascript](https://github.com/reddit/styleguide/tree/master/javascript)
  - **React**: [facebook.github.io/react/contributing/how-to-contribute.html#style-guide](https://facebook.github.io/react/contributing/how-to-contribute.html#style-guide)
  - **REI**: [reidev/js-style-guide](https://github.com/rei/code-style-guides/blob/master/docs/javascript.md)
  - **Ripple**: [ripple/javascript-style-guide](https://github.com/ripple/javascript-style-guide)
  - **SeekingAlpha**: [seekingalpha/javascript-style-guide](https://github.com/seekingalpha/javascript-style-guide)
  - **Shutterfly**: [shutterfly/javascript](https://github.com/shutterfly/javascript)
  - **Sourcetoad**: [sourcetoad/javascript](https://github.com/sourcetoad/javascript)
  - **Springload**: [springload/javascript](https://github.com/springload/javascript)
  - **StratoDem Analytics**: [stratodem/javascript](https://github.com/stratodem/javascript)
  - **SteelKiwi Development**: [steelkiwi/javascript](https://github.com/steelkiwi/javascript)
  - **StudentSphere**: [studentsphere/javascript](https://github.com/studentsphere/guide-javascript)
  - **SwoopApp**: [swoopapp/javascript](https://github.com/swoopapp/javascript)
  - **SysGarage**: [sysgarage/javascript-style-guide](https://github.com/sysgarage/javascript-style-guide)
  - **Syzygy Warsaw**: [syzygypl/javascript](https://github.com/syzygypl/javascript)
  - **Target**: [target/javascript](https://github.com/target/javascript)
  - **TheLadders**: [TheLadders/javascript](https://github.com/TheLadders/javascript)
  - **The Nerdery**: [thenerdery/javascript-standards](https://github.com/thenerdery/javascript-standards)
  - **T4R Technology**: [T4R-Technology/javascript](https://github.com/T4R-Technology/javascript)
  - **VoxFeed**: [VoxFeed/javascript-style-guide](https://github.com/VoxFeed/javascript-style-guide)
  - **WeBox Studio**: [weboxstudio/javascript](https://github.com/weboxstudio/javascript)
  - **Weggo**: [Weggo/javascript](https://github.com/Weggo/javascript)
  - **Zillow**: [zillow/javascript](https://github.com/zillow/javascript)
  - **ZocDoc**: [ZocDoc/javascript](https://github.com/ZocDoc/javascript)

**[⬆ back to top](#table-of-contents)**

## Translation

  This style guide is also available in other languages:

  - ![br](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Brazilian Portuguese**: [armoucar/javascript-style-guide](https://github.com/armoucar/javascript-style-guide)
  - ![bg](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Bulgaria.png) **Bulgarian**: [borislavvv/javascript](https://github.com/borislavvv/javascript)
  - ![ca](https://raw.githubusercontent.com/fpmweb/javascript-style-guide/master/img/catala.png) **Catalan**: [fpmweb/javascript-style-guide](https://github.com/fpmweb/javascript-style-guide)
  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese (Simplified)**: [sivan/javascript-style-guide](https://github.com/sivan/javascript-style-guide)
  - ![tw](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Taiwan.png) **Chinese (Traditional)**: [jigsawye/javascript](https://github.com/jigsawye/javascript)
  - ![fr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/France.png) **French**: [nmussy/javascript-style-guide](https://github.com/nmussy/javascript-style-guide)
  - ![de](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Germany.png) **German**: [timofurrer/javascript-style-guide](https://github.com/timofurrer/javascript-style-guide)
  - ![it](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Italy.png) **Italian**: [sinkswim/javascript-style-guide](https://github.com/sinkswim/javascript-style-guide)
  - ![jp](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [mitsuruog/javascript-style-guide](https://github.com/mitsuruog/javascript-style-guide)
  - ![kr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Korean**: [tipjs/javascript-style-guide](https://github.com/tipjs/javascript-style-guide)
  - ![pl](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Poland.png) **Polish**: [mjurczyk/javascript](https://github.com/mjurczyk/javascript)
  - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**: [leonidlebedev/javascript-airbnb](https://github.com/leonidlebedev/javascript-airbnb)
  - ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Spanish**: [paolocarrasco/javascript-style-guide](https://github.com/paolocarrasco/javascript-style-guide)
  - ![th](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Thailand.png) **Thai**: [lvarayut/javascript-style-guide](https://github.com/lvarayut/javascript-style-guide)
  - ![ua](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Ukraine.png) **Ukrainian**: [ivanzusko/javascript](https://github.com/ivanzusko/javascript)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnam**: [hngiang/javascript-style-guide](https://github.com/hngiang/javascript-style-guide)

## The JavaScript Style Guide Guide

  - [Reference](https://github.com/airbnb/javascript/wiki/The-JavaScript-Style-Guide-Guide)

## Chat With Us About JavaScript

  - Find us on [gitter](https://gitter.im/airbnb/javascript).

## Contributors

  - [View Contributors](https://github.com/airbnb/javascript/graphs/contributors)


## License

(The MIT License)

Copyright (c) 2014-2017 Airbnb

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[⬆ back to top](#table-of-contents)**

## Amendments

We encourage you to fork this guide and change the rules to fit your team's style guide. Below, you may list some amendments to the style guide. This allows you to periodically update your style guide without having to deal with merge conflicts.

# };
