```ts
@Component({
  selector: 'mat-menu',
  hostDirectives: [HasColor, {
    directive: CdkMenu,
    inputs: ['cdkMenuDisabled: disabled'],
    outputs: ['cdkMenuClosed: closed']
  }]
})
class MatMenu {}
```