Derby Lang
==========

A translation library for [Derby JS](http://derbyjs.com) that uses [messageformat.js](https://github.com/SlexAxton/messageformat.js).  
Refer to the messageformat.js docs on how to format translation strings.

[![Build Status](https://travis-ci.org/psirenny/derby-lang.png?branch=master)](https://travis-ci.org/psirenny/derby-lang)

Installation
------------

    $ npm install derby-lang --save

Server Usage
------------

In your server file, add the middleware:

    var lang = require('derby-lang').server;

    expressApp
      // ...
      // ...
      .use(lang())

Add a dictionary:

    // ..
    // ..
    .use(function (req, res, next) {
      var model = req.getModel();
      model.set('$lang.dict.strings', {
        en: {'Hello world.': 'Hello world.'},
        es: {'Hello world.': 'Hola mundo.'},
        fr: {'copyright': '© {year}'},
        it: {'foo': {'bar': 'baz'}}
      });
      next();
    });

Optionally, use [derby-lang-fs](https://github.com/psirenny/derby-lang-fs)
to define a dictionary with `*.json` files.

App Usage
---------

In your view functions:

    var lang = require('derby-lang').app;
    app.proto.t = lang.translate();

In your view:

    <p>{{t($lang.dict, 'en', 'Hello world.')}}</p>
    <p>{{t($lang.dict, 'fr', 'copyright.', {year: 2014})}}</p>
    <p>{{t($lang.dict, 'it', ['foo', 'bar'])}}

Locales
-------

It's up to you to manage what locale to display.
You can use [derby-locale](https://github.com/psirenny/derby-locale)
to automatically select the best locale for a user given the ones you support, their browser preference, etc.

Dictionaries
------------

A dictionary is just an object with translation strings.
It can be stored in the database rather than set during a middleware route.
You could subscribe to a dictionary and use ShareJS views to return only relevant languages.
