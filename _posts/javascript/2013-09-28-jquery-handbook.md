---
layout: post
title: "JQuery Handbook"
description: "JQuery Handbook"
category: javascript
tags: [JavaScript, jQuery, Handbook]
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

## jQuery Syntax
    The jQuery syntax is tailor made for selecting HTML elements and performing some action on the element(s).

###Basic syntax
    $(selector).action()

    A $ sign to define/access jQuery
    A (selector) to "query (or find)" HTML elements
    A jQuery action() to be performed on the element(s)

####Examples
    $(this).hide() - hides the current element.
    $("p").hide() - hides all <p> elements.
    $(".test").hide() - hides all elements with class="test".
    $("#test").hide() - hides the element with id="test".

###The Document Ready Event
    $(document).ready(function(){

       // jQuery methods go here...

    })

This is to prevent any jQuery code from running before the document is finished loading. The jQuery team has also created an even shorter method for the document ready event.

    $(function(){

       // jQuery methods go here...

    }); 
## jQuery Selectors
    jQuery selectors allow you to select and manipulate HTML element(s). All selectors in jQuery start with sign and parentheses: $().

###The element Selector
The jQuery element selector selects elements based the element name.

    $("p")

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
        $("button").click(function(){
            $("p").hide();
        });
    });
    </script>
    </head>
    <body>
    <h2>This is a heading</h2>
    <p>This is a paragraph.</p>
    <p>This is another paragraph.</p>
    <button>Click me</button>
    </body>
    </html>

###The \#id Selector
The jQuery `#id` selector uses the id attribute of an HTML tag to find the specific element.

    $("#test")

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
        $("button").click(function(){
            $("#test").hide();
        });
    });
    </script>
    </head>

    <body>
    <h2>This is a heading</h2>
    <p>This is a paragraph.</p>
    <p id="test">This is another paragraph.</p>
    <button>Click me</button>
    </body>

    </html>

###The .class Selector
The jQuery class selector finds elements with a specific class.

    $(".test")

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
        $("button").click(function(){
            $(".test").hide();
        });
    });
    </script>
    </head>
    <body>

    <h2 class="test">This is a heading</h2>
    <p class="test">This is a paragraph.</p>
    <p>This is another paragraph.</p>
    <button>Click me</button>
    </body>
    </html>

###More Examples

####Select all elements
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
        $("button").click(function(){
            $("*").hide();
        });
    });
    </script>
    </head>
    <body>

    <h2>This is a heading</h2>
    <p>This is a paragraph.</p>
    <p>This is another paragraph.</p>
    <button>Click me</button>
    </body>

    </html>

####Selects the current HTML element
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
        $("button").click(function(){
            $(this).hide();
        });
    });
    </script>
    </head>
    <body>
    <h2>This is a heading</h2>
    <p>This is a paragraph.</p>
    <p>This is another paragraph.</p>
    <button>Click me</button>
    </body>
    </html>

####Selects all &lt;p> elements with class="intro"
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
        $("button").click(function(){
            $("p.intro").hide();
        });
    });
    </script>
    </head>
    <body>

    <h2 class="intro">This is a heading</h2>
    <p class="intro">This is a paragraph.</p>
    <p>This is another paragraph.</p>
    <button>Click me</button>

    </body>
    </html>

####Selects the first &lt;p> element
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
        $("button").click(function(){
            $("p:first").hide();
        });
    });
    </script>
    </head>
    <body>

    <h2>This is a heading</h2>
    <p>This is a paragraph.</p>
    <p>This is another paragraph.</p>
    <button>Click me</button>

    </body>
    </html>

####Selects the first &lt;li> element of the first &lt;ul>
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
        $("button").click(function(){
            $("ul li:first").hide();
        });
    });
    </script>
    </head>
    <body>

    <p>List 1:</p>
    <ul>
      <li>Coffee</li>
      <li>Milk</li>
      <li>Tea</li>
    </ul>

    <p>List 2:</p>
    <ul>
      <li>Coffee</li>
      <li>Milk</li>
      <li>Tea</li>
    </ul>

    <button>Click me</button>

    </body>
    </html>

####Selects the first &lt;li> element of every &lt;ul>
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("ul li:first-child").hide();
      });
    });
    </script>
    </head>
    <body>

    <p>List 1:</p>
    <ul>
      <li>Coffee</li>
      <li>Milk</li>
      <li>Tea</li>
    </ul>

    <p>List 2:</p>
    <ul>
      <li>Coffee</li>
      <li>Milk</li>
      <li>Tea</li>
    </ul>

    <button>Click me</button>

    </body>
    </html>

####Selects all elements with an href attribute
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("[href]").hide();
      });
    });
    </script>
    </head>
    <body>

    <h2>This is a heading</h2>
    <p>This is a paragraph.</p>
    <p>This is another paragraph.</p>
    <p><a href="http://www.w3schools.com/html/">HTML Tutorial</a></p>
    <p><a href="http://www.w3schools.com/css/">CSS Tutorial</a></p>
    <button>Click me</button>

    </body>
    </html>

####Selects all &lt;a> elements with a target attribute value equal to "_blank"
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("a[target='_blank']").hide();
      });
    });
    </script>
    </head>
    <body>

    <h2>This is a heading</h2>
    <p>This is a paragraph.</p>
    <p>This is another paragraph.</p>
    <p><a href="http://www.w3schools.com/html/" target="_blank">HTML Tutorial</a></p>
    <p><a href="http://www.w3schools.com/css/">CSS Tutorial</a></p>
    <button>Click me</button>

    </body>
    </html>

####Selects all &lt;a> elements with a target attribute value NOT equal to "_blank"
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("a[target!='_blank']").hide();
      });
    });
    </script>
    </head>
    <body>

    <h2>This is a heading</h2>
    <p>This is a paragraph.</p>
    <p>This is another paragraph.</p>
    <p><a href="http://www.w3schools.com/html/" target="_blank">HTML Tutorial</a></p>
    <p><a href="http://www.w3schools.com/css/">CSS Tutorial</a></p>
    <button>Click me</button>

    </body>
    </html>

####Selects all &lt;button> elements and &lt;input> elements of type="button"
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $(":button").hide();
      });
    });
    </script>
    </head>
    <body>

    <h2>This is a heading</h2>
    <p>This is a paragraph.</p>
    <p>This is another paragraph.</p>
    <button>Click me</button>

    </body>
    </html>

####Selects all even &lt;tr> elements
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("tr:even").css("background-color","yellow");
    });
    </script>
    </head>
    <body>

    <h1>Welcome to My Web Page</h1>

    <table border="1">
    <tr>
      <th>Company</th>
      <th>Country</th>
    </tr>
    <tr>
    <td>Alfreds Futterkiste</td>
    <td>Germany</td>
    </tr>
    <tr>
    <td>Berglunds snabbk</td>
    <td>Sweden</td>
    </tr>
    <tr>
    <td>Centro comercial Moctezuma</td>
    <td>Mexico</td>
    </tr>
    <tr>
    <td>Ernst Handel</td>
    <td>Austria</td>
    </tr>
    <tr>
    <td>Island Trading</td>
    <td>UK</td>
    </tr>
    </table>

    </body>
    </html>

