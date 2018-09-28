# Conding Convention

## Basic

* Indentation is 2 white spaces.
* Do not use tab.
* Do not leave trailing white spaces.
* Add 1 white space before and after operators, colon (:), and after comma (,), semi-colon (;).
* Do not add white spaces before comma (,) and semi-colon(;).
* Do not write more than 80 characters in a line.
* If the line is more than 80 characters, break to a new line following below rules. (2 spaces before `.`).
  * If it is a string of methods, break line before dot . and let the dot . be the start of new line.

  ```javascript
  "one string".somethingLongLongMethod(arg1)
    .otherCoolLongMethod(arg2)
    .anotherAwsomeLongMethod(arg3)
  ```

  * If it is method definition, use () to avoid syntax error.

  ```javascript
    const longMethodName = (parameter1, parameter2, parameter3, parameter4,
      parameter5, parameter6, options)
  ```

## 1. Always set `propTypes`
Using `propType` to provide validation for each prop the component will receive. Furthermore, this also provides a self-documenting reference for how the component should be used, and what props it needs to be passed.

## 2. Naming
Using **PascalCase** for React Components, filenames and **camelCase** for their instances.

```javascript
# bad
import reservationCard from './ReservationCard';

# good
import ReservationCard from './ReservationCard';

# bad
const ReservationItem = <ReservationCard />;

# good
const reservationItem = <ReservationCard />;
```

## 3. Declaration
Do not use `displayName` for naming components. Instead, name the component by reference.

```javascript
# bad
export default React.createClass({
  displayName: 'ReservationCard',
  // stuff goes here
});

# good
export default class ReservationCard extends React.Component {
}
```

## 4. Quotes
Always use double quotes `"` for JSX attributes, but single quotes `'` for all other JS.
```
Why? Regular HTML attributes also typically use double quotes instead of single, so JSX attributes mirror this convention.
```
```html
# bad
<Foo bar='bar' />

# good
<Foo bar="bar" />

# bad
<Foo style={{ left: "20px" }} />

# good
<Foo style={{ left: '20px' }} />
```

## 5. Spacing
* Always include a single space in your self-closing tag.

```html
# bad
<Foo/>

# very bad
<Foo                 />

# bad
<Foo
 />

# good
<Foo />
```

* Do not pad JSX curly braces with spaces.

```html
# bad
<Foo bar={ baz } />

# good
<Foo bar={baz} />
```

## 6. Props
* Always use `camelCase` for prop names.

```html
# bad
<Foo
  UserName="hello"
  phone_number={12345678}
/>

# good
<Foo
  userName="hello"
  phoneNumber={12345678}
/>
```

* Omit the value of the prop when it is explicitly `true`.

```html
# bad
<Foo
  hidden={true}
/>

# good
<Foo
  hidden
/>
```

* Always include an `alt` prop on `<img>` tags. If the image is presentational, alt can be an empty string or the `<img>` must have `role="presentation"`.

```html
# bad
<img src="hello.jpg" />

# good
<img src="hello.jpg" alt="Me waving hello" />

# good
<img src="hello.jpg" alt="" />

# good
<img src="hello.jpg" role="presentation" />

```

* Do not use words like **image**, **photo**, or **picture** in `<img>` `alt` props.

```
Why? Screenreaders already announce img elements as images, so there is no need to include this information in the alt text.
```

```html
# bad
<img src="hello.jpg" alt="Picture of me waving hello" />

# good
<img src="hello.jpg" alt="Me waving hello" />
```
* Use only valid, non-abstract 

```html
# bad - not an ARIA role
<div role="datepicker" />

# bad - abstract ARIA role
<div role="range" />

# good
<div role="button" />
```

* Do not use accessKey on elements.

```
Why? Inconsistencies between keyboard shortcuts and keyboard commands used by people using
screenreaders and keyboards complicate accessibility.
```

```html
# bad
<div accessKey="h" />

# good
<div />
```

* Avoid using an array index as key prop, prefer a unique ID

```html
# bad
{todos.map((todo, index) =>
  <Todo
    {...todo}
    key={index}
  />
)}

# good
{todos.map(todo => (
  <Todo
    {...todo}
    key={todo.id}
  />
))}
```

