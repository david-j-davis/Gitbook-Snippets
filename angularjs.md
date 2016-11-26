# Angular JS Snippets
---

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
