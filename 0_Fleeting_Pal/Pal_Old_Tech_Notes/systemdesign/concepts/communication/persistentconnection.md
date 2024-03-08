### Ajax Polling
* Client requests for new information
* Server checks for new information, if not present it will send empty response.
* HTTP connection overhead

### Long Polling
* Clients requests for new information
* Server checks for new information, if not available, it waits until any new information is available.
* When new information is not available for a long time, request times-out.

### Web sockets
TODO

### Server send events
TODO