
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
  * Browser compatability
    1. AngularJS 1.2 supports IE8 (1.3 does not)
    2. AngularJS 2.0 will only support IE 10+
     * release slated for 2015, but some speculate we won't see it until 2016
     * support for 1.3 will continue at least 1.5-2 years after 2.0
     * Google has over 1600 internal apps written in 1.x [See Here](http://eisenbergeffect.bluespire.com/all-about-angular-2-0/)
     * They're talking about a migration story now [See Here](http://www.johnpapa.net/the-angular-team-on-angular-1-3-and-the-road-ahead-to-angular-2-0/)
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
  * directives and templates, ie ng-* + {{}}
    1. similar to knockout.js data-binding
    2. however, they can appear as attribute name, tag name, comments, or class name
 
            <my-dir></my-dir>
            <span my-dir="exp"></span>
            <!-- directive: my-dir exp -->
            <span class="my-dir: exp;"></span>
    3. as attributes then can appear
   
            <span ng-bind="name"></span> <br/>
            <span ng:bind="name"></span> <br/>
            <span ng_bind="name"></span> <br/>
            <span data-ng-bind="name"></span> <br/>
            <span x-ng-bind="name"></span> <br/>
    4. common ones
      * ng-model
      * ng-repeat
      * ng-controller
      * ui-view tag
      * 
      
              <ui-view></ui-view>
      * ng-repeat
      * ng-href
      * ng-include
      *

              <div ng-include="'/SPA/LOBApp/shell/navbar.html'"></div>
    5. take care with custom directives and IE8
    6. try to keep logic out of templates because it's very hard to debug
    7. {{}}
  * $scope
    1. inheritance
    2. $rootScope & $parent
    3. $scope.$watch
     
            scope.$watch('name', function(newValue, oldValue) {
              scope.counter = scope.counter + 1;
            });    
       * deep watch - 3rd parameter set to true
       * $watchCollection
       * more complex expressions are possible, but not often used
    4. $scope.$digest and $apply [Safe Apply Function](https://gist.github.com/JediMindtrick/f737a1a0e5b0d059deb8)
    5. $broadcast/$emit/$on
  * routing - two contenders
    1. both are external to angular core and therefore require loading via script tag
    2. both have useful hooks for view changes and retrieving parameters
    2. ng-route built by angular team
    3. ui-route built by angular-ui team
    4. ui-router generally preferred in the community
       * nested views
       * concept of 'state'
    5. [Example](https://github.com/JediMindtrick/DemoAngularJS/blob/master/DemoAngularJS/SPA/LOBApp/lob.html)
    6. when possible, using ng-href or ui-sref to navigate urls (views) is a good idea
  * services
    1. common ones $scope, $stateProvider, $http, $window, $log
    2. singletons
       * good for holding state
       * usable for cross-module communication
    2. retrieve by declaring a dependency on the module at the module level and a dependency on the service at the .controller()/.service()/.whatever() level
    3. 4 ways to create, but 2 common ones 
       * [See Gist Here](https://gist.github.com/JediMindtrick/8b2532de1a92afa49e83) 
       * [Stackoverflow Answer1](http://stackoverflow.com/questions/13762228/confused-about-service-vs-factory/13763886#13763886)
       * [Stackoverflow Answer2](http://stackoverflow.com/questions/15666048/service-vs-provider-vs-factory)
  * $http
    1. .get('/some/url/here')
    2. .post('/some/url/here',{thisHereObject: 'contains my data'}
    3. put/delete/patch/head/jsonp supported
    4. doesn't cache by default
    5. they return promises
       * get to know these and how to use them
       * .then(), .catch(), .finally() (I prefer these)
       * $http specific - .success(), .error()
    6. interceptors [Example](https://github.com/JediMindtrick/DemoAngularJS/blob/master/DemoAngularJS/SPA/LOBApp/lob-httpInterceptors.js)
3. General design considerations
 * Angular-seed (i.e. by layer) - if you feel like that's what you need to do
 * ngBoilerplate (i.e. by feature) - yes
 * Angular team's recent recomendation (a lot like ngBoilerplate) - yes
 * Dependency management
   1. dependencies are managed
   2. loading them is not
   3. yes, you can use RequireJS with AngularJS
   4. load order largely doesn't matter, unless you are modifying modules
 * Let the front-end model be the front-end model - consider using $httpBackend
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
