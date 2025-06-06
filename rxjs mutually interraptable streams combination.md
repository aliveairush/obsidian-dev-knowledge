It is not an official term, just to remember it somehow situation where 
## Real code examples
### [[taiga TuiHintHover]]

Hover has 2 streams toggle$ and hovered$
When user toggles (clicks) object, **hovered**$ stream will finish because of [[rxjs takeUntil(obs$)]] and recreated by [[rxjs repeat()]].
When users hovers object it will finish **toggle$** stream  and he too will be recreated .


Hover has code 
```ts
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
```
