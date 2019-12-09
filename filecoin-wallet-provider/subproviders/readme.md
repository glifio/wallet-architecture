# Subproviders

Subproviders are small packages that achieve a set of important and tightly related goals. The pattern aligns with Filecoin's [system decomposition](https://filecoin-project.github.io/specs/#intro__system) ethos.

Find more information about each subprovider in its directory.

Eventually subproviders could be easily swapped in and out. Developers could implement their own nonce tracking (using specialized private nodes), storage layer (for centralized key custodianship, alternative environments), keystore...etc. This would likely require subproviders to be named and adhere to standard interfaces.