# streamed-maxmind

Stream load maxmind data to enable maxmind geoip data updates, paid or lite, without restarting node.
This extends [runk/node-maxmind](https://github.com/runk/node-maxmind).

## Install

```
npm install streamed-maxmind
```

## Usage

```
var maxmind = require('streamed-maxmind');
maxmind.stream_init({
  'source_path': 'http://geolite.maxmind.com/download/geoip/database/GeoLiteCity.dat.gz',
  'target_path': __dirname + '/GeoLiteCity.dat',
  'on_load': function(path) { // target_path defined above
     maxmind.init(path); // init maxmind here
  },
  'load_frequency': 7*24*60*60*1000 // frequency to update, default weekly
});
```

## Crypto

Optional encryption/decryption of data for keeping paid data safe

```
maxmind.stream_init({
  'cipher': { // if your going to encrypt the data, fill in this
    'algorithm': 'aes192', // see: openssl list-cipher-algorithms for available
    'password': 'your_strong_password_here'
  },
  'decipher': { // if are going to
    'algorithm': 'aes192', // see: openssl list-cipher-algorithms for available
    'password': 'your_strong_password_here'
  }
});
```

## Stream Order

- Download
- Optionally cipher/decipher
- Gzip/Gunzip automatically appied if source or target paths end with .gz

## License: MIT
