---
layout: post
title: "Adding Metatags to AngularJS SPA with ui router"
description: ""
categories: [Angularjs, books]
tags: []
---

## Background

When I first did some PHP work in the PHP Code Ingniter framework, I had to create some SEO functionality such as the editing of title tags for a product vs dynamically generated title tags. Given that I'm now an experienced MEAN stack developer, and I haven't tried yet to add meta data to different states, this is the perfect opportunity for me to do so.

I started my research on Google with this article: [Weluse.de - Angular & SEO finally a piece of cake](https://weluse.de/blog/angularjs-seo-finally-a-piece-of-cake.html)

Basically, pre 2014-ish you had to leverage a service to pre-render html for crawlers, and lots of settings to distinguish between end users and crawlers. Alternatives include server-side rendering, and custom AJAX specific best practices for each search engine. With the implementation of <code>$locationProvider.html5Mode(true);</code> to remove the hashbangs and setting the rooth paths, Google can now index you, minus the meta information. (That line modifies the display URL through [HTML5 pushState](http://www.w3.org/TR/html5/browsers.html#history)) Also, no declaration from Bing about JavaScript crawling as of today 06-25-2015, so you may still have to do with Bing/Yahoo.

Stack Overflow comments about how Javascript changed titles are ignored in '09: ["How to dynamically change a web page's title?"](http://stackoverflow.com/questions/413439/how-to-dynamically-change-a-web-pages-title).

Google's declaration of JavaScript crawling Apr '14:["Understanding webpages better"](http://googlewebmastercentral.blogspot.de/2014/05/understanding-web-pages-better.html)

### Setting the Title Tags

Initial research suggested a few methods to change the title tag:

Bind the title to a variable (which also requires the app to be declared at the html level):

    <html ng-app="myApp">
        <title ng-bind="MetaTags.title"></title>
    </html>

Use a variable (not recommended due to flickering + sometimes Google indexes the '{{ MetaTags.title }}''):

    <html ng-app="myApp">
        <title {{ MetaTags.title }}"></title>
    </html>

Or using Javascript:

    document.title = MetaTags.title;

### Storing the Title Tags

My research also showed a few methods to store the title tags:

Store the meta information in the state declaration:

    $stateProvider
        .state('tutorial', {
            url: '/tutorial',
            templateUrl: 'js/tutorial/tutorial.html',
            controller: 'TutorialController',
            data: {
              'title': 'Welcome to my tutorial page',
              'keywords': 'best angular ui-router seo tutorial, angular, seo, metatags'
            }
        })

    <title ng-bind="$state.current.data.title"></title>

Compile the data in a helper service/factory/provider:

    app.config(function ($locationProvider, MetaTagsProvider) {
        $locationProvider.html5Mode(true);
        MetaTagsProvider
              .when('/tutorial',{
                'title': 'Welcome to my tutorial page',
                'keywords': 'best angular ui-router seo tutorial, angular, seo, metatags'
              })
              .otherwise({
                title: 'Alex Wang's Blog'
        }) // Best SEO practices really call for minimum redundant otherwise scenarios btw

        //code that when state changes, set $rootScope.MetaTags = object for the route
    });

    <title ng-bind="MetaTags.title"></title>

### User Stories

There are a few different user stories (data input) for the metatags input.

- Explicitly declared strings for each state
- Dynamically generated strings
-   a. Based on state parameter data (i.e. /books/:title)
-   b. Based on other product (i.e. actual book synposis)
-   c. Based on an API (i.e. response from /api/books/a-book-title ) - a separate simple app/database that allows stakeholders to edit tags themselves

### Technical Requirements

Since this post is specifically for ui-router, this has to address the reasons people choose ui-router over ngRoutes, including multiple view handling and nested view handling. Also, in SEO it is generally not recommended to have duplicate title/meta tags on the site, so no generic placeholder needs to be placed. Browser history also has to be supported.


Multiple view handling + Nested view handling - upon closer scrutiny, these views in general should not affect the metatags of a page. The metatags should inherit data from the state itself, and thus we would have to take into consideration child states vs parent states, instead of multiple/nested views.

### Designing the Implementation
