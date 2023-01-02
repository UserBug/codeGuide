## React Component testing - Use css Classes and "data-testid"

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

[Back to Code Guide - React Component testing](https://github.com/UserBug/codeGuide/tree/v2/docs/reactComponentTesting)

[Back to Code Guide - Readme](https://github.com/UserBug/codeGuide/tree/v2)

---
Copyright © 2017 Stanislav Kochenkov 