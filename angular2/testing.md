## `async` vs `fakeAsync`

`async` and `fakeAsync` are two different methods for handling asyncronous actions in tests.

See: [https://angular.io/docs/ts/latest/guide/testing.html#!#synchronous-tests](https://angular.io/docs/ts/latest/guide/testing.html#!#synchronous-tests)

### `async`

Allows you to wrap expectations that rely on testing asyncronous code to delay the expectations evaluation, otherwise the
the test would just complete before the the asyc code being run.

> NOTE: You must have a fixture (componet) to be able to use `asyn` with `.whenStable()` to get this to work

The following example tests a component that makes a async http request to get a random quote, wrapping the test in `async()`
and calling `fixture.whenStable().then()` ensures the expectation `expect(el.textContent).toBe(testQuote);` only gets run
after the async http call has run.

```typescript
it('should show quote after getQuote promise (async)', async(() => {
  fixture.detectChanges();
  fixture.whenStable().then(() => { // wait for async getQuote
    fixture.detectChanges();        // update view with quote
    expect(el.textContent).toBe(testQuote);
  });
}));
```

### `fakeAsync` (recommended)

`fakeAsync` allows you to call a `tick()` method in your test, which will perform any async promises to be called.
This makes your tests syncronous without relying on calling any promises containing expectiation, as well as giving
you the ability to wait for async operation multiple times in a single test.

I recommend using `fakeAsync` over `async` as it removes the need to have async code in your tests and makes them completely
syncronous and easier to understand. You can also directly replace `async` with `fakeAsync` or vice versa.

> NOTE: There is a limitation on using `fakeAsync`, which is that you cannon make any XHR calls from within the `fakeAsync`
> function call, but this should not be needed very often if ever.

The following example tests the same this as above but now using `fakeAsyn` and the `tick()` method. In this test calling
the `tick()` method will cause the test to wait for the asyn call to complete before it continues.

```typescript
it('should show quote after getQuote promise (fakeAsync)', fakeAsync(() => {
  fixture.detectChanges();
  tick();                  // wait for async getQuote
  fixture.detectChanges(); // update view with quote
  expect(el.textContent).toBe(testQuote);
}));
```
