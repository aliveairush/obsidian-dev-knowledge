- Types forms

- Page title accessibility 
```ts
const routes: Routes = [{
  path: 'home',
  component: HomeComponent
  title: 'My App - Home'  // <-- Page title
}, {
  path: 'about',
  component: AboutComponent,
  title: 'My App - About Me'  // <-- Page title
}];
```

- inject function

- prorected fields in component
```ts
@Component({
  selector: 'my-component',
  template: '{{ message }}',  // Now compiles!
})
export class MyComponent {
  protected message: string = 'Hello world';
}
```