####Selects all odd &lt;tr> elements
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("tr:odd").css("background-color","yellow");
    });
    </script>
    </head>
    <body>

    <h1>Welcome to My Web Page</h1>

    <table border="1">
    <tr>
      <th>Company</th>
      <th>Country</th>
    </tr>
    <tr>
    <td>Alfreds Futterkiste</td>
    <td>Germany</td>
    </tr>
    <tr>
    <td>Berglunds snabbk</td>
    <td>Sweden</td>
    </tr>
    <tr>
    <td>Centro comercial Moctezuma</td>
    <td>Mexico</td>
    </tr>
    <tr>
    <td>Ernst Handel</td>
    <td>Austria</td>
    </tr>
    <tr>
    <td>Island Trading</td>
    <td>UK</td>
    </tr>
    </table>

    </body>
    </html>

###Functions In a Separate File
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script src="my_jquery_functions.js"></script>
    </head> 

## jQuery Events
All the different visitor's actions that a web page can respond to are called events.

Here are some common DOM events:

    Mouse Events 	Keyboard Events 	Form Events 	Document/Window Events
    click 	        keypress 	        submit 	        load
    dblclick 	    keydown 	        change 	        resize
    mouseenter 	    keyup 	            focus 	        scroll
    mouseleave 	  	                    blur 	        unload

###jQuery Syntax For Event Methods
    $("p").click(function(){
      // action goes here!!
    }); 

###Commonly Used jQuery Event Methods
    $(document).ready()

####click\(\)
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("p").click(function(){
        $(this).hide();
      });
    });
    </script>
    </head>
    <body>

    <p>If you click on me, I will disappear.</p>
    <p>Click me away!</p>
    <p>Click me too!</p>

    </body>
    </html>

####dblclick\(\)
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("p").dblclick(function(){
        $(this).hide();
      });
    });
    </script>
    </head>
    <body>

    <p>If you double-click on me, I will disappear.</p>
    <p>Click me away!</p>
    <p>Click me too!</p>

    </body>
    </html>

####mouseenter\(\)
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("#p1").mouseenter(function(){
        alert("You entered p1!");
      });
    });
    </script>
    </head>
    <body>

    <p id="p1">Enter this paragraph.</p>

    </body>
    </html>

####mouseleave\(\)
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("#p1").mouseleave(function(){
        alert("Bye! You now leave p1!");
      });
    });
    </script>
    </head>
    <body>

    <p id="p1">This is a paragraph.</p>

    </body>
    </html>

####mousedown\(\)
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("#p1").mousedown(function(){
        alert("Mouse down over p1!");
      });
    });
    </script>
    </head>
    <body>

    <p id="p1">This is a paragraph.</p>

    </body>
    </html>

####mouseup\(\)
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("#p1").mouseup(function(){
        alert("Mouse up over p1!");
      });
    });
    </script>
    </head>
    <body>

    <p id="p1">This is a paragraph.</p>

    </body>
    </html>

####hover\(\)
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("#p1").hover(function(){
        alert("You entered p1!");
        },
        function(){
        alert("Bye! You now leave p1!");
      }); 
    });
    </script>
    </head>
    <body>

    <p id="p1">This is a paragraph.</p>

    </body>
    </html>

####focus\(\)
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("input").focus(function(){
        $(this).css("background-color","#cccccc");
      });
      $("input").blur(function(){
        $(this).css("background-color","#ffffff");
      });
    });
    </script>
    </head>
    <body>

    Name: <input type="text" name="fullname"><br>
    Email: <input type="text" name="email">

    </body>
    </html>

####blur\(\)

##-------------------------------------------------------------------------------------------------------
## jQuery Hid/Show
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $(".ex .hide").click(function(){
        $(this).parents(".ex").hide("slow");
      });
    });
    </script>
    <style type="text/css"> 
    div.ex
    {
    background-color:#e5eecc;
    padding:7px;
    border:solid 1px #c3c3c3;
    }
    </style>
    </head>
    <body>

    <h3>Island Trading</h3>
    <div class="ex">
    <button class="hide">Hide me</button>
    <p>Contact: Helen Bennett<br> 
    Garden House Crowther Way<br>
    London</p>
    </div>

    <h3>Paris specialities</h3>
    <div class="ex">
    <button class="hide">Hide me</button>
    <p>Contact: Marie Bertrand<br> 
    265, Boulevard Charonne<br>
    Paris</p>
    </div>

    </body>
    </html>

###jQuery hide\(\) and show\(\)

####Syntax
    $(selector).hide(speed,callback);
    $(selector).show(speed,callback);

####Example1
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("#hide").click(function(){
        $("p").hide();
      });
      $("#show").click(function(){
        $("p").show();
      });
    });
    </script>
    </head>
    <body>
    <p>If you click on the "Hide" button, I will disappear.</p>
    <button id="hide">Hide</button>
    <button id="show">Show</button>
    </body>
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("p").hide(1000);
      });
    });
    </script>
    </head>
    <body>
    <button>Hide</button>
    <p>This is a paragraph with little content.</p>
    <p>This is another small paragraph.</p>
    </body>
    </html>

###jQuery toggle\(\)
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("p").toggle();
      });
    });
    </script>
    </head>
    <body>

    <button>Toggle</button>
    <p>This is a paragraph with little content.</p>
    <p>This is another small paragraph.</p>
    </body>
    </html>

## jQuery Fade
With jQuery you can fade elements in and out of visibility.

###jQuery Fading Methods
    fadeIn()
    fadeOut()
    fadeToggle()
    fadeTo()

###jQuery fadeIn\(\) Method
    The jQuery fadeIn() method is used to fade in a hidden element.

####Syntax:
    $(selector).fadeIn(speed,callback);
    
    The optional speed parameter specifies the duration of the effect. It can take the following values: "slow", "fast", or milliseconds.
    The optional callback parameter is a function to be executed after the fading completes.
####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("#div1").fadeIn();
        $("#div2").fadeIn("slow");
        $("#div3").fadeIn(3000);
      });
    });
    </script>
    </head>

    <body>
    <p>Demonstrate fadeIn() with different parameters.</p>
    <button>Click to fade in boxes</button>
    <br><br>
    <div id="div1" style="width:80px;height:80px;display:none;background-color:red;"></div><br>
    <div id="div2" style="width:80px;height:80px;display:none;background-color:green;"></div><br>
    <div id="div3" style="width:80px;height:80px;display:none;background-color:blue;"></div>

    </body>
    </html>

###jQuery fadeOut\(\) Method
    The jQuery fadeOut() method is used to fade out a visible element.

####Syntax
    $(selector).fadeOut(speed, callback);

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("#div1").fadeOut();
        $("#div2").fadeOut("slow");
        $("#div3").fadeOut(3000);
      });
    });
    </script>
    </head>

    <body>
    <p>Demonstrate fadeOut() with different parameters.</p>
    <button>Click to fade out boxes</button>
    <br><br>
    <div id="div1" style="width:80px;height:80px;background-color:red;"></div><br>
    <div id="div2" style="width:80px;height:80px;background-color:green;"></div><br>
    <div id="div3" style="width:80px;height:80px;background-color:blue;"></div>

    </body>
    </html>

###jQuery fadeToggle\(\) Method
    The jQuery fadeToggle() method toggles between the fadeIn(0 and fadeOut() methods.

####Syntax
    $(selector).fadeToggle(speed,callback);

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("#div1").fadeToggle();
        $("#div2").fadeToggle("slow");
        $("#div3").fadeToggle(3000);
      });
    });
    </script>
    </head>
    <body>

    <p>Demonstrate fadeToggle() with different speed parameters.</p>
    <button>Click to fade in/out boxes</button>
    <br><br>

    <div id="div1" style="width:80px;height:80px;background-color:red;"></div>
    <br>
    <div id="div2" style="width:80px;height:80px;background-color:green;"></div>
    <br>
    <div id="div3" style="width:80px;height:80px;background-color:blue;"></div>

    </body>
    </html>

