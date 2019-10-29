# getbestblockhash Method

Returns the hash of the tallest block in the main chain.

## Example

Request body:

```json
{
   "jsonrpc": "2.0",
   "method": "getbestblockhash",
   "params":[],
   "id": 1
}
```

Response body:

```json
{
   "jsonrpc": "2.0",
   "id": 1,
   "result": "0x773dd2dae4a9c9275290f89b56e67d7363ea4826dfd4fc13cc01cf73a44b0d0e"
}
```

Response Description:

Result: The hash of the tallest block in the main chain.
