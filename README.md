# streamed-maxmind

Stream load maxmind data to incorporate geoip database updates without needed restarting node.
This wraps [runk/node-maxmind](https://github.com/runk/node-maxmind).

## Why?

To introducemaxmind data updates, paid or lite, without restarting node.

## Install

```
npm install streamed-maxmind
```

## Usage

```
var maxmind = require('streamed-maxmind');
maxmind.stream_init({
  'source_path': 'http://geolite.maxmind.com/download/geoip/database/GeoLiteCity.dat.gz',
  'storage_path': __dirname + '/GeoLiteCity.dat',
  'on_load': function(path) { // storage_path defined above
     maxmind.init(path); // init maxmind here
  },
  'check_frequency': 7*24*60*60*1000 // frequency to check for updates, default weekly
});
```

## Crypto

```
maxmind.stream_init({
  'cipher': { // if your going to encrypt the data, fill in this
  },
  'decipher': { // if are going to
  }
});
```
