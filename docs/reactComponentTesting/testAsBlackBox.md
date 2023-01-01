## React Component testing - Test as “black box”

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

[Back to Code Guide - React Component testing](https://github.com/UserBug/codeGuide/tree/v2/docs/reactComponentTesting)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 