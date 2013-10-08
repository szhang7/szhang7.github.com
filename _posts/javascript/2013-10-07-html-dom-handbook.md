---
layout: post
title: "HTML DOM Handbook"
description: "HTML DOM Handbook"
category: javascript
tags: [javascript, HTML, DOM, Handbook]
---
{% include JB/setup %}

## DOM HOME
The HTML DOM defines a standard way for accessing and manipulating HTML documents.

###HTML DOM Tree
The DOM presents an HTML document as a tree-structure.

![htmltree.gif]({{ site.img_url }}/htmltree.gif)

###Example
    <!DOCTYPE html>
    <html>
    <body>
    <script>
    function changeImage()
    {
    element=document.getElementById('myimage')
    if (element.src.match("bulbon"))
      {
      element.src="home/pic_bulboff.gif";
      }
    else
      {
      element.src="home/pic_bulbon.gif";
      }
    }
    </script>
    <img id="myimage" onclick="changeImage()" border="0" src="home/pic_bulboff.gif" width="100" height="180">
    <p>Click to turn on/off the light</p>

    </body>
    </html>

## DOM Intro

###What is the DOM?
The DOM is a W3C\(World Wide Web Consortium\) standard.

The W3C Document Object Model \(DOM\) is a platform and language-neutral interface that allows programs and scripts to dynamically access and update the content, structure, and style of a document.

The W3C DOM standard is separated into 3 different parts:

    Core DOM - standard model for any structured document
    XML DOM - standard model for XML documents
    HTML DOM - standard model for HTML documents

###What is the XML DOM?
The XML DOM defines the objects and properties of all XML elements, and the methods to access them.

###What is the HTML DOM?

    A standard object model for HTML
    A standard programming interface for HTML
    A W3C standard

## DOM Nodes

###DOM Nodes

According to the W3C HTML DOM standard, everything in an HTML document is a node:

    The entire document is a document node
    Every HTML element is an element node
    The text inside HTML elements are text nodes
    Every HTML attribute is an attribute node
    Comments are comment nodes

###The HTML DOM Node Tree
The HTML DOM views HTML documents as tree structures. The structure is called a Node Tree:

![htmltree.gif]({{ site.img_url }}/htmltree.gif)

###Node Parents, Children, and Siblings
The nodes in the node tree have a hierarchical relationship to each other.

    In a node tree, the top node is called the root
    Every node has exactly one parent, except the root (which has no parent)
    A node can have any number of children
    Siblings are nodes with the same parent

## DOM Methods
Methods are actions you can perform on nodes\(HTML Elements\).

###Programming Interface
All HTML elements are defined as objects, and the programming interface is the object methods and object properties.

    A method is an action you can do (like add or modify an element).
    A property is a value that you can get or set (like the name or content of a node).

###The getElementById\(\) Method
    <!DOCTYPE html>
    <html>
    <body>

    <p id="intro">Hello World!</p>
    <p>This example demonstrates the <b>getElementById</b> method!</p>

    <script>
    //var b=document.getElementsByTagName('body')[0];
    //var c=document.getElementById("div_content");
    var x=document.getElementById("intro");
    var c=x.parentNode;
    var e=document.createElement("p");
    //alert(c.innerHTML);
    e.innerHTML="The text from the intro paragraph: " + x.innerHTML;
    c.appendChild(e);
    //alert(c.innerHTML);
    //document.write()方法将打开—个新的输出流。它将清除当前页面内容
    //document.write("<p>The text from the intro paragraph: " + x.innerHTML + "</p>");
    </script>

    </body>
    </html>

###HTML DOM Objects - Methods and Properties
Some commonly used HTML DOM methods:

    getElementById(id) - get the node (element) with a specified id
    appendChild(node) - insert a new child node (element)
    removeChild(node) - remove a child node (element)

Some commonly used HTML DOM properties:

    innerHTML - the text value of a node (element)
    parentNode - the parent node of a node (element)
    childNodes - the child nodes of a node (element)
    attributes - the attributes nodes of a node (element)

