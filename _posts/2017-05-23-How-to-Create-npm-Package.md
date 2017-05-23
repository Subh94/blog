---
layout: blog
title: Creating npm module
category: blog
tags: [Node  Js, npm] 
summary: How to create a new npm package
image: /images/blog/npm-package.png
---


Node.js  module is  one kind of package which can be published to npm and use as a dependancy for Node.js application to extent functionality.

[Download Codes for this tutorial](https://github.com/Subh94/npm-module-tutorial)

Here we will talk about, how to create a  Node.js module from scratch. 

As a example we are going to start with greeting module, which will take name as parameter and return greeting. 


create a directory name greeting and cd into that
```
mkdir greeting
cd greeting
```

Generate package.json for this module using npm and follow instructions
```
npm init
```

We are going to keep this module too simple, so we are using single file for function. 

Create a new file named index.js with following code
```
function greeting(name, callback){
        var message = "Hello "+name+"!"
        callback(message);
}

module.exports.greeting = greeting;
```

Now change into parent directory, and install package using npm command and import that package into new JavaScript file.
```
cd ..
npm install greeting/
vim test.js
```

insert following line of code into test.js 
```
var greet = require("greeting");

greet.greeting("Subhash", function(message){
    console.log(message);
});
```

Check following output while running "node test.js" command
```
$ node test.js 
Hello Subhash!
````

You can publish your Node.js module  using "npm publish" command, you will promoted to create a new user if not logged in. 



##  References  
**1.** [Creating Node.js modules](https://docs.npmjs.com/getting-started/creating-node-modules)