## React - Use onChange/value contract

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

[Back to Code Guide - React](https://github.com/UserBug/codeGuide/tree/v2/docs/react)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 