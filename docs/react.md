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
Copyright © 2017 Stanislav Kochenkov 
