# NodeJS
Node.js is a very powerful JavaScript-based framework/platform built on Google Chrome's JavaScript V8 Engine. It is used to develop I/O intensive web applications like video streaming sites, single-page applications, and other web applications.

## Features
* **Asynchronous and Event Driven** − All APIs of Node.js library are asynchronous, that is, non-blocking. It essentially means a Node.js based server never waits for an API to return data. The server moves to the next API after calling it and a notification mechanism of Events of Node.js helps the server to get a response from the previous API call.

* **Very Fast** − Being built on Google Chrome's V8 JavaScript Engine, Node.js library is very fast in code execution.

* **Single Threaded but Highly Scalable** − Node.js uses a single threaded model with event looping. Event mechanism helps the server to respond in a non-blocking way and makes the server highly scalable as opposed to traditional servers which create limited threads to handle requests. Node.js uses a single threaded program and the same program can provide service to a much larger number of requests than traditional servers like Apache HTTP Server.

* **No Buffering** − Node.js applications never buffer any data. These applications simply output the data in chunks.

* **License** − Node.js is released under the MIT license.

## Environment

> Windows	node-v0.12.0-x64.msi
> Linux		node-v0.12.0-linux-x86.tar.gz
> Mac		node-v0.12.0-darwin-x86.tar.gz

> Linux		export PATH=$PATH:/usr/local/nodejs/bin
> Mac		export PATH=$PATH:/usr/local/nodejs/bin
> FreeBSD	export PATH=$PATH:/usr/local/nodejs/bin

```
$ cd /tmp
$ wget http://nodejs.org/dist/v0.12.0/node-v0.12.0-linux-x64.tar.gz
$ tar xvfz node-v0.12.0-linux-x64.tar.gz
$ mkdir -p /usr/local/nodejs
$ mv node-v0.12.0-linux-x64/* /usr/local/nodejs
```

## Quick Start

A Node.js application consists of the following three important components:

* **Import required modules** − We use the require directive to load Node.js modules.

* **Create server** − A server which will listen to client's requests similar to Apache HTTP Server.

* **Read request and return response** − The server created in an earlier step will read the HTTP request made by the client which can be a browser or a console and return the response.

see the example [here](helloworld.js). Just run `$ node helloworld.js`

## Package Manager

NPM comes bundled with Node.js installables after v0.6.3 version. To verify the same, open console and type the following command and see the result `$ npm --version`

If you update `npm` to the latest version, run this command:

```
$ sudo npm install npm -g
/usr/bin/npm -> /usr/lib/node_modules/npm/bin/npm-cli.js
npm@2.7.1 /usr/lib/node_modules/npm
```

By default, NPM installs any dependency in the local mode. Here local mode refers to the package installation in `node_modules` directory lying in the folder where Node application is present. Locally deployed packages are accessible via `require()` method. For example, when we installed `express` module, it created node_modules directory in the current directory where it installed the `express` module.

```
# Install a Module
$ npm install <Module Name>

# Uninstall a Module
$ npm uninstall <Module Name>

# Update a Module
$ npm update <Module Name>

# Search a Module
$ npm search <Module Name>

# Create a Module
$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sane defaults.

See 'npm help json' for definitive documentation on these fields
and exactly what they do.

Use 'npm install <pkg> --save' afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
name: (webmaster)

$ npm adduser
Username: mcmohd
Password:
Email: (this IS public) mcmohd@gmail.com

$ npm publish
```

## Modules

* **[CallBack](callback.md)**
* **[Event Loop](event-loop.md)**
* **[Event Emitter](event-emitter.md)**
* **[Buffers](buffers.md)**
* **[Streams](streams.md)**
* **[File Stream](filestream.md)**
* **[Global Objects](global-objects.md)**
* **[Web Module](web-module.md)**
* **[Express Framework](express-framework.md)**
* **[RESTFUL API](restfulAPI.md)**
* **[Scaling Application](scaling-application.md)**
