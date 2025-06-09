Main thing is `    private readonly hints$ = inject(TuiHintService);  `

It watches hints list and subscribes to changs 

```ts
@Component({  
    standalone: true,  
    selector: 'tui-hints',  
    imports: [NgForOf, PolymorpheusOutlet, TuiActiveZone, TuiAnimatedParent],  
    templateUrl: './hints.template.html',  
    styleUrls: ['./hints.style.less'],  
    // So that we do not force OnPush on custom hints  
    // eslint-disable-next-line @angular-eslint/prefer-on-push-component-change-detection    changeDetection: ChangeDetectionStrategy.Default,  
    host: {  
        'aria-live': 'polite',  
    },  
})  
export class TuiHints implements OnInit {  
    private readonly hints$ = inject(TuiHintService);  
    private readonly destroyRef = inject(DestroyRef);  
    private readonly cdr = inject(ChangeDetectorRef);  
  
    protected hints: readonly TuiPortalItem[] = [];  
  
    public ngOnInit(): void {  
        // Due to this view being parallel to app content, `markForCheck` from `async` pipe  
        // can happen after view was checked, so calling `detectChanges` instead        this.hints$.pipe(takeUntilDestroyed(this.destroyRef)).subscribe((hints) => {  
            this.hints = hints;  
            this.cdr.detectChanges();  
        });  
    }  
}
```


Html
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

 
Maybe small change is that aria-live is hardcoded, it could be changable, if we what 'assertive' aria-live.
Thou polite is aleaady good strategy by default (It says screen reader not to interrupt on content change). But nah,  dont think it is good to mention.