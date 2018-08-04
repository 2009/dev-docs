# Enzyme

[airbnb/enzyme][1]  
[Enzyme Documentation][2]  

Testing utility for React allowing you to shallow render components and giving
you a jQuery API for DOM manipulation and traversal.

Enzyme provides three types of rendering:

* Shallow `shallow()` - renders component only (no children)
* Full `mount()` -  renders component and all children
* Static `render()` - render static HTML

## Setup

[airbnb/enzyme - Installation][3]  
[Create React App: User Guide - Testing Components][4] has details on setting
up enzyme with `create-react-app`  

## Examples

### Check if component exists (props ignored)

```javascript
import React form 'react';
import { shallow } from 'enzyme';
import { Redirect } from 'react-router-dom';

import Foo from './Foo';

it('should render Redirect', () => {
  const subject = shallow(<Foo />);
  expect(
    subject.find(Redirect).exists()
  ).toEq(true);
});
```

### Snapshot Testing

Using [adriantoine/enzyme-to-json][5] setup as jest serializer:

```javascript
import React form 'react';
import { shallow } from 'enzyme';

import Foo from './Foo';

it('renders snapshot', () => {
  const tree = shallow(<Foo />);
  expect(tree).toMatchSnapshot();
});
```

[1]: https://github.com/airbnb/enzyme
[2]: http://airbnb.io/enzyme/
[3]: https://github.com/airbnb/enzyme#installation
[4]: https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#testing-components
