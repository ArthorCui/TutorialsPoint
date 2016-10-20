##Web Module

Let me first see the web application architecture:

A Web application is usually divided into four layers: 

![web_architecture](web_architecture.jpg)

* **Client** − This layer consists of web browsers, mobile browsers or applications which can make HTTP requests to the web server.
* **Server** − This layer has the Web server which can intercept the requests made by the clients and pass them the response.
* **Business** − This layer contains the application server which is utilized by the web server to do the required processing. This layer interacts with the data layer via the database or some external programs.
* **Data** − This layer contains the databases or any other source of data.

###QuickStart

* **Create a Web Server

Node.js provides an http module which can be used to create an HTTP client of a server. Following is the bare minimum structure of the HTTP server which listens at 8081 port.

The detail server code see [here](server.js). Default web server page is `index.htm`.

Just run `$ node server.js`

* **Create a Web Client

A web client can be created using http module. Let's check the following example.

The detail server code see [here](client.js).

Just run `$ node client.js`

