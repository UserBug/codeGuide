## React Hooks

### Basics
As a first step please read article from Facebook:  
[reactjs - Hooks rules](https://reactjs.org/docs/hooks-rules.html)  

* Don’t call Hooks inside loops, conditions, or nested functions.
* Only Call Hooks from React Functions
* A custom Hook is a JavaScript function whose name starts with ”use” and that may call other Hooks.

---

### Naming of useState
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

### Hooks as independent files
All Hooks should be implemented as independent functions and files.  
What benefits from it:

* The size of the component has been reduced, which increases its readability.
* Component logic is divided into clear blocks with human-readable names.
* All dependencies of each logic block are clearly distinguished,  
hidden closures become explicit arguments.
* With the increase in business logic, each hook can be independently scaled.
* Initially declares the hook as a block of logic that can be reused.
* Such an implementation is a declarative programming approach that  
helps to separate actions from their implementation practices.

##### ❌ BAD
```javascript
const MyForm = (props) => {
  const [stateItemName, setStateItemName] = useState(props.defaultItemName);
  const setItemName = useCallback((stringFromInput) => {
    setStateItemName(
      props.prefix && String(stringFromInput).indexOf(props.prefix) !== 0 ? (
        `${props.prefix}${stringFromInput}`
      ) : (stringFromInput)
    );
  }, [props.prefix]);

  return (
    <input value={stateItemName} onChange={setItemName} />
  );
};
```

##### ✔ GOOD 
```javascript
/**
 * @param {String} defaultItemName
 * @param {String} [prefix]
 * @return {[String, Function]}
 */
const useStateItemName = ({ defaultItemName, prefix = '' }) => {
  const [stateItemName, setStateItemName] = useState(defaultItemName);
  const setItemName = useCallback((stringFromInput) => {
    setStateItemName(
      prefix && String(stringFromInput).indexOf(prefix) !== 0 ? (
        `${prefix}${stringFromInput}`
      ) : (stringFromInput)
    );
  }, [prefix]);

  return [stateItemName, setItemName];
};

export default useStateItemName;
```

```javascript
import useStateItemName from './useStateItemName';

const MyForm = (props) => {
    const [itemName, setItemName] = useStateItemName({
        defaultItemName: props.defaultItemName,
        prefix: props.prefix,
    });
    return (
      <input value={itemName} onChange={setItemName} />
    );
};
```

---

### Useful custom hooks
This list of hooks is recommended for creation and use,  
as it has proven to be convenient and effective:

> ##### ReactMemo(Component, shouldComponentUpdate)
> Will memorize any Component by using function shouldComponentUpdate(prevProps, nextProps).  
> shouldComponentUpdate should be stateless function.

> ##### useComponentDidMount(fn)
> Will execute argument function only once, when Component did mount.

> ##### useComponentWillUnmount(fn)
> Will execute argument function only once, when Component will unmount.

> ##### useCallbackOnce(fn)
> Similar to useCallback.  
> Will return same function each time, to meter how often component renders.

---
Copyright © 2017 Stanislav Kochenkov 
