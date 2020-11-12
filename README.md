# Task Manager API


## Description
Developed task-manager API using Node.js, Express, Mongoose, Postman, MongoDB Atlas, and SendGrid - Email Delivery Service.

## Setup

1. Download or clone the repository
2. Open the project folder at the root in your terminal and run ```npm install``` to download the necessary dependencies needed for this project.
3. Run in development mode to run the Express server which defaults to ```localhost:3000```.
```
 npm run dev 
```
4. Setup Environment variables

    1. First setup a config folder with the variables

    2. PORT=Setup your port for the application run on Express Module

    3. SENDGRID_API_KEY=This is a API key provided by sendgrid.com (you can have a free plan by registering)

    4. MONGODB_URL=MongoDb Database URL

    5. JWT_SECRET=Json Web Token Secret Key

File-   `./config/dev.env` 

```
{
  JWT_SECRET: thisIsASecretKey // JSONWEBTOKEN SECRET STRING
  MONGODB_URL:mongodb://127.0.0.1:27017/task-manager-api// CONNECTION STRING
  SENDGRID_API_KEY: MyAPIKey // SENDGRID API KEY
  PORT: 3000// LISTEN ON PORT
}
```

## Deployed
1. The application is deployed on Heroku, https://node-ashish9-task-manager.herokuapp.com/. 

2. User can install ```Postman``` and config it to my Heroku website to perform ```CRUD operations``` using GET, POST, PATCH, DELETE on the Mongodb Atlas Database.

# The different usable url paths:

## Users paths
- Create a user
### Method & path:
POST /users

#### Data needed:
```
                {
                    "name": "Ashish",
                    "email": "ashish@example.com",
                    "password": "ashish123"
                }
            
```
You should receive an email as soon as the user is created

Password conditions:

  1 Must not contain the word "password"
  
  2 Must contain, at least, 7 characters
#### Returned data:
                {
                    "user": {
                        "age": 0,
                        "_id": "5e883e7...",
                        "name": "Ashish",
                        "email": "ashish@example.com",
                        "createdAt": "2020-04-04T07:59:53.719Z",
                        "updatedAt": "2020-04-04T07:59:53.758Z",
                        "__v": 1
                    },
                    "token": "eyJhbGciOi..."
                }
            
In case of of error an "errors" key is send back

- ## Login a user
#### Method & path:
POST /users/login

#### Data needed:
```
                {
                    "email":"ashish@example.com",
                    "password":"ashish123"
                } 
  ```          
#### Returned data:
```
                The same than the ones returned while creating a user
```       
- ## Logout a user
#### Method & path:
POST /users/logout

The user is logged out using its token

- ## Logout a user from all devices
#### Method & path:
POST /users/logoutAll

#### Data needed:
The user is logged out from all its devices using its tokens

- ## Update a user
#### Method & path:
PATCH /users/me

#### Data needed:
```
You can update the name, age, email or password

                {
                    "age": 26,
                    "name": "Dinku",
                }
   ```         
#### Password conditions:

  1. Must not contain the word "password"
  2. Must contain, at least, 7 characters
#### Returned data:
```
                {
                    "user": {
                        "age": 26,
                        "_id": "5e883e7...",
                        "name": "Dinku",
                        "email": "ashish@example.com",
                        "createdAt": "2020-04-04T07:59:53.719Z",
                        "updatedAt": "2020-04-04T07:59:53.758Z",
                        "__v": 1
                    },
                    "token": "eyJhbGciOi..."
                }
```
- ## Delete a user
#### Method & path:
DELETE /users/me

#### Data needed:
The token is used

#### Returned data:
```
                {
                    "user": {
                        "age": 26,
                        "_id": "5e883e7...",
                        "name": "Dinku",
                        "email": "ashish@example.com",
                        "createdAt": "2020-04-04T07:59:53.719Z",
                        "updatedAt": "2020-04-04T07:59:53.758Z",
                        "__v": 1
                    },
                    "token": "eyJhbGciOi..."
                }
```
            
- ## Read profile
#### Method & path:
GET /users/me

#### Data needed:
The token is used

#### Returned data:
```
                {
                    "user": {
                        "age": 0,
                        "_id": "5e883e7...",
                        "name": "Ashish",
                        "email": "ashish@example.com",
                        "createdAt": "2020-04-04T07:59:53.719Z",
                        "updatedAt": "2020-04-04T07:59:53.758Z",
                        "__v": 1
                    },
                    "token": "eyJhbGciOi..."
                }
```
            
