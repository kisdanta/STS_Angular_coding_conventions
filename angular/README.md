# Angular

## Table of Contents

1. [File Structure](#1-file-Structure)
1. [Single responsibility](#2-single-responsibility)
1. [Naming](#3-naming)
1. [Component attribute order](#4-component-attribute-order)
1. [Member order](#5-member-order)
1. [Avoid aliasing inputs and outputs](#6-avoid-aliasing-inputs-and-outputs)
1. [HostListener/HostBinding decorators versus host metadata](#7-hostListener--HostBinding-decorators-versus-host-metadata)
1. [Implement lifecycle hook interfaces](#8-implement-lifecycle-hook-interfaces)

**[⬆ back to top](#table-of-contents)**

## 1. File Structure
| Symbol        | Structure                     | Example                       |                
| ------------- | ---------------------         | ----------------------------- |
| Module        | name.module.ts                | material.module.ts            |
| Routing       | name-routing.module.ts        | user-routing.module.ts        |
| Component     | name.component.ts             | app.component.ts              |    
| Directive     | name.directive.ts             | validate.directive.ts         |    
| Pipe          | name.pipe.ts                  | format.pipe.ts                | 
| Service       | name.service.ts               | app.service.ts                | 
| Store         | name.store.ts                 | steps.store.ts                | 
| Util          | name.utils.ts                 | date.utils.ts                 |
| Model         | name.model.ts                 | student.model.ts              | 
| Interface     | name.interface.ts             | student.interface.ts          | 
| Enum          | name.enum.ts                  | http-code.enum.ts             | 
| Constant      | name.constants.ts             | key-code.constants.ts         | 
| Unit test     | name.component.spec.ts        | hero.component.spec.ts        | 
| E2E test      | name.component.e2e-spec.ts    | hero.component.e2e-spec.ts    |

**[⬆ back to top](#table-of-contents)**

## 2. Single responsibility
### 2.1 One class per file
>Do define one thing, such as a service or component, per file.
>
>Consider limiting files to 400 lines of code.

>Why? One component per file makes it far easier to read, maintain, and avoid collisions with teams in source control.
>
>Why? One component per file avoids hidden bugs that often arise when combining components in a file where they may share variables, create unwanted closures, or unwanted coupling with dependencies.
>
>Why? A single component can be the default export for its file which facilitates lazy loading with the router.
### Example:
    ✅ Good
    // student.model.ts
    export class Student {
        name: string;
    }
    
    // student-address.model.ts
    export class StudentAddress {
        street: string;
    }

    ❌ Bad
    // student.model.ts
    export class Student {
        name: string;
    }

    export class StudentAddress {
        street: string;
    }

### 2.2 Small functions
>Do define small functions
>
>Consider limiting to no more than 75 lines.

>Why? Small functions are easier to test, especially when they do one thing and serve one purpose.
>
>Why? Small functions promote reuse.
>
>Why? Small functions are easier to read.
>
>Why? Small functions are easier to maintain.
>
>Why? Small functions help avoid hidden bugs that come with large functions that share variables with external scope, create unwanted closures, or unwanted coupling with dependencies.

**[⬆ back to top](#table-of-contents)**

## 3. Naming

### 3.1 Separate file names with dots and dashes
>Do use dashes to separate words in the descriptive name.
>
>Do use dots to separate the descriptive name from the type.
>
>Do use consistent type names for all components following a pattern that describes the component's feature then its type. A recommended pattern is `feature.type.ts`.
>
>Do use conventional type names including `.service`, `.component`, `.pipe`, `.module`, and `.directive`. Invent additional type names if you must but take care not to create too many.

>Why? Type names provide a consistent way to quickly identify what is in the file.
>
>Why? Type names make it easy to find a specific file type using an editor or IDE's fuzzy search techniques.
>
>Why? Unabbreviated type names such as `.service` are descriptive and unambiguous. Abbreviations such as `.srv`, `.svc`, and `.serv` can be confusing.
>
>Why? Type names provide pattern matching for any automated tasks.
### Example:
    ✅ Good
    student-list.service.ts
    
    ❌ Bad
    student-list-service.ts
    student-list.srv.ts

### 3.2 Symbols and file names
>Do use consistent names for all assets named after what they represent.
>
>Do use upper camel case for class names.
>
>Do match the name of the symbol to the name of the file.
>
>Do append the symbol name with the conventional suffix (such as `Component`, `Directive`, `Module`, `Pipe`, or `Service`) for a thing of that type.
>
>Do give the filename the conventional suffix (such as `.component.ts`, `.directive.ts`, `.module.ts`, `.pipe.ts`, or `.service.ts`) for a file of that type.

>Why? Consistent conventions make it easy to quickly identify and reference assets of different types.

### Example 1:
    ✅ Good
    // students.component.ts
    @Component({...})
    export class StudentsComponent { }
    
    ❌ Bad
    // students.component.ts
    @Component({...})
    export class Students { }

### Example 2:
    ✅ Good
    // validation.directive.ts
    @Directive({...})
    export class ValidationDirective { }
    
    ❌ Bad
    // students.ts
    @Component({...})
    export class ValidationDirective { }

### 3.3 Component selectors
>Do use kebab-case for naming the element selectors of components.
### Example 1:
    ✅ Good
    // student-list.component.ts
    @Component({
        selector: 'student-list',
    })
    export class StudentListComponent { }
    
    ❌ Bad
    // student-list.component.ts
    @Component({
        selector: 'studentList',
    })
    export class StudentListComponent { }

### 3.3 Directive selectors
>Do Use lower camel case for naming the selectors of directives.

>Why? Keeps the names of the properties defined in the directives that are bound to the view consistent with the attribute names.
>
>Why? The Angular HTML parser is case sensitive and recognizes lower camel case.
### Example 1:
    ✅ Good
    // form-validation.directive.ts
    @Directive({
        selector: 'formValidation',
    })
    export class FormValidationDirective { }
    
    ❌ Bad
    // form-validation.directive.ts
    @Directive({
        selector: 'form-validation',
    })
    export class FormValidationDirective { }

**[⬆ back to top](#table-of-contents)**

## 4. Component attribute order
1. Structural directives
2. Animations
3. Static properties
4. Dynamic properties
5. Events
### Example:
    ✅ Good
    <input
        *ngIf="show"
        @fadeIn
        class="control"
        type="number"
        [placeholder]="placeholder"
        (keypress)="onKeyPressed($event)">
    </input>

    ❌ Bad
    <input
        (keypress)="onKeyPressed($event)"
        *ngIf="show"
        @fadeIn
        [placeholder]="placeholder"
        class="control"
        type="number">
    </input>

**[⬆ back to top](#table-of-contents)**

## 5. Member order
1. Inputs
2. Outputs
3. ViewChild
4. ViewChildren
5. HostBinding
6. HostListener
7. Private readonly properties
8. Private properties
9. Protected readonly properties
10. Protected properties
11. Public readonly properties
12. Public properties
13. Setters
14. Getters
15. Constructor
16. Lifecycle hooks
    1. ngOnChanges
    2. ngOnInit
    3. ngDoCheck
    4. ngAfterContentInit
    5. ngAfterContentChecked
    6. ngAfterViewInit
    7. ngAfterViewChecked
    8. ngOnDestroy
17. Public Methods
18. Private Methods
### Example:
    ✅ Good
    public ngOnInit(): void {
        // TODO
    }
    
    private doSomething(): void {
        // TODO
    }

    ❌ Bad
    private doSomething(): void {
        // TODO
    }

    public ngOnInit(): void {
        // TODO
    }

**[⬆ back to top](#table-of-contents)**

## 6. Avoid aliasing inputs and outputs
>Avoid input and output aliases except when it serves an important purpose.

>Why? Two names for the same property (one private, one public) is inherently confusing.
>
>Why? You should use an alias when the directive name is also an input property, and the directive name doesn't describe the property.
### Example:
    ✅ Good
    export class HeroButtonComponent {
        // No aliases
        @Input() label = '';
        @Output() heroChange = new EventEmitter<any>();
    }
    ❌ Bad
    export class HeroButtonComponent {
        // Pointless aliases
        @Input('labelAttribute') label: string;
        @Output('heroChangeEvent') heroChange = new EventEmitter<any>();
    }

**[⬆ back to top](#table-of-contents)**

## 7. HostListener/HostBinding decorators versus host metadata
>Consider preferring the @HostListener and @HostBinding to the host property of the @Directive and @Component decorators.
>
>Do be consistent in your choice.

>Why? The property associated with @HostBinding or the method associated with @HostListener can be modified only in a single place—in the directive's class. If you use the host metadata property, you must modify both the property/method declaration in the directive's class and the metadata in the decorator associated with the directive.
### Example:
    ✅ Good
    @Directive({
        selector: '[tohValidator]'
    })
    export class ValidatorDirective {
        @HostBinding('attr.role') role = 'button';
        @HostListener('mouseenter') onMouseEnter() {
            // do work
        }
    }
    ❌ Bad
    @Directive({
        selector: '[tohValidator2]',
        host: {
            '[attr.role]': 'role',
            '(mouseenter)': 'onMouseEnter()'
        }
    })
    export class Validator2Directive {
        role = 'button';
        onMouseEnter() {
            // do work
        }
    }

**[⬆ back to top](#table-of-contents)**
    
## 8. Implement lifecycle hook interfaces
> Do implement the lifecycle hook interfaces.

> Why? Lifecycle interfaces prescribe typed method signatures. Use those signatures to flag spelling and syntax mistakes.
### Example:
    ✅ Good
    export class HeroButtonComponent implements OnInit {
        ngOnInit() {
            console.log('The component is initialized');
        }
    }

    ❌ Bad
    export class HeroButtonComponent {
        onInit() { // misspelled
            console.log('The component is initialized');
        }
    }

**[⬆ back to top](#table-of-contents)**
