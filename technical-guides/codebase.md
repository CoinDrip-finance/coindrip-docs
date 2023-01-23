# Codebase

## Smart Contract code

The CoinDrip protocol is open-source, and the code is available on GitHub.

{% embed url="https://github.com/CoinDrip-finance/coindrip-protocol-sc" %}

The code is also audited by Arda, and you can check the audit report here.

## ABI

Depending on how you plan to integrate the CoinDrip protocol into your dApp, you might need CoinDrip's ABI (application binary interface).&#x20;

```json
{
    "buildInfo": {
        "rustc": {
            "version": "1.67.0-nightly",
            "commitHash": "b28d30e1e3c2b90fd08b7dd79d8e63884d1e0339",
            "commitDate": "2022-12-06",
            "channel": "Nightly",
            "short": "rustc 1.67.0-nightly (b28d30e1e 2022-12-06)"
        },
        "contractCrate": {
            "name": "coindrip",
            "version": "0.1.2-alpha"
        },
        "framework": {
            "name": "elrond-wasm",
            "version": "0.38.0"
        }
    },
    "name": "CoinDrip",
    "constructor": {
        "inputs": [],
        "outputs": []
    },
    "endpoints": [
        {
            "name": "createStream",
            "mutability": "mutable",
            "payableInTokens": [
                "*"
            ],
            "inputs": [
                {
                    "name": "recipient",
                    "type": "Address"
                },
                {
                    "name": "start_time",
                    "type": "u64"
                },
                {
                    "name": "end_time",
                    "type": "u64"
                },
                {
                    "name": "_can_cancel",
                    "type": "optional<bool>",
                    "multi_arg": true
                }
            ],
            "outputs": []
        },
        {
            "docs": [
                "This view is used to return the active balance of the sender/recipient of a stream based on the stream id and the address"
            ],
            "name": "getBalanceOf",
            "mutability": "readonly",
            "inputs": [
                {
                    "name": "stream_id",
                    "type": "u64"
                },
                {
                    "name": "address",
                    "type": "Address"
                }
            ],
            "outputs": [
                {
                    "type": "BigUint"
                }
            ]
        },
        {
            "docs": [
                "This endpoint can be used by the recipient of the stream to claim the stream amount of tokens"
            ],
            "name": "claimFromStream",
            "mutability": "mutable",
            "inputs": [
                {
                    "name": "stream_id",
                    "type": "u64"
                }
            ],
            "outputs": []
        },
        {
            "docs": [
                "This endpoint can be used the by sender or recipient of a stream to cancel the stream.",
                "!!! The stream needs to be cancelable (a property that is set when the stream is created by the sender)"
            ],
            "name": "cancelStream",
            "mutability": "mutable",
            "inputs": [
                {
                    "name": "stream_id",
                    "type": "u64"
                }
            ],
            "outputs": []
        },
        {
            "name": "getStreamData",
            "mutability": "readonly",
            "inputs": [
                {
                    "name": "stream_id",
                    "type": "u64"
                }
            ],
            "outputs": [
                {
                    "type": "Stream"
                }
            ]
        },
        {
            "name": "getStreamListByAddress",
            "mutability": "readonly",
            "inputs": [
                {
                    "name": "address",
                    "type": "Address"
                }
            ],
            "outputs": [
                {
                    "type": "variadic<u64>",
                    "multi_result": true
                }
            ]
        },
        {
            "name": "getLastStreamId",
            "mutability": "readonly",
            "inputs": [],
            "outputs": [
                {
                    "type": "u64"
                }
            ]
        }
    ],
    "events": [
        {
            "identifier": "createStream",
            "inputs": [
                {
                    "name": "stream_id",
                    "type": "u64",
                    "indexed": true
                },
                {
                    "name": "sender",
                    "type": "Address",
                    "indexed": true
                },
                {
                    "name": "recipient",
                    "type": "Address",
                    "indexed": true
                },
                {
                    "name": "payment_token",
                    "type": "EgldOrEsdtTokenIdentifier",
                    "indexed": true
                },
                {
                    "name": "payment_nonce",
                    "type": "u64",
                    "indexed": true
                },
                {
                    "name": "deposit",
                    "type": "BigUint",
                    "indexed": true
                },
                {
                    "name": "start_time",
                    "type": "u64",
                    "indexed": true
                },
                {
                    "name": "end_time",
                    "type": "u64",
                    "indexed": true
                }
            ]
        },
        {
            "identifier": "claimFromStream",
            "inputs": [
                {
                    "name": "stream_id",
                    "type": "u64",
                    "indexed": true
                },
                {
                    "name": "amount",
                    "type": "BigUint",
                    "indexed": true
                },
                {
                    "name": "finalized",
                    "type": "bool",
                    "indexed": true
                }
            ]
        },
        {
            "identifier": "cancelStream",
            "inputs": [
                {
                    "name": "stream_id",
                    "type": "u64",
                    "indexed": true
                },
                {
                    "name": "canceled_by",
                    "type": "Address",
                    "indexed": true
                }
            ]
        }
    ],
    "hasCallback": false,
    "types": {
        "Stream": {
            "type": "struct",
            "fields": [
                {
                    "name": "sender",
                    "type": "Address"
                },
                {
                    "name": "recipient",
                    "type": "Address"
                },
                {
                    "name": "payment_token",
                    "type": "EgldOrEsdtTokenIdentifier"
                },
                {
                    "name": "payment_nonce",
                    "type": "u64"
                },
                {
                    "name": "deposit",
                    "type": "BigUint"
                },
                {
                    "name": "remaining_balance",
                    "type": "BigUint"
                },
                {
                    "name": "last_claim",
                    "type": "u64"
                },
                {
                    "name": "rate_per_second",
                    "type": "BigUint"
                },
                {
                    "name": "can_cancel",
                    "type": "bool"
                },
                {
                    "name": "start_time",
                    "type": "u64"
                },
                {
                    "name": "end_time",
                    "type": "u64"
                }
            ]
        }
    }
}
```

You can also obtain the ABI JSON if you build the contract using [mxpy](https://docs.multiversx.com/sdk-and-tools/sdk-py/installing-mxpy/).

```bash
git clone https://github.com/CoinDrip-finance/coindrip-protocol-sc
cd ./coindrip-protocol-sc
mxpy contract build
```
