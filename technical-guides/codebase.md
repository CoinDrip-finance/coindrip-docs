# Codebase

## Smart Contract code

The CoinDrip protocol is open-source, and the code is available on GitHub.

{% embed url="https://github.com/CoinDrip-finance/coindrip-protocol-sc" %}

The code is also audited by Arda, and you can check the audit report [here](https://arda.run/audits/coindrip).

## ABI

Depending on how you plan to integrate the CoinDrip protocol into your dApp, you might need CoinDrip's ABI (application binary interface).&#x20;

```json
{
    "buildInfo": {
        "rustc": {
            "version": "1.66.0-nightly",
            "commitHash": "b8c35ca26b191bb9a9ac669a4b3f4d3d52d97fb1",
            "commitDate": "2022-10-15",
            "channel": "Nightly",
            "short": "rustc 1.66.0-nightly (b8c35ca26 2022-10-15)"
        },
        "contractCrate": {
            "name": "coindrip",
            "version": "1.0.1-beta"
        },
        "framework": {
            "name": "multiversx-sc",
            "version": "0.39.2"
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
                "",
                "Calculates the recipient balance based on the amount stream so far and the already claimed amount",
                "|xxxx|*******|--|",
                "S            C  E",
                "S = start time",
                "xxxx = already claimed amount",
                "C = current time",
                "E = end time",
                "The zone marked with \"****...\" represents the recipient balance"
            ],
            "name": "recipientBalance",
            "mutability": "readonly",
            "inputs": [
                {
                    "name": "stream_id",
                    "type": "u64"
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
                "Calculates the sender balance based on the recipient balance and the claimed balance",
                "|----|-------|**|",
                "S   L.C      C  E",
                "S = start time",
                "L.C = last claimed amount",
                "C = current time",
                "E = end time",
                "The zone marked with \"**\" represents the sender balance"
            ],
            "name": "senderBalance",
            "mutability": "readonly",
            "inputs": [
                {
                    "name": "stream_id",
                    "type": "u64"
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
                },
                {
                    "name": "_with_claim",
                    "type": "optional<bool>",
                    "multi_arg": true
                }
            ],
            "outputs": []
        },
        {
            "docs": [
                "After a stream was cancelled, you can call this endpoint to claim the streamed tokens as a recipient or the remaining tokens as a sender",
                "This endpoint is especially helpful when the recipient/sender is a non-payable smart contract",
                "For convenience, this endpoint is automatically called by default from the cancel_stream endpoint (is not instructed otherwise by the \"_with_claim\" param)"
            ],
            "name": "claimFromStreamAfterCancel",
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
                },
                {
                    "name": "claimed_amount",
                    "type": "BigUint",
                    "indexed": true
                }
            ]
        }
    ],
    "hasCallback": false,
    "types": {
        "BalancesAfterCancel": {
            "type": "struct",
            "fields": [
                {
                    "name": "sender_balance",
                    "type": "BigUint"
                },
                {
                    "name": "recipient_balance",
                    "type": "BigUint"
                }
            ]
        },
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
                    "name": "claimed_amount",
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
                },
                {
                    "name": "balances_after_cancel",
                    "type": "Option<BalancesAfterCancel>"
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
