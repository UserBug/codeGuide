### Split Code - Move Out Nested callbacks

A program of any complexity will most likely need to manage several asynchronous operations at various levels of
concurrency.  
A common pitfall that is easy to fall into is nesting callbacks, which makes:

* Difficult to read code
* It is difficult to understand from which level data is taken through closures.

Therefore, it is recommended to allow only 1 level of nesting.
Deeper nesting can be fixed by
[Dependency injection](https://en.wikipedia.org/wiki/Dependency_injection) through
[Higher-order function](https://en.wikipedia.org/wiki/Higher-order_function#JavaScript).

`max-nested-callbacks: ["error", 1]`  
[eslint - max-nested-callbacks](https://eslint.org/docs/latest/rules/max-nested-callbacks)
`consistent-function-scoping: ["error"]`  
[eslint-plugin-unicorn - consistent-function-scoping](https://github.com/sindresorhus/eslint-plugin-unicorn/blob/main/docs/rules/consistent-function-scoping.md)  

##### ❌ BAD

```javascript
const addHandlers = (elements) => {
    // Root level 
    elements.forEach((element) => {
        // Nested callback - 1 level 
        const pageId = element.getAttribute('pageId');
        element.addEventListener('click', () => {
            // Nested callback - 2 level 
            getPageText(pageId).then((text) => {
                // Nested callback - 3 level 
                console.log(`Text of ${pageId}: ${text}`);
            }).catch((error) => {
                // Nested callback - 3 level 
                console.error(`Fetch error for ${pageId}`, error);
            });
        });
    });
};
```

##### ✔ GOOD

```javascript
const getAndSwowPage = (pageId) => {
    // Root level 
    getPageText(pageId).then((text) => {
        // Nested callback - 1 level 
        console.log(`Text of ${pageId}: ${text}`);
    }).catch((error) => {
        // Nested callback - 1 level 
        console.error(`Fetch error for ${pageId}`, error);
    });
};

const createOnClickHandler = (pageId) => {
    // Root level 
    const onClickHandlerToShowPage = () => {
        // Nested callback - 1 level 
        getAndSwowPage(pageId);
    };
    return onClickHandlerToShowPage;
};

const addHandlers = (elements) => {
    // Root level 
    elements.forEach((element) => {
        // Nested callback - 1 level 
        const pageId = element.getAttribute('pageId');
        element.addEventListener(
            'click',
            createOnClickHandler(pageId)
        );
    });
};
```