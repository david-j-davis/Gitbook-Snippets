# NPM
---
##Best Practices
[Reference](https://cdn.ampproject.org/c/blog.risingstack.com/nodejs-at-scale-npm-best-practices/amp/)

* See current version of npm with ```npm version```
* ```npm init --yes``` allows you to quick start a package.json file, but first set defaults: ```npm config set init.author.name YOUR_NAME``` and ```npm config set init.author.email YOUR_EMAIL```
* Look up the health and popularity of certain modules with [npms.io](https://npms.io)
* To visit the home page of modules do: ```npm home your_package_name```
* To check issues with module do: ```npm bugs your_package_name```
* If you want to check your package's repo do: ```npm repo your_package_name```
* Save a module to your package.json with ```npm install your_package_name --save``` or ```npm install your_package_name --save-dev```
* It’s possible to have different versions locally then on production, if in the meantime someone just released a new version. The problem will arise, when this new version has some bug which will affect your production system. To solve this issue, you may want to use ```npm shrinkwrap```
* Check for outdated depencencies with ```npm outdated```
* Don't install development depencencies in production
* To install production dependencies only, run this ```npm install --production```. Alternatively you can set the NODE_ENV to production: ```NODE_ENV=production npm install```
* When developing packages locally use ```npm link```

####Using npm instead of grunt/gulp
[Reference](Reference: https://css-tricks.com/why-npm-scripts/)

      //Command Line:
      npm install --save-dev node-sass
      npm install --save-dev postcss-cli autoprefixer
      npm install -g eslint
      eslint --init
      npm install --save-dev eslint
      npm install --save-dev uglify-js
      npm install --save-dev imagemin-cli
      npm install --save-dev svgo svg-sprite-generator
      npm install --save-dev browser-sync
      npm install --save-dev onchange
      npm install --save-dev parallelshell

      #package.json:
      "scripts": {
        "scss": "node-sass --output-style nested --indent-type tab --indent-width 4 -o dist/css src/scss",
        "autoprefixer": "postcss -u autoprefixer --autoprefixer.browsers '&gt; 5%, ie 9' -r dist/css/*",
        "imagemin": "imagemin src/images dist/images -p",
        "lint": "eslint js",
        "uglify": "mkdir -p dist/js &amp;&amp; uglifyjs src/js/*.js -m -o dist/js/app.js &amp;&amp; uglifyjs src/js/*.js -m -c -o dist/js/app.min.js",
        "icons": "svgo -f src/images/icons &amp;&amp; mkdir -p dist/images && svg-sprite-generate -d src/images/icons -o dist/images/icons.svg",
        "serve": "browser-sync start --server --files 'dist/css/*.css, dist/js/*.js'",
        "build:images": "npm run imagemin && npm run icons",
        "build:css": "npm run scss && npm run autoprefixer",
        "build:js": "npm run lint && npm run uglify",
        "build:all": "npm run build:css && npm run build:js && npm run build:images",
        "watch:images": "onchange 'images' -- npm run build:images",
        "watch:css": "onchange 'src/scss/*.scss' -- npm run build:css",
        "watch:js": "onchange 'src/js/*.js' -- npm run build:js",
        "watch:all": "parallelshell 'npm run serve' 'npm run watch:css' 'npm run watch:images' 'npm run watch:js'",
        "postinstall": "npm run watch:all"

      }