* Always define explicit `defaultProps` for all non-required props.

```
Why? propTypes are a form of documentation, and providing defaultProps means the reader of your code
doesn’t have to assume as much. In addition, it can mean that your code can omit certain type checks.
```

```javascript
# bad
function SFC({ foo, bar, children }) {
  return <div>{foo}{bar}{children}</div>;
}
SFC.propTypes = {
  foo: PropTypes.number.isRequired,
  bar: PropTypes.string,
  children: PropTypes.node,
};

# good
function SFC({ foo, bar, children }) {
  return <div>{foo}{bar}{children}</div>;
}
SFC.propTypes = {
  foo: PropTypes.number.isRequired,
  bar: PropTypes.string,
  children: PropTypes.node,
};
SFC.defaultProps = {
  bar: '',
  children: null,
};
```
## 7. Refs
Always use ref callbacks

```html
# bad
<Foo
  ref="myRef"
/>

# good
<Foo
  ref={(ref) => { this.myRef = ref; }}
/>
```

## 8. Wrap JSX tags in parentheses when they span more than one line.
```javascript
# bad
render() {
  return <MyComponent className="long body" foo="bar">
           <MyChild />
         </MyComponent>;
}

# good
render() {
  return (
    <MyComponent className="long body" foo="bar">
      <MyChild />
    </MyComponent>
  );
}

# good, when single line
render() {
  const body = <div>hello</div>;
  return <MyComponent>{body}</MyComponent>;
}
```
## 9. Tags

* Always self-close tags that have no children.

```html
# bad
<Foo className="stuff"></Foo>

# good
<Foo className="stuff" />
```

* If your component has multi-line properties, close its tag on a new line.

```html
# bad
<Foo
  bar="bar"
  baz="baz" />

# good
<Foo
  bar="bar"
  baz="baz"
/>
```

## 10. Methods

* Use arrow functions to close over local variables.

```javascript
function ItemList(props) {
  return (
    <ul>
      {props.items.map((item, index) => (
        <Item
          key={item.key}
          onClick={() => doSomethingWith(item.name, index)}
        />
      ))}
    </ul>
  );
}
```

* Bind event handlers for the render method in the constructor

```javascript
# bad
class extends React.Component {
  onClickDiv() {
    // do stuff
  }

  render() {
    return <div onClick={this.onClickDiv.bind(this)} />;
  }
}

# good
class extends React.Component {
  constructor(props) {
    super(props);

    this.onClickDiv = this.onClickDiv.bind(this);
  }

  onClickDiv() {
    // do stuff
  }

  render() {
    return <div onClick={this.onClickDiv} />;
  }
}

```

* Do not use underscore prefix for internal methods of a React component.

```
Why? Underscore prefixes are sometimes used as a convention in other languages to denote privacy.
But, unlike those languages, there is no native support for privacy in JavaScript, everything is
public. Regardless of your intentions, adding underscore prefixes to your properties does not
actually make them private, and any property (underscore-prefixed or not) should be treated as being
public. See issues #1024, and #490 for a more in-depth discussion.
```
```javascript
# bad
React.createClass({
  _onClickSubmit() {
    // do stuff
  },
  // other stuff
});

# good
class extends React.Component {
  onClickSubmit() {
    // do stuff
  }
  // other stuff
}
```

* Be sure to return a value in your render methods.

```javascript
# bad
render() {
  (<div />);
}

# good
render() {
  return (<div />);
}
```

## 11. Ordering
Ordering for class extends `React.Component`:

1.	optional static methods
2.	constructor
3.	getChildContext
4.	componentWillMount
5.	componentDidMount
6.	componentWillReceiveProps
7.	shouldComponentUpdate
8.	componentWillUpdate
9.	componentDidUpdate
10.	componentWillUnmount
11.	_clickHandlers_ or _eventHandlers_ (Ex: `onClickSubmit()`, `onChangeDescription()`)
12.	_getter methods for render_ (Ex: `getSelectReason()`, `getFooterContent()`)
13.	_optional render methods_ (Ex: `renderNavigation()`, `renderProfilePicture()`)
14.	render

