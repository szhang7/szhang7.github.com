---
layout: post
title: "JQuery Handbook"
description: "JQuery Handbook"
category: javascript
tags: [JavaScript, JQuery, Handbook]
---
{% include JB/setup %}

## jQuery Introduction
jQuery is a lightweight, "write less, do more", JavaScript library. The jQuery will run exactly in all major browsers, including Internet Explorer 6! The jQuery library contains the following features:

    HTML/DOM manipulation
    CSS manipulation
    HTML event methods
    Effects and animations
    AJAX
    Utilities

## jQuery Install
There are several ways to start using jQuery on your web site. You can:

    Download the jQuery library from jQuery.com
    Include jQuery from a CDN, like Google

###Downloading jQuery
There are two versions of jQuery available for downloading:

    Production version - this is for your live website because it has been minified and compressed
    Development version - this is for testing and development (uncompressed and readable code)

Both versions can be downloaded from [jQuery.com](http://jquery.com/download/).

    The jQuery library is a single JavaScript file, and you reference it with the HTML <script> tag (notice that the <script> tag should be inside the <head> section):

    <head>
    <script src="jquery-1.10.2.min.js"></script>
    </head>

###Alternatives to Downloading

####Google CDN
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    </head>

####Microsoft CDN
    <head>
    <script src="http://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js">
    </script>
    </head>

###jQuery Syntax
    The jQuery syntax is tailor made for selecting HTML elements and performing some action on the element(s).

####Basic syntax
    $(selector).action()

    A $ sign to define/access jQuery
    A (selector) to "query (or find)" HTML elements
    A jQuery action() to be performed on the element(s)

####Examples
    $(this).hide() - hides the current element.
    $("p").hide() - hides all <p> elements.
    $(".test").hide() - hides all elements with class="test".
    $("#test").hide() - hides the element with id="test".

###jQuery Selectors
    jQuery selectors allow you to select and manipulate HTML element(s). All selectors in jQuery start with sign and parentheses: $().

####The element Selector
The jQuery element selector selects elements based the element name.

    <script>
    $(document).ready(function(){
        $("button").click(function(){
            $("p").hide();
        });
    });
    </script>

####The \#id Selector






## REFERENCES
- [jQuery Tutorial](http://www.w3schools.com/jquery/default.asp)

