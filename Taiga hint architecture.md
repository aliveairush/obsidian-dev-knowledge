
- Tui hints are initialized in [[tui-root]] as `<tui-hints />`
- [[TuiHintComponent]] 
	- subscribes to hints$ from [[taiga TuiHintService]]
	- show them in foreach in tempalte
- When we add [[Taiga tuiHint Directive]] to a component. We actually marking passed polymorpheus component as  [[taiga tuiAsVehicle]] 
- And when [[taiga TuiHintHover]] will call onHover  [[taiga TuiHintService]] by subscribtion will toggle all assosiated vehicles to toggle(), when toggle(true) happens Hint will be added to [[taiga TuiHintService]]  and [[TuiHintComponent]] will recevice it By observable.

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
- 