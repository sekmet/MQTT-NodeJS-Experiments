# MQTT and Node.js by mcollina

### Messaging in the Internet of Things

### [@matteocollina](http://twitter.com/matteocollina)

## MQTT

*   publish/subscribe protocol
*   multiple quality of service level..
*   ..with at-least-once and exactly-once semantics
*   low overhead (2 bytes at minimum)
*   offline messaging
*   retained messages, like a key/value store

## MQTT

*   Small core, vibrant community
*   Extreme modularity
*   Reimplement everything in Javascript

## Why Node.js matters?

*   high performance (2x at Paypal)
*   faster application development (2x at PayPal)
*   batteries not included
*   go check out  [http://www.nearform.com/nodecrunch/node-js-becoming-go-technology-enterprise](http://www.nearform.com/nodecrunch/node-js-becoming-go-technology-enterprise)

*   Almost 70.000 modules
*   3.685.510 module downloaded per day
*   Exponential growth
*   Permissive licenses
*   How to spot a good module?


## MQTT.js

*   20k packets/second parser
*   Stream based
*   High-Level Client API
*   Low-Level Server
*   Build with  by [@adamvr](http://github.com/adamvr) and [@mcollina](http://github.com/mcollina)

## Instant Gratification

<pre>var client = mqtt.createClient();

client.subscribe("mqtt/demo");

client.on("message", function(topic, payload) {
  alert([topic, payload].join(": "));
  client.end();
});

client.publish("mqtt/demo", "hello world!");
</pre>

## Pattern Matching

<pre>var client = mqtt.createClient();

client.subscribe("mqtt/+");

client.on("message", function(topic, payload) {
  alert([topic, payload].join(": "));
  client.end();
});

client.publish("mqtt/demo", "hello world!");
</pre>

## Mosca

### MQTT broker in Node.js

*   [http://npm.im/mosca](http://npm.im/mosca)
*   Standalone usage, through `$ mosca`
*   Embeddable in your app
*   Authentication APIs
*   Supports AMQP, Mongo, Redis, and MQTT as pub/sub backends
*   Needs a DB, such as LevelDB, Mongo, or Redis
*   Support websockets
*   Fast, 10k+ messages routed per second
*   Scalable, 10k+ concurrent connections

## How can it work on a Browser?

*   Works on top of WebSocket
*   Node.js excels at that :)
*   MQTT over Websocket is 'standard'
*   uses test broker at test.mosca.io
*   Thanks to [@substack](http://github.com/substack) for Browserify

## Benchmark

## Offline Mode

### First, subscribe with QoS 1 and disconnect

<pre>var client = mqtt.createClient({
  clientId: "moscaslides",
  clean: false
});

client.subscribe("mqtt/offline", { qos: 1 },
  function() {

  alert("subscribe done!");
  // called when the subscribe is successful
  client.end();
});
</pre>

## Offline Mode

### Then, someone else publish an important message

<pre>var client = mqtt.createClient();

client.publish("mqtt/offline", "hello world!", {qos:1},
  function() {

  alert("publish done!");
  client.end();
});
</pre>

## Offline Mode

### Reconnect to receive the missed messages

<pre>var client = mqtt.createClient({
  clientId: "moscaslides",
  clean: false
});

client.on("message", function(topic, payload) {
  alert([topic, payload.toString()].join(": "));

  setTimeout(client.end.bind(client), 1000);
});
</pre>

## Does Offline Mode Scale?

## Do you need a REST API?

*   Check out [Ponte](http://eclipse.org/ponte) at [http://eclipse.org/ponte](http://eclipse.org/ponte)
*   $ npm install ponte -g
*   [](http://eclipse.org/ponte)

## Ponte API

*   http://<your ponte>/resources/<your thing>
*   coap://<your ponte>/r/<your thing>
*   mqtt(s)://<your ponte>/<your thing>

### [http://github.com/mcollina](http://github.com/mcollina)

# Thanks!
