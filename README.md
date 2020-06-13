# reverse-engineering

## Description
  
A walk-through explaining each file and its purpose within a Node.js application by folder and/or file.

## Table of Contents

* [config](#config)

* [models](#models)
  
* [node_modules](#node_modules)

* [public](#public)

* [routes](#routes)

* [package-lock.json](#package-lock.json)

* [package.json](#package-lock.json)

* [server.js](#server.js)

* [Instructions_for_updates](#Instructions_for_updates)


## config 

config/middleware/isAuthenticated.js

isAuthenticated.js is the middleware file utilized by html.routes.js that determines whether a user is successfully logged in into the initial website, and then to proceed with the appropriate action.  

If the user has successfully logged in, a request is sent to process access to the member page. Otherwise, if the user is not logged in, it is redirected to the main login page. 

config/config.json

The config.json file establishes the connection between the local database and the application file.  

The json file is broken down into a development, testing, and executing/production database. The config.json file is then required by the index.js file for connecting the models to the database table created.

config/passport.js

Passport.js is the primary authorization file for username and passwords entered by the user, in order for the user to access the Members page. 

Passport.js utilizes the following npm packages and files: 

\`\`\`

passport and passport-local npm packages as the primary means of authentication the username(email) and password of the user at the Login page.

models folder to assess whether the user has existing data in the database to authenticate (email and password) via. Sequelize when the user goes through the log-in process.


\`\`\`

If the user attempts to login without a valid username and/or password, a notification will be provided that information is incorrect.

Passport.js is exported to server.js to allow for real-time authentication during application run.

Passport file is also exported to api-routes to receive post requests from the user as part of email/password authentication.


## models

models/index.js

The index.js file utilizes the following packages and files: 

\`\`\`

file system and path built-in Node packages to read and work with file and directory paths associated with other model files

sequelize to allow access the sequelize ORM for database table generation associated with the User model

path.basename() method returns the filename part of the required file paths

env and config to obtain access to the config.json development database

\`\`\`

The index.js file aggregates the information from any created model files (database tables) and then exports those models to their required files. 

For this application, the models are required in the passport.js, api-route.js and the server.js files for posting username and password information for validation.

models/user.js

The user.js file utilizes the following npm packages and files:

\`\`\`

bcrypt package, which performs password hashing. Hashing serves as a form of transforming password to non-legible text, in case of data breach.

\`\`\`

User.js sets up the user model for user information database storage via. Sequelize. 
User.js is then exported to api-routes.js and server.js via index.js, for post requests to the database to verify existing user or or add new user.

## node_modules

The node_modules folder contains all the dependencies used to allow the npm packages to work in their respective files.

## public 

public/js/login.js

Once the user hits the submit button, first the Javascript code validates that the user sends the appropriate information (email address and password) in a readable format. If the user is missing one or both pieces of information, the JavaScript forces the user to enter both pieces of information.

Once the user inputs a valid email address and password, login.js will submit the information and clear the form for future use.

The login.js file will then submit the email address and password to the api-routes (login).js file, via. a post request for further validation (i.e. to make sure the requested login data is in the system’s database). If all information is authenticated, the user is allowed access to the member page, otherwise an error is thrown.


public/js/member.js

The member Javascript file makes a get request to the api/user_data route to render the username (email) information on the member.html file, at the time of user login. 


public/js/signup.js

The signup Javascript has several functions:
Once the user hits the signup button, first the Javascript validates that the user sends the appropriate information (email address and password) in a readable format. If the user is missing one or both pieces of information, the JavaScript forces the user to enter both pieces of information.

If the user inputs appropriate information, the Javascript scripts perform a sign-up function that includes make a post route to the api-route and if function performs completely, will then forward the user to the members.html page, otherwise throwing an error.


public/stylesheets/style.css

The style.css file provides the visual formatting/styling of the login, members and signup html files.


public/login.html

The login file is the first file that the user encounters in the client web browser. This file allows the user to enter their email and password to gain access to the members page.


public/member.html

The members file is the client web browser file that is rendered if the user’s email and password are authenticated by passport.js.


public/signup.html

The signup page is received in the client web browser if the user does not have an email and password entered within the sign-up database.  The user will set up the desired email address and password on this page which is processed by the signup.js page.

## routes 

routes/api-routes.js

For this file, api-routes.js requires the following npm packages and files: 

\`\`\`

index.js, user.js (models folder) to incoporate User model to api routes for database information access

passport.js for post and get requests related to email/password authentication and user set-up.

\`\`\`

api-routes.js issues post requests to api/login route to authenticate user email and passwords entered, to then allow the user to access the member site.

The file also issues post requests to enter new user email and password and if successful, allow the new user to log in to the member site, otherwise, issue an error message.

Api-route contains a logout route that receives get requests from the user at the time the user decides to log-off from the site.

Finally, api-route contains a user_data route that receives get requests from the user and obtains data for client use (id) to render to client. If the user is not the correct user, an empty json item is returned. Otherwise the get request issues user email and unique id information.


routes/html-routes.js

For this file, html-routes.js requires the following npm packages and files: 

\`\`\`

Built in Node path package for working with file and directory paths.

isAuthenticated.js middleware file to determine if a user is properly logged onto the site.

\`\`\`

html-routes.js provides get requests from users to access the members page. If email and password are successfully authenticated from existing members or email and password are successfully generated for new users, the user gains access to the member page. 

html-routes.js also provides a get request from the user to access the members page. To obtain access, the user must have a username and password that are approved(authenticated) by the middleware file.




## package-lock.json

The package-lock.json is an automatically generated file, upon installation of a npm package, serving as a directory of dependencies and related dependencies installed.

## package.json

The package.json file is generated when a new Node project is initiated.  The file provides the metadata of the project, including license, author, git-repository and any dependencies used by the project.

## server.js

The server.js file is the file that operates the final Node application. 
For this application, server.js requires the following npm packages and files: 

\`\`\`

Express to set up server; 

Express-session to track login status for each user that accesses the site

Passport.js to complete the login authentication process

Import model files (index.js and user.js); which import the Sequelize database information; part of user username and password set up and recall 

Imports api-routes and html routes to perform appropriate get and put requests between the user and the back-end/server of email/password entry and access to the member site

\`\`\`

Express sets up the server port and prior to running the server, the db.sequelize.sync() method syncs the sequelize database items to the code for access to the database for get and post requests.
Finally, the server.js server is run and allows database for site use by the user.

## Instructions_for_updates

Indicate passwords are case sensitive or make them not case sensitive

Right now the application does not indicate at sign-up whether passwords are case sensitive or not; therefore, the user may not know that when the password is created to pay attention to password generated
For future development, I recommend to make the password non-case sensitive or notify the user that the password created is case-sensitive at sign-up screen.


Length of password currently only requires one character

I would recommend for future development  that a minimum character limit (min 6-8 characters) be placed on passwords created.


Fix “object object” when someone tries to sign up with existing information.

Currently when an existing user attempts to sign-up again, currently an [object] [object] warning appears, rather than “User account already generated” or similar verbiage.
I would recommend that this bug be fixed to provide verbiage that the user already has a profile in the database, instead of the current message. 


Forget password?

Currently, the application does not have a method for the user to recover or reset the password if forgotten.
I would recommend adding a mechanism, if possible, for the user to recover his/her password or reset the password. 

