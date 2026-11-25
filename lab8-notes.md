Lab 8 – Laravel MVC Demo

Student: Joshua Stott
Course: IS 6465 – Web Based Applications

Part 1: Application Setup and Testing

I successfully configured and ran the Peer Tutoring Hub Laravel application in GitHub Codespaces. I completed the application walkthrough, tested form validation, submitted a tutoring request, and viewed the submitted request.

I also verified database storage using Laravel Tinker. The database returned a count of one tutoring request, confirming that a record was successfully stored.

Part 2: Exploring MVC

1. Business Purpose

The Peer Tutoring Hub allows students to request tutoring sessions for specific courses. Students can provide information about what they need help with, select topics, and specify their preferred date and time. The application also allows users to browse submitted tutoring requests.

2. Route

File: routes/web.php

One route used by the application is POST /requests. This route runs when a user submits the tutoring request form. It directs the submitted information to the store() method in the TutoringRequestController.

3. Controller

File: app/Http/Controllers/TutoringRequestController.php

The TutoringRequestController handles application logic. It retrieves tutoring requests, displays the request form, validates submitted information, and uses the model to save valid requests to the database.

For example, it checks that the selected course is valid, the reason contains between 10 and 500 characters, and the preferred date is not in the past.

4. Model

File: app/Models/TutoringRequest.php

The TutoringRequest model represents the business data associated with a tutoring request, including the course, reason, topics, preferred date, and preferred time.

It uses Laravel’s Eloquent ORM to interact with the database. The model also defines which fields can be mass assigned and converts topics into an array and the preferred date into a date object.

5. View

File: resources/views/requests/create.blade.php

This Blade template displays the tutoring request form. Users can select a course, enter a reason, choose topics, and select their preferred date and time.

The view also displays validation errors, preserves previously entered information when validation fails, and includes CSRF protection.

6. MVC Workflow

When a student submits a tutoring request, the following process occurs:

1. The student completes the form in create.blade.php.
2. The form sends a POST request to /requests.
3. The route directs the request to the store() method in TutoringRequestController.
4. The controller validates the submitted information.
5. If validation succeeds, the TutoringRequest model saves the information to the SQLite database.
6. The controller redirects the user to the requests.show route.
7. The controller’s show() method returns show.blade.php, which displays the submitted request and its details.

If validation fails, the user is returned to the form with error messages and their previous input.

7. Comparison to My Course Project

My course project uses the PHP and database-driven architecture introduced throughout the semester. Laravel provides a more standardized separation between routes, controllers, models, and views.

One benefit of Laravel is that it provides built-in tools for routing, validation, database interaction, and templating. This can reduce repetitive code and make an application easier to organize and maintain.

Converting the existing course project to Laravel at this stage would require restructuring working code and learning additional framework conventions. Continuing with the existing architecture allows us to focus on completing the project requirements without introducing unnecessary complexity.

Part 3: Evidence of Completion

Running Application

Database Verification

I executed the following command using Laravel Tinker:

App\Models\TutoringRequest::count();

Result: 1

This confirmed that a tutoring request was stored in the database.

MVC Source File Evidence

MVC Area	File	Description
Route	routes/web.php	Maps URLs and HTTP requests to controller methods.
Controller	TutoringRequestController.php	Handles application logic, validation, and request processing.
Model	TutoringRequest.php	Represents tutoring request data and manages database interaction through Eloquent.
View	create.blade.php	Displays the tutoring request form and validation messages.

Reflection

Laravel made it easier for me to understand how different responsibilities within a web application can be separated and organized. Following the code from the route to the controller, model, and view helped me understand how MVC works in practice. I also found the built-in validation and database interaction useful because they reduce the amount of code developers need to write manually. The framework-specific syntax, Blade directives, and automatic database interactions were new to me and would require additional practice. Overall, the lab helped me understand why developers use frameworks like Laravel to build and maintain web applications.