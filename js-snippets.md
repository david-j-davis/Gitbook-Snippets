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

####Live Example
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
      });
      get('https://api.github.com/search/repositories?q=iot', function (err, data) {
          if (err) console.log('error, xhr: ', xhr);
          else console.log(data);
      });

##Promises
####The Promise object is used for asynchronous computations. A Promise represents a value which may be available now, or in the future, or never.

      var calculatePromise = new Promise(function(resolve, reject) {
        setTimeout(function(){
          resolve(1 + 1);
        }, 1000);
      });

      function addTwo(value) {
        return value + 2;
      }

      function printFinalValue(nextValue) {
       console.log("The final value is", nextValue);
      }

      calculatePromise
        .then(addTwo)
        .then(printFinalValue);

####Live example
{% tonic %}
var calculatePromise = new Promise(function(resolve, reject) {
  setTimeout(function(){
    resolve(1 + 1);
  }, 1000);
});

function addTwo(value) {
  return value + 2;
}

function printFinalValue(nextValue) {
 console.log("The final value is", nextValue);
}

calculatePromise
  .then(addTwo)
  .then(printFinalValue);
{% endtonic %}

##AJAX example with multiple get functions and Promise
---
      var terms = ['Brainf**k', 'Velato', 'Ook!'];

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
      }).catch(function(error) { console.log(error) });

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

##[Module Pattern: Object Literal return][1]
One of the easiest patterns is the same as we’ve declared above, the Object has no name declared locally, we just return an Object and that’s it
 ---

      var Module = (function () {

      var privateMethod = function () {};

        return {
          publicMethodOne: function () {
          // I can call `privateMethod()` you know...
          },
          publicMethodTwo: function () {

          },
          publicMethodThree: function () {

          }
        };

      })();

      Module.publicMethodOne();
      Module.publicMethodTwo();
      Module.publicMethodThree();

##[Module Pattern: Locally scoped Object Literal][2]
Local scope means a variable/function declared inside a scope. It’s much easier to see what is public, because they’ll have a locally scoped namespace attached
 ---
      var Module = (function () {

        // locally scoped Object
        var myObject = {};

        // declared with `var`, must be "private"
        var privateMethod = function () {};

        myObject.someMethod = function () {
          // take it away Mr. Public Method
        };

        return myObject;

      })();
##[Module Pattern: Stacked locally coped Object Literal][3]
Pretty much identical as the previous example, but uses the “traditional” single Object Literal notation
 ---
      var Module = (function () {

        var privateMethod = function () {};

        var myObject = {
          someMethod:  function () {

          },
          anotherMethod:  function () {

          }
        };

        return myObject;

      })();
##[Revealing Module Pattern][4]
We reveal public pointers to methods inside the Module’s scope. You can clearly see and define which methods are shipped back to the Module.
 ---
      var Module = (function () {

        var privateMethod = function () {
          // private
        };

        var someMethod = function () {
          // public
        };

        var anotherMethod = function () {
          // public
        };

        return {
          someMethod: someMethod,
          anotherMethod: anotherMethod
        };

      })();
##[Augmenting Modules][5]
Pass in our Module namespace, which gives us access to our Object to extend. notice I’ve passed in Module || {} into my second ModuleTwo, this is incase Module is undefined - we don’t want to cause errors now do we ;). What this does is instantiate a new Object, and bind our extension method to it, and return it.

      var ModuleTwo = (function (Module) {

          Module.extension = function () {
               // another method!
           };

           return Module;


      })(Module || {});

{% tonic %}
var Module = (function () {

  var privateMethod = function () {
    // private
  };

  var someMethod = function () {
    // public
  };

  var anotherMethod = function () {
    // public
  };

  return {
    someMethod: someMethod,
    anotherMethod: anotherMethod
  };

})();

var ModuleTwo = (function (Module) {

    Module.extension = function () {
        // another method!
    };

    return Module;

})(Module || {});

console.log(Module);
{% endtonic %}

####Live Example
{% tonic %}
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
console.log(counter1.value()); // Alerts 2
console.log(counter2.value()); // Alerts 0
{% endtonic %}
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
        console.log('someOtherFunction was called. Let\'s console out the config object:' + config);
        //some other logic
      }

      function start() {
        console.log('start function was called.')
        someOtherFunction();
        //some other logic
      }

      // public face of the module
      return {
          config: config,
          start: start
      };
    })();

    //Call the module:
    Configurator.start();

####Live Example
{% tonic %}
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
  console.log('someOtherFunction was called. Let\'s console out the config object:' + config);
  //some other logic
}

function start() {
  console.log('start function was called.')
  someOtherFunction();
  //some other logic
}

// public face of the module
return {
    config: config,
    start: start
};
})();

//Call the module:
Configurator.start();
{% endtonic %}

##OO Prototype Inheritance. Adapted from [RisingStack][6]
- To create an object definition, you define a constructor function.
- JavaScript is a little different, but this constructor function works a bit like a class.
- Most web languages have classes that define the properties and methods available in an object.
- You can create a method in a JavaScript object by adding a function to its prototype property.
---

//Constructor
var LivingEntity = function(location){
this.x = location.x;
this.y = location.y;
this.z = location.z;
};

//New instance
var dog = new LivingEntity({
x: 5,
y: 0,
z: 1
});

//we can add a single anonymous function to the prototype chain!
LivingEntity.prototype.makeSound = function(){
console.log('meow');
}

//dog uses its prototype because it doesn't have makeSound as an attribute
dog.makeSound(); //meow

dog.makeSound = function(){
console.log('woof');
}

//now dog has makeSound as an attribute, it will use that instead of it's prototype
dog.makeSound(); //woof

