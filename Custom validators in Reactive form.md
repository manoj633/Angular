### Creating Custom Validators in Reactive Forms in Angular

#### Overview
Custom validators in Angular's reactive forms allow you to define complex validation logic that goes beyond the built-in validators provided by Angular. These are particularly useful when you need to enforce business-specific rules or integrate external validation systems.

#### Steps to Create a Custom Validator

1. **Define a Custom Validator Function:**
   A custom validator in Angular is a function that takes a `FormControl` as an argument and returns a validation result in the form of `null` or an error object. The function should return `null` if the validation passes, or an error object if the validation fails.

   ```typescript
   import { FormControl } from '@angular/forms';

   function customValidator(control: FormControl): { [key: string]: any } | null {
     const isValid = /* your validation logic here */;
     return isValid ? null : { 'customError': true };
   }
   ```

   In this example, replace `/* your validation logic here */` with the actual logic for your custom validation.

2. **Integrate Custom Validator into Form Control:**
   Once you have defined your custom validator, you can attach it to a form control within your form group. This is done similarly to how you attach built-in validators.

   ```typescript
   import { Component } from '@angular/core';
   import { FormGroup, FormControl } from '@angular/forms';

   @Component({
     selector: 'app-custom-validator-form',
     templateUrl: './custom-validator-form.component.html'
   })
   export class CustomValidatorFormComponent {
     profileForm = new FormGroup({
       username: new FormControl('', [customValidator])  // Attach custom validator here
     });
   }
   ```

#### Displaying Custom Validation Errors in the Template

1. **Modify the HTML Template to Display Errors:**
   To provide feedback to the user, modify the HTML template to display error messages when your custom validation fails. Use Angular's form control properties like `errors` and `touched` to control when the messages are shown.

   ```html
   <!-- custom-validator-form.component.html -->
   <form [formGroup]="profileForm" (ngSubmit)="submit()">
     <div>
       <label>Username:</label>
       <input type="text" formControlName="username">
       <div *ngIf="profileForm.get('username').errors?.customError && profileForm.get('username').touched">
         Custom validation error message.
       </div>
     </div>
     <button type="submit">Submit</button>
   </form>
   ```

   In this example, the error message "Custom validation error message." is displayed if the custom validation fails and the user has touched the input field.

#### Example

Let us create a forbidden user name validator

1. **Define the Custom Validator Function:**
   The custom validator function will take a `FormControl` as its argument and check if the value of the control is in the list of forbidden usernames.

```typescript
import { FormControl } from '@angular/forms';

function forbiddenUsernameValidator(forbiddenUsernames: string[]): (control: FormControl) => { [key: string]: any } | null {
  return (control: FormControl): { [key: string]: any } | null => {
    const isForbidden = forbiddenUsernames.includes(control.value);
    return isForbidden ? { 'forbiddenUsername': { value: control.value } } : null;
  };
}
```

2. **Configure the Validator in Your Form:**
   Use the validator in a form control by passing the list of forbidden usernames to the validator function.

```typescript
import { Component } from '@angular/core';
import { FormGroup, FormControl } from '@angular/forms';

@Component({
  selector: 'app-username-form',
  templateUrl: './username-form.component.html'
})
export class UsernameFormComponent {
  forbiddenUsernames = ['admin', 'user', 'test'];

  profileForm = new FormGroup({
    username: new FormControl('', [forbiddenUsernameValidator(this.forbiddenUsernames)])
  });
}
```

3. **Modify the HTML Template to Display Errors:**
   Update your component's template to show an error message when the forbidden username error is triggered.

```html
<!-- username-form.component.html -->
<form [formGroup]="profileForm" (ngSubmit)="submit()">
  <div>
    <label>Username:</label>
    <input type="text" formControlName="username">
    <div *ngIf="profileForm.get('username').errors?.forbiddenUsername && profileForm.get('username').touched">
      Username "{{ profileForm.get('username').errors.forbiddenUsername.value }}" is not allowed.
    </div>
  </div>
  <button type="submit">Submit</button>
</form>
```


This custom validator checks if the username entered is part of a list of forbidden usernames and returns an error if it is. The error is then used in the template to display an appropriate message to the user. This approach ensures that users do not use usernames that are restricted or reserved.

#### Summary

Custom validators are a powerful feature in Angular's reactive forms that allow you to implement complex and specific validation rules. By defining a custom validator function and integrating it into your form controls, you can ensure that the data entered by users adheres to the rules required by your application. Displaying appropriate error messages enhances the user experience by providing clear feedback on what needs to be corrected. This approach is essential for creating robust, user-friendly forms that meet specific business requirements.