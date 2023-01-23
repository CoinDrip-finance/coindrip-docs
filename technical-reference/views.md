# Views

## getBalanceOf

This view is used to return the active balance of the sender/recipient of a stream based on the stream id and the address. If you call it with any other address than the sender/recipient it will return zero.

```rust
#[view(getBalanceOf)]
fn balance_of(&self, stream_id: u64, address: ManagedAddress) -> BigUint
```

You can use the MultiversX public APIs to query the CoinDrip smart contract. Let's use axios for an example of such a call:

```typescript
await axios.post('https://devnet-gateway.multiversx.com/vm-values/int',
    {
        funcName: 'getBalanceOf',
        scAddress: 'erd1qqqqqqqqqqqqqpgqfgned8q9zqwaeya4sc0stf7elpj6ylsdlpzqwhk5ye',
        args: ["STREAM ID HEX", "ADDRESS HEX"],
        value: "0"
    }
);
```

## getStreamData

This view will return a Stream struct based on the stream id.

```rust
#[view(getStreamData)]
fn get_stream(&self, stream_id: u64) -> Stream<Self::Api>
```

Because this will return a struct, we'll present you another way to query the smart contract and decode the struct using [mx js sdk](https://github.com/multiversx/mx-sdk-js-core):

```typescript
const getStreamDetails = async (streamId: number): Promise<any> => {
    let abi = new SmartContractAbi(AbiRegistry.create(ScAbi), ["CoinDrip"]);
    let contract = new SmartContract({ address: new Address(contractAddress), abi: abi });
  
    let getSteramDetails = <Interaction>contract.methods.getStreamData([streamId]);
  
    const parser = new ResultsParser();
  
    let ViewQueryResponse = await new ApiNetworkProvider(network.apiAddress).queryContract(
      getSteramDetails.buildQuery()
    );
    let ViewEndpointDefinition = contract.getEndpoint("getStreamData");
  
    let ViewValues = parser?.parseQueryResponse(ViewQueryResponse, ViewEndpointDefinition)?.firstValue?.valueOf();
  
    return ViewValues;
};
```
