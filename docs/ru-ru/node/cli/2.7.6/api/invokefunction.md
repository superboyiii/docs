# invokefunction Method

Returns the result after calling a smart contract at scripthash with the given operation and parameters.

> [!Note]
>
> This method is to test your VM script as if they were ran on the blockchain at that point in time. This RPC call does not affect the blockchain in any way.

## Parameter Description

scripthash: Smart contract scripthash

operation: The operation name (string)

params: The parameters to be passed into the smart contract operation

## Example

Request body:

```json
{
  "jsonrpc": "2.0",
  "method": "invokefunction",
  "params": [
    "ecc6b20d3ccac1ee9ef109af5a7cdb85706b1df9",
    "balanceOf",
    [
      {
        "type": "Hash160",
        "value": "bfc469dd56932409677278f6b7422f3e1f34481d"
      }
    ]
  ],
  "id": 3
}
```

Response body:

```json
{
    "jsonrpc": "2.0",
    "id": 3,
    "result": {
        "script": "141d48341f3e2f42b7f678726709249356dd69c4bf51c10962616c616e63654f6667f91d6b7085db7c5aaf09f19eeec1ca3c0db2c6ec",
        "state": "HALT, BREAK",
        "gas_consumed": "0.338",
        "stack": [
            {
                "type": "ByteArray",
                "value": "00ab510d"
            }
        ]
    }
}
```

Request body:

```json
{
  "jsonrpc": "2.0",
  "method": "invokefunction",
  "params": [
    "ecc6b20d3ccac1ee9ef109af5a7cdb85706b1df9",
    "decimals"
  ],
  "id": 3
}
```

Response body:

```json
{
    "jsonrpc": "2.0",
    "id": 3,
    "result": {
        "script": "00c108646563696d616c7367f91d6b7085db7c5aaf09f19eeec1ca3c0db2c6ec",
        "state": "HALT, BREAK",
        "gas_consumed": "0.156",
        "stack": [
            {
                "type": "Integer",
                "value": "8"
            }
        ]
    }
}
```