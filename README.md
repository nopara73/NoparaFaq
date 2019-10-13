# nopara73 - Frequently Asked Questions

## "spent" coin status in Wasabi

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