###A Real Life Object Illustration
    A person is an object.
    A person's methods could be eat(), sleep(), work(), play(), etc.
    All persons have these methods, but they are performed at different times.
    A person's properties include name, height, weight, age, eye color, etc.
    All persons have these properties, but their values differ from person to person.

###Some DOM Object Methods
    Method 	                    Description
    getElementById() 	        Returns the element that has an ID attribute with the a value
    getElementsByTagName() 	    Returns a node list (collection/array of nodes) containing all elements with a specified tag name
    getElementsByClassName() 	Returns a node list containing all elements with a specified class
      	 
    appendChild() 	            Adds a new child node to a specified node
    removeChild() 	            Removes a child node
    replaceChild() 	            Replaces a child node
    insertBefore() 	            Inserts a new child node before a specified child node
      	 
    createAttribute() 	        Creates an Attribute node
    createElement() 	        Creates an Element node
    createTextNode() 	        Creates a Text node
      	 
    getAttribute() 	            Returns the specified attribute value
    setAttribute() 	            Sets or changes the specified attribute, to the specified value

## DOM Properties
Properties are values of nodes\(HTML Elements\) that you can get or set.

###Programming Interface
The programming interface of the DOM is defined by methods and properties.

    A method is an action you can do (like add or delete a node).
    A property is a value that you can get or set (like the name or content of a node).

###The innerHTML Property
The innerHTML property is useful for getting or replacing the content of HTML elements, including `<html>` and `<body>`.

####Example
    <!DOCTYPE html>
    <html>
    <body>

    <p id="intro">Hello World!</p>

    <script>
    //var txt=document.getElementById("intro").innerHTML;
    //document.write(txt);
    var x=document.getElementById("intro");
    var c=x.parentNode;
    var e=document.createElement("p");
    //alert(c.innerHTML);
    e.innerHTML=x.innerHTML;
    c.appendChild(e);

    </script>

    </body>
    </html>

###The nodeName Property
The nodeName property specifies the name of a node.

    nodeName is read-only
    nodeName of an element node is the same as the tag name
    nodeName of an attribute node is the attribute name
    nodeName of a text node is always #text
    nodeName of the document node is always #document

###The nodeValue Property
The nodeValue property specifies the value of a node.

    nodeValue for element nodes is undefined
    nodeValue for text nodes is the text itself
    nodeValue for attribute nodes is the attribute value

###Get the Value of an Element
    <!DOCTYPE html>
    <html>
    <body>

    <p id="intro">Hello World!</p>

    <script>
    x=document.getElementById("intro");
    //document.write(x.firstChild.nodeValue);
    var c=x.parentNode;
    var e=document.createElement("p");
    //alert(c.innerHTML);
    e.innerHTML=x.firstChild.nodeValue;
    c.appendChild(e);
    </script>

    </body>
    </html>

###The nodeType Property
The nodeType property returns the type of node. nodeType is read only.

    Element type 	NodeType
    Element 	    1
    Attribute 	    2
    Text 	        3
    Comment 	    8
    Document 	    9

## DOM Access
Accessing the HTML DOM - Finding HTML elements

###Accessing HTML Elements\(Nodes\)
Accessing an HTML element is the same as accessing a Node.

You can access an HTML element in different ways:

    By using the getElementById() method
    By using the getElementsByTagName() method
    By using the getElementsByClassName() method

###The getElementById\(\) Method
The getElementById\(\) method returns the element with the specified ID.

####Syntax
    node.getElementById("id");

####Example
    <!DOCTYPE html>
    <html>
    <body>

    <p id="intro">Hello World!</p>
    <p>This example demonstrates the <b>getElementById</b> method!</p>

    <div id="result"></div>
    <script>
    var x=document.getElementById("intro");
    //document.write("<p>The text from the intro paragraph: " + x.innerHTML + "</p>");
    var d=document.getElementById("result");
    d.innerHTML="<p>The text from the intro paragraph: " + x.innerHTML + "</p>";
    </script>

    </body>
    </html>

###The getElementsByTagName\(\) Method
The getElementsByTagName\(\) returns all elements with a specified tag name.

####Syntax
    node.getElementsByTagName("tagname");

