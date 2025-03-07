# Chapter 8: Angular Forms

## Basics of Angular Forms
The Angular Forms module brings a lot of features to the table to handle form validation, form submission, and error management.

In this lesson, let’s cover the basics of form controls, access, and validation state:

The FormControl class -> https://blog.angulartraining.com/5-tips-on-using-angular-formcontrol-710ca338b896
Basic form validation with Angular -> https://www.angulartraining.com/daily-newsletter/basic-form-validation-with-angular/
Using template reference variables to access input values -> https://www.angulartraining.com/daily-newsletter/template-reference-variables/

💡 Pro TIP

Very small forms (login, search, etc.) don’t even need the Angular Forms module and can rely on template-reference variables instead. -> https://www.angulartraining.com/daily-newsletter/template-reference-variables/

## Reactive and Template-Driven Forms
Angular has two main approaches to forms:

Template-driven forms: Use Angular's intuitive template syntax, directives, and two-way data bindings. Perfect for most use cases.
Reactive forms: Use RxJs for complex, dynamic forms with tricky validation rules.
Let’s learn more about these two approaches:

Set-up of a reactive form and a template-driven form -> https://angular.dev/guide/forms#setup-in-reactive-forms https://angular.dev/guide/forms#setup-in-template-driven-forms
How to create custom validation functions that work with both approaches -> https://www.angulartraining.com/daily-newsletter/using-validation-functions-that-work-with-both-template-driven-and-reactive-forms/
How to choose between reactive and template-driven forms? => https://www.angulartraining.com/daily-newsletter/reactive-or-template-driven-forms/
Reactive forms Observables -> https://www.angulartraining.com/daily-newsletter/reactive-forms-observables/
Template-driven example with Signals -> https://www.angulartraining.com/daily-newsletter/tutorial-architecting-forms-with-signals/

## QUIZ

1. Which of the following properties is NOT a valid property of an Angular `FormControl`:

dirty


valid


untouched


async [OK]

2. What is the name of the Angular service used to create reactive forms?

FormControl


FormFactory


FormService


FormBuilder [OK]

3. Which event is emitted when the value of a form control changes in Angular reactive forms?

controlChange


input


update


valueChange [OK]

4. Which syntax is used to access the underlying `NgForm` instance in a template-driven form?

Turning an Observable into a Signal


[ngForm]="value"


#form="ngForm" [OK]


#model="ngModel"


## Add Filters to our Movies App
Challenge Description
In this challenge, we want to add filters to the UI so users can look for specific movies by title and year of release.

Requirements
Capture user input in the form using some of the tools described in our lesson.
💡 HINT: Is this a complex form or a simple one? What's the easiest approach to get a form's value?

Use the filterMovieList from movies.service to get an Observable of filtered movies based on user input.
Display a filtered list of movies to the user.
Other Considerations
If you see the data-test attribute anywhere in the boilerplate don't remove it.
Example of Finished Application
This is an example of what the functionality should look like for the completed exercise. If you’d like to mimic this style, feel free to do so, but it is not required.