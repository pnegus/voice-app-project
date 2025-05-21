# voice-app-project

The goal here is to create the simplest possible messaging/calling app for learning purposes.

Server listens on 443 only and will broker connections between clients.

I want to implement google oauth ONLY. 

The server should in no way expose sensitive details between clients. For demo purposes, only 1 live connection will be allowed at a time. 

Basic client details:

- Client should authenticate with the server and open a websocket to poll for state changes

- If another client wants to make a call, the server will first check if the requested client is available. Once both clients are in an "call accepted" state, open two ports and send both clients the respective networking info. 

- Server will close the communication ports and move both clients to a ready state after either a: 1 minute has passed or b: a client closes the connection or sends a close request to the server.

Basic server details:

- The server should be able to authenticate users using oauth2 and the google oauth provider.

- The server should store a "friends list" of email addresses as well as a pending queue of friend requests for clients.

- The server cannot be blocked by constant authentication requests so it needs some form of rate limiting.

