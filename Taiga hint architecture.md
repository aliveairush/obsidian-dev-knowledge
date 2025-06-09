
- Tui hints are initialized in [[tui-root]] as `<tui-hints />` so it becomes [[portal]] container 
- [[TuiHintsComponent]] 
	- subscribes to hints$ from [[taiga TuiHintService]]
	- show them in foreach in tempalte
- When we add [[Taiga tuiHint Directive]] to element. We actually marking content as polymopheus component . And  our hint  is  [[taiga tuiAsVehicle]] . And providing  [[TuiHintCompnent]] for hint view.
- And when [[taiga TuiHintHover]] emits value ,  [[TuiHintDriver]] will toggle all assosiated vehicles to toggle(), when toggle(true) happens Hint will be added to [[taiga TuiHintService]]  list, and [[TuiHintsComponent]] will recevice it By subscribing to observable.

By that Taiga gets very flexible architecture.

## But animations
The second most hard thing is animations, and how taiga-ui deals with on destroy animation. When we toggle off hint , it will be destroyed. But what about animation on destroy?

We need to deep dive in [[TuiAnimatedParent Directive]]
- Tui animated parent is set on general tui-hints component template
  ```html
  <div  
    *ngFor="let hint of hints"  
    role="tooltip"  
    tuiAnimatedParent  
    [tuiActiveZoneParent]="hint.activeZone || null"  
>  
    <ng-container *polymorpheusOutlet="hint.component; context: {$implicit: hint}" />  
</div>
```
- When polymorpheusOutlet changes , [[TuiAnimatedParent Directive]] checks it using [[MutationObserver]] . If content changes it deletes tui-enter class. And nominates content for deleting, (actual removal is not happening)

## Lets compare it with Angular Material
[[Angular Material]]
The main limitaion is Material hint only supports string as input.

If you  need to make it  more Generic you will have to craete your custom overlays. Or use some 3rd party library.

And you will see fat directive almoust 1000 lines  of code. Because it contains everything inside one directive.
