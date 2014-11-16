
##Agenda
1. Why and when would we use AngularJS, and when not?
  *  Single-Page-Apps - YES
    1. Consumerization of the Enterprise (people don't want to spend all day working on crappy applications)
    2. Push work-load out
  * Javascript-heavy apps - YES - the biggest hurdle in building large apps in js is structure
    1. No native module system (yet)
    2. No native observables (yet)
    3. Treated like a "toy" language (don't)
  * Line of business apps - YES
  * Heavy animation - Reconsider OR encapsulate animations in modules
    1. Example 1 - [Three.js Periodic Table](http://mrdoob.github.io/three.js/examples/css3d_periodictable.html)
  * Embedded inside another platform (ex. Dynamics CRM forms) - RECONSIDER
    1. Can it be done?  Yes, but these options are better if available...
    2. Host regular static site in virtual sub-directory
    3. Host static site on another server/runtime platform
      * For #2 & #3 use platform sdk, service endpoints, etc.
    4. Keep SPA-like behavior to a minimum and design around traditional post-back behavior
    5. Use something else :)
2. Basic angular concepts of routing, controllers, services and directives
 * Pieces of a single-page app
  1. Modularization - angular.module()
  2. Routing - $stateProvider service and OOTB router
  3. Data-binding/Templating - $scope + ng* + {{}}
  4. Ajax - $http service
 * angular.module()
  1. only one of the form angular.module('Name',[])
  2. add to the module using just angular.module('Name')
  3. .config(), .run() - before services are available, after services are available
  4. .factory(), .controller(), .directive(), .filter() ...
  5. do not handle loading, so script tags are still needed to get them on the page
  6. do handle what dependency injection (*does order of loaded scripts matter?)
 * app
  1. get on page via ng-app
  2. just another module, usually has some config/run blocks
  3. I like to put a main controller up on this module
   * provides an inherited scope
   * "app-shell"
  4. routing usually done off of this guy
 * controller
  1. just another module
  2. preferred form is: .controller('NameCtrl',['$scope','dep1',function($scope, dep1){ }]);
  3. get on page via ng-controller
  4. *they are stateless*
  5. can have more than one active at a time
  6. can nest them
3. General design considerations
 * Angular-seed (i.e. by layer) nuh-uh
 * ngBoilerplate (i.e. by feature) yep
 * Angular team's recent recomendation yep
4. Hands-On Lab

##Detailed Agenda

This would be my mostly comprehensive list of angular topics, in the order I would present them and also in order of importance (imo):

####Essential
1. Brief background
   * jQuery -> Backbone -> Angular
   * Data-binding
   * IE Support
2. Project Structure - Angular seed vs. recent recommended best practice
3. Module definition
   * Dependency injection
   * Main module
4. Controllers
   * $scope
   * $rootScope
   * nested controllers
5. Views
6. Routing
   * OOTB router
   * angular-ui router
7. Services
8. $watch

####Core, but not quite essential
1. $http & promises
2. $http interceptors
3. Filters
4. Custom Directives
5. $broadcast/$emit/$on
6. Libraries
   * Angular-UI
   * Angular-bootstrap​


####Ancillary
1. Tooling
   * nodejs/npm
   * bower
   * grunt
   * yoeman
   * chrome plugin
2. Testing
   * Karma
   * Protractor

####Useful Links
- [AnvularJS v Backbone v Ember](http://www.airpair.com/js/javascript-framework-comparison)
- [Interceptors](http://www.webdeveasy.com/interceptors-in-angularjs-and-useful-examples/)

[Boromir's Advice](http://i.imgur.com/kTh9x54.png)
[Imgur](http://i.imgur.com/huvPLDE.png)
