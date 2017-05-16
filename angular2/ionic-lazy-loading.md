## Ionic NavController

The normal way of navigation to a new page in ionic is to import the page
and use the `NavController` to push the new page onto the stack.

```typescript
import { HomePage } from './pages/home.page';

//...

this.navCtrl.push(HomePage);
```

With `HomePage` being an ordinary angular component:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'page-home',
  template: '<h1>HomePage</h1>'
})
export class HomePage {
  constructor() {}
}
```

And included in `declarations` and `entryComponents` in the module it needs access to:

```
@NgModule({
  declarations: [
    HomePage,
  ],
  entryComponents: [
    HomePage,
  ]
})
```

> Note: The page must be put in `entryComponents` to tell angular it must load the component,
> this is because we are not using the component anywhere in our views.


## Ionic Lazy Loading

To lazy load pages we first must create a module for the page and add the `@IonicPage` decorator
to the component.

```typescript
@NgModule({
  declarations: [
    HomePage,
  ],
  import: [
    IonicPageModule.forChild(HomePage),
    SomeComponentModule,
    SomeOtherComponentModule,
  ],
  export: [
    HomePage,
  ]
})
```

```typescript
import { Component } from '@angular/core';
import { IonicPage } from 'ionic-angular';

_@IonicPage()_
@Component({
  selector: 'page-home',
  template: '<h1>HomePage</h1>'
})
export class HomePage {
  constructor() {}
}
```

We all imports for the page (including in the app module) and replace all references to the class with the string for the page:

```typescript
this.navCtrl.push(_'HomePage'_)
```

