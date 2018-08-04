# Redux

* [] TODO devtools extention

## Example Apps

[gothinkster/realworld][4]  
[reactjs/redux/tree/master/examples][6]  

## `connect` from `react-redux`

TODO

## Testing

[Redux - Writing Tests][2]  
[tylercollier/redux-form-test][5] - testing react-redux-form library  

[markerikson/react-redux-links][7] - massive amount of article links w/
descriptions  


### Connected Components

[Redux: Writing Tests - Connected Components][10]  
[Testing a React-Redux app using Jest and Enzyme][9] - Connected Component
Section  


TODO
  - test plain component by exporting it
  - test interaction with react using `redux-mock-store` or Provider

#### Testing the (Dumb) Component

This requires you to export the component and connected component separatly.

```javascript
TODO
```

You can then just import the component into your test and test it as usual.

#### Testing using `redux-mock-store`

TODO

#### Testing using `<Provider>`

TODO

#### Integration Testing Notes

TODO
- higher level
- test the component ignoring actions etc and only test the result


---


There are couple of methods for testing connected components:

* Test (dumb) component and connected component separately
* Test connected component using [`react-mock-store`][8]
* Test connected component using actual store

#### Separately

Here we test the dumb component in isolation and then test the connected
component using the `react-mock-store` method.

```javascript
// Isolated Component Test

import React from 'react';
import { shallow } from 'enzyme';

describe('Foo', () => {

  it('should display the message', () => {
    const subject = shallow(<Foo message="Display me!" />);
    expect(
      subject.contains("<p>Display me!</p>")
    ).toBe(true);
  });

});
```

#### Using `react-mock-store`

TODO example

#### Using Actual Store

This is essentially and itegration test for the connected component.

TODO blah! is this even a good idea!
- with actual store you can't check an action is called unless you
are using 'redux-thunk' and mock out the action creator with jest.fn()
- 

```javascript
const store = configureStore();

it('should call the login action', () => {
  let actions;

  const subject = shallow(
    <LoginPage onLogin={onLogin} />
  );
  subject.find('#login-button').simulate('click');
  expect(onLogin).toHaveBeenCalled();


  
  actions = store.getActions();

});

### Mock Action

[Jest - Mock Implementations][3]

```
// Import the action
import { login } from './actions/authentication';

// Mock the actions module
jest.mock('./actions/authentication');

// Replace the login action with fake action
login.mockImplementation(() => ({ type: 'ignore' }));
```

## FAQs

### Where should my “business logic” go?

[Split between action creators and reducers](https://redux.js.org/faq/code-structure#how-should-i-split-my-logic-between-reducers-and-action-creators-where-should-my-"business-logic"-go)


[2]: https://github.com/reactjs/redux/blob/master/docs/recipes/WritingTests.md
[3]: https://facebook.github.io/jest/docs/en/mock-functions.html#mock-implementations
[4]: https://github.com/gothinkster/realworld
[5]: https://github.com/tylercollier/redux-form-test
[6]: https://github.com/reactjs/redux/tree/master/examples
[7]: https://github.com/markerikson/react-redux-links/blob/master/react-redux-testing.md#redux
[8]: https://github.com/arnaudbenard/redux-mock-store
[9]: https://medium.com/netscape/testing-a-react-redux-app-using-jest-and-enzyme-b349324803a9
[10]: https://redux.js.org/recipes/writing-tests#connected-components
