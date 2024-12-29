Attribute directives in Angular are used to modify the appearance or behavior of a DOM element. Unlike structural directives, which change the DOM layout by adding or removing elements, attribute directives only affect the element they are applied to.

### Key Characteristics of Attribute Directives

1. **Purpose**: Attribute directives are primarily used to change the styling or behavior of elements. They can manipulate the DOM by changing styles, classes, or attributes dynamically.

2. **Usage**: They are applied to elements as attributes, hence the name. You can think of them as custom attributes that you can create to encapsulate behavior.

3. **Lifecycle**: Like components, attribute directives have a lifecycle. They can implement lifecycle hooks such as `ngOnInit`, `ngOnChanges`, and `ngOnDestroy` to perform actions at different stages of their existence.
### Types of Attribute Directives

1. **Built-in Attribute Directives**: Angular provides some built-in attribute directives like `ngClass`, `ngStyle`, and `ngModel`.

   - **ngClass**: Adds and removes a set of CSS classes.
   - **ngStyle**: Adds and removes a set of styles.
   - **ngModel**: Binds an input, select, textarea, or custom form control to a property on the scope.
   - Read more at [[Built-in Attribute directives]]

2. **Custom Attribute Directives**: These are user-defined directives that encapsulate custom behavior. The `HighlightDirective` example above is a custom attribute directive.
### Creating an Attribute Directive

To create an attribute directive, you need to define a class and decorate it with the `@Directive` decorator. Here's a step-by-step guide:

1. **Generate a Directive**: You can use Angular CLI to generate a directive.
   ```bash
   ng generate directive highlight
   ```

2. **Define the Directive**: In the generated directive file, you will define the behavior of the directive.

   ```typescript
   import { Directive, ElementRef, Renderer2, HostListener } from '@angular/core';

   @Directive({
     selector: '[appHighlight]'
   })
   export class HighlightDirective {

     constructor(private el: ElementRef, private renderer: Renderer2) {}

     @HostListener('mouseenter') onMouseEnter() {
       this.highlight('yellow');
     }

     @HostListener('mouseleave') onMouseLeave() {
       this.highlight(null);
     }

     private highlight(color: string) {
       this.renderer.setStyle(this.el.nativeElement, 'backgroundColor', color);
     }
   }
   ```

   - **ElementRef**: This is used to access the DOM element that the directive is applied to.
   - **Renderer2**: This is used to safely manipulate the DOM. It provides methods like `setStyle` to change styles.
   - **HostListener**: This decorator listens to events on the host element. In this example, it listens for `mouseenter` and `mouseleave` events to change the background color.

3. **Use the Directive**: Apply the directive to an element in your template.

   ```html
   <p appHighlight>Hover over this text to see the highlight effect.</p>
   ```



### Conclusion

Attribute directives are a powerful feature in Angular that allow you to encapsulate and reuse behavior across your application. By understanding how to create and use them, you can enhance the interactivity and appearance of your Angular applications.