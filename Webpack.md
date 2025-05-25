## Webpack in angular
When we use `ng build`
it uses
`@angular-devkit/build-angular:browser`
which is wrapper around Webpack

Tasks
- Bundles
- Loads angular decorators @Component
- [[AOT compilation]] - by `@ngtools/webpack`
- Dev server with live load - via `webpack-dev-server`
- Minification, optimization
- Code splitting , lazy load
- Tree-shaking - works with [[Ivy]]


But we can configure webpack by 
`npm install @angular-builders/custom-webpack
`
*angular.json*
```json
"architect": {
  "build": {
    "builder": "@angular-builders/custom-webpack:browser",
    "options": {
      "customWebpackConfig": {
        "path": "./webpack.config.js"
      }
    }
  }
}
```

## Features
- i18n support  - complete support by `@angular/localize`, `ngxi18n` etc
- Comes out of the box in angular
- 
