# So simple chat

> Simple chat app with **WebSockets** ( [*express-ws*](https://www.npmjs.com/package/express-ws) )
> where both front and back are in single [Nuxt.js](https://nuxtjs.org) project.

## About

This project shows how to build simple application
with **WebSockets** in [Nuxt.js](https://nuxtjs.org).

## Build Setup

``` bash
# install dependencies
$ npm run install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm run start
```

For detailed explanation on how things work, check out [Nuxt.js docs](https://nuxtjs.org).

## Code

Most important part is opening websocket in the *server/index.js*:

```javascript
...
var expressWs = require('express-ws')(app)

app.ws('/chat', function(ws, req) {
  ws.on('message', function(msg) {
    expressWs.getWss().clients.forEach(client => client.send(msg))
  })
})
...
```
Rest is in the *pages/index.vue*.

## Good way to check this solution

1. Run application.
```bash
npm i
npm run dev
```

2. Open http://localhost:3000/ in two browsers.

3. Change nickname at least in one of pages with chat.

4. Enjoy :-)
