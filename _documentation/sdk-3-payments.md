---
# Page settings
title: Making Payments # Define a title of your page
description: Making and managing Payments using the Key Connect SDK # Define a description of your page
keywords: payments keyconnect java sdk blockchain eth xrp # Define keywords for search engines
order: 2 # Define order of this page in list of all documentation documents
comments: false # Set to "true" in order to enable comments on this page. Make sure you properly setup "disqus_forum_shortname" variable in "_config.yml"

# Hero section
hero:
    title: Making Payments
---

Payments are the simplest form of transactions on blockchain in Key Connect. Payments require a source wallet object as `BlockchainWallet` so you must have one initialised locally. You can read more about this in [managing wallets](/documentations/sdk-2-wallets). Additionally, you need a `destinationAddress` and an `amount`. Optionally you can specify a `network` if the payment that you are making is not on the `mainnet` but is on `testnet` for example.

# Quickstart guide

Here's the fastest way to make a payment:

```java
BlockchainWallet sourceWallet ...
SubmittedPayment payment = Payments.send(
    sourceWallet, 
    destinationAddress,
    amount,
    network
);
String transactionHash = payment.getTransaction().getHash();
CurrencyValue fee = payment.getTransaction().getFee();
```

Any applicable blockchain fees are calculated and applied automatically. You can examine it later from the payment object.

# Making a payment

The process of making a payment involves three steps:
1. Defining the payment
2. Signing the payment
3. Submitting the payment

Thankfully, the Key Connect SDK and the Key Connect Server work together to take care of #2 and #3. All you have to do is define #1. 

## Defining the Payment object

You can define a `Payment` as follows:

The `destinationAddress` and `amount` is the minimum amount of information you need to define a payment.

```java
Payment paymentWithAutoFee = Payments.create(destinationAddress, amount);
```

You can optionally specify a fee. If you don't specify a fee, it will automatically be calculated later before signing and submitting the transaction. If you'd like to specify the fee, you can define it when you are creating the `Payment` object:

```java
Payment paymentWithFee = Payments.create(destinationAddress, amount, fee);
```

## Signing a Payment transaction

A `Payment` needs to be signed before it is submitted. You need a `BlockchainWallet` object to sign a `Payment` object.

```java
BlockchainWallet wallet = ...
SignedPayment signedPayment = payment.sign(wallet);
```

## Submitting a signed Payment object

Now you can submit the signed payment.

```java
SubmittedPayment submittedPayment = signedPayment.submit();
```

The Key Connect SDK will submit the signed payment to the relevant blockchain. Any required parameters like blockchain `nonce`, or fees (unless specified in the payment) is automatically calculated.

The default blockchain network that the transaction is submitted to is `mainnet`. You can specify alternative network as follows:

```java
SubmittedPayment submittedPayment = signedPayment.submit("testnet");
String transactionHash = submittedPayment.getTransaction().getHash();
```

The `SubmittedPayment` object contains the details of the transaction, along with any relevant status information.

You can now use the `transactionHash` to check for the status of the transaction you just submitted. 
