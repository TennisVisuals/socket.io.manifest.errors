# socket.io.manifest.errors

This is an example of socket.io *not* working when a manifest is added

- npm install
- npm start
- open localhost:3000 in browser

everything works!

modify index.html

change
```<html>```
to
```<html manifest='index.manifest'>```

## ERROR:
socket.io-1.2.0.js:2 GET http://localhost:3000/socket.io/?EIO=3&transport=polling&t=1491065530785-0 net::ERR_FAILED

to remove the cache in Chrome:
```chrome://appcache-internals/```
