# Getting started

# Basics

## Serve Files

### Serving static files

#### Serve index.html at route '/'

```js
var express = require('express');
var app = express();
var path = require('path');

// viewed at http://localhost:8080
app.get('/', function(req, res) {
    res.sendFile(path.join(__dirname + '/index.html'));
});

app.listen(8080);
```

> This will serve file ./index.html when accessing http://localhost:8080/ in the Browser

#### Serve Folder `public` at route '/'

```js
app.use(express.static('public'));
```
> This will serve all files in directory `public` at http://localhost:xxxx/
> e.g.: `./public/css/styles.css` becomes `http://localhost:xxxx/css/styles.css`