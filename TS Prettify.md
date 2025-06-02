It is not TS type but to create one is just 1 minute of work.
## IMPORTANT
**!! IMPORTANT it Woeks only in VS Code , cause it has computed type calculation**

## Example
```ts
/**  
 * !!! THIS SHOULD BE IN EVERY PROJECT */
 * export type Prettify<T> = {  
  [K in keyof T]: T[K]  
} & {}  
  
type SomeWierdType = {  
  a: number,  
  b: string;  
  
} & {  
  c: string,  
} & {  
  d: string[]  
}  
  
/**  
 * When you hover on params its quite mess to identify whatis going on */function fn(params: SomeWierdType) {  
  return null;  
}  
  
/**  
 * Nice and clean readable formats when we hover on `params' * @param params  
 */  
function prettifiedFn(params: Prettify<SomeWierdType>) {  
  return null;  
}
```