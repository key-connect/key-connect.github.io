---
# Page settings
title: Importing the SDK # Define a title of your page
description: How to import the Key Connect SDK into your project # Define a description of your page
keywords: keyconnect java sdk blockchain eth xrp # Define keywords for search engines
order: 0 # Define order of this page in list of all documentation documents
comments: false # Set to "true" in order to enable comments on this page. Make sure you properly setup "disqus_forum_shortname" variable in "_config.yml"

# Hero section
hero:
    title: Importing SDK
---

You can use your favourite dependency management system to import the SDK.

#### Java via Maven

```xml
<dependency>
  <groupId>app.keyconnect</groupId>
  <artifactId>keyconnect-sdk</artifactId>
  <version>1.1.0</version>
</dependency>
```

*replace version with latest available at [maven central](https://mvnrepository.com/artifact/app.keyconnect/keyconnect-sdk).

# Wallets

Wallets are core to the Key Connect ecosystem. You can use the wallet methods to manage your wallet secrets as well as perform actions such as signing and sending transactions, manage payments and accounts etc. 

Key Connect SDK supports two types of wallets - standalone wallets and HD Wallets. You can read more about these in the sections below.

# Standalone Wallets

A standalone wallet is a wallet with a single unlinked private key. It can be regenerated from a mnemonic. Each standalone wallet is unique and has its own unique mnemonic.

## Generating a wallet for the first time

Every wallet in Key Connect has a `name` and an optional `passphrase`. The `name` is purely cosmetic and has no bearing on anything within the wallet. The `passphrase` is used when generating (or regenerating) the wallet seed. It is used in form of "salt", to introduce additional randomness in the wallet generation process. If it is specified during the wallet generation time, it must be specified at restore time.

You can generate a standalone wallet as follows:

```java
String passphrase = "mysecretpassphrase"; // optional, keep it safe if defined
String name = "mywallet"; // wallet name
BlockchainWallet ethWallet = new EthWallet(name, passphrase);
```

Once created, you can get the wallet address:

```java
String mnemonic = ethWallet.getMnemonic();
```

## Restoring a wallet from a mnemonic

When restoring a wallet, you need two things:

1. Mnemonic string
2. Passphrase - Optional, if it was used to generate the original wallet

```java
String passphrase = "mysecretpassphrase";
String name = "mywallet"; // wallet name
String mnemonic = "salty copper ..."
BlockchainWallet ethWallet = new EthWallet(name, passphrase, mnemonic);
```

# Hierarchical Deterministic Wallets

A Hierarchical Deterministic Wallet, also known as a HD Wallet is a single wallet that can house multiple wallets supporting multiple blockchains. Just like a standalone wallet, a HD wallet has a mnemonic that can be used to regenerate it, but unlike a standalone wallet, that single mnemonic can be used to generate all the child wallets within the HD wallet.

## Generating a wallet for the first time

A deterministic wallet does not have a `name` but does have an optional `passphrase`. This value is used to add additional randomness to the private key generation process. If a passphrase is specified at the generation time, it must be specified at restore time.

You can create a HD wallet as follows:

```java
String passphrase = "mysecretpassphrase"; // optional, keep it safe if defined
DeterministicWallet wallet = new DeterministicWallet(passphrase);
String mnemonic = wallet.getMnemonic();
```

You can create any number of child wallets under the HD wallets. To create a child wallet, you need the blockchain ID and a name for the child wallet.

```java
BlockchainWallet ethWallet = wallet.generate(ChainIdEnum.ETH, "eth 1");
BlockchainWallet xrpWallet = wallet.generate(ChainIdEnum.XRP, "xrp 1");
```

## Restoring a wallet from a mnemonic

The mnemonic can only restore the original HD wallet. Any child wallets must be regenerated once the original HD wallet is recreated. All child wallets that are created on a restored HD wallet will have the same keys and addresses as their original counterparts.

```java
DeterministicWallet recoveredWallet = new DeterministicWallet(passphrase, mnemonicCode);
BlockchainWallet ethWallet2 = wallet.generate(ChainIdEnum.ETH, "eth 1");
BlockchainWallet xrpWallet2 = wallet.generate(ChainIdEnum.XRP, "xrp 1");
```

Here `ethWallet2` and `ethWallet`, as well as `xrpWallet2` and `xrpWallet` will have same private keys.

# Payments
