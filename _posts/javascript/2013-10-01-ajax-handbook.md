---
layout: post
title: "Ajax Handbook"
description: "Ajax Handbook"
category: javascript
tags: [javascript, AJAX, Handbook]
---
{% include JB/setup %}

## AJAX Intro
    AJAX is about updating parts of a web page, without reloading the whole page.

###What You Should Already Know
efore you continue you should have a basic understanding of the following:

    HTML / XHTML
    CSS
    JavaScript / DOM

###What is AJAX?
    AJAX = Asynchronous JavaScript and XML.

    AJAX is a technique for creating fast and dynamic web pages.

    AJAX allows web pages to be updated asynchronously by exchanging small amounts of data with the server behind the scenes. This means that it is possible to update parts of a web page, without reloading the whole page.

###How AJAX Works
![ajax.gif]({{ site.img_url }}/ajax.gif)

###AJAX is Based on Internet Standards
AJAX is based on internet standards, and uses a combination of:

    XMLHttpRequest object (to exchange data asynchronously with a server)
    JavaScript/DOM (to display/interact with the information)
    CSS (to style the data)
    XML (often used as the format for transferring data)

AJAX applications are browser- and platform-independent!

###Google Suggest
AJAX was made popular in 2005 by Google, with Google Suggest.

## AJAX Example

###Example
    <!DOCTYPE html>
    <html>
    <head>
    <script>
    function loadXMLDoc()
    {
    var xmlhttp;
    if (window.XMLHttpRequest)
      {// code for IE7+, Firefox, Chrome, Opera, Safari
      xmlhttp=new XMLHttpRequest();
      }
    else
      {// code for IE6, IE5
      xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
      }
    xmlhttp.onreadystatechange=function()
      {
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
        {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
        }
      }
    xmlhttp.open("GET","ajax_info.txt",true);
    xmlhttp.send();
    }
    </script>
    </head>
    <body>

    <div id="myDiv"><h2>Let AJAX change this text</h2></div>
    <button type="button" onclick="loadXMLDoc()">Change Content</button>

    </body>
    </html>

###ajax_info.txt
    AJAX is not a new programming language.

    AJAX is a technique for creating fast and dynamic web pages.

##-------------------------------------------------------------------------------------------------------
## XHR Create Object

###The XMLHttpRequest Object
    All modern browsers support XMLHttpRequest object(IE5 and IE6 use ActiveXObject).
    
    The XMLHttpRequest object is used to exchange data with a server behind the scenes. This means that it is possible to update parts of a web page, without reloading the whole page.

###Create an XMLHttpRequest Object

####Syntax
    variable=new XMLHttpRequest();  #IE7+,Firefox,Chrome,Safari,and Opera
    variable=new ActiveObject("Microsoft.XMLHTTP"); #IE5,IE6

####Example
    var xmlhttp;
    if (window.XMLHttpRequest)
      {// code for IE7+, Firefox, Chrome, Opera, Safari
      xmlhttp=new XMLHttpRequest();
      }
    else
      {// code for IE6, IE5
      xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
      }

## XHR Request
The XMLHttpRequest object is used to exchange data with a server.

###Send a Request To a Server
    open(method,url,async) specifies the type of request
    
    method: the type of request: GET or POST
    url: the location of the file on the server
    async: true(asynchronous) or false(synchronous)
    
    send(string) sends the request off to the server
    
    string: only used for POST requests

###GET or POST
GET is simpler and faster than POST, and can be used in most cases.

However, always use POST requests when:

    A cached file is not an option (update a file or database on the server)
    Sending a large amount of data to the server (POST has no size limitations)
    Sending user input (which can contain unknown characters), POST is more robust and secure than GET

###GET Requests

