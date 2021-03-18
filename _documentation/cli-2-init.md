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

#### Setting up a local wallet

You can use the CLI to manage wallets locally. To set this up, run the `init` command:

```shell
$ kc init
You can choose a wallet seed passphrase now. A wallet seed passphrase is a piece of string used to generate the mnemonic. You will need to remember this passphrase when recovering the wallet, along with the mnemonic. It adds extra randomness that is used to generate the wallet keys.
Choose a wallet seed passphrase:
Confirm wallet seed passphrase:

Choose wallet password:
Confirm wallet password:
Creating wallet...
[main] INFO org.bitcoinj.crypto.MnemonicCode - PBKDF2 took 99.99 ms
Wallet created. 
```

Ensure you choose a strong passphrase and a strong wallet password. Your wallet will not be accessible without the wallet password.

#### Local Wallet Backup

It is strongly recommended that you backup the local wallet file itself. The local wallet file can be found in the Key Connect CLI home directory `~/.kc`:

```shell
~/.kc/.wallet
```

The file is encrypted using your wallet password, so it is safe to back it up to cloud storage solutions like Dropbox/OneDrive/Google Drive etc.

#### Create a new local wallet

The following blockchains are supported at the moment. Thus, only those types of wallets can be created. 
1. Ethereum (eth)
2. XRP (xrp)

The `new` command allows you to create a new wallet. You need to specify the blockchain of the wallet (example: `-c eth`) and a user-friendly name (example: `--name "my wallet").

```shell
$ kc new -c eth --name "my eth wallet"
Wallet password:

Loading wallet...
[main] INFO org.bitcoinj.crypto.MnemonicCode - PBKDF2 took 186.8 ms
Generated wallet: 0x3b4c95397684ab7ebadce6e268189e8447ad5800
```

Same for XRP:

```shell
$ kc new -c xrp --name "my xrp wallet"
Wallet password:

Loading wallet...
[main] INFO org.bitcoinj.crypto.MnemonicCode - PBKDF2 took 164.8 ms
Generated wallet: rU8jSipHoU4SXkHkAFueRW3CVcdfiz2cZJ
```

#### Listing local wallets

You can use the `wallets` command to list the local wallets.

```shell
$ kc wallets
Wallet password:

Loading wallet...
[main] INFO org.bitcoinj.crypto.MnemonicCode - PBKDF2 took 111.2 ms
xrp ===
0 my xrp wallet rU8jSipHoU4SXkHkAFueRW3CVcdfiz2cZJ
eth ===
0 my eth wallet 0x3b4c95397684ab7ebadce6e268189e8447ad5800
```

You can use the `--balances` option to see the wallet balances.

```shell
$ kc wallets --balances
Wallet password:

Loading wallet...
[main] INFO org.bitcoinj.crypto.MnemonicCode - PBKDF2 took 122.5 ms
xrp ===
0 my xrp wallet rU8jSipHoU4SXkHkAFueRW3CVcdfiz2cZJ unavailable
eth ===
0 my eth wallet 0x3b4c95397684ab7ebadce6e268189e8447ad5800 ETH 0E-18
```

