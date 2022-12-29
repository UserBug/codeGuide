## JavaScript - Prefer Promise

Prefer Promise and Async functions instead of Callbacks.  
Async functions as a very powerful tool of JavaScript.   
Each Promise creates a new Microtask which can be executed in the Microtask queue of the Event Loop.   
This architecture allows split calculations on "independent" tasks and does not block the whole Event Loop.   
Callbacks in some cases can create synchronous chains that block the user interface.

[MDN - Using microtasks in JavaScript](https://developer.mozilla.org/en-US/docs/Web/API/HTML_DOM_API/Microtask_guide)

##### ❌ BAD

```javascript
const someAsyncFunction = ({a, b}, cb) => {
    const businessLogicValue = a + b;
    const onEnd = (result, error) => {
        if (error) {
            cb(null, error);
        } else {
            cb(businessLogicValue * result);
        }
    };
    someCbGlobalIO(businessLogicValue, onEnd)
};

const someAsyncFunction = ({a, b}, cb) => {
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
const someAsyncFunction = ({a, b}) => (
    new Promise((res, rej) => {
        const businessLogicValue = a + b;
        const onEnd = (result, error) => {
            if (error) {
                rej(error);
            } else {
                res(businessLogicValue * result);
            }
        };
        someCbGlobalIO(businessLogicValue, onEnd)
    })
);

const someAsyncFunction = async ({a, b}) => {
    const businessLogicValue = a + b;
    const result = await someAsyncGlobalIO(businessLogicValue);
    return businessLogicValue * result;
};
```

[Back to CodeGuide - JavaScript](https://github.com/UserBug/codeGuide/tree/v2/docs/javaScript)

[Back to CodeGuide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 