###jQuery fadeTo\(\) Method
    The jQuery fadeTo() method allows fading to a given opacity(value between 0 and 1).

####Syntax
    $(selector).fadeTo(speed,opacity,callback);

    The required speed parameter specifies the duration of the effect. It can take the following values: "slow", "fast", or milliseconds.
    The required opacity parameter in the fadeTo() method specifies fading to a given opacity (value between 0 and 1).
    The optional callback parameter is a function to be executed after the function completes.

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("#div1").fadeTo("slow",0.15);
        $("#div2").fadeTo("slow",0.4);
        $("#div3").fadeTo("slow",0.7);
      });
    });
    </script>
    </head>

    <body>
    <p>Demonstrate fadeTo() with different parameters.</p>
    <button>Click to fade boxes</button>
    <br><br>
    <div id="div1" style="width:80px;height:80px;background-color:red;"></div><br>
    <div id="div2" style="width:80px;height:80px;background-color:green;"></div><br>
    <div id="div3" style="width:80px;height:80px;background-color:blue;"></div>

    </body>
    </html>

## jQuery Slide
The jQuery slide methods slides elements up and down.

###jQuery Sliding Methods
    slideDown()
    slideUp()
    slideToggle()

###jQuery slideDown\(\) Method
    The jQuery slideDown() method is used to slide down an element.

####Syntax
    $(selector).slideDown(speed,callback);
    
    The optional speed parameter specifies the duration of the effect. It can take the following values: "slow", "fast", or milliseconds.
    The optional callback parameter is a function to be executed after the sliding completes.

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script> 
    $(document).ready(function(){
      $("#flip").click(function(){
        $("#panel").slideDown("slow");
      });
    });
    </script>
     
    <style type="text/css"> 
    #panel,#flip
    {
    padding:5px;
    text-align:center;
    background-color:#e5eecc;
    border:solid 1px #c3c3c3;
    }
    #panel
    {
    padding:50px;
    display:none;
    }
    </style>
    </head>
    <body>
     
    <div id="flip">Click to slide down panel</div>
    <div id="panel">Hello world!</div>

    </body>
    </html>

###jQuery slideUp\(\) Method
    The jQuery slideUp() method is used to slide up an element.

####Syntax
    $(selector).slideUp(speed,callback);

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script> 
    $(document).ready(function(){
      $("#flip").click(function(){
        $("#panel").slideUp("slow");
      });
    });
    </script>
     
    <style type="text/css"> 
    #panel,#flip
    {
    padding:5px;
    text-align:center;
    background-color:#e5eecc;
    border:solid 1px #c3c3c3;
    }
    #panel
    {
    padding:50px;
    }
    </style>
    </head>
    <body>
     
    <div id="flip">Click to slide up panel</div>
    <div id="panel">Hello world!</div>

    </body>
    </html>

###jQuery slideToggle\(\) Method
    The jQuery slideToggle() method toggles between the slideDown() and slideUp() methods.

####Syntax
    $(selector).slideToggle(speed,callback);

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script> 
    $(document).ready(function(){
      $("#flip").click(function(){
        $("#panel").slideToggle("slow");
      });
    });
    </script>
     
    <style type="text/css"> 
    #panel,#flip
    {
    padding:5px;
    text-align:center;
    background-color:#e5eecc;
    border:solid 1px #c3c3c3;
    }
    #panel
    {
    padding:50px;
    display:none;
    }
    </style>
    </head>
    <body>
     
    <div id="flip">Click to slide the panel down or up</div>
    <div id="panel">Hello world!</div>

    </body>
    </html>

## jQuery Animate

###The animate\(\) Method
    The jQuery animate() method lets you create custom animations.

####Syntax
    $(selector).animate({params},speed,callback);

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script> 
    $(document).ready(function(){
      $("button").click(function(){
        $("div").animate({left:'250px'});
      });
    });
    </script> 
    </head>
     
    <body>
    <button>Start Animation</button>
    <p>By default, all HTML elements have a static position, and cannot be moved. To manipulate the position, remember to first set the CSS position property of the element to relative, fixed, or absolute!</p>
    <div style="background:#98bf21;height:100px;width:100px;position:absolute;">
    </div>

    </body>
    </html>

###Manipulate Multiple Properties
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script> 
    $(document).ready(function(){
      $("button").click(function(){
        $("div").animate({
          left:'250px',
          opacity:'0.5',
          height:'150px',
          width:'150px'
        });
      });
    });
    </script> 
    </head>
     
    <body>
    <button>Start Animation</button>
    <p>By default, all HTML elements have a static position, and cannot be moved. To manipulate the position, remember to first set the CSS position property of the element to relative, fixed, or absolute!</p>
    <div style="background:#98bf21;height:100px;width:100px;position:absolute;">
    </div>

    </body>
    </html>

The `animate()` method can manipulate All CSS properties. However, there is one important thing to remember: all property must be camel-cased when used with the `animate()` method: You will need write paddingLeft instead of padding-left, marginRight instead of margin-right, and so on.

Also, color animation is not included in the core jQuery library.

###Using Relative Values
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script> 
    $(document).ready(function(){
      $("button").click(function(){
        $("div").animate({
          left:'250px',
          height:'+=150px',
          width:'+=150px'
        });
      });
    });
    </script> 
    </head>
     
    <body>
    <button>Start Animation</button>
    <p>By default, all HTML elements have a static position, and cannot be moved. To manipulate the position, remember to first set the CSS position property of the element to relative, fixed, or absolute!</p>
    <div style="background:#98bf21;height:100px;width:100px;position:absolute;">
    </div>

    </body>
    </html>

###Using Pre-defined Values
You can even specify a property's animation value as "show", "hide", or "toggle".

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script> 
    $(document).ready(function(){
      $("button").click(function(){
        $("div").animate({
          height:'toggle'
        });
      });
    });
    </script> 
    </head>
     
    <body>
    <button>Start Animation</button>
    <p>By default, all HTML elements have a static position, and cannot be moved. To manipulate the position, remember to first set the CSS position property of the element to relative, fixed, or absolute!</p>
    <div style="background:#98bf21;height:100px;width:100px;position:absolute;">
    </div>

    </body>
    </html>

###Uses Queue Functionality
By default, jQuery comes with queue functionality for animations.

####Example1
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script> 
    $(document).ready(function(){
      $("button").click(function(){
        var div=$("div");
        div.animate({height:'300px',opacity:'0.4'},"slow");
        div.animate({width:'300px',opacity:'0.8'},"slow");
        div.animate({height:'100px',opacity:'0.4'},"slow");
        div.animate({width:'100px',opacity:'0.8'},"slow");
      });
    });
    </script> 
    </head>
     
    <body>
    <button>Start Animation</button>
    <p>By default, all HTML elements have a static position, and cannot be moved. To manipulate the position, remember to first set the CSS position property of the element to relative, fixed, or absolute!</p>
    <div style="background:#98bf21;height:100px;width:100px;position:absolute;">
    </div>

    </body>
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script> 
    $(document).ready(function(){
      $("button").click(function(){
        var div=$("div");  
        div.animate({left:'100px'},"slow");
        div.animate({fontSize:'3em'},"slow");
      });
    });
    </script> 
    </head>
    <body>

    <button>Start Animation</button>
    <p>By default, all HTML elements have a static position, and cannot be moved. To manipulate the position, remember to first set the CSS position property of the element to relative, fixed, or absolute!</p>
    <div style="background:#98bf21;height:100px;width:200px;position:absolute;">HELLO</div>

    </body>
    </html>

