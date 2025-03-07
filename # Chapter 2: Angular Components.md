# Chapter 2: Angular Components

## Component Selector and Decorators
Angular components require a selector, which is how Angular knows when to render a given component.

Learn about some conventions and tips and tricks around selectors:

Choosing a selector and using prefixes -> https://angular.dev/guide/components/selectors#choosing-a-selector
Angular selectors are CSS selectors -> https://www.angulartraining.com/daily-newsletter/the-power-of-angular-selectors/

Decorators are a way for Angular to add functionality to a class, a function, a method, or a class property. For instance, inputs and outputs are a very important feature of the framework to pass data between components:

Accepting data with input properties -> https://angular.dev/guide/components/inputs
Emitting data with outputs -> https://angular.dev/guide/components/outputs
View queries with @ViewChild -> https://angular.dev/guide/components/queries#view-queries
Content queries with @ContentChild -> https://angular.dev/guide/components/queries#content-queries

## Expressions and Data Bindings
Component templates are how we display data and control when the DOM structure gets updated using expressions and data bindings. In this section, let’s refresh our knowledge of component template features:

Understanding bindings -> https://angular.dev/guide/templates/binding
Expressions (or interpolations) -> https://angular.dev/guide/templates/binding#render-dynamic-text-with-text-interpolation
Template reference variables -> https://www.angulartraining.com/daily-newsletter/template-reference-variables/

💡 Pro TIP

Calling methods inside Angular expressions can have a negative impact on performance. It’s an anti-pattern. Learn more about it here.** -> https://www.angulartraining.com/daily-newsletter/anti-pattern-series-calling-a-method-in-a-template/

## Control Flow with Blocks
Control flow blocks have been introduced in Angular 17 and became stable in Angular 18. They are a great alternative to Angular directives and improve the readability of your HTML templates.

Let’s learn more about these new syntax options for control flow, called blocks:

Introduction to the new control flow and comparison with directives -> https://blog.angulartraining.com/angular-17-new-control-flow-syntax-4fbec4772d04
@let for local variables in Angular views -> https://www.angulartraining.com/daily-newsletter/let-for-local-variables-in-angular-views/
@if block documentation -> https://angular.dev/guide/templates/control-flow#if-block-conditionals
@for block documentation -> https://angular.dev/guide/templates/control-flow#for-block---repeaters
@switch block documentation -> https://angular.dev/guide/templates/control-flow#switch-block---selection

💡 Pro TIP

Using the new control flow syntax improves performance because it relies on native Javascript code instead of importing Angular directives. Also, the @for block was optimized for performance and is proven to be much faster than *ngFor on large arrays.

**QUIZ**

1.Which @for block option is required?

track [OK]


$index


trackBy


count


2. Which of the following options is not* a valid Angular selector?

<app-header> [OK]

app-header


[header]


.header

3.What is the decorator used to pass data to a component?

@Prop()


@Input() [OK]


@Data()


@Model()

4. Which of these HTML template examples would automatically render the latest value of `data` when `data` changes?
- (click)="data"
- [value]="data" [OK]
- ([ngModel])=”data”
- {data}

## Create a Component Driven by Inputs
Challenge Description
In this challenge, let's create a movie item component that receives Movie information as an input.

Requirements
Open src/movie-item/movie-item.component.ts
Add a required input of type Movie (see sample movie provided in src/app.component.ts)
Update the provided HTML template to render the movie:
Title
Release date (no formatting needed)
Budget ($ {value} million - for instance: $ 50 million)
Duration ({value} min - for instance: 152 min)
Update src/app.component.html to pass the sample movie as an input
Ensure your component is displayed properly on the screen
💡 HINT: Review our self-study content if you get stuck at any step

Other Considerations
If you see the data-test attribute anywhere in the boilerplate don't remove it.
Mini.css is preinstalled with the default config. It might be helpful for you, if you want to have some styles. (Not required)
Example of Finished Component
This is an example of what the functionality should look like for the completed exercise. If you’d like to mimic this style, feel free to do so, but it is not required.

Finished app in this challenge

## Signals
Signals are the new Angular recommendation to handle data in our applications. They’re easier to learn than RxJs, lightweight, and they’re more performant as they enable a new type of change detection that didn’t exist in Angular before.

Let’s dive into into Signals with these topics:

