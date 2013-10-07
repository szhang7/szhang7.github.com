---
layout: post
title: "JSON Handbook"
description: "JSON Handbook"
category: javascript
tags: [javascript, JSON, Handbook]
---
{% include JB/setup %}

## JSON HOME
JSON is smaller than XML, and faster and easier to parse.

###What is JSON?

    JSON stands for JavaScript Object Notation
    JSON is lightweight text-data interchange format
    JSON is language independent *
    JSON is "self-describing" and easy to understand

###JSON - Evaluates to JavaScript Objects
The JSON text format is syntactically identical to the code for creating JavaScript objects.

## JSON Intro

###Example
    <!DOCTYPE html>
    <html>
    <body>
    <h2>JSON Object Creation in JavaScript</h2>

    <p>
    Name: <span id="jname"></span><br>  
    Age: <span id="jage"></span><br> 
    Address: <span id="jstreet"></span><br> 
    Phone: <span id="jphone"></span><br> 
    </p>  

    <script>
    var JSONObject = {
      "name":"John Johnson",
      "street":"Oslo West 16", 
      "age":33,
      "phone":"555 1234567"};
    document.getElementById("jname").innerHTML=JSONObject.name  
    document.getElementById("jage").innerHTML=JSONObject.age  
    document.getElementById("jstreet").innerHTML=JSONObject.street  
    document.getElementById("jphone").innerHTML=JSONObject.phone  
    </script>

    </body>
    </html>

###Much Like XML

    JSON is plain text
    JSON is "self-describing" (human readable)
    JSON is hierarchical (values within values)
    JSON can be parsed by JavaScript
    JSON data can be transported using AJAX

###Much Unlike XML

    No end tag
    Shorter
    Quicker to read and write
    Can be parsed using built-in JavaScript eval()
    Uses arrays
    No reserved words

###Why JSON?
For AJAX applications, JSON is faster and easier than XML:

Using XML

    Fetch an XML document
    Use the XML DOM to loop through the document
    Extract values and store in variables

Using JSON

    Fetch a JSON string
    eval() the JSON string

## JSON Syntax
JSON syntax is a subset of JavaScript syntax.

###JSON Syntax Rules

    Data is in name/value pairs
    Data is separated by commas
    Curly braces hold objects
    Square brackets hold arrays

###JSON Name/Value Pairs
JSON data is written as name/value pairs.

    "firstName" : "John"

###JSON Values

    A number (integer or floating point)
    A string (in double quotes)
    A Boolean (true or false)
    An array (in square brackets)
    An object (in curly brackets)
    null

###JSON Objects
JSON objects are written inside curly brackets.

    { "firstName":"John", "lastName":"Doe" }

###JSON Arrays
JSON arrays are written inside square brackets.

    {
    "employees": [
    { "firstName":"John", "lastName":"Doe" },
    { "firstName":"Anna", "lastName":"Smith" },
    { "firstName":"Peter", "lastName":"Jones" }
    ]
    }

###JSON Uses JavaScript Syntax
Because JSON uses JavaScript syntax, no extra software is needed to work with JSON within JavaScript.

####Example
    <!DOCTYPE html>
    <html>
    <body>
    <h2>Create Object from JSON String</h2>
    <p>Original name: <span id="origname"></span></p>
    <p>New name: <span id="newname"></span></p>

    <script>
    var employees = [
    { "firstName" : "John" , "lastName" : "Doe" }, 
    { "firstName" : "Anna" , "lastName" : "Smith" }, 
    { "firstName" : "Peter" , "lastName" : "Jones" }, ];

    document.getElementById("origname").innerHTML=employees[0].firstName + " " + employees[0].lastName;

    // Set new name
    employees[0].firstName="Gilbert";
    document.getElementById("newname").innerHTML=employees[0].firstName + " " + employees[0].lastName;
    </script>

    </body>
    </html>

###JSON Files

    The file type for JSON files is ".json"
    The MIME type for JSON text is "application/json"

##JSON HowTo

###Converting a JSON Text to a JavaScript Object
    One of the most common use of JSON is to fetch JSON data from a web server (as a file or as an HttpRequest), convert the JSON data to a JavaScript object, and then it uses the data in a web page.

###JSON Example - Object From String
Create a JavaScript string containing JSON syntax:

    var txt = '{ "employees" : [' +
    '{ "firstName":"John" , "lastName":"Doe" },' +
    '{ "firstName":"Anna" , "lastName":"Smith" },' +
    '{ "firstName":"Peter" , "lastName":"Jones" } ]}';

Since JSON syntax is a subset of JavaScript syntax, the JavaScript function eval\(\) can be used to convert a JSON text into a JavaScript object.

The eval\(\) function uses the JavaScript compiler which will parse the JSON text and produce a JavaScript object. The text must be wrapped in parenthesis to avoid a syntax error:

    var obj = eval ("(" + txt + ")"); 


####Example
    <!DOCTYPE html>
    <html>
    <body>
    <h2>Create Object from JSON String</h2>
    <p>
    First Name: <span id="fname"></span><br> 
    Last Name: <span id="lname"></span><br> 
    </p> 
    <script>
    var txt = '{"employees":[' +
    '{"firstName":"John","lastName":"Doe" },' +
    '{"firstName":"Anna","lastName":"Smith" },' +
    '{"firstName":"Peter","lastName":"Jones" }]}';

    var obj = eval ("(" + txt + ")");

    document.getElementById("fname").innerHTML=obj.employees[1].firstName 
    document.getElementById("lname").innerHTML=obj.employees[1].lastName 
    </script>
    </body>
    </html>

###JSON Parser
It is safer to use a JSON parser to convert a JSON text to a JavaScript object. A JSON parser will recognize only JSON text and will not compile scripts. 

####Example
    <!DOCTYPE html>
    <html>
    <body>
    <h2>Create Object from JSON String</h2>
    <p>
    First Name: <span id="fname"></span><br> 
    Last Name: <span id="lname"></span><br> 
    </p> 
    <script>
    var txt = '{"employees":[' +
    '{"firstName":"John","lastName":"Doe" },' +
    '{"firstName":"Anna","lastName":"Smith" },' +
    '{"firstName":"Peter","lastName":"Jones" }]}';

    obj = JSON.parse(txt);

    document.getElementById("fname").innerHTML=obj.employees[1].firstName 
    document.getElementById("lname").innerHTML=obj.employees[1].lastName 
    </script>
    </body>
    </html>

## REFERENCES
- [JSON Tutorial](http://www.w3schools.com/json/default.asp)

