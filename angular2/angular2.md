## Style Guides

[Typescript](https://github.com/Microsoft/TypeScript/wiki/Coding-guidelines)
[Angular 2](https://angular.io/styleguide)

Use codelyzer to check your projects: [codelyzer](https://www.npmjs.com/package/codelyzer)
See codelyzer-ionic.md on details.

## Developing Libraries

* [Packaging Angular](https://www.youtube.com/watch?v=unICbsPGFIA) - Talk on how you should package your angular library to be compatible and aot compatible with angular apps.
* [Angular Package Format (DOC)](https://docs.google.com/document/d/1CZC2rcpxffTDfRDs6p1cfbmKNLA6x5O-NtkJglDaBVs) - Official Google Doc specifying the format of packages angualar libraries.

* [Setting up mutliplatform NPM packages](http://2ality.com/2017/04/setting-up-multi-platform-packages.html)  

### Providing build module files

The Angular Package Format recommends the following combination of module format and ES versions
be provided by your libraries:

* ESM+ES2015 (FESM15) - Webpack (Optimized with features like [Tree-Shaking](https://webpack.js.org/guides/tree-shaking/)), Closure Compiler
* ESM+ES5 (FESM5) - Webpack, Angular CLI, Rollup
* UMD - Plunker, Fiddle, ES5, script tag, Node.js
* ESM+d.ts - Typescript
* .metadata.json - Angular AOT compilation

There are a few ways of building the following formats, below I have listed some options:

* UMD - Webpack
* ESM+ES2015 / ESM+ES5 / ESM+d.ts - Typescript compiler (`tsc`) or Angular compiler (`ngc`)
* .metadata.json - Angular compiler (`ngc`)

> Using the typescript/angular compiler means you will have to have to use __inline__ templates and styles.  

#### Using `templateUrl` and `styleUrl` with the Typescript / Angular compiler

If we want to use `templateUrl`, `styleUrl` or perform any additional processing of our files (such as using
SASS) we must have an alternative build task to perform this for us.

> NOTE: For SASS you could use SASS build tools and provide a single file the consumer of your library can import.

[How to create an angular 2 library](http://www.dzurico.com/how-to-create-an-angular-library/) - setup with support for `templateUrl` and `styleUrl`  
[Inline resources script from Angular Material 2](https://github.com/angular/material2/blob/master/tools/gulp/packaging/inline-resources.ts)  

##### Can't we just use webpack?

No, this is because webpack is a javascript bundler. Webpack will handle all sorts of files if we want our
output to be a `UMD` module, but if we want ESM modules we are out of luck.

#### Glossary

* UMD - provides *comonjs*, *AMD* modules and can be included in the browser via a global window variable.
* ESM - ECMAScript modules
* ES5 - Current ECMAScript standard
* FESM5 / FESM15 - ESM modules flatened into a single file
* ES2015 - New ECMAScript features including rocket syntax
* d.ts - Typescript definition files
* .metadata.json - produced by the angular compiler, used for angular AOT
[Setting up mutliplatform NPM packages](http://2ality.com/2017/04/setting-up-multi-platform-packages.html)  

### Seed Projects/Generators for libraries

#### [filipesilva/angular-quickstart-lib](https://github.com/filipesilva/angular-quickstart-lib)

__Pros__

* Inlines HTML and CSS allowing you to use `templateUrl` and `styleUrl` in components
* Uses the Angular Package Format for builds
* Integration folder for testing build app
* Demo folder for testing
* Testing setup with karma and jasmine

__Cons__

* Pollutes `src` folder with `js` and `js.map` files during build and serve.
* Demo uses systemjs requiring you to explicitly map your imports for node modules

#### [mattlewis92/generator-angular-library](https://github.com/mattlewis92/generator-angular-library)

__Pros__

* Demo folder for testing
* Testing setup with karma, mocha and chai

__Cons__

* Does not provide Flat ESM modules (see Angular Package Format link above)
* Does not support `templateUrl` or `styleUrl`
* Only supports inline CSS
* Does not support assets
