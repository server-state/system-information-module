# system information module

[![Build Status](https://travis-ci.com/server-state/system-information-module.svg?branch=master)](https://travis-ci.com/server-state/system-information-module)
![GitHub](https://img.shields.io/github/license/server-state/system-information-module)
[![npm version](https://badge.fury.io/js/%40server-state%2Fsystem-information-module.svg)](https://badge.fury.io/js/%40server-state%2Fsystem-information-module)
[![Coverage Status](https://coveralls.io/repos/github/server-state/system-information-module/badge.svg?branch=master)](https://coveralls.io/github/server-state/system-information-module?branch=master)
![module type: official](https://img.shields.io/badge/module%20type-official-%23015ba0)

### Description

A module to view characteristics of your system. \
Its response is a object containing keys named after the request functions from the [systeminformation module](https://www.npmjs.com/package/systeminformation). The output can be defined before in [SMF](https://github.com/server-state/specs/blob/master/terminology/server-module-function.md) options with another object as the return value from the systeminformation function. \
Here is a example for a request to CPU and memory information:
```json
{
  "cpu": {
    "manufacturer": "Intel®",
    "brand": "Core™ i7-8250U",
    "vendor": "GenuineIntel",
    "family": "6",
    "model": "142",
    "stepping": "10",
    "revision": "",
    "voltage": "",
    "speed": "1.60",
    "speedmin": "0.40",
    "speedmax": "3.40",
    "cores": 8,
    "physicalCores": 4,
    "processors": 1,
    "socket": "",
    "cache": {
      "l1d": 131072,
      "l1i": 131072,
      "l2": 1,
      "l3": 8
    }
  },
  "mem": {
    "total": 16677117952,
    "free": 7204421632,
    "used": 9472696320,
    "active": 5442600960,
    "available": 11642912768,
    "buffcache": 4030095360,
    "swaptotal": 8589930496,
    "swapused": 9072640,
    "swapfree": 8580857856
  }
}
```

You can simply add this module with the [server-base](https://github.com/server-state/server-base) function and your specific options, for example:
```js
server.addModule('system-information', require('@server-state/system-information-module'), {
    cpu: [],
    mem: ['free']
});
```

to your current api server.
This results in the following output:
```json
{
  "cpu": {
    "manufacturer": "Intel®",
    "brand": "Core™ i7-8250U",
    "vendor": "GenuineIntel",
    "family": "6",
    "model": "142",
    "stepping": "10",
    "revision": "",
    "voltage": "",
    "speed": "1.60",
    "speedmin": "0.40",
    "speedmax": "3.40",
    "cores": 8,
    "physicalCores": 4,
    "processors": 1,
    "socket": "",
    "cache": {
      "l1d": 131072,
      "l1i": 131072,
      "l2": 1,
      "l3": 8
    }
  },
  "mem": {
    "free": 7204421632
  }
}
```

### Options

You can adjust the result of this module in the options as an object. \
These object contains key-value pairs. The key defines the function based the [systeminformation reference](https://www.npmjs.com/package/systeminformation#reference) to call and the value as type of array defines the filter. \
If the array or filter is empty, the result from the 'si'-function will be returned.
If the array contains strings that bases on the resulting key names in the object, the result object from the 'si'-function is filtered by the defined key names. \
For example, if you only want the number of cores from your CPU, an option object could look like:
```js
const options = {
    cpu: ['cores']
};
```
And the result defined by this option could look like: 
```json
{
  "cpu": {
    "cores": 4
  }
}
```

### About

This output generates a straight base to provide other applications useful information like server-state example [client-base](https://github.com/server-state/client-base).

This official module belongs to the organization [server-state](https://github.com/server-state).
