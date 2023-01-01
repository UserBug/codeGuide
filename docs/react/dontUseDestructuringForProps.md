## React - Dont use destructuring for props

Referring to the ```props``` object helps to easily distinguish the data that came to the component  
from the variables and functions created inside.

In components with more than 400 lines,
it is very difficult to understand what data comes from properties/state/vars.

It is easy to confuse a local variable with a property and apply unacceptable operations (for example object mutations).

There is no clear arguments to determine how deep to destructure properties:

[eslint - react/destructuring-assignment - never](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/destructuring-assignment.md)

##### ❌ BAD

```javascript
const Users = ({ users: { data: { main: { id } } } }) => {};
```

When destructuring, it is possible to set default values. Should be used defaultProps:

##### ❌ BAD

```javascript
const Users = ({ max = 10, isReadOnly = false, orderBy = 'id' }) => {}
```

##### ❌ BAD

```javascript
const MyButton = ({ type, size, text, changeType }) => {
  const [ stateCount, setStateCount ] = useState(0);
  const afterText = stateCount ? String(stateCount) : 'No count';
  const handleClick = useFunction(() => {
    setStateCount((count) => {
      if(count === 3) {
        changeType('3');
      }
      return count++;
    });
  }, [changeType]);

  return (
    <button
      type={type}
      size={size}
      onClick={handleClick}
    >{text} {afterText}</button>
  );
};
```

##### ✔ GOOD

```javascript
const myButton = (props) => {
  const [ stateCount, setStateCount ] = useState(0);
  const afterText = stateCount ? String(stateCount) : 'No count';
  const handleClick = useFunction(() => {
    setStateCount((count) => {
      if(count === 3) {
        props.changeType('3');
      }
      return count++;
    });
  }, [props.changeType]);

  return (
    <button
      type={props.type}
      size={props.size}
      onClick={handleClick}
    >{props.text} {afterText}</button>
  );
};
```

---

[Back to Code Guide - React](https://github.com/UserBug/codeGuide/tree/v2/docs/react)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 