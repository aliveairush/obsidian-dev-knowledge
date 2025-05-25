Rollup is a JS Bundler.

Used mainly in production.

## Features
- Tree shaking - removes unsed code (dead imports) from final bundle
- ESM (EcmaScript modules) first - works with modern *import/export* syntax.
- Great for libraries - creates small optimized outputs.

Example JS library . Rullup take source files and produce:
```
dist/
 ├── index.js        # ESM output
 ├── index.cjs.js    # CommonJS output
 └── index.d.ts      # TypeScript definitions

```

CommonJs - older `requier()` module system, mostly for Node.js

