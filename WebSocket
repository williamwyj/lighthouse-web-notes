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
