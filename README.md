# voice-app-project

The goal here is to create the simplest possible messaging/calling app for learning purposes.

**Client spec:**

- The client requires a server backend (hostname) to authenticate with. The server is intended to be self-hosted.
- Once the client is given a host, it will attempt to authenticate the user using google-backed OAuth.
- Once authenticated, it will load into a simple landing page with a user friends list and chats with an option to voice call from this friends list.
- The client will open a websocket with the server for communication.
- Upon sending a message, the client will call an API on the server using the JWT grabbed during auth.
- When sending a call request, the client will call the API with the necessary details.

**Server spec:**

- The server should maintain a local persistent database.
- This database needs to maintain a user list, friends list (indexed via user ID), message list (indexed via user ID), group chat list (indexed via a unique group chat ID that links to each user in the group chat).
- The server needs to redirect the client to the Google OAuth backend and then register/authenticate the client. It needs to support a client whitelist.
- Once the client is registered the server needs to pass the client a JWT.
- The server message API should support sending and deleting messages between users.
- The server should expose an API for sending call requests between users.
- The server should store an ephemeral queue of call requests between users (effectively state machines).
- When a user sends a call request, the server needs to send a call request message to the corresponding client. This request then gets pushed to the queue. The server needs to purge this queue after t=number of seconds left on oldest call request.
- If the call request is accepted, then the server needs to broker a WebRTC handshake between the two clients.
- The server should broker connections via a public STUN server and this list of available STUN servers should be user-configurable and should be verified periodically as useable by the server.
