Name that would fit better would be TuiPortalHostConnector 

[[portal]] - Dynamic component that will be placed on higher dom instead of inititialization place
[[host]] - Place where portals will be places.

Tui portal services - is actully bridge or connector between these two.

So what it does. 
- It has attach(host) method 
- It has add, remove (component/template) functions to host.





## Code 
```ts
@Injectable()  
export abstract class TuiPortalService {  
    protected host?: TuiPortals;  
  
    public attach(host: TuiPortals): void {  
        this.host = host;  
    }  
  
    public add<C>(component: PolymorpheusComponent<C>): ComponentRef<C> {  
        return this.safeHost.addComponentChild(component);  
    }  
  
    public remove<C>({hostView}: ComponentRef<C>): void {  
        this.removeTemplate(hostView);  
    }  
  
    public addTemplate<C>(templateRef: TemplateRef<C>, context?: C): EmbeddedViewRef<C> {  
        return this.safeHost.addTemplateChild(templateRef, context);  
    }  
  
    public removeTemplate<C>(viewRef: EmbeddedViewRef<C> | ViewRef): void {  
        if (!viewRef.destroyed) {  
            viewRef.destroy();  
        }  
    }  
  
    protected get safeHost(): TuiPortals {  
        if (!this.host) {  
            throw new TuiNoHostException();  
        }  
  
        return this.host;  
    }  
}
```
