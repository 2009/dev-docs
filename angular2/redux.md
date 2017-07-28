# Redux & ngrx

## When to use

See the following article by redux creator Dan Abramov: [You Might Not Need Redux][1] and [The Case for Flux][4]

* Extraneous Props (when you are passing props down through components and those components don't use the prop)
* Data that is needed in multiple places of your app
* Multiple actors (server, websockets, end-user etc) that will mutate the data

## Why use immutable state in Angular?

See this article by Victor Savkin: [Immutability vs Encapsulation][5]

## Libraries

### Redux/PlainJS
[reselect](https://github.com/reactjs/reselect) - Simple selector library

### ngrx
[ngrx/store](https://github.com/ngrx/store)

### ngrx example apps
[ngrx/example-app](https://github.com/ngrx/example-app)
[aviabird/angularspree](https://github.com/aviabird/angularspree) - spree written in angular 2 and ngrx
[ddellamico/ionic2-conference-app](https://github.com/ddellamico/ionic2-conference-app) - ionic2 conference app but written with jwt auth and ngrx

## Resources

* [You Might Not Need Redux][1]
* [Angular Service Layers: Redux, RxJs and Ngrx Store - When to Use a Store And Why?][2]
* [I Always Seem to Need Redux][3]

[1]: https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367
[2]: http://blog.angular-university.io/angular-2-redux-ngrx-rxjs/
[3]: https://medium.com/@silvenon/i-always-seem-to-need-redux-f37686c23e45
[4]: https://medium.com/swlh/the-case-for-flux-379b7d1982c6
[5]: https://vsavkin.com/immutability-vs-encapsulation-90549ab74487
