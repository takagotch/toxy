### toxy
---
https://github.com/h2non/toxy

```
npm install toxy
```

```js
var toxy = require('toxy')
var poisons = toxy.poisons
var rules = toxy.rules

var proxy = toxy()

proxy
  .forward('http://httpbin.org')
  
proxy
  .poison(poisons.latency({ jitter: 500 }))
  .rule(rules.probability(25))
  
proxy
  .get('/image/*')
  .forward('http://files.myserver.net')
  .poisons(poisons.bndwidth({ bps: 512 }))
  .withRule(rules.headers({'Authorization': /^Bearer (.*)$/i }))
  
proxy
  .get('/image/*')
  .outgoingPoison(poisons.bandwidth({ bps: 512 }))
  .withRule(rules.method('GET'))
  .with(rulws.timeThreshold({ duration: 1000, threshold: 1000 * 10 }))
  .with(rules.responseStatus({ range: [ 200, 400 ]}))
  
proxy
  .all('/download/*')
  .poison('http://files.myserver.net')
  .withRule(poisons.bandwidth({ bps: 1024 }))
  .withRule()

proxy
  .all('/api/*')
  .poison(poisons.rateLimit({ limit: 10, threshold: 1000 }))
  .withRule(rules.method(['POST', 'PUT', 'DELETE']))

proxy
  .all('/*')
  .poison(rules.method(['POST', 'PUT', 'DELETE']))
  .poison(poisons.rateLimt({ limit: 50, threshold: 1000 }))
  .withRule(rules.probability(50))
  
proxy.listen(3000)
console.log('Server listenging on port', 3000)
console.log('Test it:', 'http://localhost:3000/image/jpeg')

toxy.poson(toxy.poisons.latency({ jitter: 1000 }))
toxy.poison(toxy.poisons.latency({ max: 1000, min: 100 }))

toxy.poison(toxy.poisons.inject({
  code: 503,
  body: '{"error": "toxy injected error"}',
  headers: {'Content-Type': 'application/json'}
}))

toxy.poison(toxy.poisons.bandwidth({ bytes: 512 }))

const toxy = require('toxy')

const opts = { apiKey: 's3cr3t' }
var admin = toxy.admin(opts)

admin.listen(9000)
console.log('protected toxy admin server listening on port:', 9000)


const toxy = require('toxy')

var admin = toxy.admin({ cors: true })
admin.listen(9000)

var proxy = toxy()
proxy.listen(9000)

admin.manage(proxy)

proxy
  .forward('http://my.target.net')
  
proxy
  .get('/slow')
  .poison(toxy.poisons.bandwidth({ bps: 1024 }))
  
proxy
  .all('/*')
  .poison(toxy.poisons.bandwidth({ bps: 1024 * 5 }))
  
console.log('toxy proxy listening on port:', 3000)
console.log('toxy admin server listening on port:', 9000)


var toxy = require('toxy')
var proxy = toxy()

proxy
  .forward('http://server.net')
  .poison(toxy.poisons.bandwidth({ bps: 1024 }))
  .rule(toxy.rules.method('GET'))

var route = proxy
  .get('/foo')
  .toPath('/bar')
  .host('server.net')
  .forward('http://new.server.net')

route
  .poison(toxy.poisons.bandwidth({ bps: 512 }))
  .rule(toxy.rules.contentType('json'))

```

```
{
  "name": "latency",
  "phase": "outgoing",
  "options": { "jitter": 1000 }
}

{
  "name": "method",
  "options": "GET"
}

{
  "path": "/foo",
  "medhot": "GET",
  "forward": "http://my.server",
}

{
  "name": "method",
  "options": "GET"
}

{
  "name": "latency",
  "phase": "outgoing",
  "options": { "jitter": 1000 }
}

{
  "name": "method",
  "options": "GET"
}
```