## jQuery stop\(\)
    The jQuery stop() method is used to stop an animation or effect before it is finished.

###Syntax
    $(selector).stop(stopAll,goToEnd);

###Example1
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script> 
    $(document).ready(function(){
      $("#flip").click(function(){
        $("#panel").slideDown(5000);
      });
      $("#stop").click(function(){
        $("#panel").stop();
      });
    });
    </script>
     
    <style type="text/css"> 
    #panel,#flip
    {
    padding:5px;
    text-align:center;
    background-color:#e5eecc;
    border:solid 1px #c3c3c3;
    }
    #panel
    {
    padding:50px;
    display:none;
    }
    </style>
    </head>
    <body>
     
    <button id="stop">Stop sliding</button>
    <div id="flip">Click to slide down panel</div>
    <div id="panel">Hello world!</div>

    </body>
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script> 
    $(document).ready(function(){
      $("#start").click(function(){
        $("div").animate({left:'100px'},5000);
        $("div").animate({fontSize:'3em'},5000);
      });
      
      $("#stop").click(function(){
        $("div").stop();
      });

      $("#stop2").click(function(){
        $("div").stop(true);
      });

      $("#stop3").click(function(){
        $("div").stop(true,true);
      });
      
    });
    </script> 
    </head>
    <body>

    <button id="start">Start</button>
    <button id="stop">Stop</button>
    <button id="stop2">Stop all</button>
    <button id="stop3">Stop but finish</button>
    <p>The "Start" button starts the animation.</p>
    <p>The "Stop" button stops the current active animation, but allows the queued animations to be performed afterwards.</p>
    <p>The "Stop all" button stops the current active animation and clears the 
    animation queue; so all animations on the element is stopped.</p>
    <p>The "Stop but finish" rushes through the current active animation, then it stops.</p> 

    <div style="background:#98bf21;height:100px;width:200px;position:absolute;">HELLO</div>

    </body>
    </html>

## jQuery Callback
A callback function is executed after the current effect is finished.

###Syntax
    $(selector).hide(speed,callback);

###Example1
The example below has a callback parameter that is a function that will be executed after the hide effect is completed:

    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("p").hide("slow",function(){
          alert("The paragraph is now hidden");
        });
      });
    });
    </script>
    </head>
    <body>
    <button>Hide</button>
    <p>This is a paragraph with little content.</p>
    </body>
    </html>

###Example2
The example below has no callback parameter, and the alert box will be displayed before the hide effect is completed:

    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("p").hide(1000);
        alert("The paragraph is now hidden");
      });
    });
    </script>
    </head>
    <body>
    <button>Hide</button>
    <p>This is a paragraph with little content.</p>
    </body>
    </html>

## jQuery Chaining
    With jQuery, you can cahin together actions/methods.

###jQuery Method Chaining
    Chaining allows us to run multiple jQuery commands, one after the other, one the same element(s).

####Example1
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function()
      {
      $("button").click(function(){
        $("#p1").css("color","red").slideUp(2000).slideDown(2000);
      });
    });
    </script>
    </head>
    <body>

    <p id="p1">jQuery is fun!!</p>
    <button>Click me</button>

    </body>
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function()
      {
      $("button").click(function(){
        $("#p1").css("color","red")
          .slideUp(2000)
          .slideDown(2000);
      });
    });
    </script>
    </head>
    <body>

    <p id="p1">jQuery is fun!!</p>
    <button>Click me</button>

    </body>
    </html>

##-------------------------------------------------------------------------------------------------------
## jQuery Get
Get content and attributes.

###Get Content

    text() - Sets or returns the text content of selected elements
    html() - Sets or returns the content of selected elements (including HTML markup)
    val() - Sets or returns the value of form fields

####Example1
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("#btn1").click(function(){
        alert("Text: " + $("#test").text());
      });
      $("#btn2").click(function(){
        alert("HTML: " + $("#test").html());
      });
    });
    </script>
    </head>

    <body>
    <p id="test">This is some <b>bold</b> text in a paragraph.</p>
    <button id="btn1">Show Text</button>
    <button id="btn2">Show HTML</button>
    </body>
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        alert("Value: " + $("#test").val());
      });
    });
    </script>
    </head>

    <body>
    <p>Name: <input type="text" id="test" value="Mickey Mouse"></p>
    <button>Show Value</button>
    </body>
    </html>

###Get Attributes
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        alert($("#w3s").attr("href"));
      });
    });
    </script>
    </head>

    <body>
    <p><a href="http://www.w3schools.com" id="w3s">W3Schools.com</a></p>
    <button>Show href Value</button>
    </body>
    </html>

## jQuery Set
Set content and attributes.

###Set Content
    ext() - Sets or returns the text content of selected elements
    html() - Sets or returns the content of selected elements (including HTML markup)
    val() - Sets or returns the value of form fields

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("#btn1").click(function(){
        $("#test1").text("Hello world!");
      });
      $("#btn2").click(function(){
        $("#test2").html("<b>Hello world!</b>");
      });
      $("#btn3").click(function(){
        $("#test3").val("Dolly Duck");
      });
    });
    </script>
    </head>

    <body>
    <p id="test1">This is a paragraph.</p>
    <p id="test2">This is another paragraph.</p>
    <p>Input field: <input type="text" id="test3" value="Mickey Mouse"></p>
    <button id="btn1">Set Text</button>
    <button id="btn2">Set HTML</button>
    <button id="btn3">Set Value</button>
    </body>
    </html>

###A Callback Function
    All of the three jQuery methods above: text(), html(), and val(), also come with a callback function. The callback function has two parameters: the index of the current element in the list of elements selected and the original (old) value. You then return the string you wish to use as the new value from the function.

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("#btn1").click(function(){
        $("#test1").text(function(i,origText){
          return "Old text: " + origText + " New text: Hello world! (index: " + i + ")"; 
        });
      });

      $("#btn2").click(function(){
        $("#test2").html(function(i,origText){
          return "Old html: " + origText + " New html: Hello <b>world!</b> (index: " + i + ")"; 
        });
      });

    });
    </script>
    </head>

    <body>
    <p id="test1">This is a <b>bold</b> paragraph.</p>
    <p id="test2">This is another <b>bold</b> paragraph.</p>
    <button id="btn1">Show Old/New Text</button>
    <button id="btn2">Show Old/New HTML</button>
    </body>
    </html>

###Set Attributes
    The jQuery attr() method is also used to set/change attribute values.
    
####Example1
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("#w3s").attr("href","http://www.w3schools.com/jquery");
      });
    });
    </script>
    </head>

    <body>
    <p><a href="http://www.w3schools.com" id="w3s">W3Schools.com</a></p>
    <button>Change href Value</button>
    <p>Mouse over the link (or click on it) to see that the value of the href attribute has changed.</p>
    </body>
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("#w3s").attr({
          "href" : "http://www.w3schools.com/jquery",
          "title" : "W3Schools jQuery Tutorial"
        });
      });
    });
    </script>
    </head>

    <body>
    <p><a href="http://www.w3schools.com" id="w3s">W3Schools.com</a></p>
    <button>Change href and title</button>
    <p>Mouse over the link to see that the href attribute has changed and a title attribute is set.</p>
    </body>
    </html>

