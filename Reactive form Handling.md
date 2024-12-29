
Reactive forms provide a model-driven approach to handling form inputs whose values change over time. Each form element in the view is linked to a form model (form control, group, or array) defined in the component class.

**Key Features of Reactive Forms:**
- **Model-Driven**: Managed by the component class, not the template.
- **Immutability**: The state is immutable, meaning it is returned as a new state whenever changes occur.
- **Predictability**: Changes are predictable through the control of the form model.
- **Rich APIs**: Provides more control and the possibility to manipulate the form's state and validation with a variety of methods and properties.

**Example of a Reactive Form:**
```typescript
import { Component } from '@angular/core';
import { FormGroup, FormControl } from '@angular/forms';

@Component({
  selector: 'app-reactive-form',
  template: `
    <form [formGroup]="profileForm">
      <label>
        First Name:
        <input type="text" formControlName="firstName">
      </label>
      <label>
        Last Name:
        <input type="text" formControlName="lastName">
      </label>
      <button (click)="submit()">Submit</button>
    </form>
  `
})
export class ReactiveFormComponent {
  profileForm = new FormGroup({
    firstName: new FormControl(''),
    lastName: new FormControl('')
  });

  submit() {
    console.log(this.profileForm.value);
  }
}
```

### Template-Driven Forms
Template-driven forms are suitable for simple scenarios and are easier to use. They are asynchronous in nature and use directives in the template to create and manipulate the form and its elements.

**Key Features of Template-Driven Forms:**
- **Directive-Based**: Uses `ngModel` and other directives.
- **Two-Way Data Binding**: Uses two-way data binding to update the data model in the component as changes are made in the template.
- **Less Boilerplate**: Requires less boilerplate code compared to reactive forms.
- **Automatic Track of Form and Input Element State**: Angular keeps track of the state of the form and each input element.

**Example of a Template-Driven Form:**
```html
<!-- In your component template -->
<form #f="ngForm" (ngSubmit)="submit(f.value)">
  <label>
    First Name:
    <input type="text" name="firstName" ngModel>
  </label>
  <label>
    Last Name:
    <input type="text" name="lastName" ngModel>
  </label>
  <button type="submit">Submit</button>
</form>
```

### Differences Between Reactive and Template-Driven Forms
1. **Control**: Reactive forms offer more control and flexibility, whereas template-driven forms are easier to use but less flexible.
2. **Setup**: Reactive forms require more setup initially; template-driven forms can be simpler to start with.
3. **Form Logic**: In reactive forms, form logic is typically placed in the component class which makes it easier to unit test. In template-driven forms, logic is split between the template and the component.
4. **Scalability**: Reactive forms are more scalable due to their immutability and predictability.

Both methods have their use cases, and the choice between them often depends on the complexity of the form and the specific needs of the application.

#### [[Setting up Reactive form]]
#### [[Adding validation in Reactive form]]
#### [[Grouping controls in Reactive form]]
#### [[Array of Form controls in Reactive form]]
#### [[Custom validators in Reactive form]]

#### [[Creating custom async validator in Reactive form]]

#### [[Set and Patch Values in Reactive form]]
#### [[Reset form in Reactive form]]