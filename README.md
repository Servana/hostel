# Hostel 🏨 
Nomad Client for NodeJS. 

Includes built-in paramater, querystring and body checking.

## Setup

1) Install
```shell
npm install LKNSI/hostel
```

2) Construct
```javascript
const Hostel = require('LKNSI/hostel')
const fs = require('fs')
const main = async () => {
    var nomadAPI = new Hostel({
        connection:{
          hostname: "...", //Don't include the protocol (i.e. https://) here.
          port: "4646",
          sslEnabled: true, //Use HTTPS
          ssl:{
             privateKey: fs.readFileSync('/secrets/...'),
             cert: fs.readFileSync('/secrets/...'),
             ca: fs.readFileSync('/secrets/...'),
          },
          ignoreSecretTLSWarning: false, // Prevent Client from sending SecretID if HTTP is accidently selected. Set to true to ignore.
          ignoreTLSWarning: false // Ignore HTTPS Unauthorized warning by setting to true.
        }
    })
}
main()
```
3) Go!
```javascript
...(async function)

await nomadAPI.jobs.list().then(k => {console.log(k)})

...
```


## Features
* As close to 1:1 binding with offical REST API bindings.
* Currently supporting: 
  * Allocations
    * List
    * Read
    * Stop
    * Signal
    * Restart
  * Jobs
    * List
    * Read
    * Create
    * Parse
    * Update
    * Stop
    * Revert
    * Plan
  * Nodes
    * List
    * Read
    * Drain
    * Purge
    * Eligibility

## API Documentation

All commands follow a chainable hierarchy to their root node. Every function returns an async promise.

```javascript
  Hostel.prototype.<api>.<function>()
  ...
  nomadAPI.jobs.list()
  ...
  nomadAPI.allocations.read()
  ...
  nomadAPI.nodes.drain()

```
