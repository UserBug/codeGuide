## React Component testing

### Technology stack

##### Test runner
Jest - Allows to run and check test results. Created by Facebook.  
https://facebook.github.io/jest/

##### Unit tests for React Components
Enzyme - Provides a tool to render and manipulate the condition of component.  
Created by Airbnb.  
http://airbnb.io/enzyme/

##### End to End (Functional) testing of React Components
Cypress - Framework for End to End testing of React Applications.  
https://www.cypress.io/

---

### Names and extensions
All tests should be placed in sub-folder ```“__tests__”``` of Component.  
Tests files should have same name as file/function/component and have “*.test.js” in the
end.  
[Configuring Jest](https://jestjs.io/docs/en/configuration.html)
```
myComponent
    __tests__
        MyComponent.test.js
        MyComponentLine.test.js
    MyComponentLine.js
    MyComponent.js
    index.js
```

---

### Use describe and test
All tests should contain root describe function as container for all tests.  
[Jest - describename](https://facebook.github.io/jest/docs/en/api.html#describename-fn)

---

### Test as “black box”
Components should be tested using the “Black Box” method.  
This means that you can only change the values in the public interface, this includes:  
Props, Children, Events, Handlers, (Context in extreme cases).  

Controlling the correctness of the component is also possible only through public output, such as:  
HTML, CSS class names, calls of handlers from Props (onClick, onChange...)  

__We should not check or change state of the component.__  

Do not check methods  
(except for methods that relate directly to the framework: shouldComponentUpdate, componentDidMount… )  

If in the future the internal implementation of the component changes  
(to perform a certain task),  
but it will still correspond to the interface used in the  
application - the tests will be executed successfully.  

[Testing implementation details is a recipe for disaster](https://kentcdodds.com/blog/testing-implementation-details)  
[Testing React components the right way](https://www.valentinog.com/blog/testing-react/#testing-react-components-testing-react-components-the-right-way)  
[testing-library - Guiding Principles](https://testing-library.com/docs/guiding-principles)  

##### ❌ BAD
```javascript
test('Can be hidden', () => {
    const myComponent = mount(<MyComponent hidden={true} />);
    expect(myComponent.state('disabled')).toBe(true);
});

test('Can be hidden', () => {
    const myComponent = mount(<MyComponent />);
    myComponent.setState({ disabled: true });
    expect(myComponent.hasClass('disabled')).toBe(true);
});

test('Display children on Load', () => {
    const myComponent = mount(<MyComponent />);
    myComponent.setState({ items: [{id:1},{id:2}]});
    expect(myComponent.find('div>div>ul').children().length).toBe(2);
});
```

##### ✔ GOOD 
```javascript
test('Can be hidden', () => {
    const myComponent = mount(<MyComponent hidden={true} />);
    expect(myComponent.childAt(0).hasClass('disabled')).toBe(true);
});

test('Display children on Load', () => {
    const myComponent = mount(<MyComponent />);
    myComponent.find('.load-button').first().simulate('click');
    expect(myComponent.find('.list').children().length).toBe(2);
});
```

---

### Don't test Snapshots
Comparing the two parts of the markup can only reveal that they are not the same.  
In most cases, the user doesn't care about the markup. is it ```<div>``` or ```<span>```.  
First of all, tests should check the correctness of behavior and logic of interaction with components.  
Tests based on Snapshots will fail if a minor change is made,  
although the behavior of the component remains correct.  

---

### Use css Classes and "data-testid"
Finding elements by "data-testid" attribute allows you to remove the dependence on nesting.  
In addition, this attribute can be easily removed from the product build using a Babel plugin.  

Unfortunately, we cannot remove the dependency on css Classes.  
Often the presence of a certain class is an important indicator in the behavior of a component.  
However, it is best to minimize their use to find the element.  

[kentcdodds - data-testid query](https://kentcdodds.com/blog/making-your-ui-tests-resilient-to-change#whats-with-the-data-testid-query)  

##### ❌ BAD
```javascript
test('Display children on Load', () => {
    const myComponent = mount(<MyComponent />);
    myComponent.setState({ items: [{id:1},{id:2}]});
    expect(myComponent.find('div>div>ul').children().length).toBe(2);
});
```

##### ✔ GOOD 
```javascript
test('Display children on Load', () => {
    const myComponent = mount(<MyComponent />);
    myComponent.find('[data-testid="load-button"]').first().simulate('click');
    expect(myComponent.find('[data-testid="list"]').children().length).toBe(2);
});
```

---

### Root element of each component should have "data-testid"
"component-***"  
This practice will allow you not only to make functional testing more convenient,  
but also to easily distinguish component blocks in html.  

```javascript
const myBlock = () => (
  <div data-testid="component-myBlock">Block</div>
);
```

---
Copyright © 2017 Stanislav Kochenkov 
