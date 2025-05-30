

## Esbuild + Taiga cant be friends
import styles in esbuild causes issues
`"node_modules/@taiga-ui/core/styles/taiga-ui-fonts.less",`

```json
"build": {  
  "executor": "@angular-devkit/build-angular:application",  
  "outputs": [  
    "{options.outputPath}"  
  ],  
  "options": {  
    "outputPath": "dist/apps/taiga-ui-kit-usage",  
    "index": "apps/taiga-ui-kit-usage/src/index.html",  
    "browser": "apps/taiga-ui-kit-usage/src/main.ts",  
    "polyfills": [  
      "zone.js"  
    ],  
    "tsConfig": "apps/taiga-ui-kit-usage/tsconfig.app.json",  
    "inlineStyleLanguage": "scss",  
    "assets": [  
      {  
        "glob": "**/*",  
        "input": "apps/taiga-ui-kit-usage/public"  
      },  
      {  
        "glob": "**/*",  
        "input": "node_modules/@taiga-ui/icons/src",  
        "output": "assets/taiga-ui/icons"  
      }  
    ],  
    "styles": [  
      "node_modules/@taiga-ui/core/styles/taiga-ui-theme.less",  
      "apps/taiga-ui-kit-usage/src/styles.scss"  
    ],  
    "scripts": []  
  },
```