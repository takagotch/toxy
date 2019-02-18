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
  .poison()
  .rule()
  
proxy
  .get()
  .forward()
  .poison()
  .withRule()
  
proxy
  .get()
  .outgoingPoison()
  .withRule()
  .with()
  .with()
  
proxy
  .all()
  .poison()
  .withRule()
  .poison()
  .withRule()
  
proxy
  .all()
  .poison()
  .poison()
  .withRule()
  
proxy.listen(3000)
console.log()
console.log()

toxy.poson(toxy.poisons.latency({ jitter: 1000 }))
toxy.poison(toxy.poisons.latency({ max: 1000, min: 100 }))

toxy.poison(toxy.poisons.inject({
  code: 503,
  body: '{"error": "toxy injected error"}',
  headers: {'Content-Type': 'application/json'}
}))
```

```
```