Creating a signal and setting its value -> https://angular.dev/guide/signals#writable-signals
Official definition of Signals -> https://angular.dev/guide/signals#what-are-signals
The computed() function -> https://www.angulartraining.com/daily-newsletter/signals-computed/
The effect() function -> https://www.angulartraining.com/daily-newsletter/signals-effect/
RxJs interoperability with Signals -> https://www.angulartraining.com/daily-newsletter/rxjs-and-signals-interoperability/
Signal-based components tutorial -> https://blog.angulartraining.com/angular-signal-based-components-tutorial-4e4b4b1dfa96

## Lifecycle Hooks
Lifecycle hooks allow us to be notified by Angular when a component/directive reaches a specific state in its lifecycle.

Here are the most useful lifecycle hooks we need to learn about:

Lifecycle of Angular applications -> https://www.angulartraining.com/daily-newsletter/lifecycle-of-angular-applications/
ngOnDestroy lifecycle hook -> https://www.angulartraining.com/daily-newsletter/ngondestroy-lifecycle-hook/
ngOnChanges lifecycle hook ->  https://www.angulartraining.com/daily-newsletter/ngonchanges-lifecycle-hook/
ngOnInit lifecycle hook -> https://www.angulartraining.com/daily-newsletter/ngoninit-lifecycle-hook/

💡 Pro TIP

Always use ngOnDestroy to unsubscribe from your RxJs Observables and prevent memory leaks. This also applies to setTimeout or setInterval, which must be canceled in ngOnDestroy.**

## Other Important Topics
Some Angular component topics didn’t really fit in the previous categories (or they’d fit in several of them!) but are still important to know about for the Angular certification.

Here are these additional topics to know about:

Signal-based equivalents of query decorators -> https://www.angulartraining.com/daily-newsletter/viewchild-and-contentchild-for-signal-based-queries/
Signal-based functions for inputs, outputs, and model -> https://www.angulartraining.com/daily-newsletter/whats-new-in-angular-17-1/
What is ng-template? -> https://blog.angulartraining.com/what-is-ng-template-and-when-to-use-it-f875b46aa078
What is ng-container? -> https://www.angulartraining.com/daily-newsletter/what-is-ng-container/
Standalone components (also covered in Angular Modules and Standalone Lesson in Chapter 1) -> https://www.angulartraining.com/daily-newsletter/what-are-standalone-components/

**QUIZ**

1. The following syntax does not compile:
<div *ngIf="showItems" *ngFor="let item of items">{{item}}</div>
Which alternative syntax would generate the exact same DOM structure as intended above?


<ng-template *ngIf="showItems">
    <div *ngFor="let item of items">{{item}}</div>
</ng-template>

<div *ngIf="showItems">
    <span *ngFor="let item of items">{{item}}</span>
</div>

<div [hidden]="! showItems" *ngFor="let item of items">{{item}}</div>

<ng-container *ngIf="showItems"> [OK]
    <div *ngFor="let item of items">{{item}}</div>
</ng-container>

2. What is the purpose of the ViewChild decorator in this component example?
@Component({
 . . .
 template: '<p #test></p>'
})
export class UserDetailsComponent {
 @ViewChild('test') test;
}

It indicates that the tag be rendered as a child of the parent view that uses this component.


It makes the tag in the template support content projection.


It makes the tag visible in the final render. If @ViewChild was not used in the class, then Angular would automatically hide the tag that has #test on it.


It provides access from within the component class to the ElementRef object for the tag that has the test template reference variable. [OK]

3. Which of the following functions is not a part of the Signals API?

observable() [OK]

signal()

computed()

effect()

## Display a List of Components
Challenge Description
In this challenge, we display multiple instances of our MovieItemComponent.

Requirements
Inject MoviesService into the AppComponent
💡 HINT: Review our self-study content on dependency injection if you're stuck here

Retrieve a Signal of all movies from that service.
Use the @for block to repeat MovieItemComponent as many times as needed
💡 HINT: Feel free to remove any code that isn't needed anymore in your components

Other Considerations
If you see the data-test attribute anywhere in the boilerplate don't remove it.
Mini.css is preinstalled with the default config. It might be helpful for you, if you want to have some styles (not required)
Example of Finished Application
This is an example of what the functionality should look like for the completed exercise. If you’d like to mimic this style, feel free to do so, but it is not required.

Finished app in this challenge