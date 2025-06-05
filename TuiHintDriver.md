Simple wrapper around [[TuiDriverDirective]] that sends type property to identify driver
```ts

@Directive({  
    standalone: true,  
})  
export class TuiHintDriver extends TuiDriverDirective {  
    public readonly type = 'hint';  
}
```

Whata is ![[TuiDriverDirective]]

## What i would change 
#taiga-contribution 
I would rename it to TuiDriverManagerDirective or TuiDriverMediatorDirective. Cause this directive is not a  driver 

