Introduced in 2020 in replace of old View Engine.

- Only compiles what we use (Tree shaking)
- Each component compiles independently (fast build time)
- More readable output - easier to debug
- Improves DI handling


Examples component
```ts
@Component({
  selector: 'app-hello',
  template: `<h1>Hello {{ name }}</h1>`
})
export class HelloComponent {
  name = 'World';
}

```

Becomes something like that
```js
export class HelloComponent {
  constructor() { this.name = 'World'; }
}
HelloComponent.ɵcmp = ɵɵdefineComponent({
  type: HelloComponent,
  template: function(rf, ctx) {
    if (rf & 1) {
      ɵɵelementStart(0, "h1");
      ɵɵtext(1);
      ɵɵelementEnd();
    }
    if (rf & 2) {
      ɵɵtextInterpolate1("Hello ", ctx.name, "");
    }
  }
});

```


## Ivy metadata
ɵcmp - component
ɵfac - factory function for dependency injection

