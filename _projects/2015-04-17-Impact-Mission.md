---
layout: media
title: "Impact Mission"
image:
  teaser: "http://i.imgur.com/3kQCQGo.png"
category: projects
caption_header: WineN- Wine store
caption: MEAN stack ecommerce platform /w Cart sessions /w localStorage, cloud cart syncing, product recommendation engine
tags: [Angular.js, MEAN]
---


# Problem

In Angular, you may have experienced code such as the following not behaving as expected with setTimeout:

{% highlight javascript %}
$scope.name = "Alex";
setTimeout(function(){
  $scope.name = "John";
}, 3000);

//$scope.name remains "Alex" after 3 seconds
{% endhighlight %}

When setTimeout runs code, it actually evaluates code in another thread outside of the Angular context. Hence, our scope is not updated. Here are two ways to fix this issue:

# Solutions

$timeout is an Angular resource that can replace setTimeout and run code in the Angular context. Note: You have to dependency inject $timeout to use it. Usage:

{% highlight javascript %}
$scope.name = "Alex";
$timeout(function(){
  $scope.name = "John";
}, 3000);

//$scope.name changes to "John" after 3 seconds
{% endhighlight %}

$apply is another Angular resource you use to tell Angular the code is in Angular context, so watch for changes and digest please! Usage:

{% highlight javascript %}
$scope.name = "Alex";
setTimeout(function(){
  $scope.$apply(function(){
    $scope.name = "John";
  );
}, 3000);

//$scope.name changes to "John" after 3 seconds
{% endhighlight %}

Finally, please note that resource is used broadly, as in something that came with Angular.

Hopefully that solved your problems with setTimeout! Comment if there's any comments or questions!

