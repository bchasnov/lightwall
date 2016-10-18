# LightServer

Give me code and I will run it on my light display. Otherwise, I'll just run the default code or do nothing.

## Requirement
Uses a fork of heroic-pixel-pusher located in bchasnov/node-pixelpusher
Pixelpusher on the same network and a network that allows streaming udp packets (no firewall).

## Getting Started
### Test the pixelpusher
To install, `$ cd lightserver` and `$ npm install`
Execute the test script `$ node test_pixelpusher.js` and wait for established connection.

### Run server
Run the server `$ node lightserver.js`


## States

1. Default "breathing"
2. User code
3. L.E.D. LAB



