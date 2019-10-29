# getaccountstate Method

Queries global assets (NEO, GAS, and etc.) of the account, according to the account address.

## Parameter Description

Account Address: A 34-characters length string beginning with A, such as AJBENSwajTzQtwyJFkiJSv7MAaaMc7DsRz.

## Example

Request body:

```json
{
  "jsonrpc": "2.0",
  "method": "getaccountstate",
  "params": ["AJBENSwajTzQtwyJFkiJSv7MAaaMc7DsRz"],
  "id": 1
}
```

Response body:

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "version": 0,
        "script_hash": "0x1179716da2e9523d153a35fb3ad10c561b1e5b1a",
        "frozen": false,
        "votes": [],
        "balances": [
            {
                "asset": "0xc56f33fc6ecfcd0c225c4ab356fee59390af8560be0e930faebe74a6daff7c9b",
                "value": "94"
            }
        ]
    }
}
```

Response Description:

- Script_hash: Contract scipt hash; All accounts in NEO are contract accounts

- Frozen: Determine if the account is frozen 

- Votes: Query the amount of NEO on that address used to vote

- Balance: Balance of assets at the address

- Asset: Asset ID

- Value: Amount of Assets


