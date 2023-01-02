## React - Store hooks in separated files

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

Related: [Code Guide - Split Code - Sustain Single Responsibility](https://github.com/UserBug/codeGuide/tree/v2/docs/splitCode/sustainSingleResponsibility.md)

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
        <input value={stateItemName} onChange={setItemName}/>
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
const useStateItemName = ({defaultItemName, prefix = ''}) => {
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
        <input value={itemName} onChange={setItemName}/>
    );
};
```

---

[Back to Code Guide - React](https://github.com/UserBug/codeGuide/tree/v2/docs/react)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 