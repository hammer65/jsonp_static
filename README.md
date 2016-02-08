#React Demonstrators

This repository contains two separate projects intended to demonstrate the use of 
* React
* The Flux data flow pattern
* Polymer web components
* The use of Polymer web components with React
* How JSONP can be easily integrated with React through Polymer components

All dependencies should be present. Unlike with a real production system there is no bundling of resources or a build process
This was kept intentionally simple for demonstration purposes and to fully expose the code used. Starting a basic HTTP web server in this directory will allow you to
access both demonstrations. The server I used is the server supplied by my PHP distribution.

`php -S localhost:8080`

But Python also has a server available and any other basic web server which could be rooted in this directory would work.

##Application One

![alt text](https://github.com/hammer65/jsonp_static/blob/master/react_screen_01.png "Application 1")

This is a very basic blog application which uses a web SQL database for a store.  This store can be prepopulated by going to 

`localhost:8080/db.html`

The app itself is located in the index.html file

`localhost:8080/index.html`

This application uses React with JSX. The included Babel library compiles the JSX on the fly when the page is loaded. For production it is always recommended
to compile in a build step with Babel. The concepts demonstrated include 

* React
* React JSX
* Polymer web components
* The Flux data flow pattern.

index.html is heavily commented to walk you through the various parts. Looking through the "bower_components" directory and the 
custom_elements directory will help you to get familiar with how Polymer web components work.

I didn't sweat the CSS too much but by looking at the source you will see that the main style only has 8 rules in it. All other styles
are through style encapsulation via Polymer elements or by way of Polymers included style sheets. Those encapsulated styles have
no effect on any other scope. Elements can be themable through CSS and still have their own isolated styles.

##Application Two

This application is accessible through 

`localhost:8080/jsonp.html`

This application uses React with it's own Javascript API rather than through JSX. The code you see would be what JSX compiles to. Coding with
this API can get crazy with a lot of nesting but it is performant. 

The concepts deomonstrated with this app include 
* React
* React Flux data flow
* A Polymer JSONP implementation
* The JSONP method of communication with a server.

The JSONP element used is a custom element I wrote to wrap the Polymer iron-jsonp component. it allows a way to declaritively  set up a JSONP API 
with as many endpoints as needed.

Buttons are provided for running the demo. "Get Users" will fill the table with results from getusers.js, "Add User" will re-render the table with results from 
adduser.js and "Delete User" will show the results from deleteuser.js.

JSONP works by adding a script tag to the document. The file loaded has a function call in it which contains the data payload from the server as an argument.
As long as that function is present it will execute that function with that data. An AJAX request which would load similar data,
cannot cross "same origin" boundaries, a script tag has no such restrictions. The problem with this approach is that for every call a script tag is added to the document.

JSONP libraries must manage this by loading the script tag, waiting for the code to execute and then deleting the script tag. Polymer's iron-jsonp component
does this and also creates the callback function you specify returning it's contents in a DOM event. No external Javascript is needed to make it work.

If you have any trouble with running this let me know. Any questions you have you know how to reach me.