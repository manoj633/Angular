
#### Introduction
Pipes in Angular are a powerful feature used to transform data right in the template, before displaying it to the user. They are simple functions that take in data as input and transform it to a desired output format. Pipes can be chained, and they can also take parameters to fine-tune their output.

#### Syntax of Using Pipes
The basic syntax for using a pipe in Angular is as follows:
```html
{{ value | pipeName:parameter }}
```
Here, `value` is the data you want to transform, `pipeName` is the name of the pipe you want to apply, and `parameter` is an optional parameter that you can pass to the pipe.

#### Types of Pipes
Angular provides several built-in pipes and also allows you to create custom pipes. Here are some of the commonly used built-in pipes, along with examples:

1. **DatePipe** - Formats a date value according to locale rules.
   ```html
   {{ myDate | date:'fullDate' }}
   ```
   Example output: "Thursday, June 15, 2023"

2. **UpperCasePipe** and **LowerCasePipe** - Transforms text to uppercase or lowercase.
   ```html
   {{ 'hello' | uppercase }}
   ```
   Example output: "HELLO"

3. **DecimalPipe** - Transforms a number into a decimal format.
   ```html
   {{ 3.14159265 | number:'3.1-2' }}
   ```
   Example output: "003.14"

4. **CurrencyPipe** - Transforms a number to a currency string, formatted according to locale rules.
   ```html
   {{ 100 | currency:'USD':true:'4.2-2' }}
   ```
   Example output: "USD100.00"

5. **PercentPipe** - Transforms a number to a percent string, based on locale rules.
   ```html
   {{ 0.123456 | percent:'2.2-2' }}
   ```
   Example output: "12.35%"

6. **SlicePipe** - Creates a new Array or String containing a subset (slice) of the elements.
   ```html
   {{ 'Hello World' | slice:6:11 }}
   ```
   Example output: "World"

7. **JsonPipe** - Converts an object or array into a JSON formatted string.
   ```html
   {{ {name: 'John', age: 30} | json }}
   ```
   Example output: `{"name":"John","age":30}`

#### [[Chaining multiple pipes]]
#### [[Creating custom pipes]]
#### [[Pure and Impure pipes in Angular]]
#### [['async' pipe in Angular]]