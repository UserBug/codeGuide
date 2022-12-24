## Common JavaScript

It is recommended to use as a common rules:  
[Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)

### Use Semicolons

When JavaScript encounters a line break without a semicolon,  
it uses a set of rules called Automatic Semicolon Insertion  
to determine whether it should regard that line break as the end of a statement,  
and (as the name implies) place a semicolon into your code before the line break if it thinks so.  
ASI contains a few eccentric behaviors, though,  
and your code will break if JavaScript misinterprets your line break.  
These rules will become more complicated as new features become a part of JavaScript.  
Explicitly terminating your statements and  
configuring your linter to catch missing semicolons will help prevent you from encountering issues.

##### ❌ BAD

```javascript
// Raises exception
const luke = {}
const leia = {}
[luke, leia].forEach((jedi) => jedi.father = 'vader')

const reaction = "No! That’s impossible!"
(async function meanwhileOnTheFalcon() {
    // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
    // ...
}())

// Returns `undefined` instead of the value on the next line - always happens when `return` is on a line by itself because of ASI!
function foo() {
    return
    'search your feelings, you know it to be foo'
}
```

##### ✔ GOOD

```javascript
const luke = {};
const leia = {};
[luke, leia].forEach((jedi) => {
    jedi.father = 'vader';
});

const reaction = "No! That’s impossible!";
(async function meanwhileOnTheFalcon() {
    // handle `leia`, `lando`, `chewie`, `r2`, `c3p0`
    // ...
}());

function foo() {
    return 'search your feelings, you know it to be foo';
};
```

