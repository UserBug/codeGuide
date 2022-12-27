## JavaScript - Use only English in code

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

[Back to CodeGuide - JavaScript](https://github.com/UserBug/codeGuide/tree/v2/docs/javaScript/index.md)

[Back to CodeGuide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 