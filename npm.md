# NPM
---
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
