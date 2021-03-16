# [express](http://expressjs.com)-manifest

> Middleware which resolves requests based on generic filenames to the associated file fingerprint outlined in a manifest file. Now Supporting asset-manifest files.

This repo was forked from https://github.com/zeroEvidence/express-manifest

```js
// index.js (example ExpressJS application)

var express = require('express');
var manifest = require('express-manifest');
var app = express();

// view engine configuration...
// template engine configuration...

app.use(manifest({
  manifest: path.join(__dirname, 'public') + '/rev-manifest.json',
  prepend: path.join(__dirname, 'public'),
  reqPathFind: /^(\/?)/,
  reqPathReplace: '',
  debug: true,
  assetManifest: false
}));
app.use(express.static(path.join(__dirname, 'public')));

// routes configuration...

module.exports = app;
```
## How it works
> It obtains the incoming request path, replaces any required parts of that string and uses that string as the index within the manifest JSON file, which should return the file path relative to the "prepend" path, then if it finds the file it will send the file to the browser. QED.

## Sample manifest.json
```js
{
  "javascripts/app.js": "javascripts/app-87efdd3684ac55b9497c.js",
  "stylesheets/global.css": "stylesheets/global-692736a41c.css"
}
```

## Sample asset-manifest.json

```js
{
  "files": {
    "main.css": "/static/css/main.477617b0.chunk.css",
    "main.js": "/static/js/main.9ee1af3f.chunk.js",
    "main.js.map": "/static/js/main.9ee1af3f.chunk.js.map",
    "runtime-main.js": "/static/js/runtime-main.7a5163f1.js",
    "runtime-main.js.map": "/static/js/runtime-main.7a5163f1.js.map",
    "static/css/2.3046fb12.chunk.css": "/static/css/2.3046fb12.chunk.css",
    "static/js/2.1fd14617.chunk.js": "/static/js/2.1fd14617.chunk.js",
    "static/js/2.1fd14617.chunk.js.map": "/static/js/2.1fd14617.chunk.js.map",
    "static/js/3.39ff45eb.chunk.js": "/static/js/3.39ff45eb.chunk.js",
    "static/js/3.39ff45eb.chunk.js.map": "/static/js/3.39ff45eb.chunk.js.map",
    "index.html": "/index.html",
    "static/css/2.3046fb12.chunk.css.map": "/static/css/2.3046fb12.chunk.css.map",
    "static/css/main.477617b0.chunk.css.map": "/static/css/main.477617b0.chunk.css.map",
    "static/js/2.1fd14617.chunk.js.LICENSE.txt": "/static/js/2.1fd14617.chunk.js.LICENSE.txt"
  },
  "entrypoints": [
    "static/js/runtime-main.7a5163f1.js",
    "static/css/2.3046fb12.chunk.css",
    "static/js/2.1fd14617.chunk.js",
    "static/css/main.477617b0.chunk.css",
    "static/js/main.9ee1af3f.chunk.js"
  ]
}
```

## Sample directory structure
    .
    ├── index.js
    ├── bin
    │   └── www
    ├── package.json
    ├── public
    │   ├── javascripts
    │   |   └── app-87efdd3684ac55b9497c.js
    │   └── stylesheets
    │       └── global-692736a41c.css


## Config
[defaults.json](defaults.json) file defaults to the following configuration values:
```js
{
  "manifest": "./public/rev-manifest.json",
  "prepend": "",
  "debug": false,
  "assetManifest": false
}
```

### manifest: String

> Path to JSON manifest file relative to your "index.js".

### prepend: String

> Path to where the static assets are.

### reqPathFind: String || Regex

> The search String / Regex to modify the req.path as you see fit.

### reqPathReplace: String

> What to replace the matching "reqPathFind" value with.

### debug: Boolean

> Output useful information to the console. It, obviously, requires for one to hit the server.