* How to define `propTypes`, `defaultProps`, `contextTypes`, etc...

```javascript
import React, { PropTypes } from 'react';

const propTypes = {
  id: PropTypes.number.isRequired,
  url: PropTypes.string.isRequired,
  text: PropTypes.string,
};

const defaultProps = {
  text: 'Hello World',
};

class Link extends React.Component {
  static methodsAreOk() {
    return true;
  }

  render() {
    return <a href={this.props.url} data-id={this.props.id}>{this.props.text}</a>;
  }
}

Link.propTypes = propTypes;
Link.defaultProps = defaultProps;

export default Link;
```

## 12. const or let, var

* `const` is a sinal that **the variable won't be reassigned.**
* `let` is a signal that **the variable may be reassigned.**
* `var` is now **the weakest signal avariable** when you define a variable in JavaScript. The variable may or may not be reassigned, and the variable may or may not be used for an entire function, or just for the purpose of a block or loop.

**Don't use `var`**  in **ES6**. There is value in block scope for loops, but we can’t think of a situation where I’d prefer `var` over `let`.

## 13. Array

* Use the literal syntax for array creation.

```javascript
# bad
const items = new Array();

# good
const items = [];
```

* Use `Array#push` instead of direct assignment to add items to an array.

```javascript
const someStack = [];

# bad
someStack[someStack.length] = 'abracadabra';

# good
someStack.push('abracadabra');
```

* Use array spreads `...` to copy arrays.

```javascript
# bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i += 1) {
  itemsCopy[i] = items[i];
}

# good
const itemsCopy = [...items];
```

* To convert an array-like object to an array, use `Array.from`.

```javascript
let foo = [1,2,3,4]
foo.a = 5 // [1, 2, 3, 4, a: 5]
const nodes = Array.from(foo); // [1, 2, 3, 4]
```

* Use return statements in array method callbacks. It’s ok to omit the return if the function body consists of a single statement following. 

```javascript
# good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});

# good
[1, 2, 3].map(x => x + 1);

# bad
const flat = {};
[[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
  const flatten = memo.concat(item);
  flat[index] = flatten;
});

# good
const flat = {};
[[0, 1], [2, 3], [4, 5]].reduce((memo, item, index) => {
  const flatten = memo.concat(item);
  flat[index] = flatten;
  return flatten;
});

# bad
inbox.filter((msg) => {
  const { subject, author } = msg;
  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  } else {
    return false;
  }
});

# good
inbox.filter((msg) => {
  const { subject, author } = msg;
  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  }

  return false;
});
```

## 14. Object

* Use the literal syntax for object creation.

```javascript
# bad
const item = new Object();

# good
const item = {};
```

* Use computed property names when creating objects with dynamic property names. (`eslint:no-new-object`)

```
Why? They allow you to define all the properties of an object in one place.
```

```javascript
function getKey(k) {
  return `a key named ${k}`;
}

# bad
const obj = {
  id: 5,
  name: 'San Francisco',
};
obj[getKey('enabled')] = true;

# good
const obj = {
  id: 5,
  name: 'San Francisco',
  [getKey('enabled')]: true,
};
```

* Use object method shorthand. (`eslint: object-shorthand jscs: requireEnhancedObjectLiterals`)

```javascript
# bad
const atom = {
  value: 1,

  addValue: function (value) {
    return atom.value + value;
  },
};

# good
const atom = {
  value: 1,

  addValue(value) {
    return atom.value + value;
  },
};
```

* Use property value shorthand. (`eslint: object-shorthand jscs: requireEnhancedObjectLiterals`)

```
Why? It is shorter to write and descriptive.
```

```javascript
const lukeSkywalker = 'Luke Skywalker';

# bad
const obj = {
  lukeSkywalker: lukeSkywalker,
};

# good
const obj = {
  lukeSkywalker,
};
```

* Group your shorthand properties at the beginning of your object declaration.

```
Why? It's easier to tell which properties are using the shorthand.
```

```javascript
const anakinSkywalker = 'Anakin Skywalker';
const lukeSkywalker = 'Luke Skywalker';

# bad
const obj = {
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  lukeSkywalker,
  episodeThree: 3,
  mayTheFourth: 4,
  anakinSkywalker,
};

# good
const obj = {
  lukeSkywalker,
  anakinSkywalker,
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  episodeThree: 3,
  mayTheFourth: 4,
};
```

