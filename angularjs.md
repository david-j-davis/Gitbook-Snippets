# Angular JS Snippets
---
##routeProvider Example:

      var app = angular.module('dabbble', []);

      app.config(function ($routeProvider){
        $routeProvider
        .when("/blog/:id", {controller:"BlogCtrl", templateUrl: "partials/blog.html" })
        .when("/:category", {controller:"CategoryListCtrl", templateUrl: "partials/category_list.html" })
        .otherwise({redirectTo: "/famous"});
      });
##Pass scope from one controller to the next
####Best way to accomplish this is through rootScope dependency. Live example:[click here to view codepen](http://codepen.io/david-j-davis/pen/ZBJGdb)

      angular.module('myApp', [])

      .controller('MyController', function ($scope, $rootScope) {
          $scope.message = 'Hello from Controller 1';

          $scope.$watch('message', function () {
              $rootScope.$emit('controller1_scope_change', {
                  message: $scope.message
              });
          });

      }).controller('MyController2', function ($scope, $rootScope) {
          $scope.message = 'Hello from Controller 2';

          $rootScope.$on('controller1_scope_change', function (event, args) {
              console.log('arguments received by the handler for the event: ', args);
              $scope.message2 = args.message;
          });
      });
##Update scope with api request results
####Live example: [click here to view codepen](http://codepen.io/david-j-davis/pen/vyJgQb)
      var angular = require('angular'); // npm install - external library, core modules (fs, http, net ... )

      angular.module('myApp', []); // creating the module

      var app = angular.module('myApp'); // getter

      app.controller('MyController', function ($scope, $rootScope) {
          $scope.data = 'some information here ... ';
          $rootScope.items_info = 'Initial items: null';
          $scope.info = 'some data here ... ';

          $scope.items = [{
              name: 'kevin'
          }, {
              name: 'john'
          }, {
              name: 'dilon'
          }];

          // ajax call to the github api, get the information and display it on the front end

          $scope.$watch('items', function () {
              console.log('changed items array ...');
          });

          var xhr = new XMLHttpRequest();
          xhr.open('get', 'https://api.github.com/search/repositories?q=go');
          xhr.addEventListener('readystatechange', function () {
              console.log(xhr.readyState);
              if (xhr.readyState === 4) {
                  if (xhr.status == 200) {

                      var resp = JSON.parse(xhr.responseText);
                      // console.log(resp.items); // full_name, url, owner.avatar_url
                      $scope.items = resp.items;
                      $rootScope.items_info = 'changed the items array.';
                      console.log('$rootScope.items', $rootScope.items_info);
                      $scope.$apply();

                  }
              }
          });
          xhr.send();
      });
