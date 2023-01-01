## React - Create useful custom hooks

This list of hooks is recommended for creation and use,  
as it has proven to be convenient and effective:

```javascript
ReactMemo(Component, shouldComponentUpdate);
```  

Will memorize any Component by using function ```shouldComponentUpdate(prevProps, nextProps)```.  
shouldComponentUpdate must be stateless function.

```javascript
useComponentDidMount(fn);
```

Will execute argument function only once, when Component did mount.

```javascript
useComponentWillUnmount(fn);
```

Will execute argument function only once, when Component will unmount.

```javascript
useCallbackOnce(fn);
```

Similar to useCallback.  
Will return same function each time, no meter how often component renders.

---

[Back to Code Guide - React](https://github.com/UserBug/codeGuide/tree/v2/docs/react)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 