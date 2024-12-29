Structural directives in Angular are used to alter the DOM layout by adding, removing, or manipulating elements. They are prefixed with an asterisk (\*) when used in templates, which is a syntactic sugar for Angular's template syntax. The three most common structural directives are `*ngIf`, `*ngFor`, and `*ngSwitch`.

## Types of Structural Directives

1. **Built-in Structural directives**: 
	- Read more at [[Built-in Structural Directives]]
2. **Custom Structural directives:** 
	- Read more at [[Developing Custom Structural Directives]]



### How Structural Directives Work

Under the hood, structural directives manipulate the DOM by adding or removing elements. When you use a structural directive, Angular transforms your template into a `<ng-template>` element, which is a placeholder for the content that will be conditionally rendered.

For example, the `*ngIf` directive:

```html
<div *ngIf="isLoggedIn">
  Welcome back, user!
</div>
```

Is transformed by Angular into:

```html
<ng-template [ngIf]="isLoggedIn">
  <div>
    Welcome back, user!
  </div>
</ng-template>
```


### Conclusion

Structural directives are a powerful feature in Angular that allow you to dynamically control the DOM structure. By using built-in directives like `*ngIf`, `*ngFor`, and `*ngSwitch`, or creating custom ones, you can create flexible and dynamic user interfaces.