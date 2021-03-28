---
# Page settings
title: Initialising a local wallet # Define a title of your page
description: Setting up a local wallet using Key Connect CLI # Define a description of your page
keywords: keyconnect cli wallet blockchain eth xrp # Define keywords for search engines
order: 5 # Define order of this page in list of all documentation documents
comments: false # Set to "true" in order to enable comments on this page. Make sure you properly setup "disqus_forum_shortname" variable in "_config.yml"

# Hero section
hero:
    title: Setting up a local wallet
---

#### Making payments

When making payments, the source wallet must be a local wallet, referenced by its name (`--from "my xrp wallet"`). If the destination wallet is a local wallet, it can be referenced by its name (`--to "my another xrp wallet"`). If not, then you can use the wallet address directly (`--to-address rLP6...u4ih`).

```shell
$ kc pay -c xrp --from "my xrp wallet" --to "my another xrp wallet" --amount 200 -n testnet
Wallet password:

Loading wallet...
[main] INFO org.bitcoinj.crypto.MnemonicCode - PBKDF2 took 158.3 ms
class BlockchainAccountTransactionItem {
    status: success
    type: Payment
    sourceAccount: rU8jSipHoU4SXkHkAFueRW3CVcdfiz2cZJ
    destinationAccount: rLP6NJYJ648wWzSDMsFiXKswpBFzf5u4ih
    destinationTag: null
    fee: class CurrencyValue {
        amount: 10
        issuer: null
        currency: drops
    }
    amount: class CurrencyValue {
        amount: 200000000
        issuer: null
        currency: drops
    }
    value: null
    hash: DFFB931CCE957D15B10407429B4ED20DC886709539DD196DF92F71B8895C9E01
}

Transaction submitted. Use hash DFFB931CCE957D15B10407429B4ED20DC886709539DD196DF92F71B8895C9E01 to check for status.
```

Next you can use the `tx` command to view the details of the transaction.

```shell
$ kc tx -c xrp --transaction DFFB931CCE957D15B10407429B4ED20DC886709539DD196DF92F71B8895C9E01 -n testnet
class BlockchainAccountTransaction {
    chainId: xrp
    network: testnet
    server: s.altnet.rippletest.net
    transaction: class BlockchainAccountTransactionItem {
        status: success
        type: Payment
        sourceAccount: rU8jSipHoU4SXkHkAFueRW3CVcdfiz2cZJ
        destinationAccount: rLP6NJYJ648wWzSDMsFiXKswpBFzf5u4ih
        destinationTag: null
        fee: class CurrencyValue {
            amount: 10
            issuer: null
            currency: drops
        }
        amount: class CurrencyValue {
            amount: 200
            issuer: null
            currency: xrp
        }
        value: null
        hash: DFFB931CCE957D15B10407429B4ED20DC886709539DD196DF92F71B8895C9E01
    }
}
```

Now check balance.

```shell
$ kc wallets -c xrp --balances -n testnet
Wallet password:

Loading wallet...
[main] INFO org.bitcoinj.crypto.MnemonicCode - PBKDF2 took 160.9 ms
xrp ===
0 my xrp wallet rU8jSipHoU4SXkHkAFueRW3CVcdfiz2cZJ XRP 799.999990000000000000
1 my another xrp wallet rLP6NJYJ648wWzSDMsFiXKswpBFzf5u4ih XRP 200.000000000000000000
```
