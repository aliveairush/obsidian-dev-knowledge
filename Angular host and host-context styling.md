Imagine ther is two scenarious and you want to style component as display: block'

Well we simply write: 
```css 
:host {
	display: block;
	padding: 2rem;
}
```

**THE PROBLEM**
if we would reuse this item for example in modal , these 2 rem padding could be not needed.

So we can write 
```scss
:host(.contained) {
	display: block;
	padding: 2rem;
}

// so when we want to use our host we write
<app-comp class="contained" />
// styles would apply
```

But it is a lot of code duplication, and we might need these styles always but add possibility to disable it.

```scss
:host {
	display: block;
	border: 1px solid #ffffff;
}

:host-context(.model) {
	border: none;
}
// Now default styles would apply always but in some scenarios, if we want to use it for example in modal we add class .modal
<app-comp class="modal" />
```



