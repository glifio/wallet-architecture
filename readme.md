# Filecoin web wallet

Welcome to the Filecoin web wallet. We're currently architecting the higher-level overview of the wallet. Feel free to file issues with suggestions, comments, questions...etc!

The wallet itself is a react app that depends on the `filecoin-wallet-provider` package:

```
+----------------------------------------------------------+
|                                                          |
|                     UI                                   |
|                                                          |
|                     +                                    |
|                     |                                    |
|                     |                                    |
|                     +                                    |
|                                                          |
|           filecoin-wallet-provider                       |
|                                                          |
|              +               +                           |
|              |               |           +               |
|              |               |           |  storage      |
|              +               +           |               |
|                                          |  nonce        |
|        filecoin-msg   subproviders +---+                 |
|                                          |  keystore     |
|                                          |               |
|                                          |  rpc          |
|                                          +               |
|                                                          |
+----------------------------------------------------------+
```

More information about each package can be found in its respective directory. Note - each directory in this repo would eventually be abstracted to its own package.