###A Callback Function
The callback function has two parameters: the index of the current element in the list of elements selected and the original attribute value.

    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("#w3s").attr("href", function(i,origValue){
          return origValue + "/jquery"; 
        });
      }); 
    });
    </script>
    </head>

    <body>
    <p><a href="http://www.w3schools.com" id="w3s">W3Schools.com</a></p>
    <button>Change href Value</button>
    <p>Mouse over the link (or click on it) to see that the value of the href attribute has changed.</p>
    </body>
    </html>

## jQuery Add

###Add New HTML Content

    append() - Inserts content at the end of the selected elements
    prepend() - Inserts content at the beginning of the selected elements
    after() - Inserts content after the selected elements
    before() - Inserts content before the selected elements

###jQuery append\(\) Method
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("#btn1").click(function(){
        $("p").append(" <b>Appended text</b>.");
      });

      $("#btn2").click(function(){
        $("ol").append("<li>Appended item</li>");
      });
    });
    </script>
    </head>

    <body>
    <p>This is a paragraph.</p>
    <p>This is another paragraph.</p>
    <ol>
    <li>List item 1</li>
    <li>List item 2</li>
    <li>List item 3</li>
    </ol>
    <button id="btn1">Append text</button>
    <button id="btn2">Append list items</button>
    </body>
    </html>

###jQuery prepend\(\) Method
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("#btn1").click(function(){
        $("p").prepend("<b>Prepended text</b>. ");
      });
      $("#btn2").click(function(){
        $("ol").prepend("<li>Prepended item</li>");
      });
    });
    </script>
    </head>
    <body>

    <p>This is a paragraph.</p>
    <p>This is another paragraph.</p>
    <ol>
    <li>List item 1</li>
    <li>List item 2</li>
    <li>List item 3</li>
    </ol>

    <button id="btn1">Prepend text</button>
    <button id="btn2">Prepend list item</button>

    </body>
    </html>

###Add Several New Elements With append\(\) and prepend\(\)
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    function appendText()
    {
    var txt1="<p>Text.</p>";              // Create text with HTML
    var txt2=$("<p></p>").text("Text.");  // Create text with jQuery
    var txt3=document.createElement("p");
    txt3.innerHTML="Text.";               // Create text with DOM
    $("body").append(txt1,txt2,txt3);        // Append new elements
    }
    </script>
    </head>
    <body>

    <p>This is a paragraph.</p>
    <button onclick="appendText()">Append text</button>

    </body>
    </html>

###jQuery after\(\) and before\(\) Methods
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("#btn1").click(function(){
        $("img").before("<b>Before</b>");
      });

      $("#btn2").click(function(){
        $("img").after("<i>After</i>");
      });
    });
    </script>
    </head>

    <body>
    <img src="w3jquery.gif" alt="jQuery" width="100" height="140">
    <br><br>
    <button id="btn1">Insert before</button>
    <button id="btn2">Insert after</button>
    </body>
    </html>

###Add Several New Elements With after\(\) and before\(\)
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    function afterText()
    {
    var txt1="<b>I </b>";                    // Create element with HTML
    var txt2=$("<i></i>").text("love ");     // Create with jQuery
    var txt3=document.createElement("big");  // Create with DOM
    txt3.innerHTML="jQuery!";
    $("img").after(txt1,txt2,txt3);          // Insert new elements after img
    }
    </script>
    </head>
    <body>

    <img src="w3jquery.gif" alt="jQuery" width="100" height="140">
    <br><br>
    <button onclick="afterText()">Insert after</button>

    </body>
    </html>

## jQuery Remove

###Remove Elements/Content

    remove() - Removes the selected element (and its child elements)
    empty() - Removes the child elements from the selected element

###jQuery remove\(\) Method
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("#div1").remove();
      });
    });
    </script>
    </head>
    <body>

    <div id="div1" style="height:100px;width:300px;border:1px solid black;background-color:yellow;">

    This is some text in the div.
    <p>This is a paragraph in the div.</p>
    <p>This is another paragraph in the div.</p>

    </div>
    <br>
    <button>Remove div element</button>

    </body>
    </html>

###jQuery empty\(\) Method
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("#div1").empty();
      });
    });
    </script>
    </head>
    <body>

    <div id="div1" style="height:100px;width:300px;border:1px solid black;background-color:yellow;">

    This is some text in the div.
    <p>This is a paragraph in the div.</p>
    <p>This is another paragraph in the div.</p>

    </div>
    <br>
    <button>Empty the div element</button>

    </body>
    </html>

###Filter the Elements to be Removed
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("p").remove(".italic");
      });
    });
    </script>
    </head>
    <body>

    <p>This is a paragraph in the div.</p>
    <p class="italic"><i>This is another paragraph in the div.</i></p>
    <p class="italic"><i>This is another paragraph in the div.</i></p>
    <button>Remove all p elements with class="italic"</button>

    </body>
    </html>

## jQuery CSS Classes

    addClass() - Adds one or more classes to the selected elements
    removeClass() - Removes one or more classes from the selected elements
    toggleClass() - Toggles between adding/removing classes from the selected elements
    css() - Sets or returns the style attribute

###Example Stylesheet
    .important
    {
    font-weight:bold;
    font-size:xx-large;
    }

    .blue
    {
    color:blue;
    }

###jQuery addClass\(\) Method

####Example1
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("h1,h2,p").addClass("blue");
        $("div").addClass("important");
      });
    });
    </script>
    <style type="text/css">
    .important
    {
    font-weight:bold;
    font-size:xx-large;
    }
    .blue
    {
    color:blue;
    }
    </style>
    </head>
    <body>

    <h1>Heading 1</h1>
    <h2>Heading 2</h2>
    <p>This is a paragraph.</p>
    <p>This is another paragraph.</p>
    <div>This is some important text!</div>
    <br>
    <button>Add classes to elements</button>

    </body>
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("#div1").addClass("important blue");
      });
    });
    </script>
    <style type="text/css">
    .important
    {
    font-weight:bold;
    font-size:xx-large;
    }
    .blue
    {
    color:blue;
    }
    </style>
    </head>
    <body>

    <div id="div1">This is some text.</div>
    <div id="div2">This is some text.</div>
    <br>
    <button>Add classes to first div element</button>

    </body>
    </html>

###jQuery removeClass\(\) Method
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("h1,h2,p").removeClass("blue");
      });
    });
    </script>
    <style type="text/css">
    .important
    {
    font-weight:bold;
    font-size:xx-large;
    }
    .blue
    {
    color:blue;
    }
    </style>
    </head>
    <body>

    <h1 class="blue">Heading 1</h1>
    <h2 class="blue">Heading 2</h2>
    <p class="blue">This is a paragraph.</p>
    <p>This is another paragraph.</p>
    <br>
    <button>Remove class from elements</button>
    </body>
    </html>

###jQuery toggleClass\(\) Method
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("h1,h2,p").toggleClass("blue");
      });
    });
    </script>
    <style type="text/css">
    .blue
    {
    color:blue;
    }
    </style>
    </head>
    <body>

    <h1>Heading 1</h1>
    <h2>Heading 2</h2>
    <p>This is a paragraph.</p>
    <p>This is another paragraph.</p>
    <button>Toggle class</button>
    </body>
    </html>

## jQuery css\(\)