[Airbnb - JS Styleguide - Semicolons required](https://github.com/airbnb/javascript#semicolons--required)  
[Google - JS Styleguide - Semicolons are required](https://google.github.io/styleguide/jsguide.html#formatting-semicolons-are-required)

---

### New variables should contain null

All created, without any known values, new variables should contain null.  
This rule helps to easily distinguish non-existent properties and variables from cleaned or already created but not have
value.

Object.prototype.hasOwnProperty() cannot be conveniently applied to large objects.

It also helps maintain consistency with the server side.  
In queries "undefined" and "null" have different meanings:

- "undefined" - Value not set
- "null" - The value is set as void

[MDN Web Docs - null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)  
[eslint - init-declarations](https://eslint.org/docs/rules/init-declarations)

Combination of:  
[eslint - no-undefined](https://eslint.org/docs/latest/rules/no-undefined)  
[eslint - no-undef-init](https://eslint.org/docs/latest/rules/no-undef-init)  

##### ❌ BAD

```javascript
let a;
const obj = {
    c: undefined,
};

console.log(a) // undefined
console.log(b) // undefined
console.log(obj.c) // undefined
console.log(obj.d) // undefined
```

##### ✔ GOOD

```javascript
let a = null;
const obj = {
    c: null,
};

console.log(a); // null
console.log(b); // undefined
console.log(obj.c); // null
console.log(obj.d); // undefined
```

---

### Use destructuring in functions arguments

If function accept more than one argument use destructuring.

Benefits:

* Eliminates dependence on order of arguments
* Arguments become named

##### ❌ BAD

```javascript
const IN_BOX = 6;
const calculatePrice = (itemPrice, count, discount = 1, balance = 0) => (
  (itemPrice * count * discount) - balance 
);

const price = calculatePrice(
  5,
  IN_BOX,
  1,
  10
);
```

##### ✔ GOOD

```javascript
const IN_BOX = 6;
const calculatePrice = ({ itemPrice, count, discount = 1, balance = 0 }) => (
  (itemPrice * count * discount) - balance 
);

const price = calculatePrice({
    count: IN_BOX,
    itemPrice: 6,
    balance: 10,
});
```

---

### Avoid nested destruction

Retrieving a value from a deep level of an object using destructuring syntax  
has a number of undesirable consequences:

* Finding the paths used to get values from Objects in a project is very difficult.
* Creation of scripts for analyzing and modifying the codebase is difficult.

##### ❌ BAD

```javascript
import someVeryLargeAndMultilevelObject from 'strangeObjectsCollection';

const { varFromLevel1: { varFromLevel2: { varFromLevel3: { varFromLevel4 } }} } = someVeryLargeAndMultilevelObject;

const myObj = { varFromLevel1: { varFromLevel2: 111 } };
```

##### ✔ GOOD

```javascript
import someVeryLargeAndMultilevelObject from 'strangeObjectsCollection';

const varFromLevel4 = someVeryLargeAndMultilevelObject.varFromLevel1.varFromLevel2.varFromLevel3.varFromLevel4;
```

---

### Use arrow functions

in all cases when you don't need context of this particular function.

##### ❌ BAD

```javascript
function sum ({ a, b }) {
    return a + b;
}
```

##### ✔ GOOD

```javascript
const sum = ({ a, b }) => (a + b); // "sum" is named arrow function which has name in stacktrace
```

[Google - JS Styleguide - Features functions arrow functions](https://google.github.io/styleguide/jsguide.html#features-functions-arrow-functions)
[When should I use Arrow functions in ECMAScript 6?](https://stackoverflow.com/questions/22939130/when-should-i-use-arrow-functions-in-ecmascript-6)

---

### Prefer single return

It will be a single place you have to look to trace backwards and figure out what a function returns.  
Easier to debug and easier to modify.  
Multiple returns create interrupts in function execution,  
making it harder to find unused code.

[airbnb - single return vs multiple returns](https://github.com/airbnb/javascript/issues/761)  
[Anthony Steele - Single Return Law](https://www.anthonysteele.co.uk/TheSingleReturnLaw.html)  

##### Opposite opinion

[Szymon Krajewski - Why should you return early?](https://szymonkrajewski.pl/why-should-you-return-early/)  
[Early exit - most common deviation from structured programming](https://en.wikipedia.org/wiki/Structured_programming#Early_exit)  


##### ❌ BAD

```javascript
const sayMyName = (who) => {
  if (who === 'David Guetta') {
    return `${who}: Say my name, say my name\n If you love me, let me hear you.`;
  } else if (who === 'Breaking Bad') {
    return `${who}: You all know exactly who I am. Say my name.`
  }
  return `${who}: I do not know.`;
};
```

##### ✔ GOOD

```javascript
const sayMyName = (who) => {
  let partOfText = `${who}: I do not know.`;
  if (who === 'David Guetta') {
    partOfText = `${who}: Say my name, say my name\n If you love me, let me hear you.`;
  } else if (who === 'Breaking Bad') {
    partOfText = `${who}: You all know exactly who I am. Say my name.`
  }
  return partOfText;
};
```

---

### Use public class fields syntax

Use the constructor only when necessary,  
otherwise define public properties and methods in the class body.

* Reduce amount of code
* Autobinding

[React doc - Handling events](https://reactjs.org/docs/handling-events.html)   
[React doc - Autobinding](https://reactjs.org/docs/react-without-es6.html#autobinding)

##### ❌ BAD

```javascript
class Basket {
  constructor () {
    this.count = 0;
    this.handleAdd = this.handleAdd.bind(this);
  }

  handleAdd({ add }) {
    this.count += add;
  }
}
```

##### ✔ GOOD

```javascript
class Basket {
  count = 0;

  handleAdd = ({ add }) => {
    this.count += add;
  };
}
```

---

### Prefer Promise

Prefer Promise and Async functions instead of Callbacks.  
Async functions as a very powerful tool of JavaScript.   
Each Promise creates a new Microtask which can be executed in the Microtask queue of the Event Loop.   
This architecture allows split calculations on "independent" tasks and does not block the whole Event Loop.   
Callbacks in some cases can create synchronous chains that block the user interface.

[MDN - Using microtasks in JavaScript](https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API/Microtask_guide)

##### ❌ BAD

```javascript
const someAsyncFunction = ({ a, b }, cb) => {
  const businessLogicValue = a + b;
  const onEnd = (result, error) => {
    if(error) {
      cb(null, error);
    } else {
      cb(businessLogicValue * result);
    }
  };
  someCbGlobalIO(businessLogicValue, onEnd)
};

const someAsyncFunction = ({ a, b }, cb) => {
  const businessLogicValue = a + b;
  someAsyncGlobalIO(businessLogicValue)
    .then((result) => {
      cb(businessLogicValue * result);
    }).catch((error) => {
      cb(null, error);
    });
};
```

##### ✔ GOOD

```javascript
const someAsyncFunction = ({ a, b }) => (
  new Promise((res, rej) => {
    const businessLogicValue = a + b;
    const onEnd = (result, error) => {
      if(error) {
        rej(error);
      } else {
        res(businessLogicValue * result);
      }
    };
    someCbGlobalIO(businessLogicValue, onEnd)
  })
);

const someAsyncFunction = async ({ a, b }) => {
  const businessLogicValue = a + b;
  const result = await someAsyncGlobalIO(businessLogicValue);
  return businessLogicValue * result;
};
```

---

### No errors, warnings, logs in console

Developer console is a very powerful and helpful tool.  
It gives information to the developer about the health of the application.  
Any message in there requires attention, and usually some action.  
Errors and warnings are signals about existing bugs in the code.  
Any ticket cannot be closed if there exist those messages in the console.  
Showing some debug data in the consol it is helpful,  
but all this logs should be removed before code review and merge.

[CodeGuide - Split Code - Sustain Single Responsibility](./splitCode/sustainSingleResponsibility.md)  
[CodeGuide - Split Code - Use One "third party API" per file](./splitCode/useOneThirdPartyApiPerFile.md)

[eslint - no-console](https://eslint.org/docs/rules/no-console)  

---

### JSDoc for static typing

**JSDoc** - is a markup language used to annotate JavaScript source code files.  
**TypeScript** - is a programming language.

Benefits of JSDoc:

* Do not affect JavaScript syntax.
* No compilation required.
* As a result, they can be added at any time to any part of the code without additional changes.

**JSDoc** allows you to add static typing of the code while staying with **JavaScript**.

[Google - JS Styleguide - JSDoc](https://google.github.io/styleguide/jsguide.html#jsdoc)
[eslint - require-jsdoc](https://eslint.org/docs/rules/require-jsdoc)  
[Type Safe JavaScript and TypeScript with JSDoc](https://medium.com/@trukrs/type-safe-javascript-with-jsdoc-7a2a63209b76)

---

### Should I use TypeScript?

##### ✔ Objective advantages of TypeScript that are not part of the "HolyWar":

* Syntax similarity to other typed languages
* Small amount of additional syntax constructions which are not included in ECMAScript++

##### ❌ Frequent misconceptions about TypeScript:

* Provides only **Static Type-checking** at the time of writing code. There are no type checks in the compiled code.
  JavaScript can be typed with JSDoc.
* TypeScript it is not ECMAScript. There is absolutely no guarantee that the TypeScript features will be included in the
  next ECMAScript.
* At the moment (2020) there is no reliable and recommended way to run TypeScript for production either in the browser
  or on the server.

**Summary:** The choice between TypeScript and JavaScript most of all depends on your taste preferences.

---

### Forbidden to use any languages other than English in the code.

To display the text in a local language, use the function translator.

Benefits:

* Eliminates any issues with the encoding of files.
* Immediately adds the ability to localize the product.
* Allows you to easily edit any output text without changing the code.
* Reduces the size of the bundle.
* Comments in English show respect for all other developers.

##### ❌ BAD

```javascript
/**
* Показать ошибку если страница недоступна
*/
const renderAlert = () => (
    'الصفحة المطلوبة غير متاحة'
);

const renderWarning = () => (
  'The field did not pass validation'
);
```

##### ✔ GOOD

```javascript
/**
* Show error if page not available
*/
const renderAlert = () => (
  translate('ERROR_PAGE_NOT_AVAILABLE')
);

const renderWarning = () => (
  translate('FIELD_DID_NOT_PASS_VALIDATION')
);
```

---

### Remove unnecessary code

All console logs should be deleted from files before the feature branch can be merged to the develop.  
These unnecessary logs make it difficult for other developers to debug the code and can show private data.

Delete commented out parts of the code.  
Blocks of code in the commentaries make it very difficult to read it and unnecessarily increase the size of the files.

---

### Respect all eslint rules

Eslint is a very important tool in the development. It can be distracting in the beginning, but it allow:

* Check correct syntax.
* Perform static type checking.
* Unify the design of code throughout the project for easy understanding.
* Automatically fix minor problems, such as tabulation, spaces and quotation marks.
* Avoid many errors on writing code stage.

We are using list of Airbnb rules as common base,  
all clarifications and differences should be approved with lead developers and added to the document.

[eslint-plugin-unicorn - eslint-disable](https://github.com/sindresorhus/eslint-plugin-unicorn/blob/main/docs/rules/no-abusive-eslint-disable.md)  

---

### Discuss and describe each new npm package

If your code required some new npm package, you should:

1. Discuss the reasons and need for the package with lead developers.
2. If the package is approved, add it to file "package.md": date, your name and purpose of this package.

This information allows us to understand all project dependencies.  
Next developers can understand tools which are already in the project, and not to add new one.  
If some package will require update or replacement, information will help to find a better solution.

---

### Event handler should not return a promise

Event-driven the approach implies the presence of an event  
and queue asynchronous event processing using handlers.  
Each event can create new ones,  
but the queue does not wait for a specific response from the handler.  
This means that the return value from the handler must always be void.

At the same time, it is considered a good approach to handle exceptions for each promise.  
The asynchronous handler will return a promise that no one is willing to handle or catch errors.
Therefore, the handler must remain a synchronous function ``` () => void ```.  
Any asynchronous code must be able to catch errors inside the handler.

[MDN Web Docs - handleEvent](https://developer.mozilla.org/en-US/docs/Web/API/EventListener/handleEvent)  
[MDN Web Docs - EventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventListener)  
[Wikipedia - Event driven_programming](https://en.wikipedia.org/wiki/Event-driven_programming)  
[Wikipedia - Event driven_architecture](https://en.wikipedia.org/wiki/Event-driven_architecture)

##### ❌ BAD

```javascript
const MyComponent = (props) => {
  const onClick = useCallback((
    async () => {
      await logClick(props.id);
      await sendMessageToServer(props.id);
    }
  ), [props.id]);
  return (
    <button onClick={onClick} />
  );
};
```

##### ❌ BAD

```javascript
const onClick =  async (event) => {
  await logClick(event.someDataFromEvent);
  await sendMessageToServer(event.someDataFromEvent);
};

domElement.addEventListener('click', onClick);
```

##### ✔ GOOD

```javascript
const MyComponent1 = (props) => {
  const onClick = useCallback((
    () => {
      logClick(props.id)
        .then(() => (
          sendMessageToServer(props.id)
        ))
        .catch(catchAnyError);
    }
  ), [props.id]);
  return (
    <button onClick={onClick} />
  );
};
```

##### ✔ GOOD

```javascript
const MyComponent2 = (props) => {
  const onClick = useCallback((
    () => {
      (async () => {
        await logClick(props.id);
        await sendMessageToServer(props.id);
      })().catch(catchAnyError)
    }
  ), [props.id]);
  return (
    <button onClick={onClick} />
  );
};
```

##### ✔ GOOD

```javascript
const onClick =  (event) => {
  (async () => {
    await logClick(event.someDataFromEvent);
    await sendMessageToServer(event.someDataFromEvent);
  })().catch(catchAnyError)
};

domElement.addEventListener('click', onClick);
```

---
Copyright © 2017 Stanislav Kochenkov 
