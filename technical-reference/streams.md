# Streams

Streams are the core component of the CoinDrip protocol. All things that are built and that will be built will be around token streams for real-time payments.

A CoinDrip stream can be referred to by seven properties:

* Sender - ManagedAddress - A MultiversX address
* Recipient - ManagedAddress - A MultiversX address
* Deposit - BigUint - The number of streamed tokens
* Token - EgldOrEsdtTokenIdentifier - EGLD or ESDT Token
* Start time - u64 - The timestamp when the stream starts
* End time - u64 - The timestamp when the stream ends
* Is cancellable - bool - Can the stream be canceled after it was created?

The actual Stream struct stored on the blockchain looks like this:

```rust
struct Stream<M: ManagedTypeApi> {
    pub sender: ManagedAddress<M>,
    pub recipient: ManagedAddress<M>,
    pub payment_token: EgldOrEsdtTokenIdentifier<M>,
    pub payment_nonce: u64,
    pub deposit: BigUint<M>,
    pub claimed_amount: BigUint<M>,
    pub can_cancel: bool,
    pub start_time: u64,
    pub end_time: u64,
    pub balances_after_cancel: Option<BalancesAfterCancel<M>>
}

struct BalancesAfterCancel<M: ManagedTypeApi> {
    pub sender_balance: BigUint<M>,
    pub recipient_balance: BigUint<M>
}
```

You can find more information in the [codebase.md](../technical-guides/codebase.md "mention")section.
