# JS Snippets
---
##Javascript Notes &amp; Best Practices
- Keep global variables to a minimum because they are stored in memory
- You can call functions before they are declared because JavaScript is read before anything executes except when using function expressions- in which case you cannot call them before they are declared.
- use ‘use strict’, especially with es6
- Global variables are a bad idea, instead use closures and the module pattern
- Avoid using the line comment //. /* is much safer to use because it doesn’t cause errors when the line break is removed.
- Arrays can contain objects and vice versa
- Keep your code modularized and specialized.
- Don't nest loops inside loops as that also means taking care of several iterator variables (i,j,k,l,m...). Instead try to do specialized functions
- Loops can get slow, try to avoid large computations inside loops.
- If you find yourself creating lots and lots of HTML in JavaScript, you might be doing something wrong.

## Use .find(), the prefered method to use with data objects. Finds the match and exits the dataset.
      var placesData = [{"City":30,"State":"Albuquerque, New Mexico","Sum":504,"Population":557169,"PerCapita":"0.09%","Latitude":35.0853336,"Longitude":-106.6055534},{"City":47,"State":"Arlington, Texas","Sum":164,"Population":383204,"PerCapita":"0.04%","Latitude":32.735687,"Longitude":-97.1080656}];
      var city = 'Albuquerque, New Mexico';
      var place = placesData.find(function(item) {
        return (item.State == city);
      });
{% tonic %}
var placesData = [{"City":30,"State":"Albuquerque, New Mexico","Sum":504,"Population":557169,"PerCapita":"0.09%","Latitude":35.0853336,"Longitude":-106.6055534},{"City":47,"State":"Arlington, Texas","Sum":164,"Population":383204,"PerCapita":"0.04%","Latitude":32.735687,"Longitude":-97.1080656}];
var city = 'Albuquerque, New Mexico';
var place = placesData.find(function(item) {
  return (item.State == city);
});
{% endtonic %}
####Doing the same thing with forEach (still iterates over entire dataset)
      var placesData = [{"City":30,"State":"Albuquerque, New Mexico","Sum":504,"Population":557169,"PerCapita":"0.09%","Latitude":35.0853336,"Longitude":-106.6055534},{"City":47,"State":"Arlington, Texas","Sum":164,"Population":383204,"PerCapita":"0.04%","Latitude":32.735687,"Longitude":-97.1080656}];
      var city = 'Albuquerque, New Mexico';
      placesData.forEach(function(place) {
        if (place.State == city) {
          var state = place.State;
          return state;
        }
      });
####Doing the same thing using a for loop (still iterates over entire dataset)
      var placesData = [{"City":30,"State":"Albuquerque, New Mexico","Sum":504,"Population":557169,"PerCapita":"0.09%","Latitude":35.0853336,"Longitude":-106.6055534},{"City":47,"State":"Arlington, Texas","Sum":164,"Population":383204,"PerCapita":"0.04%","Latitude":32.735687,"Longitude":-97.1080656}];
      var city = 'Albuquerque, New Mexico';
      for (var i = 0; i < placesData.length; i++) {
        if (placesData[i].State == city) {
          var state = placesData[i].State;
          return state;
        }
      }
##Touch Events with jQuery
---
      $('obj').bind('touchstart', function(e){

      });

      or

      $('obj').bind('touchstart mousedown', function(e){
      });

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
####The Promise object is used for asynchronous computations. A Promise represents a value which may be available now, or in the future, or never.
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

##Mobile device useragent detection
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

##Module pattern with object literal return
######A closure is a special kind of object that combines two things: a function, and the environment in which that function was created.
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

##Namespacing module example
####By putting these into a configuration object and making this one public we make maintenance easy and allow for customization.
---
      var Configurator = Configurator || (function() {

        var config = {
          CSS:{
             classes:{
                current:'current',
                scrollContainer:'scroll'
             },
             IDs:{
                maincontainer:'carousel'
             }
          },
          labels:{
             previous:'back',
             next:'next',
             auto:'play'
          },
          settings:{
             amount:5,
             skin:'blue',
             autoplay:false
          },
       };

      someOtherFunction() {
        //some logic
      }

      function start() {
        //some logic
        someOtherFunction();
      }

      // public face of the module
      return {
          config: config,
          start: start
      };
    })();

    //Call the module:
    Configurator.start();

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

##Return array/object of keys in JS
######Return an array of objects according to key, value, or key and value matching
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
######Merges two (or more) objects, giving the last one precedence
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

##OO Prototype Inheritance
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

       ##jQuery scroll in view function
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

##Useragent test with JS
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
######When custom play button clicked, alternate play/pause on hover
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
