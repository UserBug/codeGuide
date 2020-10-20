## React

#### All Components must have PropTypes
This basic rule helps to identify and avoid many errors.  
PropTypes provide dynamic typing at the development stage.  
What neither TypeScript nor JSDoc can`t provide.  

```javascript
SomeComponent.propTypes = {
  name: PropTypes.string.isRequired
};
```

[reactjs.org - Typechecking With PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html)

---

#### Use Redux only for common data
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

#### Save only plain serializable objects in Redux
During operation, Redux can compare storage values or save previous copies of the data.  
Storing reference data can lead to improper operation of reducers and memory leaks.  

[redux.js.org - functions, promises, or other non-serializable](https://redux.js.org/faq/organizing-state#can-i-put-functions-promises-or-other-non-serializable-items-in-my-store-state)

---

#### Avoid “connect” of Redux
When some component "connect()" to Redux it create new wrapper,  
this is another component in the tree and another code to execute before rendering.  
All "mapStateToProps" of all components in the application will be called for any action in the application. This often leads to unnecessary rendering.  
Try to use "connect()" only for Compounds like "Page" which are controlled by router and only one of the routes will be displayed.  
Next, pass the data through the flow of "Props".  

---


---
Copyright © 2017 Stanislav Kochenkov 
