
Component will look up for it is own provider, 

The main feature is that with this annotation , service will be created for each component instance.

```js
export class AppComponent {
	constructo(@Self() private logger: LogerService) {}
}
```