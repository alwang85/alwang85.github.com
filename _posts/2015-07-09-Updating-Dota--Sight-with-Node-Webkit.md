---
layout: post
title: "Updating Dota-Sight with Node Webkit"
description: ""
categories: [reviews]
tags: []
---

# Overview

Dota-Sight has many features that are useful, however there are two issues that limit its growth and potential to scale. Fortunately a program created with node webkit can help resolve that issue.

Currently, a user has to manually navigate to a folder to copy logs before our server can parse the player IDs and retrieve data from dotabuff.com. The manual action of navigating to a folder has prevented this app from achieving greater traction. Also, another potential concern that would only matter when there's sufficient traffic, is that the gathering of specific player data from dotabuff.com is actually a web scrape of the profile pages of 10 players. If the dotabuff servers blocked our server, Dota-Sight would not work.

![Dota-Sight Structure](http://i.imgur.com/mZUkoVt.jpg)

My goal today is to implement a program created by node webkit, whose purpose would be to access the file system's specific file and monitor it for changes. When it does, it will retrieve player specific data from dotabuff from the client side node webkit program, and then it will pass the data to our Dota-Sight web app through url parameters. Something like this:

![Updated Dota-Sight Structure](http://i.imgur.com/JNiGmXb.jpg)

## Creating a native app that monitors the server_log.txt

I created a node-webkit package thats performs the following task when ran:

1. When loaded, based on your operation system, it suggests default server_log.txt path (using <code>Node.js - OS module</code>)
2. Choosing the file path
  1. If the path is correct, start
  2. If not, choose the path through a <code>file input</code> form. Note that if this program was in a browser, it would not return the file path due to security concerns. (Chrome returns "C:\fakepath\text.xls"!) the only reason this works is due to this app functioning as a native app through node webkit.
3. The Node "fs" module watches the selected file.
4. Upon file change, it parses the log on the client side into playerId's, and then passes it to our webclient.

In order to pass along a node-webkit app:

1. Zip all the contents of app with a package.json file in a .zip format
2. Rename the extension from .zip to .nw
3. Tell users to download nwjs from [nwjs.io](http://nwjs.io/)
4. Tell users to unzip the nwjs into a folder, and place your .nw file into the same folder
5. Run the nw executable!
  1. Alternatively, it is possible to package a .exe file, however it requires a few more steps and few would ever download an executable file for a program like dota-sight. Also, the .nw archive is 75kb, while the .exe file is 40+mb/

## Next Steps

I attempted to use the "request" and "cheerio" libraries on the client side to pull data from www.dotabuff.com, and that worked. The problem was passing on that information to the front end. If I tried passing the data as a url parameter, the data caused a HTTP 414 error due to a long URI (the urls are long with a big json string). Since I can't change the server settings on the heroku instance, in addition to many browsers not supporting such long urls anyway, I have to change my methodology.

Approaches I could attempt include:

1. Converting my web app into a client side app
2. Posting the client pulled data onto the server, and then piping it to the web client based on a session token
3. ??? - Investigate other technologies such as web components and chrome extensions
4. TODO- maybe if I could store the data into a local storage that can be shared by the node-webkit app and chrome, this would resolve the issue as well.

The drawbacks of approach #1 is that any future updates to the app requires a manual download/installation by the user- and we all know how much we love manually updating files. #2 seems kinda redundant in network resource efficiency, however it may be the most viable right now. Other tools I'll need to investigate include web components and chrome extensions. #4 I just thought of and will have to do more investigative work.

## Last but not least

In a sense, Dota-Sight started from a 2 day internal hackathon we had a Fullstack Academy. It actually contains the least modular code I've ever written. Before I attempt to try the above technologies to further improve Dota-Sight, I will refactor my working _legacy_ code to adhere to JS best practices. I plan to utilize Require.JS instead of using Node.js' CommonJS-style dependency management for this project. Another post for the before/after!




