- ![[NG Directive composition]]

- ![[Ng OptimizedImage]]

- Dont need `then` after module import

```ts
{
  path: 'lazy',
  loadComponent: () => import('./lazy-file'), // without then(m => m.LazyComponent),
}
```