* Only quote properties that are invalid identifiers. (`eslint: quote-props jscs: disallowQuotedKeysInObjects`)

```
Why? In general we consider it subjectively easier to read. It improves syntax highlighting, and is also more easily optimized by many JS engines.
```

```javascript
# bad
const bad = {
  'foo': 3,
  'bar': 4,
  'data-blah': 5,
};

# good
const good = {
  foo: 3,
  bar: 4,
  'data-blah': 5,
};
```

* Do not call `Object.prototype` methods directly, such as `hasOwnProperty`, `propertyIsEnumerable`, and `isPrototypeOf`.

```
Why? These methods may be shadowed by properties on the object in question - consider { hasOwnProperty: false } - or, the object may be a null object (Object.create(null)).
```

```javascript
console.log(object.hasOwnProperty(key));

# good
console.log(Object.prototype.hasOwnProperty.call(object, key));

# best
const has = Object.prototype.hasOwnProperty; // cache the lookup once, in module scope.
/* or */
import has from 'has';
// ...
console.log(has.call(object, key));
```

* Prefer the object spread operator over `Object.assign` to shallow-copy objects. Use the object rest operator

```javascript
# very bad
const original = { a: 1, b: 2 };
const copy = Object.assign(original, { c: 3 }); // this mutates `original` ಠ_ಠ
delete copy.a; // so does this

# bad
const original = { a: 1, b: 2 };
const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

# good
const original = { a: 1, b: 2 };
const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
```

## 15. String

* Use double quotes `""` for strings. (`eslint: quotes jscs: validateQuoteMarks`)
```
why? can using single quites with sentences. (He's handsome.)
```

```javascript
# bad
const name = `Capt. Janeway`;

# bad - template literals should contain interpolation or newlines
const name = `Capt. Janeway`;

# good
const name = "Capt. Janeway";
```

* Strings that cause the line to go over 100 characters should not be written across multiple lines using string concatenation.

```javascript
# bad
const errorMessage = 'This is a super long error that was thrown because \
of Batman. When you stop to think about how Batman had anything to do \
with this, you would get nowhere \
fast.';

# bad
const errorMessage = 'This is a super long error that was thrown because ' +
  'of Batman. When you stop to think about how Batman had anything to do ' +
  'with this, you would get nowhere fast.';

# good
const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
```

* When programmatically building up strings, use template strings instead of concatenation. (`eslint: prefer-template template-curly-spacing jscs: requireTemplateStrings`)

```
Why? Template strings give you a readable, concise syntax with proper newlines and string interpolation features.
```

```javascript
# bad
function sayHi(name) {
  return 'How are you, ' + name + '?';
}

# bad
function sayHi(name) {
  return ['How are you, ', name, '?'].join();
}

# bad
function sayHi(name) {
  return `How are you, ${ name }?`;
}

# good
function sayHi(name) {
  return `How are you, ${name}?`;
}
```

* **Never use** `eval()` on a string, it opens too many vulnerabilities.

* Do not unnecessarily escape characters in strings. (`eslint: no-useless-escape`)

```
Why? Backslashes harm readability, thus they should only be present when necessary.
```

```javascript
# bad
const foo = '\'this\' \i\s \"quoted\"';

# good
const foo = "'this' is \"quoted\"";
const foo = `'this' is "quoted"`;
```

##  16. Function

* Use named function expressions instead of function declarations. (`eslint: func-style jscs: disallowFunctionDeclarations`)

```
Why? Function declarations are hoisted, which means that it’s easy - too easy - to reference the function before it is defined in the file. This harms readability and maintainability. If you find that a function’s definition is large or complex enough that it is interfering with understanding the rest of the file, then perhaps it’s time to extract it to its own module! Don’t forget to name the expression - anonymous functions can make it harder to locate the problem in an Error's call stack. ([Discussion](https://github.com/airbnb/javascript/issues/794))
```