####Example1
    <!DOCTYPE html>
    <html>
    <head>
    <script>
    function loadXMLDoc()
    {
    var xmlhttp;
    if (window.XMLHttpRequest)
      {// code for IE7+, Firefox, Chrome, Opera, Safari
      xmlhttp=new XMLHttpRequest();
      }
    else
      {// code for IE6, IE5
      xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
      }
    xmlhttp.onreadystatechange=function()
      {
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
        {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
        }
    }
    xmlhttp.open("GET","request/demo_get.jsp",true);
    xmlhttp.send();
    }
    </script>
    </head>
    <body>

    <h2>AJAX</h2>
    <button type="button" onclick="loadXMLDoc()">Request data</button>
    <div id="myDiv"></div>

    </body>
    </html>

####demo_get.jsp
    <p>This content was requested using the GET method.</p>
    <p>Requested at: <%=new java.util.Date()%> <p>

In the example above, you may get a cached result.

####Example2
To avoid this, add a unique ID to the URL:

    <!DOCTYPE html>
    <html>
    <head>
    <script>
    function loadXMLDoc()
    {
    var xmlhttp;
    if (window.XMLHttpRequest)
      {// code for IE7+, Firefox, Chrome, Opera, Safari
      xmlhttp=new XMLHttpRequest();
      }
    else
      {// code for IE6, IE5
      xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
      }
    xmlhttp.onreadystatechange=function()
      {
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
        {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
        }
      }
    xmlhttp.open("GET","request/demo_get.jsp?t=" + Math.random(),true);
    xmlhttp.send();
    }
    </script>
    </head>
    <body>

    <h2>AJAX</h2>
    <button type="button" onclick="loadXMLDoc()">Request data</button>
    <p>Click the button several times to see if the time changes, or if the file is cached.</p>
    <div id="myDiv"></div>

    </body>
    </html>

####Example3
    <!DOCTYPE html>
    <html>
    <head>
    <script>
    function loadXMLDoc()
    {
    var xmlhttp;
    if (window.XMLHttpRequest)
      {// code for IE7+, Firefox, Chrome, Opera, Safari
      xmlhttp=new XMLHttpRequest();
      }
    else
      {// code for IE6, IE5
      xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
      }
    xmlhttp.onreadystatechange=function()
      {
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
        {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
        }
      }
    xmlhttp.open("GET","request/demo_get2.jsp?fname=Henry&lname=Ford",true);
    xmlhttp.send();
    }
    </script>
    </head>
    <body>

    <h2>AJAX</h2>
    <button type="button" onclick="loadXMLDoc()">Request data</button>
    <div id="myDiv"></div>
     
    </body>
    </html>

####demo_get2.jsp
    <p>Hello ${param.fname} ${param.lname}</p>

####notes
    ${param.fname} equals <% out.print(request.getParameter("fname")); %>

###POST Requests

####Example1
    <!DOCTYPE html>
    <html>
    <head>
    <script>
    function loadXMLDoc()
    {
    var xmlhttp;
    if (window.XMLHttpRequest)
      {// code for IE7+, Firefox, Chrome, Opera, Safari
      xmlhttp=new XMLHttpRequest();
      }
    else
      {// code for IE6, IE5
      xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
      }
    xmlhttp.onreadystatechange=function()
      {
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
        {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
        }
      }
    xmlhttp.open("POST","request/demo_post.jsp",true);
    xmlhttp.send();
    }
    </script>
    </head>
    <body>

    <h2>AJAX</h2>
    <button type="button" onclick="loadXMLDoc()">Request data</button>
    <div id="myDiv"></div>
     
    </body>
    </html>

####demo_post.jsp
    <p>This content was requested using the POST method.</p>
    <p>Requested at: <%=new java.util.Date()%> <p>

####Example2
    <!DOCTYPE html>
    <html>
    <head>
    <script>
    function loadXMLDoc()
    {
    var xmlhttp;
    if (window.XMLHttpRequest)
      {// code for IE7+, Firefox, Chrome, Opera, Safari
      xmlhttp=new XMLHttpRequest();
      }
    else
      {// code for IE6, IE5
      xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
      }
    xmlhttp.onreadystatechange=function()
      {
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
        {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
        }
      }
    xmlhttp.open("POST","request/demo_post2.jsp",true);
    xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
    xmlhttp.send("fname=Henry&lname=Ford");
    }
    </script>
    </head>
    <body>

    <h2>AJAX</h2>
    <button type="button" onclick="loadXMLDoc()">Request data</button>
    <div id="myDiv"></div>
     
    </body>
    </html>

