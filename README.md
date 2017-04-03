# socket.io.manifest.errors

I have been having trouble getting socket.io to work after adding .manifest file.  

- npm install
- npm start
- open localhost:3000 in browser

**everything works!**

modify ```index.html```
changing 
```<html>```
to
```<html manifest='index.manifest'>```

## Original Error
In the Javascript Console:

```
socket.io-1.7.2.js:2 GET http://localhost:3000/socket.io/?EIO=3&transport=polling&t=1491065530785-0 net::ERR_FAILED
```

to remove the cache in Chrome:
```
chrome://appcache-internals/
```

## FIX

```
var connectionOptions =  {
   "force new connection" : true,
   "reconnectionAttempts": "Infinity",
   "timeout" : 10000,
};
var socket = io(connectionOptions);
```

Now it works *exactly once* when hosted on a server with no proxy.  Reloading with the manifest again gives ```net::ERR_FAILED``` error in the Javascript console.

## Cloudflare and Nginx

Now I am running on a server using Nginx and Cloudflare.

Without the manifest file I get the following error in the Javascript console, but **everything still works**:

``` 
socket.io-1.7.2.js:7370 WebSocket connection to 'wss://hiveeye.net/socket.io/?EIO=3&transport=websocket&sid=rM2LKvCGJwaFx7RrAAAf' failed: Error during WebSocket handshake: Unexpected response code: 400
```

after modifying ```index.html```
and changing 
```<html>```
to
```<html manifest='index.manifest'>```

the client works **exactly once**, then fails with the following errors:

```
socket.io-1.7.2.js:4948 GET https://hiveeye.net/socket.io/?EIO=3&transport=polling&t=Lik5SC5&sid=rM2LKvCGJwaFx7RrAAAf net::ERR_FAILED

GET https://hiveeye.net/socket.io/?EIO=3&transport=polling&t=Lik5STN net::ERR_FAILED

GET https://hiveeye.net/socket.io/?EIO=3&transport=polling&t=Lik5STN net::ERR_FAILED
```
