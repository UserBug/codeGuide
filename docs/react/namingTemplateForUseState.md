## React - Naming template for useState

To clearly identify the variables working with the state, we should use prefixes:  
```state***``` and ```setState***```

##### ❌ BAD

```javascript
const [count, setCount] = useState(0);
```

##### ✔ GOOD

```javascript
const [stateCount, setStateCount] = useState(0);
```

---

[Back to Code Guide - React](https://github.com/UserBug/codeGuide/tree/v2/docs/react)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 