```javascript
# bad
const foo = function () {
  // ...
};

# bad
function foo() {
  // ...
}

# good
const foo = function bar() {
  // ...
};
```

* Wrap immediately invoked function expressions in parentheses. (`eslint: wrap-iife jscs: requireParenthesesAroundIIFE`)

```
Why? An immediately invoked function expression is a single unit - wrapping both it, and its invocation parens, in parens, cleanly expresses this. Note that in a world with modules everywhere, you almost never need an IIFE.
```

```javascript
// immediately-invoked function expression (IIFE)
(function () {
  console.log('Welcome to the Internet. Please follow me.');
}());
```

* Never declare a function in a non-function block (`if`, `while`, etc). (`eslint: no-loop-func`)

```javascript
# bad
if (currentUser) {
  function test() {
    console.log('Nope.');
  }
}

# good
let test;
if (currentUser) {
  test = () => {
    console.log('Yup.');
  };
}
```

* **Never** name a parameter `arguments`

```javascript
# bad
function foo(name, options, arguments) {
  // ...
}

# good
function foo(name, options, args) {
  // ...
}
```

* **Never** use `arguments`, opt to use rest syntax `...` instead

```javascript
# bad
function concatenateAll() {
  const args = Array.prototype.slice.call(arguments);
  return args.join('');
}

# good
function concatenateAll(...args) {
  return args.join('');
}
```

* Use default parameter syntax rather than mutating function arguments.

```javascript
# really bad
function handleThings(opts) {
  // No! We shouldn't mutate function arguments.
  // Double bad: if opts is falsy it'll be set to an object which may
  // be what you want but it can introduce subtle bugs.
  opts = opts || {};
  // ...
}

# still bad
function handleThings(opts) {
  if (opts === void 0) {
    opts = {};
  }
  // ...
}

# good
function handleThings(opts = {}) {
  // ...
}
```

* Avoid side effects with default parameters.

```javascript
var b = 1;
# bad
function count(a = b++) {
  console.log(a);
}
count();  // 1
count();  // 2
count(3); // 3
count();  // 3
```

* Always put default parameters last.

```javascript
# bad
function handleThings(opts = {}, name) {
  // ...
}

# good
function handleThings(name, opts = {}) {
  // ...
}
```

* Never use the `Function` constructor to create a new function. (`eslint: no-new-func`)

```javascript
# bad
var add = new Function('a', 'b', 'return a + b');

# still bad
var subtract = Function('a', 'b', 'return a - b');
```

* Spacing in a function signature. (`eslint: space-before-function-paren space-before-blocks`)

```javascript
# bad
const f = function(){};
const g = function (){};
const h = function() {};

# good
const x = function () {};
const y = function a() {};
```

* Never mutate parameters. (`eslint: no-param-reassign`)

```
Why? Manipulating objects passed in as parameters can cause unwanted variable side effects in the original caller.
```
```javascript
# bad
function f1(obj) {
  obj.key = 1;
}

# good
function f2(obj) {
  const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
}
```

* Never reassign parameters. (`eslint: no-param-reassign`)

```javascript
# bad
function f1(a) {
  a = 1;
  // ...
}

function f2(a) {
  if (!a) { a = 1; }
  // ...
}

# good
function f3(a) {
  const b = a || 1;
  // ...
}

function f4(a = 1) {
  // ...
}
```

* Prefer the use of the spread operator `...` to call variadic functions. (`eslint: prefer-spread`)

```
Why? It's cleaner, you don't need to supply a context, and you can not easily compose `new` with `apply`.
```
```javascript
# bad
const x = [1, 2, 3, 4, 5];
console.log.apply(console, x);

# good
const x = [1, 2, 3, 4, 5];
console.log(...x);

# bad
new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));

# good
new Date(...[2016, 8, 5]);
```

* Functions with multiline signatures, or invocations, should be indented just like every other multiline list in this guide: with each item on a line by itself, with a trailing comma on the last item.

```javascript
# bad
function foo(bar,
             baz,
             quux) {
  // ...
}

# good
function foo(
  bar,
  baz,
  quux,
) {
  // ...
}

# bad
console.log(foo,
  bar,
  baz);

# good
console.log(
  foo,
  bar,
  baz,
);
```
