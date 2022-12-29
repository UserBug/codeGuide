## JavaScript - Event handler should not return a promise

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
[MDN Web Docs - EventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventListener)  
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
        <button onClick={onClick}/>
    );
};
```

##### ❌ BAD

```javascript
const onClick = async (event) => {
    await logClick(event.someDataFromEvent);
    await sendMessageToServer(event.someDataFromEvent);
};

domElement.addEventListener('click', onClick);
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
        <button onClick={onClick}/>
    );
};
```

##### ✔ GOOD

```javascript
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
        <button onClick={onClick}/>
    );
};
```

##### ✔ GOOD

```javascript
const onClick = (event) => {
    (async () => {
        await logClick(event.someDataFromEvent);
        await sendMessageToServer(event.someDataFromEvent);
    })().catch(catchAnyError)
};

domElement.addEventListener('click', onClick);
```

---

[Back to CodeGuide - JavaScript](https://github.com/UserBug/codeGuide/tree/v2/docs/javaScript)

[Back to CodeGuide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 