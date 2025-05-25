Or SSR


Flow
1. Server (node.js) renders Html of angular app
2. Browser receives html immidiately (Faster paint)
	1. But! Buttons are non-interactive , routing is broken.
3. Angular hydrates ([[hydration]]) the app. It loads Js bundle , finds Dom elements and attaches event listeners to interactible elements. So app becomes normal SPA.


## Improvements done
[[Angular event replay]]

## Simple example
Create project in angular using ssr, and routing
```
npx nx g @nx/angular:app angular-ssr-example
```

