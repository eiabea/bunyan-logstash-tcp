# Logstash TCP stream for Bunyan

A tcp logger for [Logstash](http://logstash.net/docs/1.4.2/inputs/tcp)

## Configuration options

<table>
  <tr>
    <th>level</th>
    <td>string</td>
    <td><code>info</code></td>
  </tr>
  <tr>
    <th>server</th>
    <td>string</td>
    <td><code>os.hostname()</code></td>
  </tr>
  <tr>
    <th>host</th>
    <td>string</td>
    <td><code>"127.0.0.1"</code></td>
  </tr>
  <tr>
    <th>port</th>
    <td>number</td>
    <td><code>9999</code></td>
  </tr>
  <tr>
    <th>application</th>
    <td>string</td>
    <td><code>process.title</code></td>
  </tr>
  <tr>
    <th>pid</th>
    <td>string</td>
    <td><code>process.pid</code></td>
  </tr>
  <tr>
    <th>tags</th>
    <td>array|string[]</td>
    <td><code>["bunyan"]</code></td>
  </tr>
</table>

## Adding the bunyan-logstash stream to Bunyan

```
var log = bunyan.createLogger({
  streams: [
    {
      type: "raw",
      stream: require('bunyan-logstash-tcp').createStream({
        host: '127.0.0.1',
        port: 9908
      })
    }
  ]
});
```

## Example

```javascript
"use strict";

var bunyan = require('bunyan'),
    bunyantcp = require('bunyan-logstash-tcp');

var log = bunyan.createLogger({
    name: 'example',
    streams: [{
        level: 'debug',
        stream: process.stdout
    },{
        level: 'debug',
        type: "raw",
        stream: bunyantcp.createStream({
            host: '127.0.0.1',
            port: 9998
        })
    }],
    level: 'debug'
});

log.debug('test');
log.error('error test');
```

## Credits

This module is heavily based on [bunyan-logstash](https://github.com/sheknows/bunyan-logstash) and re-uses parts of [winston-logstash](https://github.com/jaakkos/winston-logstash/blob/master/lib/winston-logstash.js).

Thanks [sheknows](https://github.com/sheknows) and [jaakkos](https://github.com/jaakkos) for their amazing work

## License

MIT
