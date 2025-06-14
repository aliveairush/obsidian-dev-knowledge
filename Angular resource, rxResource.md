
## Study
Source: https://push-based.io/article/everything-you-need-to-know-about-the-resource-api?ref=angularspace.com

```ts
todoResource = resource({ request: this.todoId, loader: ({ request: todoId }) => { 
		return fetch( `https://jsonplaceholder.typicode.com/todos/${todoId}`, )
			.then((res) => res.json() as Promise<Todo>); }, 
});

```