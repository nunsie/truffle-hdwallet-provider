# truffle-hdwallet-provider-xprv
Fork of https://github.com/trufflesuite/truffle-hdwallet-provider

HD Wallet-enabled Web3 provider. Use it to sign transactions for addresses derived from an extended private key.

## Install

```
$ npm install truffle-hdwallet-provider-xprv

```
or

```
$ yarn add truffle-hdwallet-provider-xprv

```

## Requirements
```
Node >= 7.6
```

## General Usage

You can use this provider wherever a Web3 provider is needed, not just in Truffle. For Truffle-specific usage, see next section.

```javascript
var HDWalletProvider = require("truffle-hdwallet-provider-xprv");
var xprv = "xprv9s21ZrQH143K4KqQx9Zrf1eN8EaPQVFxM2Ast8mdHn7GKiDWzNEyNdduJhWXToy8MpkGcKjxeFWd8oBSvsz4PCYamxR7TX49pSpp3bmHVAY";
var provider = new HDWalletProvider(xprv, "http://localhost:8545");

// Or, alternatively pass in a zero-based address index.
var provider = new HDWalletProvider(xprv, "http://localhost:8545", 5);
```

By default, the `HDWalletProvider` will use the address of the first address that's generated from the xprv. If you pass in a specific index, it'll use that address instead. Currently, the `HDWalletProvider` manages only one address at a time, but it can be easily upgraded to manage (i.e., "unlock") multiple addresses.

Parameters:

- `xprv`: `string`. Extended private key which addresses are created from.
- `provider_uri`: `string`. URI of Ethereum client to send all other non-transaction-related Web3 requests.
- `address_index`: `number`, optional. If specified, will tell the provider to manage the address at the index specified. Defaults to the first address (index `0`).

## Truffle Usage

You can easily use this within a Truffle configuration. For instance:

truffle.js
```javascript
var HDWalletProvider = require("truffle-hdwallet-provider-xprv");

var xprv = "xprv9s21ZrQH143K4KqQx9Zrf1eN8EaPQVFxM2Ast8mdHn7GKiDWzNEyNdduJhWXToy8MpkGcKjxeFWd8oBSvsz4PCYamxR7TX49pSpp3bmHVAY";

module.exports = {
  networks: {
    development: {
      host: "localhost",
      port: 8545,
      network_id: "*" // Match any network id
    },
    ropsten: {
      provider: new HDWalletProvider(xprv, "https://ropsten.infura.io/"),
      network_id: 3
    }
  }
};
```
