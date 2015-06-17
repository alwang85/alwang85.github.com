---
layout: post
title: "Making Angular work with Minifiers"
description: ""
category: 
tags: [Angular, Angular Minification]
---
{% include JB/setup %}

# Making Angular work with Minifiers

## Problem

When you start out with code like this:

    myApp.controller('mainController', function($scope, $log) {
        console.log($scope);
    });

Minifiers end up with something like this:

    myApp.controller("mainController",function(o){console.log(o)});

Since the minified version renamed the <code>$scope</code> variable, you can no longer dependency inject <code>$scope</code>.

## Solution

If you refactor the initial code to:

    myApp.controller('mainController', ['$scope', '$log', function($scope, $log) {
        console.log($scope);
        console.log($log);
    }]);

The minification turns out like:

    myApp.controller("mainController",["$scope","$log",function(o,l){console.log(o),console.log(l)}]);

As you can imagine, <code>o</code> is substituted to <code>$scope</scope>. The replacement is determined by order in the array.

Keep in mind that usually dependency injection in Angular is order agnostic, however when using this method, the order matters.

## Solution #2

Alternatively:

        function mainController($scope, $log) {...}
        mainController.$inject = ['$scope', '$log'];
        myApp.controller('mainController', mainController);

## Other notes:

AngularJS docs -> http://docs.angularjs.org/tutorial/step_05 . Scroll down to A Note on Minification.

Also alternatively, the Angular ng-annotate can be installed and run manually/automatically converting your original code to work with minification.
