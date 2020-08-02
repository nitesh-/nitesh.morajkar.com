---
title: "How to Deploy Static Website on Openshift Using Nodejs"
date: "2015-03-06"
slug: 'how-to-deploy-static-website-on-openshift-using-nodejs'
description: 'Learn to deploy your static website on Openshift platform'
image: '/images/blog/openshift-nodejs.png'
tags: ['nodejs', 'deployment', 'openshift']
---

OpenShift is one of the best cloud servers available for free. You can easily deploy a static website using the **PHP catridge**, however the default page should be index.php.

It is no big deal to create a .php extension page, but I wanted the web stack to work with a .html page. This objective can be achieved using **NodeJs catridge** as follows:

*   Login to your Openshift account.
*   Click on the **Add Application** button.
*   Now, you’ll be asked to **Choose a type of application**. Here you select the **NodeJS** catridge.
*   Next step is to **Configure the application**. Add the appropriate details. (We won’t go into details) and then click on **Create Application**.
*   Now, Grab the **Git repo URL** and clone the repo on your local machine.
*   `cd` into the cloned directory. Find the **server.js** which is your HTTP server.
*   You have to configure the HTTP server according to your requirements. I suggest you create a **public_html**(or any other name) directory inside the cloned directory so that the Openshift files are not exposed.
*   You can Refer the server.js below if you don’t want to scratch your head.
    ``` js
    #!/bin/env node
    //  OpenShift sample Node application
    var express = require('express');
    var fs = require('fs');

    var publicDirectory = "public_html"; // Edit this accordingly

    /**
     *  Define the sample application.
     */
    var MyApp = function() {

        //  Scope.
        var self = this;

        /*  ================================================================  */
        /*  Helper functions.                                                 */
        /*  ================================================================  */

        /**
         *  Set up server IP address and port # using env variables/defaults.
         */
        self.setupVariables = function() {
            //  Set the environment variables we need.
            self.ipaddress = process.env.OPENSHIFT_NODEJS_IP;
            self.port      = process.env.OPENSHIFT_NODEJS_PORT || 8080;

            if (typeof self.ipaddress === "undefined") {
                //  Log errors on OpenShift but continue w/ 127.0.0.1 - this
                //  allows us to run/test the app locally.
                console.warn('No OPENSHIFT_NODEJS_IP var, using 127.0.0.1');
                self.ipaddress = "127.0.0.1";
            };
        };

        /**
         *  Populate the cache.
         */
        self.populateCache = function() {
            if (typeof self.zcache === "undefined") {
                self.zcache = { 'index.html': '' };
            }

            //  Local cache for static content.
            self.zcache['index.html'] = fs.readFileSync('./index.html');
        };

        /**
         *  Retrieve entry (content) from cache.
         *  @param {string} key  Key identifying content to retrieve from cache.
         */
        self.cache_get = function(key) { return self.zcache[key]; };

        /**
         *  terminator === the termination handler
         *  Terminate server on receipt of the specified signal.
         *  @param {string} sig  Signal to terminate on.
         */
        self.terminator = function(sig){
            if (typeof sig === "string") {
               console.log('%s: Received %s - terminating sample app ...',
                           Date(Date.now()), sig);
               process.exit(1);
            }
            console.log('%s: Node server stopped.', Date(Date.now()) );
        };

        /**
         *  Setup termination handlers (for exit and a list of signals).
         */
        self.setupTerminationHandlers = function(){
            //  Process on exit and signals.
            process.on('exit', function() { self.terminator(); });

            // Removed 'SIGPIPE' from the list - bugz 852598.
            ['SIGHUP', 'SIGINT', 'SIGQUIT', 'SIGILL', 'SIGTRAP', 'SIGABRT',
             'SIGBUS', 'SIGFPE', 'SIGUSR1', 'SIGSEGV', 'SIGUSR2', 'SIGTERM'
            ].forEach(function(element, index, array) {
                process.on(element, function() { self.terminator(element); });
            });
        };

        /*  ================================================================  */
        /*  App server functions (main app logic here).                       */
        /*  ================================================================  */

        /**
         *  Create the routing table entries + handlers for the application.
         */
        self.createRoutes = function() {
            self.routes = { };

            self.routes['/asciimo'] = function(req, res) {
                var link = "http" + "://i.imgur.com/kmbjB.png";
                res.send("<"+"html"+"><"+"body"+"><"+"img src='" + link + "' />"+"<"+ "/"+"body"+">"+"<"+"/"+"html"+">");
            };

            self.routes['/'] = function(req, res) {
                res.setHeader('Content-Type', 'text/html');
                res.send(self.cache_get('index.html') );
            };
        };

        /**
         *  Initialize the server (express) and create the routes and register
         *  the handlers.
         */
        self.initializeServer = function() {
            self.createRoutes();
            self.app = express.createServer();

            //  Add handlers for the app (from the routes).
            for (var r in self.routes) {
                self.app.get(r, self.routes[r]);
            }
        };

        /**
         *  Initializes the sample application.
         */
        self.initialize = function() {
            self.setupVariables();
            self.setupTerminationHandlers();

            // Create Express server
            self.app = express.createServer();

            // Gzip content
            self.app.use(express.compress()); 

            // Browser Cache
            var oneDay = 86400000;
            self.app.use('/', express.static(__dirname + '/' + publicDirectory + '/', { maxAge: oneDay }));
        };

        /**
         *  Start the server (starts up the sample application).
         */
        self.start = function() {
            //  Start the app on the specific interface (and port).
            self.app.listen(self.port, self.ipaddress, function() {
                console.log('%s: Node server started on %s:%d ...',
                            Date(Date.now() ), self.ipaddress, self.port);
            });
        };

    };

    /* My Application.  */

    /**
     *  main():  Main code.
     */
    var myAppObj = new MyApp();
    myAppObj.initialize();
    myAppObj.start();
    ```
*   Edit the `publicDirectory` variable, Commit the code and Push it to Openshift. Your static Website using nodejs should be LIVE.