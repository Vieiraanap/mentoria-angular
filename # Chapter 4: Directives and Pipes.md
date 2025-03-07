# Chapter 4: Directives and Pipes

## Basics of directives
Directives are a very common feature of Angular applications, and ngIf or ngFor can be found in pretty much every single code base.

Yet, there’s more to directives than just these two, and that’s we’re diving into in this lesson:

ngIf and ngFor directives -> https://angular.dev/api/common/NgIf?tab=usage-notes https://angular.dev/api/common/NgFor?tab=usage-notes
What is a structural directive? -> https://angular.dev/guide/directives/structural-directives
What is an attribute directive? -> https://angular.dev/guide/directives/attribute-directives
Common Angular directives -> https://angular.dev/guide/directives#built-in-attribute-directives
💡 Pro TIP

Remember to use the new control flow syntax over common Angular directives in modern Angular projects. The @for block was optimized for performance and is proven to be much faster than ngFor on large arrays.

## Custom Directives and Advanced Usage
We’ve covered the basics of Angular directives in the previous lesson, so now let’s dive into some more advanced use cases with custom directive creation, how to implement bindings in custom directives, as well as some advanced syntax options for common directives:

When should you create custom directives vs. using components? -> https://www.angulartraining.com/daily-newsletter/when-to-create-a-directive-vs-a-component/
HostListener and HostBinding decorators -> https://www.angulartraining.com/daily-newsletter/hostbinding-and-hostlistener/
5 different syntax options for ngIf -> https://blog.angulartraining.com/5-different-syntax-options-for-ngif-3408dd9050c
Local variables with ngFor -> https://www.angulartraining.com/daily-newsletter/ngfor-local-variables/

## Highlight a Specific Movie in the List on Mouse Over
Challenge Description
In this challenge, we want to highlight movies on mouse over by changing their background color to gold. We want to use a custom directive to do so.

Requirements
Edit the provided src/highlight.directive.ts
Add a way for the directive to add the CSS class highlight to its host element on mouse over (such CSS class is already defined in styles.css)
💡 HINT: Review our self-study content on host bindings and host listeners

Add a way for the directive to remove the CSS class highglight from its host element on mouse out
Apply the directive on your MovieItemComponent
Other Considerations
If you see the data-test attribute anywhere in the boilerplate don't remove it.
Example of Finished Application
This is an example of what the functionality should look like for the completed exercise. If you’d like to mimic this style, feel free to do so, but it is not required.

## Pipes
Pipes are the recommended approach to format data in your component templates. They’re optimized for change detection by default, so they don’t re-render and re-format data if the pipe input hasn’t changed.

Here is what you need to know about Angular pipes:

Common Angular pipes -> https://angular.dev/api?type=pipe#angular_common
Pipe syntax and pipe parameters -> https://angular.dev/guide/templates/pipes#overview
When to use pipes -> https://angular.dev/guide/templates/pipes#how-pipes-work
How to create custom pipes? -> https://www.angulartraining.com/daily-newsletter/how-to-create-custom-pipes/

##  Create Pipes to Improve Budget and Duration Formatting
Challenge Description
In this challenge, we want to display movie budgets as follows using a custom pipe:

If the budget is "175", render it as "$175 million"
If the budget is a range such as "175-200", render it as "$175 to $200 million"
Then create another custom pipe to format the movie duration so that "92" is displayed as "1h 32min"
Requirements
Edit the provided src/pipes/million-dollar.pipe.ts
Implement the transform method to format input values as defined in the challenge description:
If the budget is "175", render it as "$175 million"
If the budget is a range such as "175-200", render it as "$175 to $200 million"
💡 HINT: Not sure how to parse strings in Javascript? Take a look at string.split()

Add your pipe to the template of movie-item.component.ts and ensure the movie budgets are displayed as required
Edit the provided src/pipes/min-to-duration.pipe.ts
Implement the transform method to format input values as defined in the challenge description:
"92" must be displayed as "1h 32min"
Add your pipe to the template of movie-item.component.ts and ensure the movie durations are displayed as required
💡 HINT: This challenge can make use of a lot of modern Javascript features covered in the Javascript section of our training (template strings, ?? operator, and more)

Other Considerations
If you see the data-test attribute anywhere in the boilerplate don't remove it.
Example of Finished Application
This is an example of what the functionality should look like for the completed exercise. If you’d like to mimic this style, feel free to do so, but it is not required.

**QUIZ**

1. Which of the following is not an Angular directive from `@angular/common`?

ngClass


ngBind [OK]


ngSwitch


ngFor

2. Which of these options is the correct syntax for pipe parameters?

{{ amount | currency | ‘USD’ }}

{{ amount | currency : ‘USD’ }} [OK]

{{ amount | currency :: ‘$’ }}

None of the above - all are incorrect

3. What is the `HostBinding` decorator doing in this directive?
@Directive({
 selector: '[appHighlight]'
})
export class HighlightDirective {
 @HostBinding('class.highlighted') highlight = true;
}

It is creating an inline style on the host element with a CSS property named highlighted set to true.


HostBinding does not do anything on directives, it only works with components.


It is adding the CSS class named highlighted to any DOM element that has the appHighlight attribute on it. [OK]


It is adding the CSS class named highlighted to any DOM element for which the tag name is appHighlight.

4. What is the proper syntax to display a list of names in `div` elements when `display` is true?

<ng-template *ngIf="display">
  <div *ngFor="let name of names">{{name}}</div>
</ng-template>

<ng-container *ngIf="display"> [OK]
  <div *ngFor="let name of names">{{name}}</div>
</ng-container>

<ng-switch *ngSwitchCase="display">
    <div *ngFor="let name of names">{{name}}</div>
</ng-switch>

<div *ngIf="display" *ngFor="let name of names">
    {{name}}
</div>