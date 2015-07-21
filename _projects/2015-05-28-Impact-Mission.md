---
layout: media
title: "Impact Mission"
image:
  teaser: "http://i.imgur.com/Q2c2Ie9l.png"
category: projects
excerpt: Pledging activities for a cause
tags: [Angular.js, MEAN]
---

# Synopsis

Impact Mission is a personal and event goal tracking webapp for supporting nonprofits. It allows users to use fitbit/jawbone data to support nonprofits.

You can find a copy of the live app on Heroku at [http://impactmission.io](http://impactmission.io), and the repository at [https://github.com/alwang85/run4cause](https://github.com/alwang85/run4cause).


<div id="carousel-example-generic" class="carousel slide" data-ride="carousel">
  <!-- Indicators -->
  <ol class="carousel-indicators">
    <li data-target="#carousel-example-generic" data-slide-to="0" class="active"></li>
    <li data-target="#carousel-example-generic" data-slide-to="1"></li>
    <li data-target="#carousel-example-generic" data-slide-to="2"></li>
    <li data-target="#carousel-example-generic" data-slide-to="3"></li>
    <li data-target="#carousel-example-generic" data-slide-to="4"></li>
  </ol>

  <!-- Wrapper for slides -->
  <div class="carousel-inner" role="listbox">
    <div class="item active">
      <img src="http://i.imgur.com/0vjuN4Nl.png" alt="ABOUT">
      <div class="carousel-caption">
        <h3>Intro</h3>
      </div>
    </div>
    <div class="item">
      <img src="http://i.imgur.com/sLIGB9Jl.png" alt="current impacts">
      <div class="carousel-caption">
        <h3>Current Impacts</h3>
      </div>
    </div>
    <div class="item">
      <img src="http://i.imgur.com/VtXoDqBl.png" alt="create impact">
      <div class="carousel-caption">
        <h3>Create Impact</h3>
      </div>
    </div>
    <div class="item">
      <img src="http://i.imgur.com/V5t5GYbl.png" alt="personal dashboard">
      <div class="carousel-caption">
        <h3>Personal Dashboard</h3>
      </div>
    </div>
    <div class="item">
      <img src="http://i.imgur.com/X1kJxBNl.png" alt="inbox">
      <div class="carousel-caption">
        <h3>Inbox</h3>
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

1. Fitbit/Jawbone OAuth 2.0 integration & session management & metric standardization
2. Event triggered real time updates
3. Query caching with memcached
4. Angular code optimization with js-data (Object Relational Mapping layer + datastore)
5. Real time chart/stat updates through socket.io
  - When user joins an impact
  - When a user's data is synced with fitness tracking device
6. Upon event success, messages are sent to sponsors + messaging capability

## Tools used:

Gulp, AngularUI Router, Lodash, OAuth 2.0, socket.io, chart.js, moment.js, browserify, js-data, Passport.js, Mongoose, Heroku, Bootstrap, MongoDB, ExpressJS, AngularJS, and Node.js.

