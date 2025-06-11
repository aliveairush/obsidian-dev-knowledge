It is host element for cretaed portal using [[TuiDropdownDirective]]

What it does: 
- It porvides TuiDropdownService as TuiPortalService for DI tree.
- And just makes placeholder by <ng-container #viewContainer />

```ts
@Component({  
    standalone: true,  
    selector: 'tui-dropdowns',  
    template: '<ng-container #viewContainer />',  
    changeDetection: ChangeDetectionStrategy.OnPush,  
    providers: [tuiAsPortal(TuiDropdownService)],  
    host: {style: 'position: absolute; width: 100%; top: 0'},  
})  
export class TuiDropdowns extends TuiPortals {}
```