###jQuery css\(\) Method
    The css() method sets or returns one or more style properties for the selected elements.

###Return a CSS Property
    css("propertyname");

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        alert("Background color = " + $("p").css("background-color"));
      });
    });
    </script>
    </head>

    <body>
    <h2>This is a heading</h2>
    <p style="background-color:#ff0000">This is a paragraph.</p>
    <p style="background-color:#00ff00">This is a paragraph.</p>
    <p style="background-color:#0000ff">This is a paragraph.</p>
    <button>Return background-color of p</button>
    </body>
    </html>

###Set a CSS Property
    css("propertyname","value");

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("p").css("background-color","yellow");
      });
    });
    </script>
    </head>

    <body>
    <h2>This is a heading</h2>
    <p style="background-color:#ff0000">This is a paragraph.</p>
    <p style="background-color:#00ff00">This is a paragraph.</p>
    <p style="background-color:#0000ff">This is a paragraph.</p>
    <p>This is a paragraph.</p>
    <button>Set background-color of p</button>
    </body>
    </html>

###Set Multiple CSS Properties
    css({"propertyname":"value","propertyname":"value",...});

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("p").css({"background-color":"yellow","font-size":"200%"});
      });
    });
    </script>
    </head>

    <body>
    <h2>This is a heading</h2>
    <p style="background-color:#ff0000">This is a paragraph.</p>
    <p style="background-color:#00ff00">This is a paragraph.</p>
    <p style="background-color:#0000ff">This is a paragraph.</p>
    <p>This is a paragraph.</p>
    <button>Set multiple styles for p</button>
    </body>
    </html>

## jQuery Dimensions

###jQuery Dimension Methods

    width()  sets or returns the width of an element (includes NO padding, border, or margin).
    height() sets or returns the height of an element (includes NO padding, border, or margin).
    innerWidth() returns the width of an element (includes padding).
    innerHeight() returns the height of an element (includes padding).
    outerWidth() returns the width of an element (includes padding and border).
    outerHeight() returns the height of an element (includes padding and border).

###jQuery Dimensions

![img_jquerydim.gif]({{ site.img_url }}/img_jquerydim.gif)

###jQuery width\(\) and height\(\) Methods
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        var txt="";
        txt+="Width of div: " + $("#div1").width() + "</br>";
        txt+="Height of div: " + $("#div1").height();
        $("#div1").html(txt);
      });
    });
    </script>
    </head>
    <body>

    <div id="div1" style="height:100px;width:300px;padding:10px;margin:3px;border:1px solid blue;background-color:lightblue;"></div>
    <br>
    <button>Display dimensions of div</button>
    <p>width() - returns the width of an element.</p>
    <p>height() - returns the height of an element.</p>

    </body>
    </html>

###jQuery innerWidth\(\) and innerHeight\(\) Methods
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        var txt="";
        txt+="Width of div: " + $("#div1").width() + "</br>";
        txt+="Height of div: " + $("#div1").height() + "</br>";
        txt+="Inner width of div: " + $("#div1").innerWidth() + "</br>";
        txt+="Inner height of div: " + $("#div1").innerHeight();
        $("#div1").html(txt);
      });
    });
    </script>
    </head>

    <body>
    <div id="div1" style="height:100px;width:300px;padding:10px;margin:3px;border:1px solid blue;background-color:lightblue;"></div>
    <br>

    <button>Display dimensions of div</button>
    <p>innerWidth() - returns the width of an element (includes padding).</p>
    <p>innerHeight() - returns the height of an element (includes padding).</p>

    </body>
    </html>

###jQuery outerWidth\(\) and outerHeight\(\) Methods

####Example1
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        var txt="";
        txt+="Width of div: " + $("#div1").width() + "</br>";
        txt+="Height of div: " + $("#div1").height() + "</br>";
        txt+="Outer width of div: " + $("#div1").outerWidth() + "</br>";
        txt+="Outer height of div: " + $("#div1").outerHeight();
        $("#div1").html(txt);
      });
    });
    </script>
    </head>

    <body>
    <div id="div1" style="height:100px;width:300px;padding:10px;margin:3px;border:1px solid blue;background-color:lightblue;"></div>
    <br>

    <button>Display dimensions of div</button>
    <p>outerWidth() - returns the width of an element (includes padding and border).</p>
    <p>outerHeight() - returns the height of an element (includes padding and border).</p>

    </body>
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        var txt="";
        txt+="Width of div: " + $("#div1").width() + "</br>";
        txt+="Height of div: " + $("#div1").height() + "</br>";
        txt+="Outer width of div (margin included): " + $("#div1").outerWidth(true) + "</br>";
        txt+="Outer height of div (margin included): " + $("#div1").outerHeight(true);
        $("#div1").html(txt);
      });
    });
    </script>
    </head>
    <body>

    <div id="div1" style="height:100px;width:300px;padding:10px;margin:3px;border:1px solid blue;background-color:lightblue;"></div>
    <br>
    <button>Display dimensions of div</button>
    <p>outerWidth(true) - returns the width of an element (includes padding, border, and margin).</p>
    <p>outerHeight(true) - returns the height of an element (includes padding, border, and margin).</p>

    </body>
    </html>

###jQuery More width\(\) and height\(\)

####Example1
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        var txt="";
        txt+="Document width/height: " + $(document).width();
        txt+="x" + $(document).height() + "\n";
        txt+="Window width/height: " + $(window).width();
        txt+="x" + $(window).height();
        alert(txt);
      });
    });
    </script>
    </head>
    <body>

    <button>Display dimensions of document and window</button>

    </body>
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("#div1").width(500).height(500);
      });
    });
    </script>
    </head>
    <body>

    <div id="div1" style="height:100px;width:300px;padding:10px;margin:3px;border:1px solid blue;background-color:lightblue;"></div>
    <br>
    <button>Resize div</button>

    </body>
    </html>

##-------------------------------------------------------------------------------------------------------
## jQuery Traversing

###What is Traversing?
jQuery traversing, which means "move through", are used to "find" \(or select\) HTML elements based on their relation to other elements. Start with one selection and move through that selection util you reach the elements you desire.

###Traversing the DOM
jQuery provides a variety of methods that allows us to traverse the DOM. The largest category of traversal methods are tree-traversal.

## jQuery Ancestors

###Traversing Up the DOM Tree

    parent() returns the direct parent element of the selected element.
    parents() returns all ancestor elements of the selected element, all the way up to the document's root element (<html>).
    parentsUntil() returns all ancestor elements between two given arguments.

###jQuery parent\(\) Method
    <head>
    <style>
    .ancestors *
    { 
    display: block;
    border: 2px solid lightgrey;
    color: lightgrey;
    padding: 5px;
    margin: 15px;
    }
    </style>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("span").parent().css({"color":"red","border":"2px solid red"});
    });
    </script>
    </head>
    <body>

    <div class="ancestors">
      <div style="width:500px;">div (great-grandparent)
        <ul>ul (grandparent)  
          <li>li (direct parent)
            <span>span</span>
          </li>
        </ul>   
      </div>

      <div style="width:500px;">div (grandparent)
        <p>p (direct parent)
            <span>span</span>
          </p> 
      </div>
    </div>

    </body>
    </html>

###jQuery parents\(\) Method

