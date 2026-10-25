reaLITTLE LEMON DJANGO CAPSTONE — PEER REVIEW GUIDE
================================================

PROJECT OVERVIEW
----------------
Little Lemon is a restaurant web application developed using Django as part of the Meta Full-Stack Developer Capstone project. The application includes Django-served HTML pages, menu management, table booking APIs, MySQL database integration, user registration, authentication, and automated tests.

1. DJANGO WEB APPLICATION
-------------------------
Start the Django development server:

    python manage.py runserver

Open http://127.0.0.1:8000/ in your browser to access the application.

Verify that the configured Django views and URL patterns serve the application's HTML pages correctly. The exact page URL depends on the project's URL configuration.

2. GIT REPOSITORY
-----------------
The source code is maintained in a Git repository.

Reviewers can inspect the repository to verify the project structure, Django applications, configuration files, migrations, templates, API implementation, and tests.

Before submission, ensure that all required source files have been committed and pushed to the repository. Do not commit database passwords, secret keys, or other credentials.

3. MYSQL DATABASE CONFIGURATION
--------------------------------
Install MySQL Server and ensure the service is running.

Create the project database:

    CREATE DATABASE littlelemon;

Configure the database connection in settings.py using your local MySQL credentials.

Example:

    DATABASES = {
        "default": {
            "ENGINE": "django.db.backends.mysql",
            "NAME": "littlelemon",
            "USER": "your_mysql_username",
            "PASSWORD": "your_mysql_password",
            "HOST": "127.0.0.1",
            "PORT": "3306",
        }
    }

Install the required dependencies:

    pip install -r requirements.txt

Apply database migrations:

    python manage.py migrate

If the project has new model changes without migration files, generate migrations first:

    python manage.py makemigrations

The application should then be able to connect to MySQL and use the configured database.

4. MENU API
-----------
Base URL: http://127.0.0.1:8000

Endpoint:
    /api/menu/

Use Insomnia to send a GET request and inspect the menu items returned by the API.

Individual menu item endpoint, if configured:

    /api/menu/<id>/

Replace <id> with a valid menu item ID. Other HTTP methods depend on the implementation and permissions.

5. TABLE BOOKING API
--------------------
Endpoint:

    /api/booking/tables/

Use Insomnia to test the supported booking operations, such as retrieving table bookings or creating a booking with a POST request.

The request body must contain the fields required by the project's serializer and model. Supported methods and authentication requirements depend on the configured view.

6. USER REGISTRATION AND AUTHENTICATION
---------------------------------------
Registration endpoint, if configured:

    /auth/users/

Use a POST request with the required user fields to register a test account.

Authentication endpoint:

    Use the login or token endpoint configured by the project.

For example, if token authentication is configured through an appropriate authentication package:

    /auth/token/login/

Authenticate with a registered user's credentials and inspect the response.

For protected API endpoints, provide the authentication credentials in the format expected by the application. For Django REST Framework token authentication, this is commonly:

    Authorization: Token YOUR_TOKEN

Do not assume that optional authentication routes exist unless they are included in the project's URL configuration.

7. UNIT TESTS
-------------
Run the project's automated tests from the directory containing manage.py:

    python manage.py test

Review the terminal output to verify that the tests execute successfully. Tests should cover the relevant application behavior, including models, views, APIs, or authentication where implemented.

Ensure the MySQL configuration and database permissions allow Django to create and manage its test database.

8. API TESTING WITH INSOMNIA
----------------------------
To test the APIs:

1. Start the Django server:

       python manage.py runserver

2. Open Insomnia and create a request using the local base URL:

       http://127.0.0.1:8000

3. Test the menu API using GET:

       /api/menu/

4. Test the table booking API using the HTTP methods supported by the implementation:

       /api/booking/tables/

5. Test user registration and authentication using the routes configured in the project.

6. For POST and PATCH requests, select JSON as the request body format and provide valid data.

7. For protected endpoints, configure authentication in Insomnia and verify that requests receive the expected responses.

Check response status codes, response bodies, and error messages. A 404 may indicate an incorrect route, while a 401 or 403 may indicate an authentication or permission issue.

PEER REVIEW CHECKLIST
---------------------
Reviewers can use the following checklist to assess the submission:

[ ] Django serves the application's HTML content.
[ ] The project is available in a Git repository.
[ ] The backend connects to a MySQL database.
[ ] The menu API is implemented and testable.
[ ] The table booking API is implemented and testable.
[ ] User registration and authentication are configured.
[ ] Unit tests are included and can be executed.
[ ] API endpoints can be tested using Insomnia.

IMPORTANT
---------
Actual routes, HTTP methods, authentication requirements, and request fields must match the submitted source code. Configure the local environment before testing, and never publish passwords, access tokens, or production secrets.
