# Secure Auth Server with MongoDB Backend Boilerplate

Starting boilerplate for a secure auth server for web and mobile projects. 

The authentication method this boilerplate uses are **email and password**.

The backend this boilerplate written for is Mongodb. 

You will need to supply a config.js housing your secret key.  I can't tell you mine because... secrets and whatnot. 😉

With this project, you have routes configured for signing up and loggin in a user.  A secure [JWT Token](https://jwt.io/) will be generated both on the server and locally and assigned to the user. This way, the user can access multiple domains securely with just their JWT Token.

## Prerequisites
Must have node installed.  Refer to [this link](https://nodejs.org/en/ "Node Homepage") for installation instructions.
Must have mongodb installed. Refer to [this link](https://docs.mongodb.com/manual/administration/install-community/ "MongoDb Community Edition Installation") for installation instructions.

Optional, have [Postman](https://www.getpostman.com/ "Postman Homepage") installed just to confirm that you can get and recieve tokens for signing up and loggin in.


## Getting Started
Clone this repo

```
git clone git@github.com:adriandeveloper/mongodb-auth-serverBoilerplate.git
```

Cd to the directory where you cloned this repo and run
```
npm install
```

To install all the necessary packages.

## Usage

You will need two tabs in your terminal.  One for running nodemon and the other for running mongod

### Nodemon tab
Run in terminal:
```
npm run dev
```

### MongoDB tab
Run in terminal:
```
mongod
```

## IMPORTANT!
You WILL need to create a config.js file and place your secret in there.  

Basically copy this:

```
module.exports = {
  secret: // Add a string here for your secret
}
```

... into your config.js file and plug in a string for your secret.
In the gitignore, there is an option to not allow the config.js file to be pushed up to github.  

### User sign up
The fastest way to verify that the initial setup is good to go is to open up postman, create a POST request to ```localhost:3090/signup``` and supply an email and password in the 'Body' section. 

* Be sure to have raw and JSON(application/json) selected in Postman

Once signin has been successful, you will be given an JWT Token.

<p align="center">
  <img src="https://i.imgur.com/3pw46dr.png">
</p>

Due note that if you try to sign up again with the same email password, you will get the following error:

```
{
    "error": "Email is in use"
}
```

### User sign in
To verify signin, create a post request to ```localhost:3090/signin``` and use the same email and password you provided. You will recieve a local JWT Token

<p align="center">
  <img src="https://i.imgur.com/WAraQix.png">
</p>

### Testing
The root route is protected. This is thanks to adding ```requireAuth``` to the  get request.

You will need to copy your token that you have generated with your signin and add that to the header in your get requst in Postman.  Ensure that you specify the ```Key``` as ```authorization``` and the ```Value``` as the token that have been issues.  If all is well you should recieve this following in the res.body:

```
{
    "hi": "there"
}
```

EX:

<p align="center">
  <img src="https://i.imgur.com/gZFQTdG.png">
</p>



## Todos
Here is what is on the TODO list for this setup

- Sign out request
- Make branches for other backends PostgreSQL, SQL, DyanoDB, etc...
- Clean up README.md

## License
MIT
