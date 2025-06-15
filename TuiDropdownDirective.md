



## Code
```ts
@Directive({  
    standalone: true,  
    selector: '[tuiDropdown]:not(ng-container):not(ng-template)',  
    providers: [  
        tuiAsRectAccessor(TuiDropdownDirective),  
        tuiAsVehicle(TuiDropdownDirective),  
    ],  
    exportAs: 'tuiDropdown',  
    hostDirectives: [  
        TuiDropdownDriverDirective,  
        {  
            directive: TuiDropdownPosition,  
            outputs: ['tuiDropdownDirectionChange'],  
        },  
    ],  
    host: {  
        '[class.tui-dropdown-open]': 'ref()',  
    },  
})
export class TuiDropdownDirective  
    implements  
        AfterViewChecked,  
        OnDestroy,  
        OnChanges,  
        TuiPortalItem,  
        TuiRectAccessor,  
        TuiVehicle  
{  
    private readonly refresh$ = new Subject<void>();  
    private readonly service = inject(TuiDropdownService);  
    private readonly cdr = inject(ChangeDetectorRef);  
  
    // Just making Sure TuiDrivers are initialized as array
    private readonly drivers = coerceArray(  
        inject(TuiDropdownDriver, {  
            self: true,  
            optional: true,  
        }),  
    );  
  
    protected readonly sub = this.refresh$  
        .pipe(throttleTime(0, tuiZonefreeScheduler()), takeUntilDestroyed())  
        .subscribe(() => {  
            this.ref()?.changeDetectorRef.detectChanges();  
            this.ref()?.changeDetectorRef.markForCheck();  
        });  
  
    public readonly el = tuiInjectElement();  
    public readonly type = 'dropdown';  
    public readonly component = new PolymorpheusComponent(  
        inject(TUI_DROPDOWN_COMPONENT),  
        inject(INJECTOR),  
    );  
  
    public ref = signal<ComponentRef<unknown> | null>(null);  
    public content: PolymorpheusContent<TuiContext<() => void>>;  
  
    @Input()  
    public set tuiDropdown(content: PolymorpheusContent<TuiContext<() => void>>) {  
        this.content =  
            content instanceof TemplateRef  
                ? new PolymorpheusTemplate(content, this.cdr)  
                : content;  
    }  
  
    public get position(): 'absolute' | 'fixed' {  
        return tuiCheckFixedPosition(this.el) ? 'fixed' : 'absolute';  
    }  
  
    public ngAfterViewChecked(): void {  
        this.refresh$.next();  
    }  
  
    public ngOnChanges(): void {  
        if (!this.content) {  
            this.toggle(false);  
        }  
    }  
  
    public ngOnDestroy(): void {  
        this.toggle(false);  
    }  
  
    public getClientRect(): DOMRect {  
        return this.el.getBoundingClientRect();  
    }  
  
    public toggle(show: boolean): void {  
        const ref = this.ref();  
  
        if (show && this.content && !ref) {  
            this.ref.set(this.service.add(this.component));  
        } else if (!show && ref) {  
            this.ref.set(null);  
            this.service.remove(ref);  
        }  
  
        this.drivers.forEach((driver) => driver?.next(show));  
  
        // TODO: Remove in v5, only needed in Angular 16  
        this.cdr.markForCheck();  
    }  
}
```