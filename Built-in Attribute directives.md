Angular provides several built-in attribute directives that allow you to manipulate the appearance and behavior of DOM elements. Here are some of the most commonly used built-in attribute directives:

### 1. `ngClass`

The `ngClass` directive allows you to dynamically add or remove CSS classes from an element.

**Example:**

```html
<div [ngClass]="{'active': isActive, 'disabled': isDisabled}">
  This div's classes change based on component properties.
</div>
```

In this example, the `active` class will be applied if `isActive` is `true`, and the `disabled` class will be applied if `isDisabled` is `true`.

### 2. `ngStyle`

The `ngStyle` directive allows you to dynamically set CSS styles on an element.

**Example:**

```html
<div [ngStyle]="{'background-color': backgroundColor, 'font-size': fontSize + 'px'}">
  This div's styles change based on component properties.
</div>
```

Here, the background color and font size of the div are set based on the `backgroundColor` and `fontSize` properties of the component.

### 3. `ngModel`

The `ngModel` directive is used for two-way data binding between form inputs and component properties.

**Example:**

```html
<input [(ngModel)]="username" placeholder="Enter your username">
<p>Your username is: {{ username }}</p>
```

In this example, the input field is bound to the `username` property of the component. Any changes to the input field will update the `username` property, and vice versa.

These built-in attribute directives are powerful tools in Angular that allow you to dynamically control the appearance and behavior of your application. By using these directives, you can create more interactive and responsive user interfaces.