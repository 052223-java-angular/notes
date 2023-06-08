# Angular

## Table of Contents

- [Introduciton](#introduction)
- [Getting Started](#getting-started)
- [Generating Components and Services](#generating-components-and-services)
- [Angular Life Cycle](#angular-life-cycle)
- [Routing](#routing)
- [Reactive Form](#reactive-form)
- [Data Binding](#data-binding)
- [Observable](#observable)
- [Services](#services)

## Introduction

Angular is a popular frontend framework for building web applications. It is developed and maintained by Google. Angular allows developers to create dynamic and responsive web pages using HTML, CSS, and TypeScript.

With Angular, developers can easily build complex web applications that are easy to maintain and scale. It provides a set of tools and features that simplify the process of building web applications, including data binding, components, services, and directives.

Angular is a powerful framework that is used by many companies and developers worldwide. It is ideal for building large-scale enterprise applications that require high performance and scalability.

If you are looking to learn Angular, there are many resources available online, including tutorials, documentation, and community forums. With its growing popularity, learning Angular can be a valuable skill for any frontend developer.

- Angular is a frontend framework for building web applications developed and maintained by Google
- It allows developers to create dynamic and responsive web pages using HTML, CSS, and TypeScript
- Angular provides a set of tools and features that simplify the process of building web applications, including data binding, components, services, and directives
- It is a powerful framework used by many companies and developers worldwide, ideal for building large-scale enterprise applications that require high performance and scalability
- There are many resources available online for learning Angular, including tutorials, documentation, and community forums

## Getting Started

To start an Angular project, you'll need to follow a few steps. Here's a step-by-step guide to help you get started:

### Set up the Development Environment:

Ensure that you have Node.js installed on your machine. You can download it from the official Node.js website (**[https://nodejs.org](https://nodejs.org/)**).

Verify that Node.js and npm (Node Package Manager) are properly installed by running the following commands in your terminal:

```bash
node -v
npm -v
```

Install the Angular CLI globally by running the following command:

```bash
npm install -g @angular/cli
```

Create a New Angular Project:

```java
ng new my-angular-app
```

## Generating Components and Services

To generate a new component in Angular using the terminal, you can use the Angular CLI command `ng generate component`. Here's an example command to generate a new component called `example`:

```bash
ng generate component example
```

To generate a new service in Angular, you can use the Angular CLI command `ng generate service`. Here's an example command to generate a new service called `example`:

```bash
ng generate service example
```

## Angular Life Cycle

Angular has a set of life cycle hooks that allow developers to tap into various stages of a component's life cycle. These hooks can be used to perform various actions such as initializing and destroying component properties, detecting changes, and more.

Here are the main Angular life cycle hooks:

- `ngOnChanges` - Called every time a component's input properties change.
- `ngOnInit` - Called once when the component is initialized.
- `ngDoCheck` - Called during every change detection cycle.
- `ngAfterContentInit` - Called once after the component's content is initialized.
- `ngAfterContentChecked` - Called after every check of the component's content.
- `ngAfterViewInit` - Called once after the component's view has been initialized.
- `ngAfterViewChecked` - Called after every check of the component's view.
- `ngOnDestroy` - Called just before the component is destroyed.

These hooks can be used to perform various actions such as initializing and destroying component properties, detecting changes, and more.

## Routing

### **Step 1: Configure Routes**

Open the **`src/app/app-routing.module.ts`** file.

Import the `**ExampleComponent**` at the top of the file:

```tsx
import { ExampComponent } from "./home/example.component";
```

Define the routes inside the **`const routes`** array:

```tsx
const routes: Routes = [{ path: "example", component: ExampleComponent }];
```

Here, we define two routes: an empty path for the home component and a **`/example`** path for the about component.

### **Step 2: Add Router Outlet**

Open the **`src/app/app.component.html`** file.

Replace the existing content with the following code:

```html
<router-outlet></router-outlet>
```

The **`<router-outlet>`** directive is a placeholder that Angular uses to render the appropriate component based on the current route.

### **Step 3: Add Navigation Links**

Open the **`src/app/app.component.html`** file.

Modify the content to include navigation links:

```html
<nav>
  <a routerLink="/example">Example</a>
</nav>
<router-outlet></router-outlet>
```

The **`routerLink`** attribute tells the app where to go when you click the link.

The first link takes you to the example page.

### **Step 4: Perform Component Routing**

Inside your component's code, you can use the Router service to navigate to a specific component:

```tsx
// Import the necessary modules
import { Router } from '@angular/router';

// Inject the Router service
constructor(private router: Router) {}

// Perform component routing
goToAboutComponent() {
  this.router.navigate(['/example']);
}
```

## Reactive Form

### **Step 1: Import Reactive Forms Module**

Open the **`src/app/app.module.ts`** file.

Import the **`ReactiveFormsModule`** module from **`@angular/forms`**:

```tsx
import { ReactiveFormsModule } from "@angular/forms";
```

Add **`ReactiveFormsModule`** to the **`imports`** array:

```tsx
imports: [
  // Other imports...
  ReactiveFormsModule
],
```

### **Step 4: Create a Reactive Form**

Open the **`src/app/form/form.component.ts`** file.

Import the necessary modules:

```tsx
import { Component, OnInit } from "@angular/core";
import { FormBuilder, FormGroup, Validators } from "@angular/forms";
```

Declare a form group property and initialize it in the component's constructor:

```tsx
formGroup: FormGroup;

constructor(private fb: FormBuilder) { }
```

Inside the **`ngOnInit`** method, build the form structure using the **`FormBuilder`**:

```tsx
ngOnInit() {
  this.formGroup = this.fb.group({
    name: ['', Validators.required],
    email: ['', [Validators.required, Validators.email]],
    password: ['', [Validators.required, Validators.minLength(6)]],
  });
}
```

### **Step 5: Display the Form in the Template**

Open the **`src/app/form/form.component.html`** file.

Add the form markup to the template:

```html
<form [formGroup]="formGroup" (ngSubmit)="submitForm()">
  <label>
    Name:
    <input type="text" formControlName="name" />
  </label>
  <br />
  <label>
    Email:
    <input type="email" formControlName="email" />
  </label>
  <br />
  <label>
    Password:
    <input type="password" formControlName="password" />
  </label>
  <br />
  <button type="submit" [disabled]="formGroup.invalid">Submit</button>
</form>
```

The **`[formGroup]`** directive in Angular connects a form element to a **`FormGroup`**. This way, any changes made in the form are reflected in the **`FormGroup`**. It helps create a two-way binding between the form and the component's data model in Reactive Forms.

**`(ngSubmit)`** is a directive in Angular that connects the form submission event to a method in the component.

**`formControlName`** is a feature in Angular that links a form control element to a form control in the component. This way, any adjustments you make to the form control will automatically be updated in the component's data model and vice versa.

### **Step 6: Handle Form Submission**

Open the **`src/app/form/form.component.ts`** file.

Implement the **`submitForm`** method to handle form submission:

```tsx
submitForm() {
  if (this.formGroup.invalid) {
    return;
  }

  // Perform form submission logic
  console.log(this.formGroup.value);
}

```

## Data Binding

### One Way Data Binding

One-way data binding is a feature in Angular that allows data to flow only in one direction, from the component to the view. An example of one-way data binding is when a component's property is displayed in the view using interpolation syntax, like this:

```html
<h1>{{ title }}</h1>
```

Here, `title` is a property of the component that is being displayed in the view using the `{{ }}` syntax. Any changes made to the `title` property in the component will automatically be reflected in the view.

### Two Way Data Binding

Two-way data binding in Angular lets data flow both ways, from component to view and view to component. You can display a component's property in the view using `[(ngModel)]` syntax, which is an example of two-way data binding.

```html
<input [(ngModel)]="name" />
```

Here, `name` is a property of the component that is being displayed in the view using the `[(ngModel)]` syntax. Any changes made to the `name` property in the component or in the view will automatically be reflected in both the component and the view.

### Method Binding

To bind an element to a method in Angular, you can use event binding. Here's an example:

```html
<button (click)="doSomething()">Click me</button>
```

Here, the `(click)` directive is used to bind the `click` event of the button to the `doSomething()` method of the component. When the button is clicked, the `doSomething()` method will be executed.

You can also pass an event object to the method by using the `$event` variable:

```html
<button (click)="doSomething($event)">Click me</button>
```

In this case, the `$event` variable contains the event object, which can be used in the `doSomething()` method to access information about the event.

Here's an example of how to access the event value in the method:

```tsx
doSomething(event: Event) {
  console.log(event.target.value);
}
```

In this example, `event.target.value` is used to access the value of the element that triggered the event.

## Observable

In Angular, observables are used for handling asynchronous data. They allow you to subscribe to data streams and react to changes in the data over time. You'll find observables used a lot in Angular's HTTP module for asynchronously requesting data from APIs and handling the responses.

In computer programming, asynchronous means that a program can keep doing other things while waiting for a long task to finish. This is different from blocking the program and waiting for the task to finish before going on to the next thing. Asynchronous processing can help make the program work better and faster.

Here's an example of how to create an observable:

```tsx
import { Observable } from "rxjs";

const observable = new Observable((observer) => {
  observer.next("Hello");
  observer.next("World");
  observer.complete();
});
```

In this example, the observable emits the values 'Hello' and 'World' using the `observer.next()` method. It then completes the data stream using the `observer.complete()` method.

To subscribe to this observable and handle the emitted values, you can do the following:

```tsx
observable.subscribe({
  next: (value) => console.log(value),
  error: (error) => console.error(error),
  complete: () => console.log("Complete"),
});
```

In this example, the `subscribe()` method is used to subscribe to the observable and define callbacks for handling the emitted values. The `next` callback is called for each emitted value, the `error` callback is called if an error occurs, and the `complete` callback is called when the data stream is complete.

## Services

Here's an example of an `AuthService`:

```tsx
@Injectable({
  providedIn: "root",
})
export class UserService {
  baseUrl = environment.apiBaseUrl;

  constructor(private http: HttpClient) {}

  /* --------------------------- Methods --------------------------- */

  login(payload: LoginPayload): Observable<Auth> {
    return this.http.post<Auth>(`${this.baseUrl}/auth/login`, payload);
  }

  register(payload: RegisterPayload): Observable<Auth> {
    return this.http.post<Auth>(`${this.baseUrl}/auth/register`, payload);
  }
}
```

This class that represents a user service. It is decorated with the `@Injectable` decorator, which means it can be injected as a dependency in other parts of the application. It has a `"baseUrl"` property that gets its value from an environment file, and a constructor that injects the `"HttpClient"` service.

The class has two methods: `"login"`, which sends a POST request to the server's login endpoint with the provided payload and returns an Observable of the `"Auth"` type, and `"register"`, which sends a POST request to the server's register endpoint with the provided payload and returns an Observable of the `"Auth"` type.
