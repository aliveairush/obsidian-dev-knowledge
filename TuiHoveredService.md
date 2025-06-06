Its [[pure observable-based state service]]

It is simple service that is used as a state of stream that emits only  mouseenter, and mouseleave events.

We take this events in [[taiga TuiHintHover]] directive and do some operations. 

```ts
@Injectable()  
export class TuiHoveredService extends Observable<boolean> {  
    private readonly el = tuiInjectElement();  
    private readonly zone = inject(NgZone);  
  
    private readonly stream$ = merge(  
        tuiTypedFromEvent(this.el, 'mouseenter').pipe(map(TUI_TRUE_HANDLER)),  
        tuiTypedFromEvent(this.el, 'mouseleave').pipe(map(TUI_FALSE_HANDLER)),  
        // Hello, Safari  
        tuiTypedFromEvent(this.el, 'mouseout').pipe(  
            filter(movedOut),  
            map(TUI_FALSE_HANDLER),  
        ),  
    ).pipe(distinctUntilChanged(), tuiZoneOptimized(this.zone));  
  
    constructor() {  
        super((subscriber) => this.stream$.subscribe(subscriber));  
    }  
}
```

## Interesting code used in it
- [[tuiZoneOptimizer()]]