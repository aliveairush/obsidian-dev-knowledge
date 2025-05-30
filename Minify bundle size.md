
Install
`npm install --save-dev source-map-explorer`

Build project
`nx build d3-tree-demo --configuration=production --source-map
`
Run analyzer
`npx source-map-explorer dist/apps/d3-tree-demo/browser/main.*.js
`

Search for heavy packages and try to get rid of them or minify usage.