####Example1
    <head>
    <style>
    .ancestors *
    { 
    display: block;
    border: 2px solid lightgrey;
    color: lightgrey;
    padding: 5px;
    margin: 15px;
    }
    </style>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("span").parents().css({"color":"red","border":"2px solid red"});
    });
    </script>
    </head>

    <body class="ancestors">body (great-great-grandparent)
      <div style="width:500px;">div (great-grandparent)
        <ul>ul (grandparent)  
          <li>li (direct parent)
            <span>span</span>
          </li>
        </ul>   
      </div>
    </body>

    <!-- The outer red border, before the body element, is the html element (also an ancestor) -->
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    .ancestors *
    { 
    display: block;
    border: 2px solid lightgrey;
    color: lightgrey;
    padding: 5px;
    margin: 15px;
    }
    </style>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("span").parents("ul").css({"color":"red","border":"2px solid red"});
    });
    </script>
    </head>

    <body class="ancestors">body (great-great-grandparent)
      <div style="width:500px;">div (great-grandparent)
        <ul>ul (grandparent)  
          <li>li (direct parent)
            <span>span</span>
          </li>
        </ul>   
      </div>
    </body>

    <!-- The outer red border, before the body element, is the html element (also an ancestor) -->
    </html>

###jQuery parentsUntil\(\) Method
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    .ancestors *
    { 
    display: block;
    border: 2px solid lightgrey;
    color: lightgrey;
    padding: 5px;
    margin: 15px;
    }
    </style>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("span").parentsUntil("div").css({"color":"red","border":"2px solid red"});
    });
    </script>
    </head>

    <body class="ancestors"> body (great-great-grandparent)
      <div style="width:500px;">div (great-grandparent)
        <ul>ul (grandparent)  
          <li>li (direct parent)
            <span>span</span>
          </li>
        </ul>   
      </div>
    </body>

    </html>

## jQuery Descendants

###Traversing Down the DOM Tree

    children() returns all direct children of the selected element.
    find() returns descendant elements of the selected element, all the way down to the last descendant.

###jQuery children\(\) Method

####Example1
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    .descendants *
    { 
    display: block;
    border: 2px solid lightgrey;
    color: lightgrey;
    padding: 5px;
    margin: 15px;
    }
    </style>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("div").children().css({"color":"red","border":"2px solid red"});
    });
    </script>
    </head>
    <body>

    <div class="descendants" style="width:500px;">div (current element) 
      <p>p (child)
        <span>span (grandchild)</span>     
      </p>
      <p>p (child)
        <span>span (grandchild)</span>
      </p> 
    </div>

    </body>
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    .descendants *
    { 
    display: block;
    border: 2px solid lightgrey;
    color: lightgrey;
    padding: 5px;
    margin: 15px;
    }
    </style>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("div").children("p.1").css({"color":"red","border":"2px solid red"});
    });
    </script>
    </head>
    <body>

    <div class="descendants" style="width:500px;">div (current element) 
      <p class="1">p (child)
        <span>span (grandchild)</span>     
      </p>
      <p class="2">p (child)
        <span>span (grandchild)</span>
      </p> 
    </div>

    </body>
    </html>

###jQuery find\(\) Method

####Example1
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    .descendants *
    { 
    display: block;
    border: 2px solid lightgrey;
    color: lightgrey;
    padding: 5px;
    margin: 15px;
    }
    </style>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("div").find("span").css({"color":"red","border":"2px solid red"});
    });
    </script>
    </head>
    <body>

    <div class="descendants" style="width:500px;">div (current element) 
      <p>p (child)
        <span>span (grandchild)</span>     
      </p>
      <p>p (child)
        <span>span (grandchild)</span>
      </p> 
    </div>

    </body>
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    .descendants *
    { 
    display: block;
    border: 2px solid lightgrey;
    color: lightgrey;
    padding: 5px;
    margin: 15px;
    }
    </style>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("div").find("*").css({"color":"red","border":"2px solid red"});
    });
    </script>
    </head>
    <body>

    <div class="descendants" style="width:500px;">div (current element) 
      <p>p (child)
        <span>span (grandchild)</span>     
      </p>
      <p>p (child)
        <span>span (grandchild)</span>
      </p> 
    </div>

    </body>
    </html>

## jQuery Siblings

###Traversing 

    siblings() returns all sibling elements of the selected element.
    next() returns the next sibling element of the selected element.
    nextAll() returns all next sibling elements of the selected element.
    nextUntil() returns all next sibling elements between two given arguments.
    prev() returns the previous sibling element of the selected element.
    prevAll() returns all previous sibling element of the selected element.
    prevUntil() returns all previous sibling elements between two given arguments.

###jQuery siblings\(\) Method

####Example1
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    .siblings *
    { 
    display: block;
    border: 2px solid lightgrey;
    color: lightgrey;
    padding: 5px;
    margin: 15px;
    }
    </style>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("h2").siblings().css({"color":"red","border":"2px solid red"});
    });
    </script>
    </head>
    <body class="siblings">

    <div>div (parent)
      <p>p</p>
      <span>span</span>
      <h2>h2</h2>
      <h3>h3</h3>
      <p>p</p>
    </div>

    </body>
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    .siblings *
    { 
    display: block;
    border: 2px solid lightgrey;
    color: lightgrey;
    padding: 5px;
    margin: 15px;
    }
    </style>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("h2").siblings("p").css({"color":"red","border":"2px solid red"});
    });
    </script>
    </head>
    <body class="siblings">

    <div>div (parent)
      <p>p</p>
      <span>span</span>
      <h2>h2</h2>
      <h3>h3</h3>
      <p>p</p>
    </div>

    </body>
    </html>

###jQuery next\(\) Method
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    .siblings *
    { 
    display: block;
    border: 2px solid lightgrey;
    color: lightgrey;
    padding: 5px;
    margin: 15px;
    }
    </style>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("h2").next().css({"color":"red","border":"2px solid red"});
    });
    </script>
    </head>
    <body class="siblings">

    <div>div (parent)
      <p>p</p>
      <span>span</span>
      <h2>h2</h2>
      <h3>h3</h3>
      <p>p</p>
    </div>

    </body>
    </html>

###jQuery nextAll\(\) Method
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    .siblings *
    { 
    display: block;
    border: 2px solid lightgrey;
    color: lightgrey;
    padding: 5px;
    margin: 15px;
    }
    </style>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("h2").nextAll().css({"color":"red","border":"2px solid red"});
    });
    </script>
    </head>
    <body class="siblings">

    <div>div (parent)
      <p>p</p>
      <span>span</span>
      <h2>h2</h2>
      <h3>h3</h3>
      <p>p</p>
    </div>

    </body>
    </html>

###jQuery nextUntil\(\) Method
    <!DOCTYPE html>
    <html>
    <head>
    <style>
    .siblings *
    { 
    display: block;
    border: 2px solid lightgrey;
    color: lightgrey;
    padding: 5px;
    margin: 15px;
    }
    </style>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("h2").nextUntil("h6").css({"color":"red","border":"2px solid red"});
    });
    </script>
    </head>
    <body class="siblings">

    <div>div (parent)
      <p>p</p>
      <span>span</span>
      <h2>h2</h2>
      <h3>h3</h3>
      <h4>h4</h4>
      <h5>h5</h5>
      <h6>h6</h6>
      <p>p</p>
    </div>

    </body>
    </html>

###jQuery prev\(\), prevAll\(\) &amp; prevUntil\(\) Methods
    The prev(), prevAll() and prevUntil() methods work just like the methods above but with reverse functionality: they return previous sibling elements (traverse backwards along sibling elements in the DOM tree, instead of forward).

