# DigiByte.JS v0.14

## Principles

DigiByte is a powerful new peer-to-peer platform for the next generation of financial technology. The decentralized nature of the DigiByte network allows for highly resilient digibyte infrastructure, and the developer community needs reliable, open-source tools to implement digibyte apps and services. DigiByte.JS provides a reliable API for JavaScript apps that need to interface with DigiByte.

To get started, just `npm install digibyte` or `bower install digibyte`.

# Documentation Index

## Addresses and Key Management

* [Addresses](https://github.com/digibyte/digibyte-lib/blob/master/docs/address.md)
* [Using Different Networks](https://github.com/digibyte/digibyte-lib/blob/master/docs/networks.md)
* [Private Keys](https://github.com/digibyte/digibyte-lib/blob/master/docs/privatekey.md) and [Public Keys](https://github.com/digibyte/digibyte-lib/blob/master/docs/publickey.md)
* [Hierarchically-derived Private and Public Keys](https://github.com/digibyte/digibyte-lib/blob/master/docs/hierarchical.md)

## Payment Handling
* [Using Different Units](https://github.com/digibyte/digibyte-lib/blob/master/docs/unit.md)
* [Acknowledging and Requesting Payments: DigiByte URIs](https://github.com/digibyte/digibyte-lib/blob/master/docs/uri.md)
* [The Transaction Class](https://github.com/digibyte/digibyte-lib/blob/master/docs/transaction.md)

## DigiByte Internals
* [Scripts](https://github.com/digibyte/digibyte-lib/blob/master/docs/script.md)
* [Block](https://github.com/digibyte/digibyte-lib/blob/master/docs/block.md)

## Extra
* [Crypto](https://github.com/digibyte/digibyte-lib/blob/master/docs/crypto.md)
* [Encoding](https://github.com/digibyte/digibyte-lib/blob/master/docs/encoding.md)

## Module Development
* [Browser Builds](https://github.com/digibyte/digibyte-lib/blob/master/docs/browser.md)

# Examples

## Create and Save a Private Key

```javascript
var privateKey = new digibyte.PrivateKey();

var exported = privateKey.toWIF();
// e.g. L3T1s1TYP9oyhHpXgkyLoJFGniEgkv2Jhi138d7R2yJ9F4QdDU2m
var imported = digibyte.PrivateKey.fromWIF(exported);
var hexa = privateKey.toString();
// e.g. 'b9de6e778fe92aa7edb69395556f843f1dce0448350112e14906efc2a80fa61a'
```

## Create an Address

```javascript
var address = privateKey.toAddress();
```

## Create a Multisig Address

```javascript
// Build a 2-of-3 address from public keys
var p2shAddress = new digibyte.Address([publicKey1, publicKey2, publicKey3], 2);
```

## Request a Payment

```javascript
var paymentInfo = {
  address: 'DCXiSSQwi7gw9YXrMY4mxt2i4hQZEBb5Yv',
  amount: 120000 //satoshis
};
var uri = new digibyte.URI(paymentInfo).toString();
```

## Create a Transaction

```javascript
var transaction = new Transaction()
    .from(utxos)          // Feed information about what unspent outputs one can use
    .to(address, amount)  // Add an output with the given amount of satoshis
    .change(address)      // Sets up a change address where the rest of the funds will go
    .sign(privkeySet)     // Signs all the inputs it can
```

## Connect to the Network

```javascript
var peer = new Peer('5.9.85.34');

peer.on('inv', function(message) {
  // new inventory
});

peer.connect();
```
