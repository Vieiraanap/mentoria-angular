# Chapter 6: Angular Router

## Basics of Routing
The Angular Router allows users to move between components and views while maintaining the illusion of a traditional multi-page website, all in the browser without involving any server-side navigation.

In this lesson, we cover the essentials of what you need to know about the Angular Router, including the HashLocationStrategy for legacy browsers or scenarios where you can’t configure your server to support client-side URLs:

Basics of RouterModule configuration -> https://angular.dev/guide/routing/router-reference
Router outlet and router links -> https://angular.dev/guide/routing/router-reference#router-outlet https://angular.dev/guide/routing/router-reference#router-links
Router module HashLocationStrategy -> https://v16.angular.io/guide/router#hashlocationstrategy

## Access Control with the Router
Route guards act as sentinels, protecting access to specific routes within your Angular application.

In this section, we cover all you need to know about guards (both the legacy syntax and the new function-based, standalone-friendly approach), as well as how to access route parameters from the Angular Router:

All you need to know about router guards -> https://angular.dev/guide/routing/common-router-tasks#preventing-unauthorized-access
Comparison of legacy syntax vs. new function-based config and guards since v14 ->  https://blog.angulartraining.com/router-utility-functions-in-angular-14-8d843b50d2e2
How to read route parameters? -> https://www.angulartraining.com/daily-newsletter/accessing-route-information-with-angular/

## Lazy Loading
When we use lazy-loading, instead of building our application as one single bundle of code that gets downloaded as soon as our user accesses the app in a browser, we divide our code into several different pieces that get downloaded on-demand when they are needed.

Such lazy loading depends on the Angular Router, as bundles of code get downloaded when new URLs get activated.

In this section, learn more about lazy-loading, why it matters, and how to use it, as well as the new approach using the @defer block:

What you need to know about lazy-loading -> https://www.angulartraining.com/daily-newsletter/lazy-loading-for-better-angular-performance/
Lazy-loading standalone components -> https://www.angulartraining.com/daily-newsletter/lazy-loading-standalone-components/
Lazy-loading with @defer -> https://www.angulartraining.com/daily-newsletter/angular-17-lazy-loading-with-defer/

🚨 Pro TIP Lazy-loading is the most important feature of Angular to improve the performance of large applications by dividing your application code into smaller chunks. If you’re building a medium to large Angular app, consider using lazy-loading.

## QUIZ

1.In Angular, what is the purpose of the <router-outlet> tag?

It indicates where routed components will be rendered [OK]


It specifies navigation links for the user


It defines the root component of the application

2. Considering the following router config, which component will be rendered when a user navigates to /products/21?
RouterModule.forRoot([
     { path: '', component: ProductListComponent },
     { path: 'products/:productId', component: ProductDetailsComponent }
])

A 404 page would show up


ProductDetailsComponent [OK]


None; there is no mapping for that route


ProductListComponent

3. Which of the following is not an existing guard function that can be used with the Angular router?

CanDeactivate


CanNavigate [OK]


CanLoad


CanActivateChild


It's a way to embed an iframe in an Angular application

4. What is one requirement for this syntax to work?
loadComponent:
    () => import('./admin/admin.component').then(comp => comp.AdminComponent)

AdminComponent must be in a lazy-loaded module


This syntax does not work


AdminComponent must be a standalone component [OK]


AdminComponent must be the default export in its source file

## Use the Router to Display Movie Details
Challenge Description
In this challenge, we want to be able to display movie details by clicking on the "Details" button of any movie displayed on the screen, using the component router and lazy-loading.

Requirements
Edit the provided src/home/home.component.ts to make it the new landing page that displays the list of movies.
Change app.component.ts to display just a <router-outlet />. The entire page will be controlled by the router.
Change the router config in app.routes.ts by adding two routes:
A route for the default path "" goes to HomeComponent (landing page with movies list)
A route for the path "details/:id" lazy-loads MovieDetailsComponent (page with details for a single movie)
💡 HINT: Not sure how to use lazy-loading? Head back to our lesson section on lazy-loading

Update the "Details" button in MovieItemComponent so it uses a routerLink to navigate to the proper movie details.
Other Considerations
If you see the data-test attribute anywhere in the boilerplate don't remove it.
Example of Finished Application
This is an example of what the functionality should look like for the completed exercise. If you’d like to mimic this style, feel free to do so, but it is not required.

