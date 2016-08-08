# JS Snippets
---
##Javascript Best Practices
- Keep global variables to a min. because they are stored in memory
- You can call functions before they are declared because JavaScript is read before anything executes except when using function expressions- in which case you cannot call them before they are declared.
- use ‘use strict’, especially with es6
- Arrays can contain objects and vice versa

##AJAX jQuery Example
---

    $(document).ready(function () {

     $('form').submit(function(e) {
          e.preventDafault();
          var url = $(this).attr("action");
          //Grab data
          var formData = $(this).serialize();
          //Post data
          $.ajax(url, {
               data: formData,
               type: "POST",
               success: function(response) {
                    $(#some-div).html(response);
               };

          }).fail(function (jqXHR) {
               $('#myDiv').html("<p>Sorry! " + jqXHR.statusText + "error.</p>");
          }); //End ajax

     }); //End submit function
     }); //End DOM ready

##AJAX JavaScript example
 ---
    var xhr = new XMLHttpRequest();
    xhr.open('get', 'https://api.github.com/search/repositories?q=go');
    xhr.addEventListener('readystatechange', function() {
      console.log(xhr.readyState);
      //readyState equal to 4 means call is complete
      if (xhr.readyState === 4) {
        if (xhr.status == 200) {
        var resp = JSON.parse(xhr.responseText);
        //console.log(resp);
        //console.log(resp.items);
        $scope.items = resp.items;
        $rootScope.items_info = "changed the items array";
        console.log($rootScope.item_info);
        //$scope.$digest(); // updates the rootscope
        $scope.$apply(); //most time you want to use this though it has performance issues
        }
      }
    });
    xhr.send();

##AJAX JavaScript example with multiple get functions
---
      function get(url, callback) {
        var xhr = new XMLHttpRequest();
        xhr.open('get', url);
        xhr.addEventListener('readystatechange', function () {
            if (xhr.readyState === 4) {
                if (xhr.status === 200) {
                    console.log('successful ... should call callback ... ');
                    callback(null, JSON.parse(xhr.responseText));
                } else {
                    console.log('error ... callback with error data ... ');
                    callback(xhr, null);
                }
            }
        });
        xhr.send();
      }

      get('https://api.github.com/search/repositories?q=nodejs', function (err, data) {
          if (err) console.log('error, xhr: ', xhr);
          else console.log(data);
      }); // 63342, 3000
      get('https://api.github.com/search/repositories?q=iot', function (err, data) {
          if (err) console.log('error, xhr: ', xhr);
          else console.log(data);
      });

##AJAX JavaScript example with multiple get functions and Promise
---
      var terms = ['nodejs', 'iot', 'go'];

      function get(url, callback) {
          var xhr = new XMLHttpRequest();
          xhr.open('get', url);
          xhr.addEventListener('readystatechange', function () {
              if (xhr.readyState === 4) {
                  if (xhr.status === 200) {
                      console.log('successful ... should call callback ... ');
                      callback(null, JSON.parse(xhr.responseText));
                  } else {
                      console.log('error ... callback with error data ... ');
                      callback(xhr, null);
                  }
              }
          });
          xhr.send();
      }

      function getPromise(url) {
          return new Promise(function (resolve, reject) {
              get(url, function (err, result) {
                  if (err) reject(err);
                  else resolve(result);
              });
          });
      }

      var promises = terms.map(function (term) {
           return getPromise('https://api.github.com/search/repositories?q=' + term);
      });

      Promise.all(promises).then(function (data) {
          console.log(data);
      });

##Browser Detection
 Mobile device useragent detection
 ---
     function detectBrowser() {
        var useragent = navigator.userAgent;
        var mapdiv = document.getElementById("map");
        if (useragent.indexOf('iPhone') != -1 || useragent.indexOf('Android') != -1 ) {
          mapdiv.style.width = '100%';
          mapdiv.style.height = '100%';
        } else {
          mapdiv.style.width = '600px';
          mapdiv.style.height = '800px';
        }
      }

    $(document).ready(function(){
      if(!(navigator.userAgent.match(/Android/i) || navigator.userAgent.match(/iPhone/i) || navigator.userAgent.match(/iPod/i) || navigator.userAgent.match(/webOS/i) || navigator.userAgent.match(/IEMobile/i))){
        //logic
      } else {
        //logic
      }
    });

####JavaScript OO closure function
 A closure is a special kind of object that combines two things: a function, and the environment in which that function was created.
---

      var makeCounter = function() {
        var privateCounter = 0;
        function changeBy(val) {
          privateCounter += val;
        }
        return {
          increment: function() {
            changeBy(1);
          },
          decrement: function() {
            changeBy(-1);
          },
          value: function() {
            return privateCounter;
          }
        }  
      };
      //save an instance of makeCounter() as seperate variables
      var counter1 = makeCounter();
      var counter2 = makeCounter();

      counter1.increment();
      counter1.increment();
      alert(counter1.value()); // Alerts 2
      alert(counter2.value()); // Alerts 0

##JavaScript OO Prototype
- The first thing to put in every JavaScript file is the "use strict" declaration.
- To create an object definition, you define a constructor function.
- JavaScript is a little different, but this constructor function works a bit like a class.
- Most web languages have classes that define the properties and methods available in an object.
- You can create a method in a JavaScript object by adding a function to its prototype property.
---

    function Car(make) {
    "use strict";
    this.make = make;
    }

    Car.prototype.company = 'audi';

    var a6 = new Car('A6');

    console.log(a6.make);
    console.log(a6.company);


##JavaScript Namespacing function
---
    var Configurator = Configurator || (function() {

      someOtherFunction() {
        //some logic
      }

      function start() {
        //some logic
        someOtherFunction();
      }

      // public face of the module
      return {
          start: start
      };
    })();

    //Call the module:
    Configurator.start();

##JavaScript OO with ES6
---
    'use strict';

    class Person {
      constructor(name) {
        this.name = name;
      }
      sayHello() {
        console.log("hello from ", this.name);
      }
    }

    var sarath = new Person('Sarath');

    sarath.sayHello();

    //babel es6-compile.js --out-file es6.js

##jQuery $.when().done() callback
---
      $('.hamburger').on('click', function(){

        var toggleNav = function() {
          $('body').toggleClass('fixed');
          $('header, header nav').toggleClass('show');
          $('.hamburger .fa').toggleClass('hidden');
        }

        $.when( toggleNav() ).done(function() {
          var w = $(window).height();
          var n = $('header nav.show').height();
          //console.log(w + ',' + n);
          if (n > w) {
            $('header nav.show').css('height', w-60); //tel issue requires 60px
          }
        });

      });

##jQuery $.promise().done() callback
 ---
     $( "button" ).on( "click", function() {
      $( "p" ).append( "Started..." );

      $( "div" ).each(function( i ) {
        $( this ).fadeIn().fadeOut( 1000 * ( i + 1 ) );
      });

      $( "div" ).promise().done(function() {
        $( "p" ).append( " Finished! " );
      });
    });

##jQuery in view
---
    jQuery(document).ready(function($) {
    var s = $("html.desktop .release");
    s.each(function() {
            $(this).offset().top > $(window).scrollTop() + .75 * $(window).height() && $(this).addClass("hidden")
        }), $(window).on("scroll", function() {
            s.each(function() {
                $(this).offset().top <= $(window).scrollTop() + .75 * $(window).height() && $(this).hasClass("hidden") && $(this).removeClass("hidden").addClass("move")
            })
        })
    });

      CSS (example):

      .hidden {visibility:hidden}@-webkit-keyframes fadeInUp{0%{opacity:0;-webkit-transform:translateY(20px)}100%{opacity:1;-webkit-transform:translateY(0)}}@keyframes fadeInUp{0%{opacity:0;transform:translateY(20px)}100%{opacity:1;transform:translateY(0)}}

      .move {-webkit-animation-duration:1s;animation-duration:1s;-webkit-animation-fill-mode:both;animation-fill-mode:both;-webkit-animation-name:fadeInUp;animation-name:fadeInUp}

---

    //Scroll opacity function
    var changeOpacity = function(){
        var elements = $(‘.someDiv, .aSecondDiv');

                var st = $(this).scrollTop();
                elements.css({ 'opacity' : (1 - st/600) });

    }
    $(window).scroll(function(){
    changeOpacity();
    });

##Return array/object of keys in JS
 Return an array of objects according to key, value, or key and value matching
---

    function getObjects(obj, key, val) {
        var objects = [];
        for (var i in obj) {
            if (!obj.hasOwnProperty(i)) continue;
            if (typeof obj[i] == 'object') {
                objects = objects.concat(getObjects(obj[i], key, val));
            } else
            //if key matches and value matches or if key matches and value is not passed (eliminating the case where key matches but passed value does not)
            if (i == key && obj[i] == val || i == key && val == '') { //
                objects.push(obj);
            } else if (obj[i] == val && key == ''){
                //only add if the object is not already in the array
                if (objects.lastIndexOf(obj) == -1){
                    objects.push(obj);
                }
            }
        }
        return objects;
    }

    //return an array of keys that match on a certain value
    function getKeys(obj, val) {
        var objects = [];
        for (var i in obj) {
            if (!obj.hasOwnProperty(i)) continue;
            if (typeof obj[i] == 'object') {
                objects = objects.concat(getKeys(obj[i], val));
            } else if (obj[i] == val) {
                objects.push(i);
            }
        }
        return objects;
    }

    //return an array of values that match on a certain key
    function getValues(obj, key) {
        var objects = [];
        for (var i in obj) {
            if (!obj.hasOwnProperty(i)) continue;
            if (typeof obj[i] == 'object') {
                objects = objects.concat(getValues(obj[i], key));
            } else if (i == key) {
                objects.push(obj[i]);
            }
        }
        return objects;
    }
##Merge two Objects in JS
 Merges two (or more) objects, giving the last one precedence
---
    function merge(target, source) {
      if ( typeof target !== 'object' ) {         
        target = {};     
        }         
      for (var property in source) {                 
        if ( source.hasOwnProperty(property) ) {                         
          var sourceProperty = source[ property ];                         
          if ( typeof sourceProperty === 'object' ) {                 
            target[ property ] = util.merge( target[ property ], sourceProperty );                 
            continue;             }                         
            target[ property ] = sourceProperty;                     
            }             
            }         
            for (var a = 2, l = arguments.length; a < l; a++) {         
              merge(target, arguments[a]);     
              }         
              return target; };

##Smooth Scroll with jQuery
---
    var smoothScroll = function() {

    $('a[href*=#]:not([href=#])').click(function() {
    if (location.pathname.replace(/^\//,'') == this.pathname.replace(/^\//,'') && location.hostname == this.hostname) {
    var target = $(this.hash);
    target = target.length ? target : $('[name=' + this.hash.slice(1) +']');
    if (target.length) {
      $('html,body').animate({
      scrollTop: target.offset().top
    }, 500);
    return false;
    }
    }
    });
    }; smoothScroll();
---
    //smooth scroll on load
    jQuery(document).ready(function() {

        var hash = window.location.hash;

        if(hash != ""){
                var target = jQuery(hash);
                if(target.length){
                        jQuery('html,body').animate({
                        scrollTop: target.offset().top
                        }, 500);
                }
        }

       });

##Useragent with JS
---
    function getInternetExplorerVersion(){
    var rv = -1;
    if (navigator.appName == 'Microsoft Internet Explorer'){
        var ua = navigator.userAgent;
        var re  = new RegExp("MSIE ([0-9]{1,}[\.0-9]{0,})");
        if (re.exec(ua) != null)
        rv = parseFloat( RegExp.$1 );
    }
    return rv;
    };


    if (getInternetExplorerVersion() >= 10){
        $('body').addClass('ie11');
    };

##Useragent test with Modernizr
---
    //Add Modernizr test
    Modernizr.addTest('iOS6', function() {
        return /(iphone|ipad|ipod)\sOS\s6/i.test(navigator.userAgent);
    });
    Modernizr.load([{
        test: Modernizr.iOS6,
        yep: 'vendor/cycle2-ios6fix.js’,
         nope: …,
    }]);

##HTML5 Video jQuery Play/Pause
 When custom play button clicked, alternate play/pause on hover
---
    $('.video .play-button#play').on('click', function(e) {
        e.preventDefault();
        //console.log('you clicked it');
        if($('#video')[0].paused == true) {
            //console.log('paused is true');
            $('#video')[0].play();
            $('.video .play-button#play').fadeOut();
            checkHover();
        }
    });

    function checkHover() {
        $('.video').on('mouseover', function(){

            if( $('#video')[0].paused == true) {
               $('.video .play-button#play').stop().fadeIn();
            } else {
                $('.video .play-button#play').hide();
                $('.video .play-button#pause').stop().fadeIn();
                $('.video .play-button#pause').on('click', function(e){
                e.preventDefault();
                $('#video')[0].pause();
                $('.video .play-button#pause').hide();
                $('.video .play-button#play').stop().fadeIn();

                });

            }
        }).on('mouseout', function(){

            if( $('#video')[0].paused == false) {
                $('.video .play-button#pause').stop().fadeOut();
            } else {

            }

        });
    }
##Youtube API
- [Play button with youtube](https://css-tricks.com/play-button-youtube-and-vimeo-api/)
- [Youtube google dev](https://developers.google.com/youtube/player_parameters?hl=en)
---


      var player;

      function onPlayerReady(event) {

        // bind events
        var playButton = document.getElementById("yt-play-button");
        playButton.addEventListener("click", function() {
          player.playVideo();
        });

        var pauseButton = document.getElementById("yt-pause-button");
        pauseButton.addEventListener("click", function() {
          player.pauseVideo();
        });

          //set height of iframe to container
          //on player ready
          //Then on window resize adjust to parent container

      }

      function onYouTubePlayerAPIReady() {
        // create the global player from the specific iframe (#video)
        player = new YT.Player('video', {
          events: {
            // call this function when player is ready to use
            'onReady': onPlayerReady
          }
        });
      }

      // Load YouTube Frame API
      (function(){ //Closure, to not leak to the scope
        var s = document.createElement("script");
        s.src = "http://www.youtube.com/player_api"; /* Load Player API*/
        var before = document.getElementsByTagName("script")[0];
        before.parentNode.insertBefore(s, before);
      })();

##Touch Events with jQuery
---
      $('obj').bind('touchstart', function(e){

      });

      or

      $('obj').bind('touchstart mousedown', function(e){
      });
