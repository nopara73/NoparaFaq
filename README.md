# nopara73 - Frequently Asked Questions

## [ARCHIVED] "spent" coin status in Wasabi

The "spent" coin status is a symptom of corrupted wallet state. Currently this is the largest known bug in Wasabi Wallet. I estimate this affects about 1-5% of users. This issue was introduced to Wasabi with the [v1.1.4 release](https://github.com/zkSNACKs/WalletWasabi/releases/tag/v1.1.4) in April, 2019 by adding a wallet cache, that resulted in 12 times faster wallet load. It was [thought to be fixed](https://old.reddit.com/r/WasabiWallet/comments/c2hco8/announcement_spent_coin_and_lost_unconfirmed/) in June by adding an autocorrection mechanism, but some users are still reporting this issue, so it is not fixed.  

The easy fix could be removing the wallet cache altogether, but that would make the wallet load painfully slow, which makes it a no-go. Because of this I am working on a comprehensive refactoring of wallet internals for a fairly long time now and I slowly getting there to fix this issue without performance hit. Read more: [[WIP1 - Wasabi Improvement Proposal] Refactoring Internals](https://github.com/zkSNACKs/WalletWasabi/issues/2359).

### What can you do in the meantime?

Change the network in your wallet file from mainnet to testnet. This will result in rebuilding the wallet cache when you load your wallet on the mainnet.

#### Step By Step

Open your wallet in a text editor. (`File`/`Open`/`Wallets Folder`)

Change the value of the `Network` field to `TestNet`.

From this:

![](https://i.imgur.com/2uq9Nrr.png)

To this:

![](https://i.imgur.com/kHkKnC7.png)

Finally load your wallet. Wasabi will think that the wallet was loaded in the `TestNet` last time, so it will think it does not have a wallet cache built for the `Main` network, so it will clear the cache and build it again.

### Update (2019-11-14)

A new Bitcoin Core bug has been uncovered that may have resulted in the Wasabi coordinator missing to build some client side filters. At this point it's not clear if the bug is regtest specific or also happens on the mainnet. Our investigation and workaround is ongoing.
https://github.com/bitcoin/bitcoin/issues/17451, https://github.com/zkSNACKs/WalletWasabi/issues/1741

### Update (2019-11-22)

In PR https://github.com/zkSNACKs/WalletWasabi/pull/2599 we fixed the spent issue. (It doesn't yet run against the mainnet or the testnet yet, because that needs deployment of this PR.)

### Update (2019-12-05)

With v1.1.10 Release Candidate the spent issue seems to be completely gone: https://github.com/zkSNACKs/WalletWasabi/releases/tag/v1.1.10rc1
