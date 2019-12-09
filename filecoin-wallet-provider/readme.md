# filecoin-wallet-provider

Inspired by MetaMask's [`web3-provider-engine`](https://github.com/MetaMask/web3-provider-engine)

## Methods

For a first version, the `filecoin-wallet-provider` package is meant to handle the following methods:

```
WalletNew
WalletHas
WalletList
WalletBalance
WalletSign
WalletSignMessage
WalletDefaultAddress
WalletSetDefault
WalletExport
WalletImport
StateWaitMsg
MpoolPending
MpoolPush
MpoolPushMessage
MpoolGetNonce
ChainHead
ChainGetBlock
```

## Usage

```js
const FilecoinWallet = require('filecoin-wallet-provider')

// Note, API method & constructor signatures have not been thoroughly thought out yet. They will change.

const wallet = new FilecoinWallet({apiAddr: '/ip4/127.0.0.1/tcp/3453/http'})

// Call any of the supported methods directly off the wallet object:
const newWallet = await wallet.methods('WalletNew')

const nonce = await wallet.methods('MpoolGetNonce')

const message =  {
  To: to,
  From: from,
  Nonce: nonce,
  Value: AttoFil, // ?
  GasPrice: 1000,
  GasLimit: 0,
  Method: 0, // send
  Params: [null],
}

const signedMessage = await wallet.methods('WalletSignMessage', [message])
const sentMessage = await wallet.methods('MpoolPushMessage', [signedMessage])

// Ideally all methods are async/await and "thenable".
wallet.methods('WalletNew')
      .then(newWallet => {
        // handle it
      })
      .catch(err => {
        // handle errors
      })

// With time, we could even build easier-to-use wallet methods that take care of multiple steps.
const sentMessage = await wallet.sendSignedMsg({ To: '0x...', ... })

// We could also add security with something similiar to EIP1102: https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1102.md.
const enabled = await wallet.enable()

// Alternatively, methods could adhere to a more "javascript" styled interface (rather than the jsonrpc style used above):
wallet.new()
wallet.messagePool.push()

// We will weigh the pros and cons of the different styles with respect to developer UX, backwards compatibility, maintainability...etc.
```

## Under the hood

The `filecoin-wallet-provider` provides shims for the [Filecoin api methods](https://github.com/filecoin-project/lotus/blob/master/api/api_full.go) it supports. Not all supported methods need to be (or should be) handled by the Filecoin client. For example, the `WalletNew` method shouldn't actually send a jsonrpc request to a remote node with the user's private key - instead, the method would handle new wallet creation through the keystore subprovider, and store the created key in the storage subprovider.

This MetaMask inspired subprrovider structure provides maximum flexibility for developers to configure their Filecoin wallets for different environments and purposes. It also makes security auditing easier and more effective because operations that require audit are isolated in their own places within the code.

## Composable subproviders

The `filecoin-wallet-provider` could be composable with optional subproviders. Thinking it might be good to wait for composable subproviders until a V2 or V3 wallet. We will have a much better understanding of the best way to structure subproviders after the V1 wallet is finished.

```js
// package names made up
const FilecoinWallet = require('filecoin-wallet-provider')
const NonceTracker = require('filecoin-nonce-tracker')
const Keystore = require('filecoin-keystore')
const Storage = require('filecoin-indexedDB-storage')

// Note, API method and constructor signatures have not been thoroughly thought out yet. They will change.

const wallet = new FilecoinWallet({apiAddr: '/ip4/127.0.0.1/tcp/3453/http'})

// More questions in './subproviders/readme.md'.
wallet.addSubprovider(new NonceTracker())
wallet.addSubprovider(new Keystore())
wallet.addSubprovider(new Storage())
```

## Future integrations

In the future, the `filecoin-wallet-provider` could be used in conjuction with a more complete jsonrpc Filecoin wrapper like [`js-filecoin-api-client`](https://github.com/filecoin-shipyard/js-filecoin-api-client). Passing the Filecoin wallet shims certain methods. The shimmed methods get handled without calling the jsonrpc. It would look something like this:<br />

```js
const Filecoin = require('filecoin-api-client')
const FilecoinWallet = require('filecoin-wallet-provider')

const fc = Filecoin(new FilecoinWallet({
  apiAddr: '/ip4/127.0.0.1/tcp/3453/http' // (optional, default)
}))
```

This pattern would be familiar to Ethereum app developers who have used the [`new Web3(window.web3.currentProvider)` pattern](https://web3js.readthedocs.io/en/v1.2.4/getting-started.html#adding-web3-js). Note, MetaMask uses the `ethereum` window object, and no longer requires developers to require Web3.js.

The aim of this package is to make it easy for developers to create their own Filecoin wallets.