####demo_post2.jsp
    <p>Hello ${param.fname} ${param.lname}</p>

###The url - A File On a Server
    xmlhttp.open("GET","ajax_test.jsp",true);
    
    The url parameter is an address to a file on a server.

###Asynchronous - True or False?
    xmlhttp.open("GET","ajax_test.jsp",true);
    
With AJAX, the JavaScript does not have to wait for the server response, but can instead:

    execute other scripts while waiting for server response
    deal with the response when the response ready

####Async=true
    xmlhttp.onreadystatechange=function()
      {
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
        {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
        }
      }
    xmlhttp.open("GET","ajax_info.txt",true);
    xmlhttp.send();

####Async=false
    <!DOCTYPE html>
    <html>
    <head>
    <script>
    function loadXMLDoc()
    {
    var xmlhttp;
    if (window.XMLHttpRequest)
      {// code for IE7+, Firefox, Chrome, Opera, Safari
      xmlhttp=new XMLHttpRequest();
      }
    else
      {// code for IE6, IE5
      xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
      }
    xmlhttp.open("GET","example/ajax_info.txt",false);
    xmlhttp.send();
    document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
    </script>
    </head>
    <body>

    <div id="myDiv"><h2>Let AJAX change this text</h2></div>
    <button type="button" onclick="loadXMLDoc()">Change Content</button>

    </body>
    </html>

## XHR Response

###Server Response
To get the response from a server, use the responseText or responseXML property of the XMLHttpRequest object.

    responseText    get the response data as a string
    responseXML     get the response data as XML data

###The responseText Property
If the response from the server is not XML, use the responseText property.

####Example
    document.getElementById("myDiv").innerHTML=xmlhttp.responseText;

###The responseXML Property
If the response from the server is XML, and you want to parse it as an XML object, use the responseXML property.

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script>
    function loadXMLDoc()
    {
    var xmlhttp;
    var txt,x,i;
    if (window.XMLHttpRequest)
      {// code for IE7+, Firefox, Chrome, Opera, Safari
      xmlhttp=new XMLHttpRequest();
      }
    else
      {// code for IE6, IE5
      xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
      }
    xmlhttp.onreadystatechange=function()
      {
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
        {
        xmlDoc=xmlhttp.responseXML;
        txt="";
        x=xmlDoc.getElementsByTagName("ARTIST");
        for (i=0;i<x.length;i++)
          {
          txt=txt + x[i].childNodes[0].nodeValue + "<br>";
          }
        document.getElementById("myDiv").innerHTML=txt;
        }
      }
    xmlhttp.open("GET","xml/cd_catalog.xml",true);
    xmlhttp.send();
    }
    </script>
    </head>

    <body>

    <h2>My CD Collection:</h2>
    <div id="myDiv"></div>
    <button type="button" onclick="loadXMLDoc()">Get my CD collection</button>
     
    </body>
    </html>

## XHR readyState

###The onreadystatechange event
When a request to a server is sent, we want to perform some actions based on the response. Three important properties of the XMLHttpRequest object:

    onreadystatechange 	Stores a function (or the name of a function) to be called automatically each time the readyState property changes
    readyState 	        Holds the status of the XMLHttpRequest. Changes from 0 to 4:
                        0: request not initialized
                        1: server connection established
                        2: request received
                        3: processing request
                        4: request finished and response is ready
    status 	            200: "OK"
                        404: Page not found

####Example
When readyState is 4 and status is 200, the response is ready:

    xmlhttp.onreadystatechange=function()
      {
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
        {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
        }
      } 

###Using a Callback Function
A callback function is a function passed as a parameter to another function.

####Example
    <!DOCTYPE html>
    <html>
    <head>
    <script>
    var xmlhttp;
    function loadXMLDoc(url,cfunc)
    {
    if (window.XMLHttpRequest)
      {// code for IE7+, Firefox, Chrome, Opera, Safari
      xmlhttp=new XMLHttpRequest();
      }
    else
      {// code for IE6, IE5
      xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
      }
    xmlhttp.onreadystatechange=cfunc;
    xmlhttp.open("GET",url,true);
    xmlhttp.send();
    }
    function myFunction()
    {
    loadXMLDoc("example/ajax_info.txt",function()
      {
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
        {
        document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
        }
      });
    }
    </script>
    </head>
    <body>

    <div id="myDiv"><h2>Let AJAX change this text</h2></div>
    <button type="button" onclick="myFunction()">Change Content</button>

    </body>
    </html>

##-------------------------------------------------------------------------------------------------------
## AJAX ASP/PHP

###AJAX ASP/PHP Example
The following example will demonstrate how a web page can communicate with a web server while a user type characters in an input field:

###Example
    <!DOCTYPE html>
    <html>
    <head>
    <script>
    function showHint(str)
    {
    var xmlhttp;
    //alert("Input: "+str);
    if (str.length==0)
      { 
      document.getElementById("txtHint").innerHTML="";
      return;
      }
    if (window.XMLHttpRequest)
      {// code for IE7+, Firefox, Chrome, Opera, Safari
      xmlhttp=new XMLHttpRequest();
      }
    else
      {// code for IE6, IE5
      xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
      }
    xmlhttp.onreadystatechange=function()
      {
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
        {
        document.getElementById("txtHint").innerHTML=xmlhttp.responseText;
        }
      }
    //alert("Input: "+str);
    xmlhttp.open("GET","aspphp/gethint.jsp?keyword="+str,true);
    xmlhttp.send();
    }
    </script>
    </head>
    <body>

    <h3>Start typing a name in the input field below:</h3>
    <form action=""> 
    First name: <input type="text" id="txt1" onkeyup="showHint(this.value)" />
    </form>
    <p>Suggestions: <span id="txtHint"></span></p> 

    </body>
    </html>

###The JSP File
    <%
    //out.print(request.getParameter("keyword"));
    //String keyword=request.getParameter("keyword");
    //out.print(keyword);
    // Fill up array with names
    String varstr="Anna|Brittany|Cinderella|Diana|Eva|Fiona|Gunda|Hege|Inga|Johanna|Kitty|Linda|Nina|Ophelia|Petunia|Amanda|Raquel|Cindy|Doris|Eve|Evita|Sunniva|Tove|Unni|Violet|Liza|Elizabeth|Ellen|Wenche|Vicky";

    //String varstr="ljb|liujianst|www.jxnu.edu.cn|okajax|sd|we|ljb";
    String[] str=varstr.split("\\|"); 

    //get the keyword parameter from URL
    String keyword=request.getParameter("keyword");
    //out.print(keyword);
    String res="";
    if(keyword==null){
        System.out.print("no suggestion");
    }
    else {
        for(int i=0;i<str.length;i++) {
            //System.out.println(str[i]);
            //if(str[i].contains(keyword)) {
            if(str[i].toLowerCase().startsWith(keyword.toLowerCase())){
                if(res.equals("")) {
                    res=str[i];
                } else {
                    res=res+","+str[i];
                }
            }
        }
    }

    out.print(res);
    %>

## AJAX Database
AJAX can be used for interactive communication with a database.

###Example
    <!DOCTYPE html>
    <html>
    <head>
    <script>
    function showCustomer(str)
    {
    var xmlhttp;    
    if (str=="")
      {
      document.getElementById("txtHint").innerHTML="";
      return;
      }
    if (window.XMLHttpRequest)
      {// code for IE7+, Firefox, Chrome, Opera, Safari
      xmlhttp=new XMLHttpRequest();
      }
    else
      {// code for IE6, IE5
      xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
      }
    xmlhttp.onreadystatechange=function()
      {
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
        {
        document.getElementById("txtHint").innerHTML=xmlhttp.responseText;
        }
      }
    xmlhttp.open("GET","database/getcustomer.jsp?id="+str,true);
    xmlhttp.send();
    }
    </script>
    </head>
    <body>

    <form action=""> 
    <select name="customers" onchange="showCustomer(this.value)">
    <option value="">Select a customer:</option>
    <option value="ALFKI">Alfreds Futterkiste</option>
    <option value="NORTS ">North/South</option>
    <option value="WOLZA">Wolski Zajazd</option>
    </select>
    </form>
    <br>
    <div id="txtHint">Customer info will be listed here...</div>

    </body>
    </html>

###The AJAX Server Page
    <%@ page contentType="text/html; charset=utf8" %>
    <%@ page language="java" %>
    <%@ page import="com.mysql.jdbc.Driver" %>
    <%@ page import="java.sql.*" %>

    <%
    String driverName="com.mysql.jdbc.Driver";
    String username="cbay";
    String password="cbay";
    String database="ajax";
    String url="jdbc:mysql://localhost:7077/"+database+"?user="+username+"&password="+password;
    //out.println(url);
    Class.forName(driverName).newInstance();
    Connection connection=DriverManager.getConnection(url);
    Statement statement=connection.createStatement();

    String sql="select * from customers where CustomerID=";
    sql=sql+"'"+request.getParameter("id")+"'";

    ResultSet rs=statement.executeQuery(sql);
    ResultSetMetaData md=rs.getMetaData();
    int count=md.getColumnCount();

    out.println("<table>");
    while(rs.next()){
        for(int i=2;i<=count;i++){
            String field=md.getColumnName(i);
            String value=rs.getString(field);
            out.println("<tr><td><b>" +field+ "</b></td>");
            out.println("<td>" +value+ "</td></tr>");
        }
    }
    out.println("</table>");
    %>

## AJAX XML File
AJAX can be used for interactive communication with an XML file

###Example
    <!DOCTYPE html>
    <html>
    <head>
    <script>
    function loadXMLDoc(url)
    {
    var xmlhttp;
    var txt,x,xx,i;
    if (window.XMLHttpRequest)
      {// code for IE7+, Firefox, Chrome, Opera, Safari
      xmlhttp=new XMLHttpRequest();
      }
    else
      {// code for IE6, IE5
      xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
      }
    xmlhttp.onreadystatechange=function()
      {
      if (xmlhttp.readyState==4 && xmlhttp.status==200)
        {
        txt="<table border='1'><tr><th>Title</th><th>Artist</th></tr>";
        x=xmlhttp.responseXML.documentElement.getElementsByTagName("CD");
        for (i=0;i<x.length;i++)
          {
          txt=txt + "<tr>";
          xx=x[i].getElementsByTagName("TITLE");
            {
            try
              {
              txt=txt + "<td>" + xx[0].firstChild.nodeValue + "</td>";
              }
            catch (er)
              {
              txt=txt + "<td> </td>";
              }
            }
          xx=x[i].getElementsByTagName("ARTIST");
            {
            try
              {
              txt=txt + "<td>" + xx[0].firstChild.nodeValue + "</td>";
              }
            catch (er)
              {
              txt=txt + "<td> </td>";
              }
            }
          txt=txt + "</tr>";
          }
        txt=txt + "</table>";
        document.getElementById('txtCDInfo').innerHTML=txt;
        }
      }
    xmlhttp.open("GET",url,true);
    xmlhttp.send();
    }
    </script>
    </head>
    <body>

    <div id="txtCDInfo">
    </div>
    <button onclick="loadXMLDoc('xml/cd_catalog.xml')">Get CD info</button>

    </body>
    </html>

###cd_catalog.xml
    <?xml version="1.0" encoding="windows-1252"?>
    <!-- Edited by XMLSpy® -->
    <CATALOG>
	    <CD>
		    <TITLE>Empire Burlesque</TITLE>
		    <ARTIST>Bob Dylan</ARTIST>
		    <COUNTRY>USA</COUNTRY>
		    <COMPANY>Columbia</COMPANY>
		    <PRICE>10.90</PRICE>
		    <YEAR>1985</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Hide your heart</TITLE>
		    <ARTIST>Bonnie Tyler</ARTIST>
		    <COUNTRY>UK</COUNTRY>
		    <COMPANY>CBS Records</COMPANY>
		    <PRICE>9.90</PRICE>
		    <YEAR>1988</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Greatest Hits</TITLE>
		    <ARTIST>Dolly Parton</ARTIST>
		    <COUNTRY>USA</COUNTRY>
		    <COMPANY>RCA</COMPANY>
		    <PRICE>9.90</PRICE>
		    <YEAR>1982</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Still got the blues</TITLE>
		    <ARTIST>Gary Moore</ARTIST>
		    <COUNTRY>UK</COUNTRY>
		    <COMPANY>Virgin records</COMPANY>
		    <PRICE>10.20</PRICE>
		    <YEAR>1990</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Eros</TITLE>
		    <ARTIST>Eros Ramazzotti</ARTIST>
		    <COUNTRY>EU</COUNTRY>
		    <COMPANY>BMG</COMPANY>
		    <PRICE>9.90</PRICE>
		    <YEAR>1997</YEAR>
	    </CD>
	    <CD>
		    <TITLE>One night only</TITLE>
		    <ARTIST>Bee Gees</ARTIST>
		    <COUNTRY>UK</COUNTRY>
		    <COMPANY>Polydor</COMPANY>
		    <PRICE>10.90</PRICE>
		    <YEAR>1998</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Sylvias Mother</TITLE>
		    <ARTIST>Dr.Hook</ARTIST>
		    <COUNTRY>UK</COUNTRY>
		    <COMPANY>CBS</COMPANY>
		    <PRICE>8.10</PRICE>
		    <YEAR>1973</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Maggie May</TITLE>
		    <ARTIST>Rod Stewart</ARTIST>
		    <COUNTRY>UK</COUNTRY>
		    <COMPANY>Pickwick</COMPANY>
		    <PRICE>8.50</PRICE>
		    <YEAR>1990</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Romanza</TITLE>
		    <ARTIST>Andrea Bocelli</ARTIST>
		    <COUNTRY>EU</COUNTRY>
		    <COMPANY>Polydor</COMPANY>
		    <PRICE>10.80</PRICE>
		    <YEAR>1996</YEAR>
	    </CD>
	    <CD>
		    <TITLE>When a man loves a woman</TITLE>
		    <ARTIST>Percy Sledge</ARTIST>
		    <COUNTRY>USA</COUNTRY>
		    <COMPANY>Atlantic</COMPANY>
		    <PRICE>8.70</PRICE>
		    <YEAR>1987</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Black angel</TITLE>
		    <ARTIST>Savage Rose</ARTIST>
		    <COUNTRY>EU</COUNTRY>
		    <COMPANY>Mega</COMPANY>
		    <PRICE>10.90</PRICE>
		    <YEAR>1995</YEAR>
	    </CD>
	    <CD>
		    <TITLE>1999 Grammy Nominees</TITLE>
		    <ARTIST>Many</ARTIST>
		    <COUNTRY>USA</COUNTRY>
		    <COMPANY>Grammy</COMPANY>
		    <PRICE>10.20</PRICE>
		    <YEAR>1999</YEAR>
	    </CD>
	    <CD>
		    <TITLE>For the good times</TITLE>
		    <ARTIST>Kenny Rogers</ARTIST>
		    <COUNTRY>UK</COUNTRY>
		    <COMPANY>Mucik Master</COMPANY>
		    <PRICE>8.70</PRICE>
		    <YEAR>1995</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Big Willie style</TITLE>
		    <ARTIST>Will Smith</ARTIST>
		    <COUNTRY>USA</COUNTRY>
		    <COMPANY>Columbia</COMPANY>
		    <PRICE>9.90</PRICE>
		    <YEAR>1997</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Tupelo Honey</TITLE>
		    <ARTIST>Van Morrison</ARTIST>
		    <COUNTRY>UK</COUNTRY>
		    <COMPANY>Polydor</COMPANY>
		    <PRICE>8.20</PRICE>
		    <YEAR>1971</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Soulsville</TITLE>
		    <ARTIST>Jorn Hoel</ARTIST>
		    <COUNTRY>Norway</COUNTRY>
		    <COMPANY>WEA</COMPANY>
		    <PRICE>7.90</PRICE>
		    <YEAR>1996</YEAR>
	    </CD>
	    <CD>
		    <TITLE>The very best of</TITLE>
		    <ARTIST>Cat Stevens</ARTIST>
		    <COUNTRY>UK</COUNTRY>
		    <COMPANY>Island</COMPANY>
		    <PRICE>8.90</PRICE>
		    <YEAR>1990</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Stop</TITLE>
		    <ARTIST>Sam Brown</ARTIST>
		    <COUNTRY>UK</COUNTRY>
		    <COMPANY>A and M</COMPANY>
		    <PRICE>8.90</PRICE>
		    <YEAR>1988</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Bridge of Spies</TITLE>
		    <ARTIST>T'Pau</ARTIST>
		    <COUNTRY>UK</COUNTRY>
		    <COMPANY>Siren</COMPANY>
		    <PRICE>7.90</PRICE>
		    <YEAR>1987</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Private Dancer</TITLE>
		    <ARTIST>Tina Turner</ARTIST>
		    <COUNTRY>UK</COUNTRY>
		    <COMPANY>Capitol</COMPANY>
		    <PRICE>8.90</PRICE>
		    <YEAR>1983</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Midt om natten</TITLE>
		    <ARTIST>Kim Larsen</ARTIST>
		    <COUNTRY>EU</COUNTRY>
		    <COMPANY>Medley</COMPANY>
		    <PRICE>7.80</PRICE>
		    <YEAR>1983</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Pavarotti Gala Concert</TITLE>
		    <ARTIST>Luciano Pavarotti</ARTIST>
		    <COUNTRY>UK</COUNTRY>
		    <COMPANY>DECCA</COMPANY>
		    <PRICE>9.90</PRICE>
		    <YEAR>1991</YEAR>
	    </CD>
	    <CD>
		    <TITLE>The dock of the bay</TITLE>
		    <ARTIST>Otis Redding</ARTIST>
		    <COUNTRY>USA</COUNTRY>
		    <COMPANY>Atlantic</COMPANY>
		    <PRICE>7.90</PRICE>
		    <YEAR>1987</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Picture book</TITLE>
		    <ARTIST>Simply Red</ARTIST>
		    <COUNTRY>EU</COUNTRY>
		    <COMPANY>Elektra</COMPANY>
		    <PRICE>7.20</PRICE>
		    <YEAR>1985</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Red</TITLE>
		    <ARTIST>The Communards</ARTIST>
		    <COUNTRY>UK</COUNTRY>
		    <COMPANY>London</COMPANY>
		    <PRICE>7.80</PRICE>
		    <YEAR>1987</YEAR>
	    </CD>
	    <CD>
		    <TITLE>Unchain my heart</TITLE>
		    <ARTIST>Joe Cocker</ARTIST>
		    <COUNTRY>USA</COUNTRY>
		    <COMPANY>EMI</COMPANY>
		    <PRICE>8.20</PRICE>
		    <YEAR>1987</YEAR>
	    </CD>
    </CATALOG>


##-------------------------------------------------------------------------------------------------------

## REFERENCES
- [AJAX Tutorial](http://www.w3schools.com/ajax/default.asp)

