# Redux

## Async Actions

See this stack overflow answer: [How to dispatch a redux action with a timeout][1]

[Redux - Async Actions](https://redux.js.org/advanced/async-actions)  
[gaearon/redux-thunk](https://github.com/gaearon/redux-thunk) - good examples on use  
[redux-saga/redux-saga](https://github.com/redux-saga/redux-saga) - if thunk is not enough  

## Presentation (dumb) & Container (smart) Components

### Presentational / Dumb / Component

Responsible for how things look.

- Contains styles
- Get data through props
- Minimal state (only state relating to presentation)


### Container / Smart

Responsible for how things work.

- Don't contain styles
- Very minimal HTML
- Handles data and state managment

[Smart and Dumb Components - Dan Abramov](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)

## Testing

[Redux - Writing Tests][2]

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


[1]: https://stackoverflow.com/questions/35411423/how-to-dispatch-a-redux-action-with-a-timeout/35415559#35415559
[2]: https://github.com/reactjs/redux/blob/master/docs/recipes/WritingTests.md
[3]: https://facebook.github.io/jest/docs/en/mock-functions.html#mock-implementations
