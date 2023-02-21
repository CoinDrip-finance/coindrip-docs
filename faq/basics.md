---
description: Start streaming tokens in seconds...
---

# Basics

## How can I access the CoinDrip protocol?

The easiest way of accessing the CoinDrip protocol is by using our [CoinDrip dApp](https://app.coindrip.finance/).

We're working with various projects from the MultiversX ecosystem to make the CoinDrip protocol accessible through more and more dApps. _If you're a project building on MultiversX and want to integrate the CoinDrip protocol, check out the_ [technical-guides](../technical-guides/ "mention") _and_ [technical-reference](../technical-reference/ "mention") _or contact us at contact@coindrip.finance or on_ [_Twitter_](https://twitter.com/CoinDripHQ)_._

## What is token streaming?

You define the number of tokens distributed in a specific time period. During that period, tokens unlock each second, and the recipient can claim them whenever he wants.

## How does token streaming work?

Let's say you want to send 2000 USDC to John from 1 Jan to 1 Feb. You'll create the stream with all these details. John's funds will start to unlock from 1 Jan each second. For example, on 15 Jan, John can claim half of his funds.

## How can I create a stream?

You need a MultiversX wallet, some EGLD, and/or an ESDT like USDC. Then, using any interface like the CoinDrip dApp, fill in the recipient, amount of tokens, and the duration, click the button and sign the transaction. That's it!

## Where are the tokens held?&#x20;

The tokens are locked inside our smart contract from the deposit until the recipient claims them. You can always use any MultiversX explorer to check on that.

## How can recipients access their tokens?

As tokens are streamed using the CoinDrip Protocol, the recipients can withdraw them at any time using the CoinDrip dApp or any other interface.

## Can I cancel a stream?

Yes, the sender and recipient can cancel a stream at any time if the stream was not marked as non-cancellable by the sender during creation. All funds are returned to the sender if the stream is canceled before the start time. If you cancel the stream after the start time but before the end time, the amount streamed so far is transferred to the recipient, and the remaining tokens return to your wallet. If the stream is canceled after the end time, all funds are transferred to the recipient.

## Can I modify a stream?

No, streams are not editable. After it was created, you can only cancel it based on the above conditions.
