# Nodejs
---
####Structure notes
      // DON'T

      ├── controllers
      |   ├── product.js
      |   └── user.js
      ├── models
      |   ├── product.js
      |   └── user.js
      ├── views
      |   ├── product.hbs
      |   └── user.hbs

The problems with this approach are:

- to understand how the product pages work, you have to open up three different directories, with lots of context switching,
- you end up writing long paths when requiring modules: require('../../controllers/user.js')
- Instead of this, you can structure your Node.js applications around product features / pages / components. It makes understanding a lot easier:

      // DO

      ├── product
      |   ├── index.js
      |   ├── product.js
      |   └── product.hbs
      ├── user
      |   ├── index.js
      |   ├── user.js
      |   └── user.hbs

Use these files only to export functionality, like:

      // product/index.js
      var product = require('./product')

      module.exports = {  
        create: product.create
      }

Put your additional test files to a separate test folder to avoid confusion.

      .
      ├── test
      |   └── setup.spec.js
      ├── product
      |   ├── index.js
      |   ├── product.js
      |   ├── product.spec.js
      |   └── product.hbs
      ├── user
      |   ├── index.js
      |   ├── user.js
      |   ├── user.spec.js
      |   └── user.hbs


      Node Hero - Node.js Project Structure Tutorial
       10 hours ago
       Node.js · nodehero · tutorial · project structure · folder structure
      This is the 7th part of the tutorial series called Node Hero - in these chapters, you can learn how to get started with Node.js and deliver software products using it.

      Most Node.js frameworks don't come with a fixed directory structure and it might be challenging to get it right from the beginning. In this tutorial, you will learn how to properly structure a Node.js project to avoid confusion when your applications start to grow.

      Upcoming and past chapters:

      Getting started with Node.js
      Using NPM
      Understanding async programming
      Your first Node.js HTTP server
      Node.js database tutorial
      Node.js request module tutorial
      Node.js project structure tutorial [you are reading it now]
      Authenticating users
      Testing Node.js applications
      Debugging Node.js
      Securing your application
      Deploying Node.js application to a PaaS
      Monitoring and operating Node.js applications
      The 5 fundamental rules of a Node.js Project Structure

      There are a lot of possible ways to organize a Node.js project - and each of the known methods has their ups and downs. However, according to our experience, developers always want to achieve the same things: clean code and the possibility of adding new features with ease.

      In the past years at RisingStack, we had a chance to build efficient Node applications in many sizes, and we gained numerous insights regarding the dos and donts of project structuring.

      We have outlined five simple guiding rules which we enforce during Node.js development. If you manage to follow them, your projects will be fine:

      Rule 1 - Organize your Files Around Features, Not Roles

      Imagine, that you have the following directory structure:

      // DON'T
      .
      ├── controllers
      |   ├── product.js
      |   └── user.js
      ├── models
      |   ├── product.js
      |   └── user.js
      ├── views
      |   ├── product.hbs
      |   └── user.hbs
      The problems with this approach are:

      to understand how the product pages work, you have to open up three different directories, with lots of context switching,
      you end up writing long paths when requiring modules: require('../../controllers/user.js')
      "Rule 1: Organize your files around features, not roles!" via @risingstack

      CLICK TO TWEET

      Instead of this, you can structure your Node.js applications around product features / pages / components. It makes understanding a lot easier:

      // DO
      .
      ├── product
      |   ├── index.js
      |   ├── product.js
      |   └── product.hbs
      ├── user
      |   ├── index.js
      |   ├── user.js
      |   └── user.hbs
      Rule 2 - Don't Put Logic in index.js Files

      Use these files only to export functionality, like:

      // product/index.js
      var product = require('./product')

      module.exports = {  
        create: product.create
      }
      Rule 3 - Place Your Test Files Next to The Implementation

      Tests are not just for checking whether a module produces the expected output, they also document your modules (you will learn more on testing in the upcoming chapters). Because of this, it is easier to understand if test files are placed next to the implementation.

      "Rule 3: Place your test files next to the implementation." via @risingstack

      CLICK TO TWEET

      Put your additional test files to a separate test folder to avoid confusion.

      .
      ├── test
      |   └── setup.spec.js
      ├── product
      |   ├── index.js
      |   ├── product.js
      |   ├── product.spec.js
      |   └── product.hbs
      ├── user
      |   ├── index.js
      |   ├── user.js
      |   ├── user.spec.js
      |   └── user.hbs
      Rule 4 - Use a config Directory

To place your configuration files, use a config directory.

      .
      ├── config
      |   ├── index.js
      |   └── server.js
      ├── product
      |   ├── index.js
      |   ├── product.js
      |   ├── product.spec.js
      |   └── product.hbs

Create a separate directory for your additional long scripts in package.json

      .
      ├── scripts
      |   ├── syncDb.sh
      |   └── provision.sh
      ├── product
      |   ├── index.js
      |   ├── product.js
      |   ├── product.spec.js
      |   └── product.hbs