## jQuery Filtering

###Narrow Down The Search For Elements
    first() returns the first element of the selected elements.
    last() returns the last element of the selected elements.
    eq() returns an element with a specific index number of the selected elements.
    filter() returns all elements that match the criteria.
    not() returns all elements that do not match the criteria.

###jQuery first\(\) Method
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("div p").first().css("background-color","yellow");
    });
    </script>
    </head>
    <body>

    <h1>Welcome to My Homepage</h1>
    <div>
    <p>This is a paragraph in a div.</p>
    </div>

    <div>
    <p>This is a paragraph in another div.</p>
    </div>

    <p>This is also a paragraph.</p>

    </body>
    </html>

###jQuery last\(\) Method
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("div p").last().css("background-color","yellow");
    });
    </script>
    </head>
    <body>

    <h1>Welcome to My Homepage</h1>
    <div>
    <p>This is a paragraph in a div.</p>
    </div>

    <div>
    <p>This is a paragraph in another div.</p>
    </div>

    <p>This is also a paragraph.</p>

    </body>
    </html>

###jQuery eq\(\) Method
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("p").eq(1).css("background-color","yellow");
    });
    </script>
    </head>
    <body>

    <h1>Welcome to My Homepage</h1>
    <p>My name is Donald (index 0).</p>
    <p>Donald Duck (index 1).</p>
    <p>I live in Duckburg (index 2).</p>
    <p>My best friend is Mickey (index 3).</p>

    </body>
    </html>

###jQuery filter\(\) Method
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("p").filter(".intro").css("background-color","yellow");
    });
    </script>
    </head>
    <body>

    <h1>Welcome to My Homepage</h1>
    <p>My name is Donald.</p>
    <p class="intro">I live in Duckburg.</p>
    <p class="intro">I love Duckburg.</p>
    <p>My best friend is Mickey.</p>

    </body>
    </html>

###jQuery not\(\) Method
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("p").not(".intro").css("background-color","yellow");
    });
    </script>
    </head>
    <body>

    <h1>Welcome to My Homepage</h1>
    <p>My name is Donald.</p>
    <p class="intro">I live in Duckburg.</p>
    <p class="intro">I love Duckburg.</p>
    <p>My best friend is Mickey.</p>

    </body>
    </html>

##-------------------------------------------------------------------------------------------------------
## jQuery AJAX Intro

###What is AJAX?
AJAX is about loading data in the background and display it on the webpage, without reloading the whole page.

###What About jQuery and AJAX
With the jQuery AJAX methods, you can request text, HTML, XML, or JSON from a remote server using both HTTP Get and HTTP Post - And you can load the external data directly into the selected HTML elements of your web page!

## jQuery Load

###jQuery load\(\) Method
    load() loads data from a server and puts the returned data into the selected element.
    
####Syntax
    $(selector).load(URL,data,callback);
    
    The required URL parameter specifies the URL you wish to load.
    The optional data parameter specifies a set of querystring key/value pairs to send along with the request.
    The optional callback parameter is the name of a function to be executed after the load() method is completed.

####Example1
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("#div1").load("demo_test.txt");
      });
    });
    </script>
    </head>
    <body>

    <div id="div1"><h2>Let jQuery AJAX Change This Text</h2></div>
    <button>Get External Content</button>

    </body>
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("#div1").load("demo_test.txt #p1");
      });
    });
    </script>
    </head>
    <body>

    <div id="div1"><h2>Let jQuery AJAX Change This Text</h2></div>
    <button>Get External Content</button>

    </body>
    </html>

####demo_test.txt
    jQuery and AJAX is FUN!

    <div id="p1">This is some text in a paragraph.</div> 

####Exampe3
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $("#div1").load("demo_test.txt",function(responseTxt,statusTxt,xhr){
          if(statusTxt=="success")
            alert("External content loaded successfully!");
          if(statusTxt=="error")
            alert("Error: "+xhr.status+": "+xhr.statusText);
        });
      });
    });
    </script>
    </head>
    <body>

    <div id="div1"><h2>Let jQuery AJAX Change This Text</h2></div>
    <button>Get External Content</button>

    </body>
    </html>

## jQuery Get/Post
    The jQuery get() and post() methods are used to request data from the server with an HTTP GET or POST request.

###HTTP Request: GET vs. POST
Two commonly used methods for a request-response between a client and server are:

    GET - Requests data from a specified resource
    POST - Submits data to be processed to a specified resource

###jQuery $.get\(\) Method
    The $.get() method requests data from the server with an HTTP GET request.

####Syntax
    $.get(URL,callback):

    The required URL parameter specifies the URL you wish to request.
    The optional callback parameter is the name of a function to be executed if the request succeeds.

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $.get("demo_test.asp",function(data,status){
          alert("Data: " + data + "\nStatus: " + status);
        });
      });
    });
    </script>
    </head>
    <body>

    <button>Send an HTTP GET request to a page and get the result back</button>

    </body>
    </html>

####demo_test.asp
    <%
    response.write("This is some text from an external ASP file.")
    %>

###jQuery $.post\(\) Method
    The $.post() method requests data from the server using an HTTP POST request.

####Syntax
    $.post(URL,data,callback);

    The required URL parameter specifies the URL you wish to request.
    The optional data parameter specifies some data to send along with the request.
    The optional callback parameter is the name of a function to be executed if the request succeeds.

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $(document).ready(function(){
      $("button").click(function(){
        $.post("demo_test_post.asp",
        {
          name:"Donald Duck",
          city:"Duckburg"
        },
        function(data,status){
          alert("Data: " + data + "\nStatus: " + status);
        });
      });
    });
    </script>
    </head>
    <body>

    <button>Send an HTTP POST request to a page and get the result back</button>

    </body>
    </html>

####demo_test_post.asp

    <%
    dim fname,city
    fname=Request.Form("name")
    city=Request.Form("city")
    Response.Write("Dear " & fname & ". ")
    Response.Write("Hope you live well in " & city & ".")
    %>

##-------------------------------------------------------------------------------------------------------
## jQuery noConflict\(\)

###The jQuery noConflict\(\) Method
    The noConflict() method releases the hold on the $ shortcut identifer, so that other scripts can use it.

####Example1
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $.noConflict();
    jQuery(document).ready(function(){
      jQuery("button").click(function(){
        jQuery("p").text("jQuery is still working!");
      });
    });
    </script>
    </head>

    <body>
    <p>This is a paragraph.</p>
    <button>Test jQuery</button>
    </body>
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    var jq=$.noConflict();
    jq(document).ready(function(){
      jq("button").click(function(){
        jq("p").text("jQuery is still working!");
      });
    });
    </script>
    </head>

    <body>
    <p>This is a paragraph.</p>
    <button>Test jQuery</button>
    </body>
    </html>

####Example3
    <!DOCTYPE html>
    <html>
    <head>
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js">
    </script>
    <script>
    $.noConflict();
    jQuery(document).ready(function($){
      $("button").click(function(){
        $("p").text("jQuery is still working!");
      });
    });
    </script>
    </head>

    <body>
    <p>This is a paragraph.</p>
    <button>Test jQuery</button>
    </body>
    </html>

##-------------------------------------------------------------------------------------------------------

## REFERENCES
- [jQuery Tutorial](http://www.w3schools.com/jquery/default.asp)
- [jQery ajax——load()方法示例介绍_AJAX教程](http://www.mb5u.com/biancheng/ajax/ajax_97693.html)