####Example1
    <!DOCTYPE html>
    <html>
    <body>

    <p>Hello World!</p>
    <p>The DOM is very useful!</p>
    <p>This example demonstrates the <b>getElementsByTagName</b> method.</p>

    <div id="result"></div>
    <script>
    x=document.getElementsByTagName("p");
    //document.write("Text of first paragraph: " + x[0].innerHTML);
    var d=document.getElementById("result");
    d.innerHTML="Text of first paragraph: " + x[0].innerHTML;
    </script>

    </body>
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <body>

    <p>Hello World!</p>

    <div id="main">
    <p>The DOM is very useful.</p>
    <p>This example demonstrates the <b>getElementsByTagName</b> method</p>
    </div>

    <div id="result"></div>
    <script>
    x=document.getElementById("main").getElementsByTagName("p");
    //document.write("First paragraph inside the div: " + x[0].innerHTML);
    var d=document.getElementById("result");
    d.innerHTML="First paragraph inside the div: " + x[0].innerHTML;
    </script>

    </body>
    </html>

###The getElementsByClassName\(\) Method
    document.getElementsByClassName("intro");

####NOTE
`getElementsByClassName()` does not work in Internet Explorer 5,6,7,and 8.

## DOM Modify
Modifying HTML = Changing Elements, Attributes, Styles, and Events.

###Modifying HTML Elements
Modifying the HTML DOM can be many different things

    Changing HTML content
    Changing CSS styles
    Changing HTML attributes
    Creating new HTML elements
    Removing existent HTML elements
    Changing event(handlers)

###Changing HTML Content
The easiest way to change the content of an element is by using the `innerHTML` property.

####Example
    <!DOCTYPE html>
    <html>
    <body>

    <p id="p1">Hello World!</p>

    <script>
    document.getElementById("p1").innerHTML="New text!";
    </script>

    <p>The paragraph above was changed by a script.</p>

    </body>
    </html>

###Changing HTML Style
    <!DOCTYPE html>
    <html>
    <body>

    <p id="p1">Hello world!</p>
    <p id="p2">Hello world!</p>

    <script>
    document.getElementById("p2").style.color="blue";
    document.getElementById("p2").style.fontFamily="Arial";
    document.getElementById("p2").style.fontSize="larger";
    </script>

    </body>
    </html>

###Creating New HTML Elements
    <!DOCTYPE html>
    <html>
    <body>

    <div id="div1">
    <p id="p1">This is a paragraph.</p>
    <p id="p2">This is another paragraph.</p>
    </div>

    <script>
    var para=document.createElement("p");
    var node=document.createTextNode("This is new.");
    para.appendChild(node);

    var element=document.getElementById("div1");
    element.appendChild(para);
    </script>

    </body>
    </html>

## DOM Content

###Changing HTML Content
The easiest way to change the content of an element is by using the innerHTML property.

###Changing HTML Style
With the HTML DOM you can access the style object of HTML elements.

###Using Events
Events are generated by the browser when "things happen" to HTML elements:

    An element is clicked on
    The page has loaded
    Input fields are changed

####Example1
    <!DOCTYPE html>
    <html>
    <body>

    <input type="button"
    onclick="document.getElementById('div_content').style.backgroundColor='lavender';"
    value="Change background color">

    </body>
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <body>

    <script>
    function ChangeBackground()
    {
    //document.body.style.backgroundColor="lavender";
    document.getElementById("div_content").style.backgroundColor="lavender";
    }
    </script>

    <input type="button" onclick="ChangeBackground()" value="Change background color" />

    </body>
    </html>

####Example3
    <!DOCTYPE html>
    <html>
    <body>

    <p id="p1">Hello world!</p>

    <script>
    function ChangeText()
    {
    document.getElementById("p1").innerHTML="New text!";
    }
    </script>

    <input type="button" onclick="ChangeText()" value="Change text" />

    </body>
    </html>

## DOM Elements
Adding, Removing, and Replacing HTML Elements.

