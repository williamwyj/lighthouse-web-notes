```js
// require the ws package
require('ws');

//create a new WebSocket connection to the URL indicated
const ws = new WebSocket('ws://www.example.com');

// ws.on function makes sure the call back is executed after the connection is established.
// ws.send sends a specificed message to the server
ws.on('open', function open() {
  ws.send('something');
});

//receives data from the server
ws.on('message', function incoming(data) {
  console.log(data);
});
```

```js
// require the ws package
require('ws');

//create a new WebSocket connection with the port from the server indicated
const wss = new WebSocket.Server({ port: 8080 });

// ws.on function makes sure the call back is executed after the connection is established.
wss.on('connection', function connection(ws) {

// receive data from the client
  ws.on('message', function incoming(message) {
    console.log('received: %s', message);
  });

//send data to the client
  ws.send('something');
});
```
