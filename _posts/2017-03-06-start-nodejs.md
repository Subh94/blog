---
layout: blog
title: Getting Start With NodeJs and Express
category: blog
tags: [Node  Js, Express] 
summary: Here we will discuss about getting start with node js and writing a basic  website using node js.
image: /images/blog/nodejs_logo_green.jpg
---

## Introduction

There are tons of tutorial on web to write "Hello World!" program in node.js, but here we will discuss a how to write a complete simple app from scratch. We will also discuss aboute writing routing, playing with get, post, query, parameter and all. We will talk a little about installing node.js, express and other dependancy first, then we will move to writing app part. 

## Installation
This tutorial assume that you are running Ubuntu 16.04 and have ''sudo'' access on your system. 

For Installing Distro stable version

```
$ sudo apt-get update
$ sudo apt-get install nodejs 
#For npm installation 
$ sudo apt-get install npm
```

This is sufficient for working on node.js and enough for now, if you want to try latest or unstable version then follow this link [Node js instalation by package manager](https://nodejs.org/en/download/package-manager/)


Now we will install Express-generator, which will be used to generate express skelton code for our app. 

	$ npm install express-generator -g

Getting help for express 

	$ express -h

		Usage: express [options] [dir]
	
	  	Options:
	
	  	  -h, --help          output usage information
	  	      --version       output the version number
	  	  -e, --ejs           add ejs engine support
	  	      --hbs           add handlebars engine support
	  	      --pug           add pug engine support
	  	  -H, --hogan         add hogan.js engine support
	  	  -v, --view <engine> add view <engine> support (ejs|hbs|hjs|jade|pug|twig|vash) (defaults to jade)
	  	  -c, --css <engine>  add stylesheet <engine> support (less|stylus|compass|sass) (defaults to plain 	css)	
  	      --git           add .gitignore
  	  -f, --force         force on non-empty directory



Now let's cook some app with express, we are using ejs temple engine for this tutorial you can use some other one also like pug. 


	$ express --view=ejs myapp
		create : myapp
		create : myapp/package.json
		create : myapp/app.js
		create : myapp/public
		create : myapp/public/javascripts
		create : myapp/public/images
		create : myapp/routes
		create : myapp/routes/index.js
		create : myapp/routes/users.js
		create : myapp/public/stylesheets
		create : myapp/public/stylesheets/style.css
		create : myapp/views
		create : myapp/views/index.ejs
		create : myapp/views/layout.ejs
		create : myapp/views/error.ejs
		create : myapp/bin
		create : myapp/bin/www



Now we will look what dependencies we have in package.json and install them:
	

	{
	"name": "myapp",
	"version": "0.0.0",
	"private": true,
	"scripts": {
		"start": "node ./bin/www"
		},
		"dependencies": {
    	"body-parser": "~1.15.2",
    	"cookie-parser": "~1.4.3",
    	"debug": "~2.2.0",
    	"ejs": "~2.5.2",
    	"express": "~4.14.0",
    	"morgan": "~1.7.0",
    	"serve-favicon": "~2.3.0"
    	}
    }


Now Install them using:

	$ cd myapp
	$ npm install

Now to start application on MacOS or Linux, run:

	$ DEBUG=myapp:* npm start

and on Windows: 

	> set DEBUG=myapp:* & npm start

Let's see our app file tree and then we will move next

	.
	├── app.js
	├── bin
	│   └── www
	├── package.json
	├── public
	│   ├── images
	│   ├── javascripts
	│   └── stylesheets
	│       └── style.css
	├── routes
	│   ├── index.js
	│   └── users.js
	└── views
	    ├── error.ejs
	    ├── index.ejs
	    └── layout.ejs
	
	7 directories, 9 files

In route folder our routes part is written and in views folder our views exists, similarly public folder contain public file like stylesheets, image and statcs file. 

Now we will understand what and how routing file are used in application and how to extend them. 

## Understanding Routing 
Before understanding route file and content lets look how to add them in our application. 

Let's look for this code in app.js reside inq project root folder:

	1 | var index = require('./routes/index');
	2 | var users = require('./routes/users');
	3 |
	3 | app.use('/', index);
	4 | app.use('/users', users);

if you look closely then in first two line we have made a variable from __"./routes/index"__ and __"./routes/users"__ module and then we are using later with respective router in this __"app.use('/', index)"__  and __"app.use('/users', users)"__ line.

Let's look some code in routes/index.js

	1 | var express = require('express');
	2 | var router = express.Router();
	3 | 
	4 | /* GET home page. */
	5 | router.get('/', function(req, res, next) {
	6 |   res.render('index', { title: 'Express' });
	7 | });
	8 | 
	9 | module.exports = router;

Let's  consider this example, we  have used get method for root page or router and rendoring  a  template file with provided data in json format. We will check how to use this data into template file in view part. 


## Getting View part 

In above routing section, we checked how to write GET, POST, PUT method for routing and rendoring html file with some data,  now we will check here how to use this data in templates file to generate html file dynamically. 

Note: This method depends on choice of view engine for node, and may defer from your choice but concept will nearly same. Here we are using ejs templates engine, which is based on javascript syntax with html. syntax for your choice can be found on your view engine home page. 

First we will see how to include view engine in your main app.js located on root directory of your project. 

```
// view engine setup
app.set('views', path.join(__dirname, 'views'));
app.set('view engine', 'ejs');
```
here you can see, that how we have included view engine in app.js. You don't have to setup this, if you have used given method to generate skelton code. 

Now we will check index.ejs located in views folder
```
<!DOCTYPE html>
<html>
  <head>
    <title><%= title %></title>
    <link rel='stylesheet' href='/stylesheets/style.css' />
  </head>
  <body>
    <h1><%= title %></h1>
    <p>Welcome to <%= title %></p>
  </body>
</html>
```

Here you can spot <%= title %> in this code, this is variable title we have passed from get method as name title. in ejs you can specify variable using this <%= your variable name %>. 


## Finally 

now we will check how to run our site locally and how to access in web browser and in next part we will discuss more about writing routing using GET, POST and other method. 

Now got to root folder of project and type
```
npm start 
```

Now point your browser to localhost:3000 or 127.0.0.1:3000 and you will see page like this. 

![Alt](/blog/images/post/express-start.png)




##  Referances  
**1.** [https://expressjs.com/en/starter/generator.html](https://expressjs.com/en/starter/generator.html)