###Creating New HTML Elements - appendChild\(\)
    <script>
    var para=document.createElement("p");
    var node=document.createTextNode("This is new.");
    para.appendChild(node);

    var element=document.getElementById("div1");
    element.appendChild(para);
    </script>

###Creating new HTML Elements - insertBefore\(\)
    <!DOCTYPE html>
    <html>
    <body>

    <div id="div1">
    <p id="p1">This is a paragraph.</p>
    <p id="p2">This is another paragraph.</p>
    </div>

    <script>
    var para=document.createElement("p");
    var node=document.createTextNode("This is new.");
    para.appendChild(node);

    var element=document.getElementById("div1");
    var child=document.getElementById("p1");
    element.insertBefore(para,child);
    </script>

    </body>
    </html>

###Removing Existing HTML Elements
    <!DOCTYPE html>
    <html>
    <body>

    <div id="div1">
    <p id="p1">This is a paragraph.</p>
    <p id="p2">This is another paragraph.</p>
    </div>

    <script>
    var parent=document.getElementById("div1");
    var child=document.getElementById("p1");
    parent.removeChild(child);
    //child.parentNode.removeChild(child);
    </script>

    </body>
    </html>

####NOTE
Here is a common workaround: Find the child you want to remove, and use its parentNode property to find the parent:

    var child=document.getElementById("p1");
    child.parentNode.removeChild(child);

###Replacing HTML Elements
    <!DOCTYPE html>
    <html>
    <body>

    <div id="div1">
    <p id="p1">This is a paragraph.</p>
    <p id="p2">This is another paragraph.</p>
    </div>

    <script>
    var parent=document.getElementById("div1");
    var child=document.getElementById("p1");
    var para=document.createElement("p");
    var node=document.createTextNode("This is new.");
    para.appendChild(node);
    parent.replaceChild(para,child);
    </script>

    </body>
    </html>

## DOM Events
HTML DOM allows JavaScript to react to HTML events.

###Reacting to Events
To execute code when a user clicks on an element, add JavaScript code to an HTML event attribute:

    onclick=JavaScript

####Examples of HTML events:

    When a user clicks the mouse
    When a web page has loaded
    When an image has been loaded
    When the mouse moves over an element
    When an input field is changed
    When an HTML form is submitted
    When a user strokes a key

####Example1
    <!DOCTYPE html>
    <html>
    <body>

    <h1 onclick="this.innerHTML='Ooops!'">Click on this text!</h1>

    </body>
    </html>

####Example2
    <!DOCTYPE html>
    <html>
    <head>
    <script>
    function changetext(id)
    {
    id.innerHTML="Ooops!";
    }
    </script>
    </head>
    <body>

    <h1 onclick="changetext(this)">Click on this text!</h1>

    </body>
    </html>

###HTML Event Attributes
    <!DOCTYPE html>
    <html>
    <body>

    <p>Click the button to execute the <em>displayDate()</em> function.</p>

    <button onclick="displayDate()">Try it</button>

    <script>
    function displayDate()
    {
    document.getElementById("demo").innerHTML=Date();
    }
    </script>

    <p id="demo"></p>

    </body>
    </html> 

###Assign Events Using the HTML DOM
    <!DOCTYPE html>
    <html>
    <head>
    </head>
    <body>

    <p>Click the button to execute the <em>displayDate()</em> function.</p>

    <button id="myBtn">Try it</button>

    <script>
    document.getElementById("myBtn").onclick=function(){displayDate()};
    function displayDate()
    {
    document.getElementById("demo").innerHTML=Date();
    }
    </script>

    <p id="demo"></p>

    </body>
    </html> 

###The onload and onunload Events
The onload and onunload events are triggered when the user enters or leaves the page.

####Example
    <!DOCTYPE html>
    <html>
    <body onload="checkCookies()">

    <script>
    function checkCookies()
    {
    if (navigator.cookieEnabled==true)
	    {
	    alert("Cookies are enabled")
	    }
    else
	    {
	    alert("Cookies are not enabled")
	    }
    }
    </script>

    <p>An alert box should tell you if your browser has enabled cookies or not.</p>
    </body>
    </html> 

