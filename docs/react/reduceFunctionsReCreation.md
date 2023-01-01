## React - Reduce functions re-creation

In body of Functional Component each variable will be created again during render.  
It can lead to child re-renders because they will receipt new function each time.  
To improve performance, we should not create renderProps inside functional components  
and avoid re-creation of handlers.

[reactjs.org - useCallback](https://ru.reactjs.org/docs/hooks-reference.html#usecallback)

##### ❌ BAD

```javascript
const MyComponent = (props) => {
  const onClick = (e) => (
    console.log(e)
  );
  const renderContent = () => (
    <span>{props.text}</span>
  );
  return (
    <Header
      onClick={onClick}
      renderContent={renderContent}
    />
  );
};
```

##### ✔ GOOD

```javascript
const onClick = (e) => (
  console.log(e)
);

const MyComponent = (props) => {
  const renderContent = useCallback((
    () => (
      <span>{props.text}</span>
    )
  ), [props.text]);
  return (
    <Header
      onClick={onClick}
      renderContent={renderContent}
    />
  );
};
```

---

[Back to Code Guide - React](https://github.com/UserBug/codeGuide/tree/v2/docs/react)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 