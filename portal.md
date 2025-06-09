## In web
It means that component will be displayed not where it was initialized, so it teleports threw the portal . Portal logic is usually done by service , and a component that initialized in root. 
For example how it is done in [[Taiga UI]]
```html
<div class="t-root-content"><ng-content /></div>  
<ng-container *ngIf="top()">  
    <tui-scroll-controls  
        *ngIf="scrollbars"  
        class="t-root-scrollbar"  
    />  
    <tui-popups />    <ng-content select="tuiOverContent" />  
    <tui-dialogs />    <ng-content select="tuiOverDialogs" />  
    <tui-alerts />    <ng-content select="tuiOverAlerts" />  
    <tui-dropdowns />    <ng-content select="tuiOverDropdowns" />  
    <tui-hints />    <ng-content select="tuiOverHints" />  
</ng-container>
```

Here we can see that hints , are displayed not in the main content. But hint was declared in <ng-content> but displayed in <tui-hint> . So hint was teleported. so it will be above other components.

