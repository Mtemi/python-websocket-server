Websockets Server
=======================

A minimal Websockets Server in Python with no external dependencies.

  * Works with Python2 and Python3
  * Clean simple API
  * Multiple clients
  * No dependencies
  
Notice that this Websocket Server doesn't support the more advanced features
like SSL etc. The main usage for this server is to include it in your program
as means of providing GUI.


Usage
=======================
You can get a feel of how to use the websocket server by running

    python server.py
    
Then you need to connect from a client. Use the client.html file to connect
by using your browser's websocket implementation.


Using on your project
=======================
In order to use the websocket server in your project, simply
copy `websocket.py` to your project and `from websocket import WebSocketsServer`.
Then use the documented API below to manage the behaviour of your server.


API
=======================

The API is simply methods and properties of a WebSocketsServer instance.

**Properties**

| Property | Description          |
|----------|----------------------|
| clients  | A list of `client`   |


**Structures**
````
client = {
	'id'      : client_id,
	'handler' : client_handler,
	'address' : (addr, port)
}
````

**Methods**
| Method                    | Description                                                                         | Takes           | Gives |
|---------------------------|-------------------------------------------------------------------------------------|-----------------|-------|
| set_fn_new_client()       | Sets a callback function that will be called for every new client connecting to us  | function        | None  |
| set_fn_client_left()      | Sets a callback function that will be called for every client disconnecting from us | function        | None  |
| set_fn_message_received() | Sets a callback function that will be called when a client sends a message          | function        | None  |
| send_message()            | Sends a message to a specific client. The message is a simple string.               | client, message | None  |
| send_message_to_all()     | Sends a message to all connected clients. The message is a simple string.           | message         | None  |


**Callback functions**
| Set by                    | Description                                   | Parameters              |
|---------------------------|-----------------------------------------------|-------------------------|
| set_fn_new_client()       | Called for every new client connecting to us  | client, server          |
| set_fn_client_left()      | Called for every client disconnecting from us | client, server          |
| set_fn_message_received() | Called when a client sends a message          | client, server, message |

The client gives access to the structure client. The server is merely passed to be able and send messages to clients.

Example:
````
from websocket import WebSocketsServer

def new_client(client, server):
	server.send_message_to_all("Hey all, a new client has joined us")

server = WebSocketsServer(13254)
server.set_fn_new_client(new_client)
server.run_forever()
````
