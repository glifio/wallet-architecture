# Keystore

Inspired by MetaMask's [`KeyringController`](https://github.com/MetaMask/KeyringController).

An [observable](https://github.com/MetaMask/obs-store) keystore that handles:

1. Wallet encryption (for browser storage)
2. Wallet decryption (for signing txs)
3. Creating and importing a new wallet (shimming WalletNew and WalletImport)
4. Checking if a wallet exists in the keystore (shimming WalletHas)
5. Listing wallets (shimming WalletList)
6. Signing (shimming WalletSignMessage and WalletSign)
7. Exporting wallet (shimming WalletExport)

Shimming in this context means that a jsonrpc call to the Filecoin node will not be made.

The keyring controller is the most involved subprovider because it requires its own sub modules in order to work in different environments:

- keyrings (mnemonic based, single account, ledger)
- encryption / decryption (will use [browser-passworder](https://github.com/danfinlay/browser-passworder))

## Questions:
- How to properly create keys compatible with Lotus
- Terminology:
  - Defining keycontroller, keyring, wallet, account, password, seed, mnemonic and understanding their direct relationships with one another
  - Is a "wallet" a single key pair? Or an entire mnemonic?
- Can we support mnemonics from day1 since we aren't creating keys on the Filecoin node?
- How do ledger api calls work? [MetaMask example](https://github.com/MetaMask/eth-ledger-bridge-keyring)
