It is a simple function for example used in [[Taiga tuiHint Directive]]

This function accepts some 

```ts
  
export function tuiAsRectAccessor(accessor: Type<TuiRectAccessor>): ExistingProvider {  
    return tuiProvide(TuiRectAccessor, accessor, true);  
}
```

**accessor** - is a class that should have implemented TuiRectAccessor 
![[Taiga TuiRectAccessor]]

So basicly if we will use **tuiAsRectAccessor** on our component typescript will tell use to implement **TuiAccessor**


# General purpose
It is just wrapper for type safety. And it  [[DRY]] principle


When we use this function , it will provide **TuiRectAccessor** to injection tree, and use class we send ass **accessor** , and when some other component will ask for **TuiRectAccessor** he will get **accessor** component.

We can even ignore that function and just write, app will behave same way. It does not add much except type safety and less repeatable code.  
```ts
{
  provide: TuiRectAccessor,
  useExisting: TuiHintDirective,
  multi: true
}
```

