The name is kind of missleading, if i could name it longer i would name it **tuiAnimateOnChildrenChange**

It has directive WaMutationObserver is angular wrapper under [[MutationObserver]]

But first before getting events from it we confgure providers telling to watch for every child 
1) Watch for childs (Child is dynamic component)
```ts
providers: [provideMutationObserverInit({childList: true})],
```
2) Add two directives [[TuiAnimated Directive]] , and WaMutationObserver itself plus make waMutationObserver event visible in directive
3) when host waMutationObserver event occurs we call `handle()` method

4)  handle logic is 
	1) When hosts children are changes we remove tui-enter class to stop animation on onter
	2) All children elements will be added to `this.renderer.data[TUI_LEAVE]` list , this is just like nominated objects to be removed. The actual removal is not happening. 
	   #tui-doc One more example how the function does not tell anything what it does in reality

But main thing is that it has [[TuiAnimated]] , it is applied to the parent as well.

## Code 
```ts
@Directive({  
    standalone: true,  
    selector: '[tuiAnimatedParent]',  
    providers: [provideMutationObserverInit({childList: true})],  
    hostDirectives: [  
        TuiAnimated,  
        {  
            directive: WaMutationObserver,  
            outputs: ['waMutationObserver'],  
        },  
    ],  
    host: {  
        '(waMutationObserver)': 'handle()',  
    },  
})  
export class TuiAnimatedParent {  
    private readonly el = tuiInjectElement();  
    private readonly renderer = inject(Renderer2);  
  
    protected handle(): void {  
        this.el.classList.remove(TUI_ENTER);  
        this.renderer.data[TUI_LEAVE] = Array.from(this.el.children);  
    }  
}
```