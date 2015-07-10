---
layout: post
title: "Updating Dota-Sight with Node Webkit"
description: ""
categories: [reviews]
tags: []
---

# Overview

Dota-Sight is a well designed app, however there are two issues that limit its growth and potential to scale. Fortunately a program created with node webkit can help resolve that issue.

Currently, a user has to manually navigate to a folder to copy logs before our server can parse the player IDs and retrieve data from dotabuff.com. Currently, the manual action of navigating to a folder has prevented this app from achieving greater traction. Also, another concern that would only matter when there's sufficient traffic, is that the gathering of specific player data from dotabuff.com is actually a web scrape of 10 players. If the dotabuff servers blocked our service, Dota-Sight would not work.

![Dota-Sight Structure](http://i.imgur.com/mZUkoVt.jpg)

My goal today is to implement a program created by node webkit, whose purpose would be to access the file system's specific file and monitor it for changes. When it does, it will retrieve player specific data from dotabuff from the client side node webkit program, and then it will pass the data to our Dota-Sight web app through url parameters. Something like this:

![Updated Dota-Sight Structure](http://i.imgur.com/JNiGmXb.jpg)

## Creating a node webkit app

To start, we create a folder in our current repository called "webkit-client".