Offical docs https://v17.angular.io/guide/svg-in-templates


We can create something like that
![[Angular svg as template ex.png]]
Code base 
```html
<svg width="420" [attr.height]="barHeight * chartItems().length + (barGap * chartItems().length)">  
  @for (bar of chartItems(); track bar.name; let index = $index) {  
    <g class="_bar-item" (click)="$$activeIndex.set(index)" [class._active]="$$activeIndex() === index">  
      <rect [attr.width]="bar.count * 10" [attr.y]="index * (barHeight + barGap)" [attr.height]="barHeight" fill="steelblue" />  
      <text [attr.x]="bar.count * 10 + 5" [attr.y]="index * (barHeight + barGap) + barHeight * 0.75">{{ bar.name }}</text>  
    </g>  }  
</svg>
```

Component
```ts
@Component({  
  selector: 'app-svg-chart-bar',  
  imports: [],  
  templateUrl: './svg-chart-bar.component.svg',  
  styleUrl: './svg-chart-bar.component.scss'  
})  
export class SvgChartBarComponent {  
  chartItems = input.required<Array<{count: number, name: string}>>();  
  
  barHeight = 20;  
  barGap = 2;  
  
  $$activeIndex = signal<number | null>(null)  
}
```

Scss
```scss
._bar-item._active {  
  rect {  
    fill: orange;  
  }  
  text {  
    fill: orange;  
  }  
}  
  
._bar-item {  
  cursor: pointer;  
}
```

## Ex 2 
We can check component library in angular-monorepo . Lib to create balanced tree using angular

