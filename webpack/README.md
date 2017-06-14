# Webpack

> Webpack is a _module bundler_ for modern JavaScript applications. When webpack
> processes your application, it recursively builds a dependency graph that
> includes every module your application needs, then packages all of those
> modules into a small number of bundles - often only one - to be loaded by the
> browser.

These bundles can then be included straight in your `index.html` and work in the browser.

Webpack only understands javascript and processes any `require()`/`import` statement to
bundle your code into a small bundles.
Adding __Loaders__ allows you transform other files webpack does not understand into
modules it can use, this allows you to `require()`/`import` things like `css` and `html`.
This lets you make assets in your project webpacks concern rather than your browsers.
__Loaders__ also can transform your code, e.g. compiling typscript or scss, before it
is bundled together.

[Awesome Webpack - Curated Resource List](https://github.com/webpack-contrib/awesome-webpack)  

[Webpack Concepts](https://webpack.js.org/concepts/)  
[Webpack Gudes](https://webpack.js.org/guides/)  

[Setting up mutliplatform NPM packages](http://2ality.com/2017/04/setting-up-multi-platform-packages.html)  

## With Angular 4

> NOTE: For angular AOT (Ahead-of-Time Compilation) you must use `ngc` (angular compiler).  
> This means if you need to process any additional assets (SCSS, images) you must have
> an alternative build task to handle this.

[Angular Guide: Webpack Introduction](https://angular.io/docs/ts/latest/guide/webpack.html) - Good introduction to the parts of webpack config and setting webpack up with angular 2. Provides examples with different environments and testing with karma.  
[Angular Guide: Deployment](https://angular.io/guide/deployment) - Lists different deployment methods for angular 4 apps, with a list of optimizations that can be performed.  

[How to create an angular 2 library](http://www.dzurico.com/how-to-create-an-angular-library/) - setup with support for `templateUrl` and `styleUrl`  
[Angular2 AOT with Webpack and Lazy Loading](http://www.dzurico.com/angular-aot-webpack-lazy-loading/) - setup  

### Tools

[@ngtools/webpack](https://github.com/angular/angular-cli/tree/master/packages/%40ngtools/webpack) - Angular Ahead-of-Time Webpack Plugin  
[angular2-template-loader](https://github.com/TheLarkInn/angular2-template-loader) - replaces `styleUrl` and `templateUrl` with module require  

