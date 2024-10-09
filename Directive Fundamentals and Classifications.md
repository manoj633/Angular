In Angular, a directive is a class that can modify the structure or behavior of elements in the DOM. Directives are a core feature of Angular and are used to extend the capabilities of HTML by adding custom behavior to elements and components.

### Where Directives are Used

Directives are used in Angular applications to:

1. **Manipulate the DOM**: They can change the appearance or behavior of elements in the DOM.
2. **Add Event Listeners**: Directives can listen to and respond to user events.
3. **Apply Styles and Classes**: They can dynamically apply styles or classes to elements.
4. **Create Reusable Components**: Directives can encapsulate common behavior that can be reused across different parts of an application.

### Types of Directives

Angular provides three main types of directives:

1. **Components**: Technically, components are a type of directive with a template. They are the most common type of directive and are used to create reusable UI components. Components have their own view (HTML template) and logic (TypeScript class).

2. **Structural Directives**: These directives change the structure of the DOM by adding or removing elements. They are typically denoted by an asterisk (*) before the directive name. Common structural directives include:
   - `*ngIf`: Conditionally includes or excludes an element based on a boolean expression.
   - `*ngFor`: Iterates over a collection and creates a template instance for each item.
   - `*ngSwitch`: Switches between different templates based on a value.
   - Read more at [[Structural Directives]]

3. **Attribute Directives**: These directives change the appearance or behavior of an existing element. They are applied as attributes to elements. Common attribute directives include:
   - `ngClass`: Dynamically adds or removes CSS classes.
   - `ngStyle`: Dynamically sets inline styles.
   - `ngModel`: Binds input elements to model properties, enabling two-way data binding.
   - Read more at [[Attribute Directives]]

### Conclusion

Directives are a powerful feature in Angular that allow developers to create dynamic and interactive web applications. By understanding and utilizing the different types of directives, you can enhance the functionality and reusability of your Angular applications.