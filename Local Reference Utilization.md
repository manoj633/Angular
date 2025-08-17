
---

## What is a Template Reference Variable?

- A **template reference variable** is a variable declared in an Angular template that refers to a DOM element, component, or directive.
- It allows you to access the element’s properties, methods, or pass it to component/directive inputs within the template.

---

## How to Create a Template Reference Variable

### 1. Standard Syntax

- Use the `#` symbol followed by the variable name on an element:
  ```html
  <input #myInput type="text">
  ```

### 2. Using `ref-` Prefix (Alternative Syntax)

- You can also use the `ref-` prefix (less common, but valid):
  ```html
  <input ref-myInput type="text">
  ```

---

## Ways to Use Template Reference Variables

### 1. Accessing Native DOM Elements

- You can access the native DOM element in the template:
  ```html
  <input #myInput type="text">
  <button (click)="myInput.value = ''">Clear</button>
  ```

### 2. Passing to Methods

- Pass the variable as an argument to a method:
  ```html
  <input #username>
  <button (click)="greet(username.value)">Greet</button>
  ```

### 3. Accessing Component or Directive Instances

- If the variable is on a component or directive, it refers to the instance:
  ```html
  <app-child #childComp></app-child>
  <button (click)="childComp.doSomething()">Call Child Method</button>
  ```

### 4. With Built-in Directives

- For example, using `ngForm`:
  ```html
  <form #myForm="ngForm"></form>
  ```

### 5. With ViewChild (in Component Class)

- You can access the variable in the component class using `@ViewChild`:
  ```typescript
  @ViewChild('myInput') inputElement: ElementRef;
  ```

---

## Gotchas and Limitations

- **Scope**: Template reference variables are only accessible within the template where they are declared (not in the component class unless using `@ViewChild`).
- **No Type Safety**: The variable is loosely typed in the template; you must know what it refers to.
- **Not Available in Component Class by Default**: Direct access in TypeScript requires `@ViewChild`.
- **Shadowing**: If you declare a variable with the same name in nested templates (like inside an `ngFor`), the inner one shadows the outer.
- **Only in Templates**: Cannot be used in external scripts or styles.

---

## Summary Table

| Aspect          | Details/Example                                    |
| --------------- | -------------------------------------------------- |
| Syntax          | `<input #myVar>`, `<input ref-myVar>`              |
| Refers to       | DOM element, component, or directive instance      |
| Usage           | Access value, call methods, pass to functions      |
| Access in class | Use `@ViewChild('myVar')`                          |
| Scope           | Only within the template                           |
| Gotchas         | No type safety, shadowing, not in class by default |

---

**In summary:**  
Template reference variables (`#var` or `ref-var`) are a powerful way to interact with DOM elements, components, or directives directly in Angular templates. They are easy to use but limited to the template scope unless accessed via `@ViewChild` in the component class. Use them for simple, template-level interactions.