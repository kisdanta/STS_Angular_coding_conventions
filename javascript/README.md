# JavaScript Style Guide

*A mostly reasonable approach to JavaScript*

Forked from the excellent [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript), slightly modified to
fit STS's conventions.

## Table of Contents

1. [References](#references)
1. [Objects](#objects)
1. [Arrays](#arrays)
1. [Destructuring](#destructuring)
1. [Strings](#strings)
1. [Functions](#functions)
1. [Arrow Functions](#arrow-functions)
1. [Classes & Constructors](#classes--constructors)
1. [Modules](#modules)
1. [Properties](#properties)
1. [Variables](#variables)
1. [Comparison Operators & Equality](#comparison-operators--equality)
1. [Blocks](#blocks)
1. [Control Statements](#control-statements)
1. [Comments](#comments)
1. [Whitespace](#whitespace)
1. [Commas](#commas)
1. [Type Casting & Coercion](#type-casting--coercion)
1. [Naming Conventions](#naming-conventions)
1. [Resources](#resources)
1. [License](#license)

**[⬆ back to top](#table-of-contents)**

## 1. References

#### 1.1 Use `const` for all of your references; avoid using `var`. 
eslint: [`prefer-const`](https://eslint.org/docs/rules/prefer-const.html), [`no-const-assign`](https://eslint.org/docs/rules/no-const-assign.html)

> Why? This ensures that you can’t reassign your references, which can lead to bugs and difficult to comprehend code.

```javascript
✅ Good
const a = 1;
const b = 2;

❌ Bad
var a = 1;
var b = 2;
```

#### 1.2 If you must reassign references, use `let` instead of `var`.
eslint: [`no-var`](https://eslint.org/docs/rules/no-var.html)

> Why? `let` is block-scoped rather than function-scoped like `var`.

```javascript
✅ Good
let count = 1;
if (true) {
    count += 1;
}

❌ Bad
var count = 1;
if (true) {
    count += 1;
}
 ```

**[⬆ back to top](#table-of-contents)**

## 2. Objects

#### 2.1 Use the literal syntax for object creation. 
eslint: [`no-new-object`](https://eslint.org/docs/rules/no-new-object.html)

```javascript
✅ Good
const item = {};

❌ Bad
const item = new Object();
```

#### 2.2 Use object method shorthand.
eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)

```javascript
✅ Good
const atom = {
  value: 1,

  addValue(value) {
    return atom.value + value;
  },
};

❌ Bad
const atom = {
    value: 1,

    addValue: function (value) {
      return atom.value + value;
    },
};
```

#### 2.3 Use property value shorthand.

eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)

> Why? It is shorter and descriptive.

```javascript
const lukeSkywalker = 'Luke Skywalker';

✅ Good
const obj = {
  lukeSkywalker,
};

❌ Bad
const obj = {
    lukeSkywalker: lukeSkywalker,
};
 ```

#### 2.4 Group your shorthand properties at the beginning of your object declaration.

> Why? It’s easier to tell which properties are using the shorthand.

```javascript
const anakinSkywalker = 'Anakin Skywalker';
const lukeSkywalker = 'Luke Skywalker';

✅ Good
const obj = {
  lukeSkywalker,
  anakinSkywalker,
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  episodeThree: 3,
  mayTheFourth: 4,
};

❌ Bad
const obj = {
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  lukeSkywalker,
  episodeThree: 3,
  mayTheFourth: 4,
  anakinSkywalker,
};
 ```

#### 2.5 Only quote properties that are invalid identifiers.

eslint: [`quote-props`](https://eslint.org/docs/rules/quote-props.html)

> Why? In general, we consider it subjectively easier to read. It improves syntax highlighting, and is also more easily optimized by many JS engines.

```javascript
✅ Good
const good = {
  foo: 3,
  bar: 4,
  'data-blah': 5,
};

❌ Bad
const bad = {
  'foo': 3,
  'bar': 4,
  'data-blah': 5,
};
```

**[⬆ back to top](#table-of-contents)**

## 3. Arrays

#### 3.1 Use the literal syntax for array creation.

eslint: [`no-array-constructor`](https://eslint.org/docs/rules/no-array-constructor.html)

```javascript
✅ Good
const items = [];

❌ Bad
const items = new Array();
```

#### 3.2 Use array spreads `...` to copy arrays.

```javascript
❌ Bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i += 1) {
  itemsCopy[i] = items[i];
}

✅ Good
const itemsCopy = [...items];
```

**[⬆ back to top](#table-of-contents)**

## 4. Destructuring

#### 4.1 Use object destructuring when accessing and using multiple properties of an object.

eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

> Why? Destructuring saves you from creating temporary references for those properties, and from repetitive access of the object. Repeating object access creates more repetitive code, requires more reading, and creates more opportunities for mistakes. Destructuring objects also provides a single site of definition of the object structure that is used in the block, rather than requiring reading the entire block to determine what is used.

```javascript
✅ Good
function getFullName(user) {
  const { firstName, lastName } = user;
  return `${firstName} ${lastName}`;
}

✅ Best
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}

❌ Bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;

  return `${firstName} ${lastName}`;
}
```

#### 4.2 Use array destructuring.

eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

  ```javascript
  const arr = [1, 2, 3, 4];

✅ Good
const [first, second] = arr;

  ❌ Bad
  const first = arr[0];
  const second = arr[1];
  ```

**[⬆ back to top](#table-of-contents)**

## 5. Strings

#### 5.1 Use single quotes `''` for strings.
  eslint: [`quotes`](https://eslint.org/docs/rules/quotes.html)

  ```javascript
✅ Good
const name = 'Capt. Janeway';

  ❌ Bad
  const name = "Capt. Janeway";

  ❌ Bad
  // template literals should contain interpolation or newlines
  const name = `Capt. Janeway`;
  ```

#### 5.2 Strings that cause the line to go over 100 characters should not be written across multiple lines using string concatenation.

  > Why? Broken strings are painful to work with and make code less searchable.

  ```javascript
✅ Good
const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

  ❌ Bad
  const errorMessage = 'This is a super long error that was thrown because \
  of Batman. When you stop to think about how Batman had anything to do \
  with this, you would get nowhere \
  fast.';

  ❌ Bad
  const errorMessage = 'This is a super long error that was thrown because ' +
    'of Batman. When you stop to think about how Batman had anything to do ' +
    'with this, you would get nowhere fast.';
  ```

#### 5.3 When programmatically building up strings, use template strings instead of concatenation.

eslint: [`prefer-template`](https://eslint.org/docs/rules/prefer-template.html) [`template-curly-spacing`](https://eslint.org/docs/rules/template-curly-spacing)

  > Why? Template strings give you a readable, concise syntax with proper newlines and string interpolation features.

  ```javascript
  ✅ Good
  function sayHi(name) {
    return `How are you, ${name}?`;
  }

  ❌ Bad
  function sayHi(name) {
    return 'How are you, ' + name + '?';
  }

  ❌ Bad
  function sayHi(name) {
    return ['How are you, ', name, '?'].join();
  }

  ❌ Bad
  function sayHi(name) {
    return `How are you, ${ name }?`;
  }
  ```

**[⬆ back to top](#table-of-contents)**

## 6. Functions

#### 6.1 **Note:** ECMA-262 defines a `block` as a list of statements. A function declaration is not a statement.

  ```javascript
  ✅ Good
  let test;
  if (currentUser) {
    test = () => {
      console.log('Yup.');
    };
}

  ❌ Bad
  if (currentUser) {
    function test() {
      console.log('Nope.');
    }
  }
  ```

#### 6.2 Never mutate parameters.
  eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign.html)

  > Why? Manipulating objects passed in as parameters can cause unwanted variable side effects in the original caller.

  ```javascript
  ✅ Good
  function f2(obj) {
    const key = obj['key'] ? obj.key : 1;
  }

  ❌ Bad
  function f1(obj) {
    obj.key = 1;
  }
  ```

#### 6.3 Never reassign parameters.
  eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign.html)

  > Why? Reassigning parameters can lead to unexpected behavior, especially when accessing the `arguments` object. It can also cause optimization issues, especially in V8.

  ```javascript
  ✅ Good
  function f3(a) {
    const b = a || 1;
    // ...
  }
  
  function f4(a = 1) {
    // ...
  }

  ❌ Bad
  function f1(a) {
    a = 1;
    // ...
  }

  function f2(a) {
    if (!a) { a = 1; }
    // ...
  }
  ```

**[⬆ back to top](#table-of-contents)**

## 7. Arrow Functions

#### 7.1 When you must use an anonymous function (as when passing an inline callback), use arrow function notation. 

eslint: [`prefer-arrow-callback`](https://eslint.org/docs/rules/prefer-arrow-callback.html)
  , [`arrow-spacing`](https://eslint.org/docs/rules/arrow-spacing.html)

  > Why? It creates a version of the function that executes in the context of `this`, which is usually what you want, and is a more concise syntax.

  > Why not? If you have a fairly complicated function, you might move that logic out into its own named function expression.

  ```javascript
  ✅ Good
  [1, 2, 3].map((x) => {
    const y = x + 1;
    return x * y;
  });

  ❌ Bad
  [1, 2, 3].map(function (x) {
    const y = x + 1;
    return x * y;
  });
  ```

#### 7.1 Avoid confusing arrow function syntax (`=>`) with comparison operators (`<=`, `>=`).
  eslint: [`no-confusing-arrow`](https://eslint.org/docs/rules/no-confusing-arrow)

  ```javascript
  ✅ Good
  const itemHeight = (item) => (item.height <= 256 ? item.largeSize : item.smallSize);
  
✅ Good
  const itemHeight = (item) => {
    const { height, largeSize, smallSize } = item;
    return height <= 256 ? largeSize : smallSize;
  };
  
  ❌ Bad
  const itemHeight = (item) => item.height <= 256 ? item.largeSize : item.smallSize;

  ❌ Bad
  const itemHeight = (item) => item.height >= 256 ? item.largeSize : item.smallSize;
  ```

**[⬆ back to top](#table-of-contents)**

## 8. Classes & Constructors

#### 8.1 Always use `class`. Avoid manipulating `prototype` directly.

  > Why? `class` syntax is more concise and easier to reason about.

  ```javascript
  ❌ Bad
  function Queue(contents = []) {
    this.queue = [...contents];
  }
  Queue.prototype.pop = function () {
    const value = this.queue[0];
    this.queue.splice(0, 1);
    return value;
  };

  ✅ Good
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

#### 8.2 Classes have a default constructor if one is not specified. An empty constructor function or one that just delegates to a parent class is unnecessary.
  eslint: [`no-useless-constructor`](https://eslint.org/docs/rules/no-useless-constructor)

  ```javascript
  ✅ Good
  class Rey extends Jedi {
    constructor(...args) {
      super(...args);
      this.name = 'Rey';
    }
  }
  
  ❌ Bad
  class Jedi {
    constructor() {}

    getName() {
      return this.name;
    }
  }

  ❌ Bad
  class Rey extends Jedi {
    constructor(...args) {
      super(...args);
    }
  }
  ```

**[⬆ back to top](#table-of-contents)**

## 9. Modules

#### 9.1 Always use modules (`import`/`export`) over a non-standard module system. You can always transpile to your preferred module system.

  > Why? Modules are the future, let’s start using the future now.

  ```javascript
  ✅ Ok
  import AirbnbStyleGuide from './AirbnbStyleGuide';
  export default AirbnbStyleGuide.es6;
  
  ✅ Good
  import { es6 } from './AirbnbStyleGuide';
  export default es6;

  ❌ Bad
const AirbnbStyleGuide = require('./AirbnbStyleGuide');
  module.exports = AirbnbStyleGuide.es6;
  ```

#### 9.2 Do not use wildcard imports.

  > Why? This makes sure you have a single default export.

  ```javascript
  ✅ Good
  import AirbnbStyleGuide from './AirbnbStyleGuide';

❌ Bad
  import * as AirbnbStyleGuide from './AirbnbStyleGuide';
  ```

#### 9.3 And do not export directly from an import.

  > Why? Although the one-liner is concise, having one clear way to import and one clear way to export makes things consistent.

  ```javascript
✅ Good
// filename es6.js
import { es6 } from './AirbnbStyleGuide';
export default es6;

  ❌ Bad
  // filename es6.js
  export { es6 as default } from './AirbnbStyleGuide';
  ```

#### 9.4 Only import from a path in one place.
  eslint: [`no-duplicate-imports`](https://eslint.org/docs/rules/no-duplicate-imports)
  > Why? Having multiple lines that import from the same path can make code harder to maintain.

  ```javascript
  ❌ Bad
  import foo from 'foo';
  // … some other imports … //
  import { named1, named2 } from 'foo';

  ✅ Good
  import foo, { named1, named2 } from 'foo';

  ✅ Good
  import foo, {
    named1,
    named2,
  } from 'foo';
  ```

#### 9.5 Do not export mutable bindings.
  eslint: [`import/no-mutable-exports`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/no-mutable-exports.md)
  > Why? Mutation should be avoided in general, but in particular when exporting mutable bindings. While this technique may be needed for some special cases, in general, only constant references should be exported.

  ```javascript
✅ Good
const foo = 3;
export { foo };

  ❌ Bad
  let foo = 3;
  export { foo };
  ```

#### 9.6 In modules with a single export, prefer default export over named export.
  eslint: [`import/prefer-default-export`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/prefer-default-export.md)
  > Why? To encourage more files that only ever export one thing, which is better for readability and maintainability.

  ```javascript
✅ Good
export default function foo() {}

  ❌ Bad
  export function foo() {}
  ```

#### 9.7 Put all `import`s above non-import statements.
  eslint: [`import/first`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/first.md)
  > Why? Since `import`s are hoisted, keeping them all at the top prevents surprising behavior.

  ```javascript
✅ Good
import foo from 'foo';
import bar from 'bar';

foo.init();

  ❌ Bad
  import foo from 'foo';
  foo.init();

  import bar from 'bar';
  ```

**[⬆ back to top](#table-of-contents)**

## 10. Properties

#### 10.1 Use dot notation when accessing properties.
  eslint: [`dot-notation`](https://eslint.org/docs/rules/dot-notation.html)

  ```javascript
  const luke = {
    jedi: true,
    age: 28,
  };

✅ Good
const isJedi = luke.jedi;

  ❌ Bad
  const isJedi = luke['jedi'];
  ```

**[⬆ back to top](#table-of-contents)**

## 11. Variables

#### 11.1 Group all your `const`s and then group all your `let`s.

  > Why? This is helpful when later on you might need to assign a variable depending on one of the previously assigned variables.

  ```javascript
✅ Good
const goSportsTeam = true;
const items = getItems();
let dragonball;
let i;
let length;

  ❌ Bad
  let i, len, dragonball,
      items = getItems(),
      goSportsTeam = true;

  ❌ Bad
  let i;
  const items = getItems();
  let dragonball;
  const goSportsTeam = true;
  let len;
  ```

#### 11.2 Assign variables where you need them, but place them in a reasonable place.

  > Why? `let` and `const` are block scoped and not function scoped.

  ```javascript
  ✅ Good
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

❌ Bad
  // unnecessary function call
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
  ```

#### 11.3 Avoid hardcodes values
  > Why? Someone looking at the code would have no idea what the number/ string stands for, how it was calculated and what's the business logic behind this. Instead of hardcoding this value, we could've created a constant as follows:

  ```javascript
  ✅ Good
  const DAY_IN_MILLISECONDS = 3600 * 24 * 1000; // 86400000
  
  setInterval(() => {
    // do something
  }, DAY_IN_MILLISECONDS);
  
  ✅ Good
  const USER_TYPES = {
    REGULAR_EMPLOYEE: '1'
  }
  createUser('JohnDoe', 'Software Developer', USER_TYPES.REGULAR_EMPLOYEE);

  ❌ Bad
  setInterval(() => {
    // do something
  }, 86400000);
  // WHAT IS THIS 86400000 ??? 🤔

  ❌ Bad
  const createUser = (name, designation, type) => {
    console.log({name, designation, type});
  }

  createUser('JohnDoe', 'Software Developer', '1');
  // WHAT IS this '1'? 🤔
  ```

**[⬆ back to top](#table-of-contents)**

## 12. Comparison Operators & Equality

#### 12.1 Use `===` and `!==` over `==` and `!=`.
  eslint: [`eqeqeq`](https://eslint.org/docs/rules/eqeqeq.html)

#### 12.2 Use shortcuts for booleans, but explicit comparisons for strings and numbers.

  ```javascript
  ✅ Good
  if (isValid) {
    // ...
  }
  
  ❌ Bad
  if (isValid === true) {
    // ...
  }
  
  ✅ Good
  if (name !== '') {
    // ...
  }
  
  ❌ Bad
  if (name) {
    // ...
  }
  
  ✅ Good
  if (collection.length > 0) {
    // ...
  }

  ❌ Bad
  if (collection.length) {
    // ...
  }
  ```

#### 12.3 Use braces to create blocks in `case` and `default` clauses that contain lexical declarations (e.g. `let`, `const`, `function`, and `class`).
  
eslint: [`no-case-declarations`](https://eslint.org/docs/rules/no-case-declarations.html)

> Why? Lexical declarations are visible in the entire `switch` block but only get initialized when assigned, which only happens when its `case` is reached. This causes problems when multiple `case` clauses attempt to define the same thing.

  ```javascript
  ✅ Good
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

  ❌ Bad
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
  ```

#### 12.4 Ternaries should not be nested and generally be single line expressions.
  eslint: [`no-nested-ternary`](https://eslint.org/docs/rules/no-nested-ternary.html)

  ```javascript
  // split into 2 separated ternary expressions
  const maybeNull = value1 > value2 ? 'baz' : null;

  ✅ Better
  const foo = maybe1 > maybe2
          ? 'bar'
          : maybeNull;
  
  ✅ Best
  const foo = maybe1 > maybe2 ? 'bar' : maybeNull;
    
  ❌ Bad
  const foo = maybe1 > maybe2
    ? "bar"
    : value1 > value2 ? "baz" : null;
  ```

#### 12.5 Avoid unneeded ternary statements.
  eslint: [`no-unneeded-ternary`](https://eslint.org/docs/rules/no-unneeded-ternary.html)

  ```javascript
  ✅ Good
  const foo = a || b;
  const bar = !!c;
  const baz = !c;
  
  ❌ Bad
  const foo = a ? a : b;
  const bar = c ? true : false;
  const baz = c ? false : true;
  ```

**[⬆ back to top](#table-of-contents)**

## 13. Blocks

#### 13.1 Use braces with all multiline blocks.
  eslint: [`nonblock-statement-body-position`](https://eslint.org/docs/rules/nonblock-statement-body-position)

  ```javascript
  ✅ Good
  if (test) return false;
  
  ✅ Good
  if (test) {
    return false;
  }
  
  ✅ Good
  function bar() {
    return false;
  }
  
  ❌ Bad
  if (test)
    return false;
  
  ❌ Bad
  function foo() { return false; }
  ```

#### 13.2 If an `if` block always executes a `return` statement, the subsequent `else` block is unnecessary. A `return` in an `else if` block following an `if` block that contains a `return` can be separated into multiple `if` blocks. 
eslint: [`no-else-return`](https://eslint.org/docs/rules/no-else-return)

  ```javascript
  ✅ Good
  function foo() {
    if (x) {
      return x;
    }
  
    return y;
  }
  
  ✅ Good
  function cats() {
    if (x) {
      return x;
    }
  
    if (y) {
      return y;
    }
  }

  ❌ Bad
  function foo() {
    if (x) {
      return x;
    } else {
      return y;
    }
  }

  ❌ Bad
  function cats() {
    if (x) {
      return x;
    } else if (y) {
      return y;
    }
  }

  ❌ Bad
  function dogs() {
    if (x) {
      return x;
    } else {
      if (y) {
        return y;
      }
    }
  }
  ```

**[⬆ back to top](#table-of-contents)**

## 14. Control Statements

#### 14.1 In case your control statement (`if`, `while` etc.) gets too long or exceeds the maximum line length, each (grouped) condition could be put into a new line. The logical operator should begin the line.

  > Why? Requiring operators at the beginning of the line keeps the operators aligned and follows a pattern similar to method chaining. This also improves readability by making it easier to visually follow complex logic.

  ```javascript
  ✅ Good
  if (
          foo === 123
          && bar === 'abc'
  ) {
    thing1();
  }
  
  ✅ Good
  if (
          (foo === 123 || bar === 'abc')
          && doesItLookGoodWhenItBecomesThatLong()
          && isThisReallyHappening()
  ) {
    thing1();
  }
  
  ✅ Good
  if (foo === 123 && bar === 'abc') {
    thing1();
  }

  ❌ Bad
  if ((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
    thing1();
  }

  ❌ Bad
  if (foo === 123 &&
    bar === 'abc') {
    thing1();
  }

  ❌ Bad
  if (foo === 123
    && bar === 'abc') {
    thing1();
  }

  ❌ Bad
  if (
    foo === 123 &&
    bar === 'abc'
  ) {
    thing1();
  }
  ```

#### 14.2 Don't use selection operators in place of control statements.

  ```javascript
  ✅ Good
  if (!isRunning) {
    startRunning();
  }
  
  ❌ Bad
  !isRunning && startRunning();
  ```

**[⬆ back to top](#table-of-contents)**

## Comments

#### 15.1 Use `/** ... */` for multiline comments.

  ```javascript
  ✅ Good
  /**
   * make() returns a new element
   * based on the passed-in tag name
   */
  function make(tag) {

    // ...

    return element;
  }
  
  ❌ Bad
  // make() returns a new element
  // based on the passed in tag name
  //
  // @param {String} tag
  // @return {Element} element
  function make(tag) {
  
    // ...
  
    return element;
  }
  ```

#### 15.2 Use `//` for single line comments. Place single line comments on a newline above the subject of the comment. Put an empty line before the comment unless it’s on the first line of a block.

  ```javascript
  ✅ Good
  // is current tab
  const active = true;

  ✅ Good
  function getType() {
    console.log('fetching type...');
  
    // set the default type to 'no type'
    const type = this.type || 'no type';
  
    return type;
  }
  
  ✅ Good
  function getType() {
    // set the default type to 'no type'
    const type = this.type || 'no type';
  
    return type;
  }

  ❌ Bad
  const active = true;  // is current tab

  ❌ Bad
  function getType() {
    console.log('fetching type...');
    // set the default type to 'no type'
    const type = this.type || 'no type';

    return type;
  }
  ```

**[⬆ back to top](#table-of-contents)**

## 16. Whitespace

#### 16.1 Use soft tabs (space character) set to 2 spaces.
  eslint: [`indent`](https://eslint.org/docs/rules/indent.html)

  ```javascript
  ✅ Good
  function baz() {
  ∙∙let name;
  }
  
  ❌ Bad
  function foo() {
  ∙∙∙∙let name;
  }

  ❌ Bad
  function bar() {
  ∙let name;
  }
  ```

#### 16.2 Leave a blank line after blocks and before the next statement.

  ```javascript
  ✅ Good
  if (foo) {
    return bar;
  }
  
  return baz;
  
  ✅ Good
  const obj = {
    foo() {
    },
  
    bar() {
    },
  };

  return obj;
  
  ✅ Good
  const arr = [
    function foo() {
    },
  
    function bar() {
    },
  ];
  
  return arr;
  
  ❌ Bad
  if (foo) {
    return bar;
  }
  return baz;

  ❌ Bad
  const obj = {
    foo() {
    },
    bar() {
    },
  };
  return obj;

  ❌ Bad
  const arr = [
    function foo() {
    },
    function bar() {
    },
  ];
  return arr;
  ```

#### 16.3 Avoid trailing spaces at the end of lines.
  eslint: [`no-trailing-spaces`](https://eslint.org/docs/rules/no-trailing-spaces)

```javascript
✅ Good
var foo = 0;
var baz = 5;

❌ Bad
var foo = 0;//•••••
var baz = 5;//••
```

**[⬆ back to top](#table-of-contents)**

## 17. Commas

#### 17.1 Additional trailing comma: **Yup.**
  eslint: [`comma-dangle`](https://eslint.org/docs/rules/comma-dangle.html)

  > Why? This leads to cleaner git diffs. Also, transpilers like Babel will remove the additional trailing comma in the transpiled code which means you don’t have to worry about the [trailing comma problem](https://github.com/airbnb/javascript/blob/es5-deprecated/es5/README.md#commas) in legacy browsers.

  ```diff
  ✅ Good
  // git diff with trailing comma
  const hero = {
       firstName: 'Florence',
       lastName: 'Nightingale',
  +    inventorOf: ['coxcomb chart', 'modern nursing'],
  };
  
  ❌ Bad
  // git diff without trailing comma
  const hero = {
       firstName: 'Florence',
  -    lastName: 'Nightingale'
  +    lastName: 'Nightingale',
  +    inventorOf: ['coxcomb chart', 'modern nursing']
  };
  ```

**[⬆ back to top](#table-of-contents)**

## 18. Type Casting & Coercion

#### 18.1 Perform type coercion at the beginning of the statement.

#### 18.2 Booleans: 
eslint: [`no-new-wrappers`](https://eslint.org/docs/rules/no-new-wrappers)

  ```javascript
  const age = 0;

  ✅ Good
  const hasAge = Boolean(age);
  
  ✅ Best
  const hasAge = !!age;

  ❌ Bad
  const hasAge = new Boolean(age);
  ```

**[⬆ back to top](#table-of-contents)**

## 19. Naming Conventions

#### 19.1 Avoid single letter names. Be descriptive with your naming.
  eslint: [`id-length`](https://eslint.org/docs/rules/id-length)

  ```javascript
  ✅ Good
  function query() {
    // ...
  }
  
  ❌ Bad
  function q() {
    // ...
  }
  ```

#### 19.2 Use camelCase when naming objects, functions, and instances.
  eslint: [`camelcase`](https://eslint.org/docs/rules/camelcase.html)

  ```javascript
  ✅ Good
  const thisIsMyObject = {};
  function thisIsMyFunction() {}

  ❌ Bad
  const OBJEcttsssss = {};
  const this_is_my_object = {};
  function c() {}
  ```

<a name="naming--PascalCase"></a>

#### 19.3 Use PascalCase only when naming constructors or classes.
  eslint: [`new-cap`](https://eslint.org/docs/rules/new-cap.html)

  ```javascript
  ✅ Good
  class User {
    constructor(options) {
      this.name = options.name;
    }
  }
  
  const good = new User({
    name: 'yup',
  });

  ❌ Bad
  function user(options) {
    this.name = options.name;
  }

  const bad = new user({
    name: 'nope',
  });
  ```

#### 19.4 Use camelCase when you export-default a function. Your filename should be identical to your function’s name.

  ```javascript
  function makeStyleGuide() {
    // ...
  }

  export default makeStyleGuide;
  ```

#### 19.5 Use PascalCase when you export a constructor / class / singleton / function library / bare object.

  ```javascript
  const AirbnbStyleGuide = {
    es6: {
    },
  };

  export default AirbnbStyleGuide;
  ```

#### 19.6 You may optionally uppercase a constant only if it (1) is exported, (2) is a `const` (it can not be reassigned), and (3) the programmer can trust it (and its nested properties) to never change.

> Why? This is an additional tool to assist in situations where the programmer would be unsure if a variable might ever change. UPPERCASE_VARIABLES are letting the programmer know that they can trust the variable (and its properties) not to change.
>- What about all `const` variables? - This is unnecessary, so uppercasing should not be used for constants within a
      file. It should be used for exported constants however.
>- What about exported objects? - Uppercase at the top level of export (e.g. `EXPORTED_OBJECT.key`) and maintain that  all nested properties do not change.

  ```javascript
  ✅ Good
  // allowed but does not supply semantic value
  export const apiKey = 'SOMEKEY';
  
  // better in most cases
  export const API_KEY = 'SOMEKEY';
  
  export const MAPPING = {
    key: 'value'
  };

  ❌ Bad
  const PRIVATE_VARIABLE = 'should not be unnecessarily uppercased within a file';

  ❌ Bad
  export const THING_TO_BE_CHANGED = 'should obviously not be uppercased';

  ❌ Bad
  export let REASSIGNABLE_VARIABLE = 'do not use let with uppercase variables';
  
  ❌ Bad
  // unnecessarily uppercases key while adding no semantic value
  export const MAPPING = {
    KEY: 'value'
  };
  ```

**[⬆ back to top](#table-of-contents)**

## Resources

**Learning ES6+**

- [Latest ECMA spec](https://tc39.github.io/ecma262/)
- [ExploringJS](https://exploringjs.com/)
- [ES6 Compatibility Table](https://kangax.github.io/compat-table/es6/)
- [Comprehensive Overview of ES6 Features](http://es6-features.org/)
- [The Modern JavaScript Tutorial](https://javascript.info/)

**Read This**

- [Standard ECMA-262](https://www.ecma-international.org/ecma-262/6.0/index.html)

**Tools**

- Code Style Linters
    - [ESlint](https://eslint.org/)
      - [Airbnb Style .eslintrc](https://github.com/airbnb/javascript/blob/master/linters/.eslintrc)
    - [JSHint](https://jshint.com/)
      - [Airbnb Style .jshintrc](https://github.com/airbnb/javascript/blob/master/linters/.jshintrc)
- Neutrino Preset - [@neutrinojs/airbnb](https://neutrinojs.org/packages/airbnb/)

**Other Style Guides**

- [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)
- [Google JavaScript Style Guide (Old)](https://google.github.io/styleguide/javascriptguide.xml)
- [jQuery Core Style Guidelines](https://contribute.jquery.org/style-guide/js/)
- [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwaldron/idiomatic.js)
- [StandardJS](https://standardjs.com)

**Other Styles**

- [Naming this in nested functions](https://gist.github.com/cjohansen/4135065) - Christian Johansen
- [Conditional Callbacks](https://github.com/airbnb/javascript/issues/52) - Ross Allen
- [Popular JavaScript Coding Conventions on GitHub](http://sideeffect.kr/popularconvention/#javascript) - JeongHoon Byun
- [Multiple var statements in JavaScript, not superfluous](https://benalman.com/news/2012/05/multiple-var-statements-javascript/)
  - Ben Alman

**Further Reading**

- [Understanding JavaScript Closures](https://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/)
  - Angus Croll
- [Basic JavaScript for the impatient programmer](https://www.2ality.com/2013/06/basic-javascript.html) - Dr. Axel
  Rauschmayer
- [You Might Not Need jQuery](https://youmightnotneedjquery.com/) - Zack Bloom & Adam Schwartz
- [ES6 Features](https://github.com/lukehoban/es6features) - Luke Hoban
- [Frontend Guidelines](https://github.com/bendc/frontend-guidelines) - Benjamin De Cock

**Books**

- [JavaScript: The Good Parts](https://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742) - Douglas
  Crockford
- [JavaScript Patterns](https://www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752) - Stoyan Stefanov
- [Pro JavaScript Design Patterns](https://www.amazon.com/JavaScript-Design-Patterns-Recipes-Problem-Solution/dp/159059908X)
  - Ross Harmes and Dustin Diaz
- [High Performance Web Sites: Essential Knowledge for Front-End Engineers](https://www.amazon.com/High-Performance-Web-Sites-Essential/dp/0596529309)
  - Steve Souders
- [Maintainable JavaScript](https://www.amazon.com/Maintainable-JavaScript-Nicholas-C-Zakas/dp/1449327680) - Nicholas C.
  Zakas
- [JavaScript Web Applications](https://www.amazon.com/JavaScript-Web-Applications-Alex-MacCaw/dp/144930351X) - Alex
  MacCaw
- [Pro JavaScript Techniques](https://www.amazon.com/Pro-JavaScript-Techniques-John-Resig/dp/1590597273) - John Resig
- [Smashing Node.js: JavaScript Everywhere](https://www.amazon.com/Smashing-Node-js-JavaScript-Everywhere-Magazine/dp/1119962595)
  - Guillermo Rauch
- [Secrets of the JavaScript Ninja](https://www.amazon.com/Secrets-JavaScript-Ninja-John-Resig/dp/193398869X) - John
  Resig and Bear Bibeault
- [Human JavaScript](http://humanjavascript.com/) - Henrik Joreteg
- [Superhero.js](http://superherojs.com/) - Kim Joar Bekkelund, Mads Mobæk, & Olav Bjorkoy
- [JSBooks](https://jsbooks.revolunet.com/) - Julien Bouquillon
- [Third Party JavaScript](https://www.manning.com/books/third-party-javascript) - Ben Vinegar and Anton Kovalyov
- [Effective JavaScript: 68 Specific Ways to Harness the Power of JavaScript](https://amzn.com/0321812182) - David
  Herman
- [Eloquent JavaScript](https://eloquentjavascript.net/) - Marijn Haverbeke
- [You Don’t Know JS: ES6 & Beyond](https://shop.oreilly.com/product/0636920033769.do) - Kyle Simpson

**Blogs**

- [JavaScript Weekly](https://javascriptweekly.com/)
- [JavaScript, JavaScript...](https://javascriptweblog.wordpress.com/)
- [Bocoup Weblog](https://bocoup.com/weblog)
- [Adequately Good](https://www.adequatelygood.com/)
- [NCZOnline](https://www.nczonline.net/)
- [Perfection Kills](http://perfectionkills.com/)
- [Ben Alman](https://benalman.com/)
- [Dmitry Baranovskiy](http://dmitry.baranovskiy.com/)
- [nettuts](https://code.tutsplus.com/?s=javascript)
- [JavaScript Is Sexy](https://javascriptissexy.com/)

**Podcasts**

- [JavaScript Air](https://javascriptair.com/)
- [JavaScript Jabber](https://devchat.tv/js-jabber/)

**[⬆ back to top](#table-of-contents)**

## License

(The MIT License)

Copyright (c) 2012 Airbnb

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated
documentation files (the
'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify,
merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software
is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the
Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE
WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR
OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[⬆ back to top](#table-of-contents)**
