Web Components - in simple words you write in angular but create js code that can be attached as widget. 

In nerdy way:
Web Components are a set of standardized browser APIs that allow developers to create **reusable, encapsulated custom elements** using:
- **Custom Elements**: Define your own HTML tags.
- **Shadow DOM**: Encapsulation of styles and DOM structure.
- **HTML Templates**: Reusable content templates.

## Use cases
- Third party widget distribution 
- Legacy app migration
 - Embedding angular to non angular project
- Gradual migration

## Drawbacks
- Heavy bundle size - take a lot of angular with some litle widget
- No ssr (means no seo)
- ShadowDom issues 
- Limited angular features


## Summary
*avoid Angular Web Components unless you really must*.

Use them only when all these apply:
- You already have the logic written in Angular.
- You must embed Angular-based UI into non-Angular apps.
- The consumers don’t care about bundle size or performance.
- Your team doesn’t have time to reimplement it in something lighter.


## Practice task
Write angular web component , deploy it, and add to some React project.
And write it in [[Lit]] . And compare bundle size ...