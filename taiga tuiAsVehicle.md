Logic behind this compnent the same as [[taiga tuiAsRectAccessor]]


```ts
export abstract class TuiVehicle {  
    public abstract readonly type: string;  
    public abstract toggle(value: boolean): void;  
}  
  
export function tuiAsVehicle(vehicle: Type<TuiVehicle>): ExistingProvider {  
    return tuiProvide(TuiVehicle, vehicle, true);  
}
```

It is short verions of and vehicle had to implement abstract class TuiVehicle
```ts
{
  provide: TuiVehicle,
  useExisting: vehicle,
  multi: true
}
```

## question 
Why did they name it as Vehicle ? I DK. I would raname it to TuiTogglableVehicle
#taiga-contribution
