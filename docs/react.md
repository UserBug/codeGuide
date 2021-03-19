## React

### All Components must have PropTypes
This basic rule helps to identify and avoid many errors.  
PropTypes provide dynamic typing at the development stage.  
What neither TypeScript nor JSDoc can`t provide.  

```javascript
SomeComponent.propTypes = {
  name: PropTypes.string.isRequired
};
```

[reactjs.org - Typechecking With PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html)  
[eslint - react/prop-types](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prop-types.md)

---

### Dont use destructuring for props
Referring to the ```props``` object helps to easily distinguish the data that came to the component  
from the variables and functions created inside.  

##### ❌ BAD
```javascript
const myButton = ({ type, size, text, changeType }) => {
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

### Use Redux only for common data
Redux is a useful tool, but it has disadvantages.  
Each called action causes a complete copy of the entire storage.  
In an App with only one reducer, this behavior slows the rendering of components insignificantly.  
The slowing increases with each new middleware.  
In addition, careless work with the repository can lead to the accumulation of unnecessary data and memory leaks.  

Therefore, use connection to Redux only if:

* The data needs to be cached.
* The data needs to be saved after the component has been unmount.
* Data is used by 2 or more components that do not have a single close parent in the tree.

For example: User credential, current localization, chat data, company data…  

[redux.js - Using local component state is fine](https://redux.js.org/faq/organizing-state#do-i-have-to-put-all-my-state-into-redux-should-i-ever-use-reacts-setstate)

---

### Save only plain serializable objects in Redux
During operation, Redux can compare storage values or save previous copies of the data.  
Storing reference data can lead to improper operation of reducers and memory leaks.  

[redux.js.org - functions, promises, or other non-serializable](https://redux.js.org/faq/organizing-state#can-i-put-functions-promises-or-other-non-serializable-items-in-my-store-state)

---

### Avoid “connect” of Redux
When some component "connect()" to Redux it create new wrapper,  
this is another component in the tree and another code to execute before rendering.  
All "mapStateToProps" of all components in the application will be called for any action in the application. This often leads to unnecessary rendering.  
Try to use "connect()" only for Compounds like "Page" which are controlled by router and only one of the routes will be displayed.  
Next, pass the data through the flow of "Props".  

---

### Contract value/onChange
Interfaces should be standardized, use properties “onChange” and “value” for the controlled components.  
Using standard names for the properties of the controlled components helps to better understand their purpose,  
eliminates duplicates and zoo of property names.  
For components working with complex entities, 
it is better to specify the form of this entity and return it all in the method “onChange”.  

* Data schema of the “value” must be the same as the data schema returned from “onChange” handler.
* You should put to “value” only data which is the result of User actions or can be changed by the User.

##### ❌ BAD
```javascript
DatePicker.propTypes = {
    onDateChange: PropTypes.func,
    date: PropTypes.string,
}

ProductEditor.propTypes = {
    itemType: PropTypes.string.isRequired,
    onPriceChange: PropTypes.func,
    onNameChange: PropTypes.func,
    price: PropTypes.number,
    name: PropTypes.string.isRequired,
}
```

##### ✔ GOOD 
```javascript
DatePicker.propTypes = {
    onChange: PropTypes.func,
    value: PropTypes.string,
}

ProductEditor.propTypes = {
    itemType: PropTypes.string.isRequired, // User cant change itemType
    onChange: PropTypes.func,
    value: PropTypes.shape({
        price: PropTypes.number.isRequired, // User can change price
        name: PropTypes.string.isRequired, // User can change name
    }).isRequired,
}
```

---

### Always memorize components
To prevent unnecessary rerender of component and increases performance,  
each component should be memorized.  
Use recommended ways:

* shouldComponentUpdate
* extends React.PureComponent (Be careful, PureComponent correctly checks only immutable properties, objects are checked by reference.)
* React.memo

[reactjs.org - shouldComponentUpdate In Action](https://reactjs.org/docs/optimizing-performance.html#shouldcomponentupdate-in-action)

---

### Don't use context
One of the most important reason:  
Parents did not know about context that need for children.  
This can lead to a lack of updates in children.  
Main idea of React is Components, they are "lazy" and react only on Props change.  
(PS: That's why library called "React")  

If you want change something in child Component you should set new Props to it.

* All Props are as clear and visible as possible.  
But the context remains hidden and unseen.  
This leads to a misunderstanding of code and data source on the page,  
which greatly increases the number of bugs and the time to resolve them.
* Props have strict typing and involved in the life cycle of the component.
* Passing data thru props give possibility to use clear ways of memorization.

Context does not have these advantages.

Official React documentation say:  
"If you only want to avoid passing some props through many levels, component composition is often a simpler solution than context."  
[reactjs.org - Before You Use Context](https://reactjs.org/docs/context.html#before-you-use-context)

> After the release of React 16.3, the context became much safer. Despite this, the context should be used only in special exceptional cases.

---

### Functional Components and new functions
In body of Functional Component each variable will be created again during render.  
It can lead to child re renders because they will receipt new function each time.  
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

### Async event handlers
Event-driven the approach implies the presence of an event  
and queue asynchronous event processing using handlers.  
Each event can create new ones,  
but the queue does not wait for a specific response from the handler.  
This means that the return value from the handler must always be void.

At the same time, it is considered a good approach to handle exceptions for each promise.  
The asynchronous handler will return a promise that no one is willing to handle or catch errors.
Therefore, the handler must remain a synchronous function ``` () => void ```.  
Any asynchronous code must be able to catch errors inside the handler.  

[MDN Web Docs - handleEvent](https://developer.mozilla.org/en-US/docs/Web/API/EventListener/handleEvent)  
[Wikipedia - Event driven_programming](https://en.wikipedia.org/wiki/Event-driven_programming)  
[Wikipedia - Event driven_architecture](https://en.wikipedia.org/wiki/Event-driven_architecture)  

##### ❌ BAD
```javascript
const MyComponent = (props) => {
  const onClick = useCallback((
    async () => {
      await logClick(props.id);
      await sendMessageToServer(props.id);
    }
  ), [props.id]);
  return (
    <button onClick={onClick} />
  );
};
```

##### ✔ GOOD
```javascript
const MyComponent1 = (props) => {
  const onClick = useCallback((
    () => {
      logClick(props.id)
        .then(() => (
          sendMessageToServer(props.id)
        ))
        .catch(catchAnyError);
    }
  ), [props.id]);
  return (
    <button onClick={onClick} />
  );
};

const MyComponent2 = (props) => {
  const onClick = useCallback((
    () => {
      (async () => {
        await logClick(props.id);
        await sendMessageToServer(props.id);
      })().catch(catchAnyError)
    }
  ), [props.id]);
  return (
    <button onClick={onClick} />
  );
};
```

---
Copyright © 2017 Stanislav Kochenkov 
