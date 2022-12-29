## JavaScript - Use destructuring in functions arguments

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
const calculatePrice = ({itemPrice, count, discount = 1, balance = 0}) => (
    (itemPrice * count * discount) - balance
);

const price = calculatePrice({
    count: IN_BOX,
    itemPrice: 6,
    balance: 10,
});
```

---

[Back to CodeGuide - JavaScript](https://github.com/UserBug/codeGuide/tree/v2/docs/javaScript)

[Back to CodeGuide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 