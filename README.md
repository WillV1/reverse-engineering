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



## node_modules

The node_modules folder contains all the dependencies used to allow the npm packages to work in their respective files.

## public 



## routes 



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


