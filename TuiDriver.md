This is just an abstract class which extends Observable 
```ts
export abstract class TuiDriver extends Observable<boolean> {  
    public abstract readonly type: string;  
}
```

It just tells to some implementing class that we need to specify `type` property.

And also 

Usage for example in [[taiga TuiHintHover]]