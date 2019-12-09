The storage interface provides basic setting and getting functionality into a storage layer. This package is used for caching block and nonce data and storing encrypted information.

For the filecoin-web-wallet, we expect `indexedDB` to be the best client side storage. It's only accessible via the website that created the indexedDB store, so other tabs cannot get access to the user's encrypted vault.

If someone wanted to implement their own storage subprovider (for a chrome extension, mobile app...etc), they could expose `get` and `set` functions (although this will probably change once we start building):

```ts
function set(key: string, value: any): void

function get(key: string): any
```