---
layout: media
title: "Dota-Sight"
image:
  teaser: "http://i.imgur.com/CQXeNeTl.png"
category: projects
excerpt: Player intelligence for DotA 2
tags: [Angular.js, MEAN]
---

# Synopsis

Dota-Sight is a opponent intelligence tool for the popular game DotA 2. Given a server log entry upon joining a game (when a match is found), our app parses the log and pulls player character specific history from the site www.dotabuff.com. With the stats, combined with general aggregate date for player agnostic statistics, we supply some prediction algorithms of a side's win rate based on the current team lineup.

You can find a copy of the live app on Heroku at [http://dota-sight.herokuapp.com](http://dota-sight.herokuapp.com), and the repository at [https://github.com/dkstevekwak/dota](https://github.com/dkstevekwak/dota).


<div id="carousel-example-generic" class="carousel slide" data-ride="carousel">
  <!-- Indicators -->
  <ol class="carousel-indicators">
    <li data-target="#carousel-example-generic" data-slide-to="0" class="active"></li>
    <li data-target="#carousel-example-generic" data-slide-to="1"></li>
  </ol>

  <!-- Wrapper for slides -->
  <div class="carousel-inner" role="listbox">
    <div class="item active">
      <img src="http://i.imgur.com/CQXeNeTl.png" alt="Interface">
      <div class="carousel-caption">
        <h3>Interface</h3>
      </div>
    </div>
    <div class="item">
      <img src="http://i.imgur.com/mEzfOR0l.png" alt="upload">
      <div class="carousel-caption">
        <h3>Uploading Logs</h3>
      </div>
    </div>
  </div>

  <!-- Controls -->
  <a class="left carousel-control" href="#carousel-example-generic" role="button" data-slide="prev">
    <span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>
    <span class="sr-only">Previous</span>
  </a>
  <a class="right carousel-control" href="#carousel-example-generic" role="button" data-slide="next">
    <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
    <span class="sr-only">Next</span>
  </a>
</div>

## Features:

1. Server side caching with memcached for general character data
2. Angular interface for selecting characters and real-time calculated stats
3. Production/Development servers used to test features before pushing live
4. Data crawling/parsing with Node.js
5. Google Analytics implemented with ui-router compatability as we tested app with live users 2 days after starting

## Tools used:

Gulp, AngularUI Router, Lodash, cheerio, Memcached, request, RegEx, async, Mongoose, Google Analytics, Heroku, Bootstrap, MongoDB, ExpressJS, AngularJS, and Node.js.  

## Expansion:

Further improved to automate server_log.txt parsing through an Autohotkey script and node-webkit client. Details on the process are [here](http://alwang85.github.io/reviews/2015/07/09/Updating-Dota--Sight-with-Node-Webkit.html).



