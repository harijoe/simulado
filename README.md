# Simulado

[![Circle CI](https://circleci.com/gh/ldabiralai/simulado.svg?style=svg)](https://circleci.com/gh/ldabiralai/simulado)

### Install
```bash
npm i simulado --save-dev
```

### Basic Usage ( Proposed )
#### ES2015
```javascript
import simulado from 'simulado';

let simuladoServer;

// Start Simulado server
simuladoServer = simulado.start({
  port: 1234, // Default: 7001
  keepAlive: true // Keep server running even if main process is killed. Default: false
});

// Mock a response
simulado.addMock({
  method: 'GET',
  path: '/data',
  status: 200,
  body: {
    data: 'Some Data'
  }
});

// Stop Simulado server once done
simuladoServer.close();
```

Once a response is mocked you can then make a normal HTTP request to it.
```bash
curl -X GET http://localhost:9999/data #=> { "data": "Some data" }
```

### API ( Proposed )

#### start([options])
Start Simulado

* options `<Object>`
  * `port` `<number>` - Specify the port number to start Simulado on. Default: `7001`
  * `keepAlive` `<Boolean>` - Keep Simulado running after main process it killed. Default `false`

#### `addMock(mockResponse)`
Add a mock response
* `mockResponse` `<MockResponse>` - Add a response to the store.


#### `lastRequests(method, path[, limit])`
Fetch the last requests for a path
* `method` `<String>` - The request method for the requests you want to fetch
* `path` `<String>` - The path of the requests you want to fetch
* `limit` `<number>` - Only return the given number of last requests


#### `lastRequest(method, path)`
Fetch the last request for a path
* `method` `<String>` - The request method for the requests you want to fetch
* `path` `<String>` - The path of the requests you want to fetch


#### `clearResponses()`
Clear all mocked responses from the store.


#### `clearRequests()`
Clear all captured requests from the store.


#### `stop()`
Stop Simulado.