/*The Prototype Chain
Every object has a prototype, including the prototype object. This "chain" goes all the way back until it reaches an object that has no prototype, usually Object's prototype. Prototype's version of "Inheritance" involves adding another link to the end of this prototype chain, as shown below.*/

var Dragon = function(location){

// <Function>.call is a method that executes the defined function,
// but with the "this" variable pointing to the first argument,
// and the rest of the arguments being arguments of the function
// that is being "called". This essentially performs all of
// LivingEntity's constructor logic on Dragon's "this".

LivingEntity.call(this, location);
//canFly is an attribute of the constructed object and not Dragon's prototype
this.canFly = true;
};

// Object.create(object) creates an object with a prototype of the
// passed in object. This example will return an object
// with a prototype that has the "moveWest" and "makeSound" functions,
// but not x, y, or z attributes.

Dragon.prototype = Object.create(LivingEntity.prototype);

// If we didn't reset the prototype's constructor
// attribute, it would look like any Dragon objects
// were constructed with a LivingEntity constructor

Dragon.prototype.constructor = Dragon;

// Now we can assign prototype attributes to Dragon without affecting
// the prototype of LivingEntity.

Dragon.prototype.fly = function(y){
this.y += y;
}

var sparky = new Dragon({
x: 0,
y: 0,
z: 0
});


####Live Example
{% tonic %}
//Constructor
var LivingEntity = function(location){
this.x = location.x;
this.y = location.y;
this.z = location.z;
};

//New instance
var dog = new LivingEntity({
x: 5,
y: 0,
z: 1
});

//we can add a single anonymous function to the prototype chain!
LivingEntity.prototype.makeSound = function(){
console.log('meow');
}

//dog uses its prototype because it doesn't have makeSound as an attribute
dog.makeSound(); //meow

dog.makeSound = function(){
console.log('woof');
}

//now dog has makeSound as an attribute, it will use that instead of it's prototype
dog.makeSound(); //woof

/*The Prototype Chain
Every object has a prototype, including the prototype object. This "chain" goes all the way back until it reaches an object that has no prototype, usually Object's prototype. Prototype's version of "Inheritance" involves adding another link to the end of this prototype chain, as shown below.*/

var Dragon = function(location){

// <Function>.call is a method that executes the defined function,
// but with the "this" variable pointing to the first argument,
// and the rest of the arguments being arguments of the function
// that is being "called". This essentially performs all of
// LivingEntity's constructor logic on Dragon's "this".

LivingEntity.call(this, location);
//canFly is an attribute of the constructed object and not Dragon's prototype
this.canFly = true;
};

// Object.create(object) creates an object with a prototype of the
// passed in object. This example will return an object
// with a prototype that has the "moveWest" and "makeSound" functions,
// but not x, y, or z attributes.

Dragon.prototype = Object.create(LivingEntity.prototype);

// If we didn't reset the prototype's constructor
// attribute, it would look like any Dragon objects
// were constructed with a LivingEntity constructor

Dragon.prototype.constructor = Dragon;

// Now we can assign prototype attributes to Dragon without affecting
// the prototype of LivingEntity.

Dragon.prototype.fly = function(y){
this.y += y;
}

var sparky = new Dragon({
x: 0,
y: 0,
z: 0
});
{% endtonic %}

## OO Prototype Pattern (Real prototypal inheritance)
**Object.create** creates an object which has a specified prototype and optionally contains specified properties as well (e.g Object.create( prototype, optionalDescriptorObjects )).

    var myCar = {
 
    name: "Ford Escort",
   
    drive: function () {
      console.log( "Weeee. I'm driving!" );
    },
   
    panic: function () {
      console.log( "Wait. How do you stop this thing?" );
    }
   
    };
     
    // Use Object.create to instantiate a new car
    var yourCar = Object.create( myCar );
     
    // Now we can see that one is a prototype of the other
    console.log( yourCar.name );

**Object.create** also allows us to easily implement advanced concepts such as differential inheritance where objects are able to directly inherit from other objects. We saw earlier that Object.create allows us to initialise object properties using the second supplied argument. For example:

    var vehicle = {
      getModel: function () {
        console.log( "The model of this vehicle is.." + this.model );
      }
    };
     
    var car = Object.create(vehicle, {
     
      "id": {
        value: MY_GLOBAL.nextId(),
        // writable:false, configurable:false by default
        enumerable: true
      },
     
      "model": {
        value: "Ford",
        enumerable: true
      }
     
    });


## The Factory Pattern
The Factory pattern is another creational pattern concerned with the notion of creating objects. Where it differs from the other patterns in its category is that it doesn't explicitly require us use a constructor. Instead, a Factory can provide a generic interface for creating objects, where we can specify the type of factory object we wish to be created.

**When to use a factory:**

* When our object or component setup involves a high level of complexity
* When we need to easily generate different instances of objects depending on the environment we are in
* When we're working with many small objects or components that share the same properties
* When composing objects with instances of other objects that need only satisfy an API contract (aka, duck typing) to work. This is useful for decoupling.

**When not to use a factory:**

When applied to the wrong type of problem, this pattern can introduce an unnecessarily great deal of complexity to an application. Unless providing an interface for object creation is a design goal for the library or framework we are writing, I would suggest sticking to explicit constructors to avoid the unnecessary overhead.

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
[1]: https://toddmotto.com/mastering-the-module-pattern/#anonymous-object-literal-return
[2]: https://toddmotto.com/mastering-the-module-pattern/#locally-scoped-object-literal
[3]: https://toddmotto.com/mastering-the-module-pattern/#stacked-locally-scoped-object-literal
[4]: https://toddmotto.com/mastering-the-module-pattern/#revealing-module-pattern
[5]: https://toddmotto.com/mastering-the-module-pattern/#augmenting-modules
[6]: https://community.risingstack.com/javascript-prototype-chain-inheritance/
