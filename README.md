# Web Sockets in Express

This project provides a streamlined way to integrate WebSockets into your Express.js applications using TypeScript. It offers a simple and well-documented approach for establishing real-time communication channels within your Node.js projects.

## Installation

1. Initialize an empty Node.js project.

```bash
npm init -y
```

2. Add tsconfig to it

```bash
npx tsc --init
```

3. Update tsconfig

```bash
"rootDir": "./src",
"outDir": "./dist",
```

4. Install ws

```bash
npm i ws @types/ws
```

5. Install Express
```bash
npm install express @types/express
```

6. Code using Express
```bash
import express from 'express'
import { WebSocketServer, WebSocket } from 'ws'

const app = express()
const httpServer = app.listen(8080)

const wss = new WebSocketServer({ server: httpServer });

let userCount = 0;
wss.on('connection', function connection(ws) {
  ws.on('error', console.error);

  ws.on('message', function message(data, isBinary) {
    wss.clients.forEach(function each(client) {
      if (client.readyState === WebSocket.OPEN) {
        client.send(data, { binary: isBinary });
      }
    });
  });

  console.log("User Count: ", ++userCount);
  ws.send('Hello! Message From Server!!');
});
```

7. Compile the Typescript Code to Javascript Code
```bash
tsc -b
```

8. Run the Server
```bash
node dist/index.js
```