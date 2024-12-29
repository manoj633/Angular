### Adding Validation to Input Fields in Reactive Forms in Angular

#### Overview
In Angular's reactive forms, validation is handled by attaching validators to form controls within the form group. Validators are functions that check the value of a form control and determine whether it meets specific criteria. Angular provides several built-in validators for common use cases like required fields, minimum or maximum values, email validation, and pattern matching.

#### Steps to Add Validation

1. **Import Validators Module:**
   First, ensure that you import the `Validators` module from `@angular/forms` alongside `FormGroup` and `FormControl`.

   ```typescript
   import { Component } from '@angular/core';
   import { FormGroup, FormControl, Validators } from '@angular/forms';
   ```

2. **Attach Validators to Form Controls:**
   When defining your form controls within a `FormGroup`, you can attach validators by passing them as the second argument in the `FormControl` constructor. Validators can be composed using `Validators.compose` if you need to apply multiple validation functions to a single control.

   ```typescript
   @Component({
     selector: 'app-reactive-form',
     templateUrl: './reactive-form.component.html'
   })
   export class ReactiveFormComponent {
     profileForm = new FormGroup({
       firstName: new FormControl('', Validators.required),
       lastName: new FormControl('', [Validators.required, Validators.minLength(3)])
     });
   }
   ```

   In the example above, the `firstName` field is required, and the `lastName` field is required and must have a minimum length of 3 characters.

#### Displaying Validation Errors in the Template

1. **Modify the HTML Template:**
   To provide feedback to the user, you can modify the HTML template to display error messages when validation fails. Use Angular's form control properties like `errors`, `touched`, and `dirty` to control when the messages are shown.

   ```html
   <!-- reactive-form.component.html -->
   <form [formGroup]="profileForm" (ngSubmit)="submit()">
     <div>
       <label>First Name:</label>
       <input type="text" formControlName="firstName">
       <div *ngIf="profileForm.get('firstName').errors?.required && profileForm.get('firstName').touched">
         First name is required.
       </div>
     </div>
     <div>
       <label>Last Name:</label>
       <input type="text" formControlName="lastName">
       <div *ngIf="profileForm.get('lastName').errors?.required && profileForm.get('lastName').touched">
         Last name is required.
       </div>
       <div *ngIf="profileForm.get('lastName').errors?.minLength && profileForm.get('lastName').touched">
         Last name must be at least 3 characters long.
       </div>
     </div>
     <button type="submit">Submit</button>
   </form>
   ```

#### Summary

Validation in reactive forms is powerful and flexible, allowing developers to easily enforce input requirements. By using Angular's built-in validators, you can ensure that the data your application processes meets the criteria you specify. Displaying error messages helps guide users to provide the necessary information correctly. This approach is essential for creating robust, user-friendly forms in Angular applications.