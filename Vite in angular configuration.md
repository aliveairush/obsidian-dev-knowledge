# DONT USE IT
It is quite pain in the ass to make it work using  angular even thou there is a plugin for vite+angular. 

It is still quite not usable.
Simple action: create angular app using [[nx]] and you might see [[vite.config.ts]] file , the thing is , this config file is never used, Fun and interactive experience it was discovering it. 
Angular will still would use [[angular-devkit]] with [[Webpack]]  , so ther is no point using it.


# BUT WHAT IF I WANT VITE?
[[Analog js]] probably is the way , they handled configuring it and powered up with extra features.

But seriously just use it for now in React app for example. 
I found it on 30.05.2025  so maybe next day it will be easier to use vite with angular.


## Detailed answer why not to use it
### Cant generate vite project with nx
Even if we use NX generation 
`npx create-nx-workspace@latest --bundler=vite`

it actually will not use [[Vite]] as builder in result project, in fact it wont even install Vite deps, default 
@angular-devkit/core ([[Webpack]] ) will be used
```json 
"devDependencies": {  
  "@angular-devkit/build-angular": "~19.2.0",  
  "@angular-devkit/core": "~19.2.0",  
  "@angular-devkit/schematics": "~19.2.0",  
  "@angular/cli": "~19.2.0",  
  "@angular/compiler-cli": "~19.2.0",  
  "@angular/language-service": "~19.2.0",  
  "@eslint/js": "^9.8.0",  
  "@nx/angular": "21.1.2",  
  "@nx/eslint": "21.1.2",  
  "@nx/eslint-plugin": "21.1.2",  
  "@nx/js": "21.1.2",  
  "@nx/web": "21.1.2",  
  "@nx/workspace": "21.1.2",  
  "@schematics/angular": "~19.2.0",  
  "@swc-node/register": "~1.9.1",  
  "@swc/core": "~1.5.7",  
  "@swc/helpers": "~0.5.11",  
  "@typescript-eslint/utils": "^8.19.0",  
  "angular-eslint": "^19.2.0",  
  "eslint": "^9.8.0",  
  "eslint-config-prettier": "^10.0.0",  
  "nx": "21.1.2",  
  "prettier": "^2.6.2",  
  "tslib": "^2.3.0",  
  "typescript": "~5.7.2",  
  "typescript-eslint": "^8.19.0"  
}
```

If we ran `npx create-nx-workspace@latest` it will make us choose builder, we can specify [[esbuild]] and assumption can be , maybe it can create vite config, BUT no It will still be using default 
@angular-devkit/core (Webpack ) .

So there is no fast way to create angular app with vite builder using nx. Looks like Bug.




### Just nodes of configuration
nx 

- Move index html one folder before in application packages
- Problem dont forget to     <script type="module" src="/src/main.ts"></script>
- 
