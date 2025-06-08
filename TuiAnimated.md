
1) Getting instance of renderer to access his private methods (This is not angular way to do it , becouse it  prone to errors if some angular verion will change inner logic, it is even possible that they wont describe it in changelog, because it is private logic)
```ts
    private readonly renderer = inject(ViewContainerRef)._hostLView?.[11];  
```
2) Constructing   animation logic 
```ts
        const renderer = this.renderer.delegate || this.renderer;  
```
Trying to access AnimationRenderer - AnimationRenderer is accessable in delegate 

3) Accessing private properties like removeChild function , and data objects (taiga stores there objects that are nominated for tui-leave animations)
```ts
const {removeChild, data} = renderer;
```

4) If data aleady has TUI_LEAVE list in it , then we just push current element to that list.
```ts
        if (data[TUI_LEAVE]) {  
            data[TUI_LEAVE].push(this.el);  
  
            return;  
        }  
        data[TUI_LEAVE] = [this.el];  
```
 Else we assign new list only with current element.

5) afterNextRender(() => { ...logic })

[[afterNextRender]]




## CODE
```ts
@Directive({  
    standalone: true,  
    selector: '[tuiAnimated]',  
    host: {  
        class: TUI_ENTER,  
        '(animationend.self)': 'remove()',  
        '(animationcancel.self)': 'remove()',  
    },  
})  
export class TuiAnimated implements OnDestroy {  
    private readonly el = tuiInjectElement();  
    private readonly app = inject(ApplicationRef);  
  
    // @ts-ignore https://github.com/angular/angular/blob/main/packages/core/src/render3/interfaces/view.ts#L56  
    private readonly renderer = inject(ViewContainerRef)._hostLView?.[11];  
  
    constructor() {  
        console.log('\n TuiAnimated - Constructor', this.el)  
        if (!this.renderer) {  
            console.log('\n TuiAnimated - Missing renderer')  
  
            return;  
        }  
  
        // delegate is used in Angular Animations renderer  
        const renderer = this.renderer.delegate || this.renderer;  
        const {removeChild, data} = renderer;  
  
        if (data[TUI_LEAVE]) {  
            console.log('\n TuiAnimated - Renderer has tui-leave data , so just adding 1 element and calling return');  
            data[TUI_LEAVE].push(this.el);  
  
            return;  
        }  
  
        data[TUI_LEAVE] = [this.el];  
  
        afterNextRender(() => {  
            console.log('**<b>After nex Render</b> **')  
            this.remove();  
  
            renderer.removeChild = (parent: Node, el: Node, host?: boolean) => {  
                console.log('**<b>removeChild Callback</b> **')  
  
                const remove = (): void => removeChild.call(renderer, parent, el, host);  
                const elements: Element[] = data[TUI_LEAVE];  
                const element = elements.find((leave) => el.contains(leave));  
                const {length} = element?.getAnimations() || [];  
  
                if (!element) {  
                    remove();  
  
                    return;  
                }  
  
                elements.splice(elements.indexOf(element), 1);  
                element.classList.add(TUI_LEAVE);  
  
                const animations = element.getAnimations();  
                const last = animations[animations.length - 1];  
                const finish = (): void => {  
                    if (!parent || parent.contains(el)) {  
                        remove();  
                        this.app.tick();  
                    }  
                };  
  
                if (animations.length > length && last) {  
                    last.onfinish = finish;  
                    last.oncancel = finish;  
                } else {  
                    remove();  
                }  
            };  
        });  
    }  
  
    public ngOnDestroy(): void {  
        const data = this.renderer?.data || {[TUI_LEAVE]: []};  
  
        setTimeout(() => {  
            data[TUI_LEAVE] = data[TUI_LEAVE].filter((e: Element) => e !== this.el);  
        });  
    }  
  
    protected remove(): void {  
        if (this.el.isConnected && !this.el.getAnimations().length) {  
            console.log('Remove tui enter class')  
            this.el.classList.remove(TUI_ENTER);  
        }  
    }  
}
```