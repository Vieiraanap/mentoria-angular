# Chapter 1: Basics of Angular

## What’s the difference between Angular JS and Angular?
Angular JS refers to version 1 of the framework, which hasn’t been supported anymore since January 2022.

Angular refers to the modern iteration of the framework, released as Angular 2 in 2016 and now reaching versions 18 and 19 in 2024.

You can find the release history here. -> https://github.com/angular/angular/releases

## The Angular CLI
The Angular CLI is the go-to command line interface to generate, compile, build, and deploy Angular code.

Learn about the main commands and options by reading this section of the official docs:

Command reference -> https://angular.dev/cli
Introduction to the Angular CLI -> https://angular.dev/tools/cli

## Conventions and Style Guide
The official Angular style guide is a mine of information about best practices and how to organize your code in files and folders.

Also, remember that when using the Angular CLI, you’re automatically following the recommended naming conventions for files, classes, and selectors.

You can read it here:

Angular style guide -> https://angular.dev/style-guide

**QUIZ**

    1. Which CLI command should we run to compile and serve our project locally in development mode?

        ng serve [OK]

        ng build

        ng deploy

        ng development

    2.What does Angular refer to?

        Version 1 of the framework


        Version 16 of the framework


        Version 3 of the framework


        The latest version of the framework (Angular 2+) [OK]

    3.Which of the following file names does not follow the Angular style-guide conventions?

        app.component.ts


        name.service.ts


        uppercase-pipe.ts [OK]


        highlight-all.directive.ts

    4.Which one of the following is not a valid Angular CLI command?

        ng test

        ng build

        ng fix [OK]

        ng add

## Features of the framework
Angular is made up of many concepts, features, and APIs. In this section, we want to ensure you know the basic definitions of a component, directive, pipe, and service and that you understand how Angular differs from other technologies.

Learn about the main concepts of Angular with these resources:

Overview of the Angular framework -> https://angular.dev/overview
Directives vs. components: How to decide which one to use? -> https://www.angulartraining.com/daily-newsletter/when-to-create-a-directive-vs-a-component/
Creating custom pipes -> https://www.angulartraining.com/daily-newsletter/how-to-create-custom-pipes/
When to use services -> https://www.angulartraining.com/daily-newsletter/using-services-to-cache-data/

## Angular Modules and Standalone
Angular modules (or NgModules) can be tricky to understand and are often confusing. In this lesson, let’s learn why Angular modules exist in the first place and what’s in store for them in the future with the apparition of standalone features, the default mode in new applications built with Angular 17+:

What you need to know about Angular modules -> https://www.angulartraining.com/daily-newsletter/what-you-need-to-know-about-ngmodules/
Config options of the NgModule decorator -> https://angular.dev/api/core/NgModule
What are standalone components? -> https://www.angulartraining.com/daily-newsletter/what-are-standalone-components/
PDF DOWNLOAD: Standalone components cheatsheet -> 

💡 Pro TIP

Modules will most likely get removed from the Angular framework in the future. Modern Angular relies on standalone components instead.

**QUIZ**

    1.Which one of these concepts does not exist in the Angular framework?

        Standalone components


        Redux reducers [OK]


        NgModules


        Structural directives

    2.Which of the following statements is true?

        Directives are a way to interact with server-side APIs


        Component libraries cannot be customized to our needs


        Pipes are used to format data such as dates and numbers [OK]


        Services link components to server-side HTML templates

    3.What's the main language of the Angular framework?

        JSP


        TypeScript [OK]


        JavaScript


        AppScript

    4.Which @NgModule decorator option defines the main component of an Angular application?

        bootstrap: [AppComponent] [OK]

        main: [AppComponent]

        bootstrap: AppComponent

        start: AppComponent