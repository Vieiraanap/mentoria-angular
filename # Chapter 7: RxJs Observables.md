# Chapter 7: RxJs Observables

## Basics of RxJs
RxJS (Reactive Extensions for JavaScript) is a library that helps Angular development by providing tools for handling asynchronous operations and event-based programming. At its core, RxJS introduces the concept of Observables, streams of data that emit values over time.

These Observables represent anything from user input and HTTP responses to timers and complex data transformations. RxJS also offers a vast array of operators, allowing you to filter, transform, combine, and manipulate data streams with ease.

In this lesson, we dive into the basics of RxJS to get you started with the library:

What are Observables , and how do we use them? -> https://blog.angulartraining.com/rxjs-observables-in-5-minutes-144abf13cac8
Basic operators and usage syntax -> https://v16.angular.io/guide/rx-library#operators
Strategies to unsubscribe from Observables -> https://blog.angulartraining.com/how-to-automatically-unsubscribe-your-rxjs-observables-tutorial-2f98b0560298

## Important Operators
RxJs Operators allow Angular developers to manipulate Observables in various ways, such as filtering, mapping, combining, and error handling. Common operators include map, filter, switchMap, and catchError.

By leveraging RxJS operators, developers can write more concise, declarative, and maintainable code for handling complex asynchronous scenarios.

In this lesson, we highlight some of the most important operators to know about:

map operator -> https://rxjs.dev/api/operators/map
filter operator -> https://rxjs.dev/api/index/function/filter
tap operator -> https://www.angulartraining.com/daily-newsletter/rxjs-tap-operator/
switchMap operator -> https://www.angulartraining.com/daily-newsletter/rxjs-switchmap-operator/
combineLatest operator -> https://www.angulartraining.com/daily-newsletter/rxjs-combinelatest-operator/
Error handling in RxJS -> https://www.angulartraining.com/daily-newsletter/error-handling-in-rxjs/

💡 Pro TIP

Websites such as rxmarbles.com are very helpful for learning more about operators. Here is some more information about how to use RXMarbles. -> https://www.angulartraining.com/daily-newsletter/how-to-learn-more-about-rxjs-operators/

## QUIZ

1. Which of the following is an incorrect statement regarding RxJS observables?

They are objects we subscribe to


They are a way to work with asynchronous data


They make our code synchronous [OK]


They are used by the HttpClient of Angular

2. When using Rxjs Observables, what does the `.pipe()` method do?

It enables the use of Angular pipes with RxJs


It turns an Observable into an Angular pipe


It automatically subscribes and unsubscribes from an Observable


It enables chaining multiple RxJs operators [OK]

3. What does the RxJs `map()` operator do?

Applies a given function to each array emitted by the source Observable, and returns the resulting values as an Observable of arrays


Applies a given function to each value emitted by the source Observable, and returns the resulting values as an array


Applies a given function to each value emitted by the source Observable, and emits the resulting values as an Observable [OK]


Applies a given function to the source Observable, subscribes to it, and emits the resulting values as an Observable


4. Which of the following is a common use case for `switchMap` in Angular?

Making HTTP requests based on user input, like searching or fetching data [OK]


Turning an Observable into a Signal


Managing application state


Creating animations

## Use RxJs Observables to Display Data
Challenge Description
In this challenge, our lead developer decided to update movies.service.ts to make it return Observables instead of Signals. As a result, we have to update our components to use Observables instead of Signals.

Requirements
Update src/home/home.component.ts to make it handle the new Observable and render the list of all movies.
💡 HINT: Remember the async pipe? Now is a good time to use it!

Update MovieDetailsComponent to make it handle the new Observable and render movie details.
The app should work just like it did before with no visible difference to the user.
Other Considerations
If you see the data-test attribute anywhere in the boilerplate don't remove it.
Example of Finished Application
This is an example of what the functionality should look like for the completed exercise. If you’d like to mimic this style, feel free to do so, but it is not required.
