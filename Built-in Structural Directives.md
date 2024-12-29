### 1. `*ngIf`

The `*ngIf` directive conditionally includes or excludes an element in the DOM based on a boolean expression.

**Example:**

```html
<div *ngIf="isLoggedIn">
  Welcome back, user!
</div>
```

In this example, the `<div>` element will only be rendered if the `isLoggedIn` property is `true`.

### 2. `*ngFor`

The `*ngFor` directive is used to repeat a block of HTML for each item in a collection.
[[ngFor deep dive]]


**Example:**

```html
<ul>
  <li *ngFor="let item of items">
    {{ item }}
  </li>
</ul>
```

Here, the `<li>` element is repeated for each item in the `items` array. The `let item of items` syntax is used to iterate over the array.

### 3. `*ngSwitch`

The `*ngSwitch` directive is used to display one element from a set of elements based on a switch expression.

**Example:**

```html
<div [ngSwitch]="color">
  <p *ngSwitchCase="'red'">Red selected</p>
  <p *ngSwitchCase="'blue'">Blue selected</p>
  <p *ngSwitchCase="'green'">Green selected</p>
  <p *ngSwitchDefault>Color not selected</p>
</div>
```

In this example, the paragraph that matches the `color` value will be displayed. If none of the cases match, the `ngSwitchDefault` will be shown.
