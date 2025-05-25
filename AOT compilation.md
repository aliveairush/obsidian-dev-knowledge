Ahead of time Compilation 
Angular pre-compiles templates and decorators during build time.

Why?
- Faster startup (No need to parse template in browser)
- No need to ship angular compiler in browser (Smaller bundle)

Related topics  [[JIT compliation]] 
[[AOT vs JIT]]


## How Ivy work together with AOT

`ng build --prod`

1. Ivy compile components to `ɵcmp`, `ɵfac`, etc
2. Uses AOT to transform all templates + decorators into JS
3. Removes Angular Compiler from final bundle
4. Output optimized JS to run in the browser
