pouchdb-getting-started-todo
============================

A clone of the source repository for the getting started tutorial for PouchDB

I made a change to app.js to pick up the name of the server that it's on

I set up a server as a folder in Apache, which serves the index.html and javascript files. At first I did a direct connection to CouchDB through port 5984, but went through all kinds of config hassles with CORS, and then I found I couldn't access it from work because the port was blocked, even after poking a hole in my firewall.

I found a tip on setting up a reverse proxy in Apache, with a rewrite rule to pass anything starting with /db/ to go directly to CouchDB. Works like a charm, all on port 80. Much better than fighting with CORS.

In apache my configs look like this:

     RewriteEngine On
     RewriteOptions Inherit

     RewriteRule ^/db/(.*) http://192.168.1.4:5984/$1?user=%{LA-U:REMOTE_USER} [QSA,P]

I needed to enable apache mods rewrite, proxy and proxy_http to make it all work

