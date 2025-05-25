Craeted by Evan You (author of Vue.js) - April 2020 in response of slow webpack. Name comes from french 'fast'.


## Core features
- Dev mode - fast transpilation , serves raw esm files using [[Esbuild]].
- Production mode tree-shakes  using [[Rollup]]
- Monification - fast execution by [[Esbuild]]

### Comparison to Webpack
- Dev startup - No bundling at all. Uses native ES Modules in the browser. !Webpack bundles whole app.
- Hot module reload - Fast. Only reloads changed module. !Webpack rebuilds - and then patches changes.
- Build time (Prod) - Fast uses [[Rollup]], but may not be faster than webpack.
- Transpilation fast - Uses [[Esbuild]] written in Go , faster . *Webpack* uses Babel or angular-compiler, ts-loader

## What it uses
Uses [[Esbuild]] under the hood for better dev experience, and for Prod transpilation and  code minifications.

For prod uses [[Rollup]] for great production build 


## Vite in angular
Vite does not natively understands angular, so it is done by [[Analog js]] by plugin `@analogjs/vite-plugin-angular`

What plugin does
- Detects angular decorators and parses them using NGC (Angular compiler)
- Runs AOT (Ahead of time compilation) = uses `@angular/compiler`
- Handles templates and styles
- Outputs ES modules - for HMR
- Uses esbuild - form typescript transpilation 

So plugin acts as angular compiler