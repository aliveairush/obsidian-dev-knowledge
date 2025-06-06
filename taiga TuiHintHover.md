

Most interisting in this directive is how it provides Driver (Plugin) for [[Taiga tuiHint Directive]]

This code   providers: [tuiAsDriver(TuiHintHover)] will mark TuiHintHover as Driver (Plugin) with type 'hint' and it will be added to drivers list in [[TuiDriverDirective]]]

Also it provides [[TuiHoveredService]]

## What it does
It extends of TuiDriver (so it extends observable) and for that it has parent constuctor which accepts stream as parameter. So its [[pure observable-based state service]].
And it immidiately subscribed. So when **stream$** (i would rename it to visibilityStream) emits value [[TuiDriverDirective]] will catch event and will toggle Vehicles with same type .


### hint with inner hint
When we hover on an item, parent hint should be visible too.
```ts
  
    public toggle(visible = !this.visible): void {  
        this.toggle$.next(visible);  
        this.parent?.toggle(visible);  
    }  
  
```

## Cool code
#cool-code

Move it to another link [[rxjs mutually interraptable streams combination]]



## Code 
```ts
@Directive({  
    standalone: true,  
    providers: [tuiAsDriver(TuiHintHover), TuiHoveredService],  
    exportAs: 'tuiHintHover',  
})  
export class TuiHintHover extends TuiDriver {  
    private readonly isMobile = inject(TUI_IS_MOBILE);  
    private readonly el = tuiInjectElement();  
    private readonly hovered$ = inject(TuiHoveredService);  
    private readonly options = inject(TUI_HINT_OPTIONS);  
    private visible = false;  
    private readonly toggle$ = new Subject<boolean>();  
    private readonly stream$ = merge(  
        this.toggle$.pipe(  
            switchMap((visible) =>  
                this.isMobile  
                    ? of(visible)  
                    : of(visible).pipe(delay(visible ? 0 : this.tuiHintHideDelay)),  
            ),  
            takeUntil(this.hovered$),  
            repeat(),  
        ),  
        this.hovered$.pipe(  
            switchMap((visible) =>  
                this.isMobile  
                    ? of(visible)  
                    : of(visible).pipe(  
                          delay(visible ? this.tuiHintShowDelay : this.tuiHintHideDelay),  
                      ),  
            ),  
            takeUntil(this.toggle$),  
            repeat(),  
        ),  
    ).pipe(  
        filter(() => this.enabled),  
        map(  
            (value) =>  
                value &&  
                (this.el.hasAttribute('tuiHintPointer') || !tuiIsObscured(this.el)),  
        ),  
        tap((visible) => {  
            this.visible = visible;  
        }),  
    );  
  
    private readonly parent = inject(TuiHintHover, {  
        optional: true,  
        skipSelf: true,  
    });  
  
    @Input()  
    public tuiHintShowDelay: TuiHintOptions['showDelay'] = this.options.showDelay;  
  
    @Input()  
    public tuiHintHideDelay: TuiHintOptions['hideDelay'] = this.options.hideDelay;  
  
    public readonly type = 'hint';  
  
    public enabled = true;  
  
    constructor() {  
        super((subscriber) => this.stream$.subscribe(subscriber));  
    }  
  
    public toggle(visible = !this.visible): void {  
        this.toggle$.next(visible);  
        this.parent?.toggle(visible);  
    }  
  
    public close(): void {  
        this.toggle$.next(false);  
    }  
}
```



#taiga-contribution 
Add interface TuiHintHoverStrategy 
and add custom classes TuiHintHoverMobileStraregy , and default WebStrategy
with function delay. 

And import     delay(this.strategy.delay(...)) ,     map(() => this.strategy.shouldShow(this.el))

So we use [[Open Closed]] principle. Class is closed but open to modification, and each modification can be changed without touching class itselft

#taiga-contribution 
I would add option to disable parent propagation 