###The onchange Event
The onchange event are often used in combination with validation of input fields.

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script>
    function myFunction()
    {
    var x=document.getElementById("fname");
    x.value=x.value.toUpperCase();
    }
    </script>
    </head>
    <body>

    Enter your name: <input type="text" id="fname" onchange="myFunction()">
    <p>When you leave the input field, a function is triggered which transforms the input text to upper case.</p>

    </body>
    </html>

###The onmouseover and onmouseout Events
The onmouseover and onmouseout events can be used to trigger a function when the user mouses over, or out of, an HTML element.

####Example
    <!DOCTYPE html>
    <html>
    <body>

    <div onmouseover="mOver(this)" onmouseout="mOut(this)" style="background-color:#D94A38;width:120px;height:20px;padding:40px;">Mouse Over Me</div>

    <script>
    function mOver(obj)
    {
    obj.innerHTML="Thank You"
    }

    function mOut(obj)
    {
    obj.innerHTML="Mouse Over Me"
    }
    </script>

    </body>
    </html> 

###The onmousedown, onmouseup and onclick Events
The onmousedown, onmouseup, and onclick events are all parts of a mouse-click.

####Example
    <!DOCTYPE html>
    <html>
    <body>

    <div onmousedown="mDown(this)" onmouseup="mUp(this)" style="background-color:#D94A38;width:90px;height:20px;padding:40px;">Click Me</div>

    <script>
    function mDown(obj)
    {
    obj.style.backgroundColor="#1ec5e5";
    obj.innerHTML="Release Me"
    }

    function mUp(obj)
    {
    obj.style.backgroundColor="#D94A38";
    obj.innerHTML="Thank You"
    }
    </script>

    </body>
    </html> 

## DOM Navigation
With the HTML DOM, you can navigate the node tree using node relationships.

###HTML DOM Node List
A node list is an array of nodes.

####Example
    <!DOCTYPE html>
    <html>
    <body>

    <p>Hello World!</p>
    <p>The DOM is very useful!</p>
    <div id="result"></div>
    <script>
    x=document.getElementsByTagName("p");
    //document.write("The innerHTML of the second paragraph is: " + x[1].innerHTML);
    document.getElementById("result").innerHTML="The innerHTML of the second paragraph is: " + x[1].innerHTML;
    </script>

    </body>
    </html>

###HTML DOM Node List Length
The length property defines the number of nodes in a node-list.

####Example
    <!DOCTYPE html>
    <html>
    <body>

    <p>Hello World!</p>
    <p>The DOM is very useful!</p>
    <p>This example demonstrates the <b>length</b> property.</p>
    <div id="result"></div>
    <script>
    x=document.getElementsByTagName("p");
    var txt="<br>";
    for (i=0;i<x.length;i++)
      { 
      //document.write(x[i].innerHTML);
      //document.write("<br>");
      txt+=x[i].innerHTML;
      txt+="<br>";
      }
    document.getElementById("result").innerHTML=txt;
    </script>
    </body>
    </html>

###Navigating Node Relationships
You can use the three node properties: parentNode, firstChild, and lastChild, to navigate in the document structure.

####Example
    <!DOCTYPE html>
    <html>
    <body>

    <p id="intro">Hello World!</p>
    <div id="result"></div>
    <script>
    x=document.getElementById("intro");
    //document.write(x.firstChild.nodeValue);
    document.getElementById("result").innerHTML=x.firstChild.nodeValue;
    </script>

    </body>
    </html>

###childNodes and nodeValue
    <!DOCTYPE html>
    <html>
    <body>

    <p id="intro">Hello World!</p>
    <div id="result"></div>

    <script>
    txt=document.getElementById("intro").childNodes[0].nodeValue;
    //document.write(txt);
    document.getElementById("result").innerHTML=txt;
    </script>

    </body>
    </html>

## HTML DOM Summary
This tutorial has taught you how to use the HTML DOM to make your web site more dynamic and interactive. You have learned how to manipulate HTML elements in response of different scenarios.

## REFERENCES
- [HTML DOM Tutorial](http://www.w3schools.com/htmldom/default.asp)

