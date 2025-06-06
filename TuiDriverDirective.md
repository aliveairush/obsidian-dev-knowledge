Interesting architecture solution where directive acts as Bridge between  directive and his plugin directives.
### Code
```ts
export abstract class TuiDriver extends Observable<boolean> {  
    public abstract readonly type: string;  
}  
  
export function tuiAsDriver(driver: Type<TuiDriver>): ExistingProvider {  
    return tuiProvide(TuiDriver, driver, true);  
}  
  
@Directive()  
export abstract class TuiDriverDirective implements AfterViewInit {  
    public abstract type: string;  
  
    private readonly destroyRef = inject(DestroyRef);  
    private readonly drivers: readonly TuiDriver[] =  
        inject<any>(TuiDriver, {self: true, optional: true}) || [];  
  
    private readonly vehicles: readonly TuiVehicle[] = inject<any>(TuiVehicle, {  
        self: true,  
        optional: true,  
    });  
  
    public ngAfterViewInit(): void {  
        const vehicle = this.vehicles?.find(({type}) => type === this.type);  
  
        merge(...this.drivers.filter(({type}) => type === this.type))  
            .pipe(distinctUntilChanged(), takeUntilDestroyed(this.destroyRef))  
            .subscribe((value) => {  
                vehicle?.toggle(value);  
            });  
    }  
}
```

- **type** - should be initialized by core directive example [[Taiga tuiHint Directive]] in hostDirectives.

- **drivers** - array of [[TuiDriver]] (Tui driver is like Plugin) , so it is list of plugins for vehicle 

- **vehicles** - lets take [[Taiga tuiHint Directive]] and [[taiga dropdown]] they both are vehicals. And `<div tuiHint tuiDropdown></div>`, will make so there are 2 vehicles . 
  And when some Driver (Plugin) for example TuiHover emits value we take  Vehicle with same type. And toggle it.
  
  {self:  true, } because we need only directive itself, no need to  search in DI TREE. 

- [[ngAfterViewInit]] - Why exactly that lifecycle subscribtion ? 
	- At this stage all siblings already initialized.
- 