- ## Uploading an Image
#### Method & path:
POST /users/me/avatar

#### Data needed:
enctype="multipart/form-data", the key must be named "avatar"

Delete an Image
Method & path:
DELETE /users/me/avatar

Data needed:
The token is used

# Tasks paths
- ## Create a task
#### Method & path:
POST /tasks

#### Conditions:
User must be connected and have a token

#### Data needed:
```
                {
                    "description": "First",
                    "completed": false
                }
```
            
The "completed" key is not required, its default value is false.

#### Returned data:
```
                {
                    "completed": false,
                    "_id": "5e884...",
                    "description": "First",
                    "owner": "5e883e7...",
                    "createdAt": "2020-04-04T09:05:42.877Z",
                    "updatedAt": "2020-04-04T09:05:42.877Z",
                    "__v": 0
                }
  ```
- ## Read a specific task
#### Method & path:
GET /tasks/:id'

#### Conditions:
replace /:id in the url by the id's task

#### Returned data:
```
                {
                    "completed": false,
                    "_id": "5e884...",
                    "description": "First",
                    "owner": "5e883e7...",
                    "createdAt": "2020-04-04T09:05:42.877Z",
                    "updatedAt": "2020-04-04T09:05:42.877Z",
                    "__v": 0
                }
 ```
            
 - ## Read all the tasks
#### Method & path:
GET /tasks

#### Data needed:
The token is used

#### Returned data:
A table of task objects is returned
```
                [
                    {
                        "completed": false,
                        "_id": "5e884...",
                        "description": "First",
                        "owner": "5e883e7...",
                        "createdAt": "2020-04-04T09:05:42.877Z",
                        "updatedAt": "2020-04-04T09:05:42.877Z",
                        "__v": 0
                    }
                ]
```
            
#### Options
Filtering your tasks
To fetch only the complete/incomplete tasks use the completed key in the query with true or false

/tasks?completed=false

 - Sortering your tasks
You can sort your tasks by description/completed/createdAt/updatedAt

- /tasks?sortBy=description:desc
- /tasks?sortBy=completed:desc
- /tasks?sortBy=createdAt:desc
- /tasks?sortBy=updatedAt:desc
- :desc => descending order, :asc => ascending order

- ## Update a task
#### Method & path:
PATCH /tasks/:id'

#### Conditions:
Replace /:id in the url by the id's task

- ## Delete a task
#### Method & path:
DELETE /tasks/:id'

#### Conditions:
Replace /:id in the url by the id's task

- ## Add a picture to a task
#### Method & path:
POST /tasks/:id/picture

#### Conditions:
replace /:id/ in the url by the id's task

#### Data needed:
enctype="multipart/form-data", the key must be named "taskPicture"

Returned data:
```
                {
                    "completed": false,
                    "_id": "5e884...",
                    "description": "First",
                    "owner": "5e883e7...",
                    "createdAt": "2020-04-04T09:05:42.877Z",
                    "updatedAt": "2020-04-04T10:11:39.660Z",
                    "__v": 0
                }
```            
- ## Display task's picture
#### Method & path:
GET /tasks/:id/picture

#### Conditions:
replace /:id/ in the url by the id's task

#### Returned data:
Return the picture

- ## Delete task's picture
#### Method & path:
DELETE /tasks/:id/picture

#### Conditions:
Replace /:id/ in the url by the id's task

#### Returned data:
Return the task
```
                {
                    "completed": false,
                    "_id": "5e884...",
                    "description": "First",
                    "owner": "5e883e7...",
                    "createdAt": "2020-04-04T09:05:42.877Z",
                    "updatedAt": "2020-04-04T10:20:43.254Z",
                    "__v": 0
                }
 ```           
 
 ## Technology used:

- Node.js (JavaScript runtime) with Express framework and Mongoose for modelling data
- NPM packages and services 
    - JWT, bcrypt(authentication)
    - Multer (Node.js Middleware), 
    - Sharp  Files and Images formatting (e.g. JPEG, JPG, PNG, PDF, DOC, DOCX, etc.) 
    - SendGrid (Email Delivery Service)
    - validator - Type Validators (e.g. emails, etc.)
    - env-cmd - Config environment variables
- Postman to make HTTP requests (authentication via token, forms) and set up environments for development and production
- Heroku to deploy the API
- MongoDB Atlas((DaaS:Database-as-a-Service)) and MongoDB Compass and Robo 3T as MongoDB GUIs



