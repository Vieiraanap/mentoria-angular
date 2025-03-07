# Chapter 9: Challenge roundup

## Car Configurator: Model and Color
Challenge Description
The app you have to build is a simplified version of https://www.tesla.com/modelx/design. You can use that website for inspiration if you want, but our API and possible configurations are a lot simpler. In this challenge, we focus on selecting a car model and color.

Requirements
Models and colors must be retrieved from the API included in the project and accessible at the http://localhost:4200/models endpoint.
Data types are pre-generated for you in src/app/models.type.ts
A configurator.service has been started with a Signal that holds all available car models.
Images for all models and colors can be found at https://interstate21.com/tesla-app/images/
Complete the step1.component to display the right information in the two select dropdowns.
When a Model and Color are selected, the proper image should be displayed on the screen as illustrated below.
💡 HINT: Use Signals as much as possible in configurator.service to store the current state of your configuration (selected model, selected color)

Other Considerations
If you see the data-test attribute anywhere in the boilerplate don't remove it.
The project has mini.css as a dependency for basic styling.
Example of Finished Application
This is an example of what the functionality should look like for the completed exercise. If you’d like to mimic this style, feel free to do so, but it is not required.

## Car Configurator: Config Options
Challenge Description
The app you have to update is a simplified version of https://www.tesla.com/modelx/design. In this challenge, we focus on selecting a car config and options that affect range, maximum speed, and total cost.

Requirements
Update the router config to add routes to http://localhost:4200/step2 that renders the pre-generated step2.component, as well as http://localhost:4200/step1 that renders step1.component.
Add router links in the navigation bar to both these routes so we can navigate between these steps.
Disallow step 2 route navigation as long as car and color aren't selected on step 1.
Complete configurator.service to handle the car configuration and options. Models can have different configs with different prices.
In the step 2 screen, use the /options/:modelCode API endpoint to get the different configs and options available for the selected car.
The two possible options cost $1,000 each and must only be displayed (not checked by default) when available on the selected car model: yoke steering wheel and tow hitch package. The API has two booleans to indicate whether these options are available or not on the select model.
When a config is selected, display the associated range, max speed, and cost
Complete the step2.component to display the right information in the dropdown and checkboxes.
💡 HINT: Use Signals as much as possible in configurator.service to store the current state of your configuration (selected config, selected options)

Other Considerations
If you see the data-test attribute anywhere in the boilerplate don't remove it.
The project has mini.css as a dependency for basic styling.
Example of Finished Application
This is an example of what the functionality should look like for the completed exercise. If you’d like to mimic this style, feel free to do so, but it is not required.

## Car Configurator: Summary and Price
Challenge Description
The app you have to update is a simplified version of https://www.tesla.com/modelx/design. In this challenge, we focus on displaying a recap of the total cost of the selected car model and options.

Requirements
Update the router config to add a route to http://localhost:4200/step3 that renders the pre-generated step3.component.
Disallow step 3 route navigation as long as car and color aren't selected on step 1 and config isn't selected in step 2.
Complete configurator.service to compute the car's total price using a computed Signal.
Complete the step3.component to display the right information: Cost of every chosen option (color, config, yoke, tow hitch, etc.) in properly formatted USD prices as illustrated below, as well as the total cost.
The user should be able to go back to step 1 or 2 and change the configuration, then come back to step 3 to see the updated cost.
Other Considerations
If you see the data-test attribute anywhere in the boilerplate don't remove it.
The project has mini.css as a dependency for basic styling.
Example of Finished Application
This is an example of what the functionality should look like for the completed exercise. If you’d like to mimic this style, feel free to do so, but it is not required.

## Car Configurator: Bug Fixes
Challenge Description
Our application is now completed, but we identified a couple of bugs in it.

Bug #1: If the user creates a Cybertruck config and selects "tow hitch" as an option, then the option remains active if the user switches to a different model. Here is an example where Model 3 has a tow hitch package, which shouldn't be possible:

bug1.png

Bug #2: After selecting a new model, another bug is present on step 2. Step 3 is clickable before selecting a car config:

bug2.png

Bug #3: When going back to step 1, the current car model and color do not show as selected. Here Cybertruck should be selected with the right color:

bug3.png

Requirements
Fix the three bugs described above. Selecting a new model should properly reset all configs and colors associated to the previous model.
Ensure step 3 is only enabled when a config is selected in step 2.
Other Considerations
If you see the data-test attribute anywhere in the boilerplate don't remove it.
Example of Fixed Application
This is an example of what the functionality should look like for the completed exercise.

