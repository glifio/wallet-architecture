# Filecoin message generator

Inspired by [`ethereumjs-tx`](https://github.com/ethereumjs/ethereumjs-tx)

This package is useful for handling serialization, deserialization, and signing of Filecoin messages. We don't know much about how this works yet, but it seems to be useful to abstract into its own package that can be used in different contexts. Might be unecessary for a V1, and could just be ripped out and modularized later on.
