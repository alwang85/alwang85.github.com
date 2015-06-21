---
layout: post
title: "Making Angular work with Minifiers"
description: ""
category: 
tags: [Angular, Angular Minification]
---
{% include JB/setup %}

## Problem

When you start out with code like this:

    myApp.controller('mainController', function($scope, $log) {
        console.log($scope);
    });

Minifiers end up with something like this:

    myApp.controller("mainController",function(o){console.log(o)});

Since the minified version renamed the <code>$scope</code> variable, you can no longer dependency inject <code>$scope</code>.

Inside the console, you see an error like this:

![Imgur](http://i.imgur.com/KM2Qq7D.png)

## Solution

If you refactor the initial code to:

    myApp.controller('mainController', ['$scope', '$log', function($scope, $log) {
        console.log($scope);
        console.log($log);
    }]);

The minification turns out like:

    myApp.controller("mainController",["$scope","$log",function(o,l){console.log(o),console.log(l)}]);

As you can imagine, <code>o</code> is substituted to <code>$scope</code>. The replacement is determined by order in the array.

Keep in mind that usually dependency injection in Angular is order agnostic, however when using this method, the order matters.

## Solution #2

Alternatively:

        function mainController($scope, $log) {...}
        mainController.$inject = ['$scope', '$log'];
        myApp.controller('mainController', mainController);

## Other notes:

AngularJS docs -> [http://docs.angularjs.org/tutorial/step_05](http://docs.angularjs.org/tutorial/step_05) . Scroll down to A Note on Minification.

Also alternatively, the [ng-annotate library](https://www.npmjs.com/package/ng-annotate) can be installed and run manually/automatically converting your original code to work with minification.

In the readme, there are automation tools support for grunt, gulp, rails, and a whole lot more.

For the gulp config files, its as simple as adding:

    var ngAnnotate = require('gulp-ng-annotate'); //don't forget to npm install this!'
    ..//somewhere in a sample task definition

    gulp.task('buildJSProduction', function () {
        return gulp.src(['./browser/js/app.js', './browser/js/**/*.js'])
            .pipe(concat('main.js'))
            .pipe(babel())              //ES6 compatability
            .pipe(ngAnnotate())         //allows for minification while preserving dependency injection variable names
            .pipe(uglify())             //we're using ngAnnotate to support minification :)
            .pipe(gulp.dest('./public'));
    });

