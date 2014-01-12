---
layout: post_page
---

I’ve had the occasion the last couple of days to use [AngularJS](http://angularjs.org/) on my project. And although I’m not very experienced with it yet, I like what I’ve seen so far. Actually, I like it a lot. After fiddling around with it to get the screen flow right, and learning a ton in the process, I needed to address remaining details such as localization of the UI. I live in Belgium, and therefore unfortunately most web sites support multiple languages.

I am aware of nice implementations such as this one, which, when your application takes a dependency on it, in essence take the browser locale, and use it to choose a resource file based on naming conventions, and translate elements on the page annotated with a particular attribute (typical a data-* attribute). However, most of the localized applications I have worked on, don’t implement localization on top of the locale of the browser, but rather localize views based on a user language selection. Further more, the application I’m using angular in is all but a full-blown SPA, but rather an ASP.NET application that uses local resource files. For these reasons, I was looking for a solution that lets me manage all localization in these ASP.NET resource files.

Luckily, the Angular framework is build on an excellent dependency injection infrastructure, which on can use and extend with customizations. All that is needed is to go find the module, and have it provide a resource object:

	var module = angular.module(‘module’); 
	module.value(‘resources’, {
	    resource1=”<%= GetLocalResourceObject(‘resource1’)%>”, 
	    resource2=”<%= GetLocalResourceObject(‘resource2’)%>”, 
	    …}); 

and then our controller takes a dependency on that provided value:

	var module = angular.module(‘module’, []);
	var Ctrl = module.controller(‘controller’, [‘$scope’, ‘resources’, function($scope, resources) {
	    …
	}]);

And that’s all there is to it. Biggest disadvantage is that you have to ‘pollute’ your html markup with the piece of code needed to create the resources object. But for now I’m okay with that.

