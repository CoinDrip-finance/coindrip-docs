# Endpoints

## Create Stream

The create stream endpoint requires the sender to transfer the streamed token to the CoinDrip smart contract. If the transaction is successful, the stream is registered on the blockchain. As soon as the start time is reached, the CoinDrip protocol will unlock tokens for the recipient.

```rust
#[payable("*")]
#[endpoint(createStream)]
fn create_stream(
    &self,
    recipient: ManagedAddress,
    start_time: u64,
    end_time: u64,
    can_cancel: OptionalValue<bool>
) 
```

{% hint style="info" %}
You must also send the token you want to stream in the create stream transaction.
{% endhint %}

{% hint style="danger" %}
The start\_time must be bigger than `self.blockchain().get_block_timestamp(),` or the transaction will fail.
{% endhint %}

Example of building a create stream transaction payload using [mx js sdk](https://github.com/multiversx/mx-sdk-js-core):

```typescript
TransactionPayload.contractCall()
      .setFunction(new ContractFunction("ESDTTransfer"))
      .addArg(new BytesValue(Buffer.from('USDC-a2sd58', "utf-8"))) // streamed token identifier
      .addArg(new BigUIntValue(TokenPayment.egldFromAmount('100').valueOf())) // streamed token amount
      .addArg(new BytesValue(Buffer.from("createStream", "utf-8")))
      .addArg(new AddressValue(new Address('erd1aaaa.....'))) // recipient address
      .addArg(new U64Value(1674158572)) // start time
      .addArg(new U64Value(1674159572)) // end time
      .build();
```

## Claim from stream

This endpoint transfers the amount of already streamed tokens from the CoinDrip smart contract to the recipient's wallet.&#x20;

```rust
#[endpoint(claimFromStream)]
fn claim_from_stream(
    &self,
    stream_id: u64
)
```

{% hint style="info" %}
The recipient of the stream can only call this endpoint after the present time went over the start time of the stream.
{% endhint %}

Example of building a claim from stream transaction payload using [mx js sdk](https://github.com/multiversx/mx-sdk-js-core):

```typescript
TransactionPayload.contractCall()
      .setFunction(new ContractFunction("claimFromStream"))
      .addArg(new U64Value(12)) // stream id
      .build();
```

## Cancel stream

This endpoint can be called by the sender or the recipient and will cancel a stream at any time **if the stream was not marked as non-cancellable by the sender during creation**. If the stream is canceled before the start time, all funds are returned to the sender. If you cancel the stream after the start time, but before the end time, the amount that was streamed so far is transferred to the recipient, and the remaining tokens come back to your wallet. If the stream is canceled after the end time, all funds are transferred to the recipient.

```rust
#[endpoint(cancelStream)]
fn cancel_stream(
    &self,
    stream_id: u64,
    with_claim: OptionalValue<bool>
)
```

Example of building a cancel stream transaction payload using [mx js sdk](https://github.com/multiversx/mx-sdk-js-core):

```typescript
TransactionPayload.contractCall()
      .setFunction(new ContractFunction("cancelStream"))
      .addArg(new U64Value(9)) // stream id
      .build();
```
