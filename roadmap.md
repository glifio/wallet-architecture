# Development Roadmap

Each month we have a few "highlight" deliverables to focus on. Completing these deliverables within the month means we're on track.

Target start date: Monday December 16th, 2019
Target finish date: Friday February 14th, 2020

## December 16, 2019 - January 1, 2020

Highlights:
- [ ] One node.js function that takes a private key, and sends a signed message to our private node. This encompasses a lot of the "wallet" functionality like calculating nonces, and forming / sending signed transactions
- [ ] Documented jsonrcp request parameters via postman or curl (to make sure we know how to form all jsonrpc requests)
- [ ] First iteration of UX mockups
- [ ] Color palette, branding
- [ ] Extremely simple static site deployed

## January - Feb 1, 2020

Highlights:
- [ ] Finish first version of `filecoin-wallet-provider` (this includes finishing a first version of `filecoin-msg` package and all 3 subprovider packages) (Note - the separate modules will probably live in the same repo and share one package.json to save overhead time. Can abstract after launch in a maintenance period).
- [ ] ledger integration
- [ ] High fidelity UI mockups complete
- [ ] Security auditors chosen and booked for February

## Feb - Feb 14, 2020

Highlights:
- [ ] Security audit and adjustments
- [ ] Frontend application complete

## Feb 14 - Mar 1, 2020
- [ ] QA
- [ ] Mnemonic support

## Future
- [ ] Abstract modules into their own npm packages?
- [ ] Show individual transactions UI?
- [ ] Miner interactions via the web?
- [ ] Payment for mining in alternative currencies?
- [ ] Chrome extension to expose the `filecoin-wallet-provider`?
- [ ] Mobile support?
