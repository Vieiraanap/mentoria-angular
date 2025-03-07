# Chapter 5: Services and Dependency Injection

## Basics of Dependency Injection
Dependency injection, or DI, is one of the fundamental concepts in Angular. DI is wired into the Angular framework and allows classes with Angular decorators, such as Components, Directives, Pipes, and Injectables, to configure dependencies that they need.

In this lesson, let’s look at:

How to provide a dependency -> https://angular.dev/guide/di/dependency-injection#providing-a-dependency
How to inject a dependency with inject() -> https://www.angulartraining.com/daily-newsletter/the-inject-function/
How to inject a dependency using a constructor -> https://angular.dev/guide/di/dependency-injection#injecting-consuming-a-dependency
Provider configuration options -> https://www.angulartraining.com/daily-newsletter/dependency-injection-and-provider-config/

## Characteristics of Services
Angular services are singleton objects that share data and logic across different components in an Angular application. By encapsulating specific functionalities, they promote modularity, reusability, and maintainability of code.

In this lesson, learn more about these main characteristics of Angular services:

Basics of Angular services -> https://angular.dev/tutorials/first-app/09-services#conceptual-preview-of-services
Services are singletons -> https://angular.dev/style-guide#services-are-singletons
Using services to cache data: An example -> https://www.angulartraining.com/daily-newsletter/using-services-to-cache-data/

💡 Pro TIP

Services are great but using too many of them can become an anti-pattern over time. Sometimes, a simple function can do the work of a service. You can read more about this topic here. -> https://www.angulartraining.com/daily-newsletter/anti-pattern-series-using-too-many-services/

**QUIZ**

1. In Angular, which of the following decorators is used to register a class as a service?

@NgService


@Service


@Inject


@Injectable [OK]

2. Can the following class be injected into a component as-is?
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable()
export class CartService {

    constructor(private http: HttpClient) {}

    getCartContents() {
        // Some code
    }

}

No, it does not have the @Service decorator


No, it has to be added to an array of providers first [OK]


Yes


No, that code does not compile

3. According to the following code, how many instances of TokenService can we have in an Angular application?
(assuming there's no other dependency injection configuration anywhere else for that service)

@Injectable({
  providedIn: 'root'
})
export class TokenService {
  // ... (rest of the class implementation)
}

It could be any number of instances


One


Zero or one [OK]


One per module

4. One of the following syntaxes is correct for injecting a `LoginService` in `LoginComponent`.
Which one is it?


@Injectable()
loginService: LoginService;

myService = inject(LoginService); [OK]

loginservice = create(LoginService)

loginService = constructor(loginService: LoginService);

## Use a Service to Manage Favorite Movies
Challenge Description
In this challenge, we want to be able to manage favorite movies in the app by:

Adding a movie as a favorite by clicking on a "star" icon ☆
Displaying current favorite movies by displaying their "star" icon in yellow color ⭐
Removing a movie from our favorites by clicking again on the "star" icon ☆
Requirements
Edit the provided src/services/favorites.service.ts
Use a Signal to store the list of current favorite movies (empty array by default)
Implement a method toggleFavorite to toggle (add/remove) a movie from the list of favorites
💡 HINT: Not sure how to work with Signals? Head back to our section on Signals in Chapter 2

Implement a method isFavorite(movie) that returns whether a movie is a favorite or not
Add inputs/outputs to movie-item.component.ts to pass the information when a movie is a favorite, as well as emit an event when the "star" icon is clicked.
Use the active CSS class to turn the ☆ icon into ⭐. Remove that class to do the opposite.
Update app.component.ts to handle the interactions with favorites.service.ts and pass the favorite information to movie-item.component.ts.
🚨 PRO TIP: Using inputs/outputs to avoid injecting services in too many components is a fundamental architectural concept known as using presentation and container components. -> https://www.angulartraining.com/daily-newsletter/container-vs-presentation-components/

Other Considerations
If you see the data-test attribute anywhere in the boilerplate don't remove it.
Example of Finished Application
This is an example of what the functionality should look like for the completed exercise. If you’d like to mimic this style, feel free to do so, but it is not required.