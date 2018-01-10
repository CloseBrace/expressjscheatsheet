# Express.js Cheat Sheet - http://expressjscheatsheet.com

A handy collection of Express.js commands

## Simple Server Setup

```
const express = require('express');
const http = require('http');
const app = express();
const server = http.createServer(app);
server.listen(3000);
server.on('error', erorHandler);
server.on('listening', listeningHandler);
app.get('/', (req, res) => res.send('Hello World'));
```

## Settings

```
app.set('view engine', 'ejs');
app.get('view engine'); // "ejs"
app.set('mySetting', true);
app.get('mySetting'); // true
```

## Body Parsing

```
const bodyParser = require('body-parser');
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({
    extended: true
}));
```

## Routing

```
/* In app.js =============================== */
const posts= require('./routes/posts');
app.use('/posts', posts);

/* In /routes/posts.js ======================== */const express = require('express');
const router = express.Router();
router.all('*', (req, res) => { // handler });
router.delete('/remove', (req, res) => { // handler });
router.get('/list', (req, res) => { // handler });
router.param('id', (req, res, next, id) => { // handler });
router.post('/add', (req, res) => { // handler });
router.put('/update', (req, res) => { // handler });router.use('optional', (req, res) => { //middleware });module.exports = router;
```

## Request

```
/* Request Header Info ====================== */
req.baseUrl  // route root URL (/posts)req.hostname // app hostname (example.com)
req.ip // app ip (127.0.0.1)req.method // request method (GET, POST, etc)
req.path // path section of request URL
req.protocol // http or https
req.route // current route object

/* Request Data ============================ */
req.body // POST body
req.cookies // cookie values (needs cookie-parser)
req.params // Route parameters
req.query // GET querystring values
req.signedCookies // signed cookies (cookie-parser)
```

## Response

```
res.cookie(name, value, options); // set cookie
res.clearCookie(name, options]); // clear cookie
res.json({ postId: req.params.id }); // send JSON
res.locals // set data accessible by view / template
res.location('/example'); // set HTTP location header
res.redirect('/home'); // redirect user
res.render('index'); // render a view
res.send('Hello World!'); // send response
res.sendFile(fileName, options, callback); // send file
res.status(400); // send HTTP status
```

## Middleware

```
/* In app.js =============================== */
app.use(myMiddleWare);

/* In /routes/posts.js ======================== */
router.all('/posts', (req, res, next) => {
  console.log('Post API contacted');
  next();
});

router.get('/posts/:id', (req, res, next) => {
  const post = getPostById(req.params.id);
  res.json(post);
});
```

Brought to you by [CloseBrace](http://closebrace.com) &mdash; Full-Stack JavaScript Training