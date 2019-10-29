# API Reference

Each NEO-CLI node provides an API interface for obtaining blockchain data from it, making it easy to develop blockchain applications. The interface is provided via [JSON-RPC](http://wiki.geekdream.com/Specification/json-rpc_2.0.html), and the underlying protocol uses HTTP/HTTPS for communication. To start a node that provides an RPC service, run the following command:

`dotnet neo-cli.dll /rpc`

## Configuring the config.json file

To access the RPC server via HTTPS, you need to modify the configuration file config.json before starting the node and set the domain name, certificate, and password:

```json
{
  "ApplicationConfiguration": {
    "Paths": {
      "Chain": "Chain"
    },
    "P2P": {
      "Port": 10333,
      "WsPort": 10334
    },
    "RPC": {
      "Port": 10331,
      "SslCert": "YourSslCertFile.xxx",
      "SslCertPassword": "YourPassword"
    }
  }
}                                      
```

To invoke some API methods that require you to open a wallet, you also need to make the following changes in `config.json` before starting the node:

- Change the UnlockWallet status `IsActive` to `true`.
- Specify the file name and password of the desired wallet.

```json
...
"UnlockWallet": {
      "Path": "YourWallet.json",
      "Password": "YourPassword",
      "StartConsensus": false,
      "IsActive": true
    }
...
```

Thereafter, when you open NEO-CLI, the client will automatically open the specified wallet and download the wallet index after it has been synchronized to the latest block height. 

## Listening ports 

After the JSON-RPC server starts, it will monitor the following ports, corresponding to the Main and Test nets:

For P2P and WebSocket information see [Node Introduction](../../../node/introduction.md).

|                | Main Net | Test Net |
| -------------- | -------- | -------- |
| JSON-RPC HTTPS | 10331    | 20331    |
| JSON-RPC HTTP  | 10332    | 20332    |

## Command List

| Command                                         | Reference                                   | Explanation                                                  | Comments                     |
| ----------------------------------------------- | ------------------------------------------- | ------------------------------------------------------------ | ---------------------------- |
| [claimgas](api/claimgas.md) | [address] | Claims GAS in the wallet. | Need to open the wallet |
| [dumpprivkey](api/dumpprivkey.md)               | \<address>                                  | Exports the private key of the specified address             | Need to open the wallet      |
| [getaccountstate](api/getaccountstate.md)       | \<address>                                  | Checks account asset information according to account address |                              |
| [getapplicationlog]() | \<txid> | Returns the contract log based on the specified txid. |  |
| [getassetstate](api/getassetstate.md)           | \<asset_id>                                 | Queries asset information according to the specified asset number |                              |
| [getbalance](api/getbalance.md)                 | \<asset_id>                                 | Returns the balance of the corresponding asset in the wallet according to the specified asset number. | Need to open the wallet      |
| [getbestblockhash](api/getbestblockhash.md)     |                                             | Gets the hash of the tallest block in the main chain         |                              |
| [getblock](api/getblock.md)                     | \<hash> [verbose=0]                         | Returns the corresponding block information according to the specified hash value |                              |
| [getblock](api/getblock2.md)                    | \<index> [verbose=0]                        | Returns the corresponding block information according to the specified index |                              |
| [getblockcount](api/getblockcount.md)           |                                             | Gets the number of blocks in the main chain                  |                              |
| [getblockhash](api/getblockhash.md)             | \<index>                                    | Returns the hash value of the corresponding block based on the specified index |                              |
| [getblockheader](api/getblockheader.md)         | \<hash> [verbose=0]                         | Returns the corresponding block header information according to the specified script hash |                              |
| [getblocksysfee](api/getblocksysfee.md)         | \<index>                                    | Returns the system fees before the block according to the specified index |                              |
| [getclaimable](api/getclaimable.md) | \<address> | Returns claimable GAS information of the specified address. | |
| [getconnectioncount](api/getconnectioncount.md) |                                             | Gets the current number of connections for the node          |                              |
| [getcontractstate](api/getcontractstate.md)     | \<script_hash>                              | Returns information about the contract based on the specified script hash |                              |
| [getmetricblocktimestamp](api/getmetricblocktimestamp.md) | \<blocks numbers>  \<endHeight> | Returns timestamps of the specified block and its previous n blocks. | |
| [getnep5balances](api/getnep5balances.md) | \<address> | Returns the balance of all NEP-5 assets in the specified address. | |
| [getnep5transfers](api/getnep5transfers.md) | \<address> | Returns all the NEP-5 transaction information occurred in the specified address. | |
| [getnewaddress](api/getnewaddress.md)           |                                             | Creates a new address                                        | Need to open the wallet      |
| [getrawmempool](api/getrawmempool.md)           |                                             | Gets a list of unconfirmed transactions in memory            |                              |
| [getrawtransaction](api/getrawtransaction.md)   | \<txid> [verbose=0]                         | Returns the corresponding transaction information based on the specified hash value |                              |
| [getunclaimed](api/getunclaimed.md) | \<address> | Returns unclaimed GAS amount of the specified address. | |
| [getunclaimedgas](api/getunclaimedgas.md) |  | Gets the amount of unclaimed GAS in the wallet. | Need to open the wallet |
| [getunspents](api/getunspents.md) | \<address> | Returns information of the unspent UTXO assets at the specified address. |  |
| [getstorage](api/getstorage.md)                 | \<script_hash>  \<key>                      | Returns the stored value based on the contract script hash and key |                              |
| [gettransactionheight](api/gettransactionheight.md)| \<txid>                                  | Returns the block index in which the transaction is found. ||
| [gettxout](api/gettxout.md)                     | \<txid> \<n>                                | Returns the corresponding transaction output (change) information based on the specified hash and index |                              |
| [getpeers](api/getpeers.md)                     |                                             | Gets a list of nodes that are currently connected/disconnected by this node |                              |
| [getversion](api/getversion.md)                 |                                             | Gets version information of this node                        |                              |
| [getvalidators](api/getvalidators.md)           |                                             | Gets NEO consensus nodes information                         |                              |
| [getwalletheight](api/getwalletheight.md)       |                                             | Gets the current wallet index height.                        |  Need to open the wallet |
| [importprivkey](api/importprivkey.md) | \<key> | Imports the private key to the wallet. | Need to open the wallet |
| [invokefunction](api/invokefunction.md)         | \<script_hash>  \<operation>  \<params>     | Invokes a smart contract at specified script hash, passing in an operation and its params |                              |
| [invokescript](api/invokescript.md)             | \<script>                                   | Runs a script through the virtual machine and returns the results |                              |
| [listaddress](api/listaddress.md)               |                                             | Lists all the addresses in the current wallet.               | Need to open the wallet      |
| [listplugins](api/listplugins.md)               |                                             | Returns a list of plugins loaded by the node.||
| [sendrawtransaction](api/sendrawtransaction.md) | \<hex>                                      | Broadcast a transaction over the network. |                              |
| [sendfrom](api/sendfrom.md)                     | \<asset_id> \<address> \<value> [fee=0]     | Transfers from the specified address to the destination address. | Need to open the wallet |
| [sendtoaddress](api/sendtoaddress.md)           | \<asset_id> \<address> \<value> [fee=0]     | Transfer to specified address                                | Need to open the wallet      |
| [sendmany](api/sendmany.md)                     | \<outputs_array> \[fee=0] \[change_address] | Bulk transfer order                                          | Need to open the wallet      |
| [submitblock](api/submitblock.md)               | \<hex>                                      | Relay a new block to the network                             | Needs to be a consensus node |
| [validateaddress](api/validateaddress.md)       | \<address>                                  | Verify that the address is a correct NEO address             |                              |

## GET request example

The format of a typical JSON-RPC GET request is as follows:

Here is an example of how to get the number of blocks in the main chain.

Request URL:

```
http://somewebsite.com:10332?jsonrpc=2.0&method=getblockcount&params=[]&id=1
```

After sending the request, you will get the following response:

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": 909129
}
```

## POST request example

The format of a typical JSON-RPC Post request is as follows:

Here is an example of how to get the number of blocks in the main chain.

Request URL:

```
http://somewebsite.com:10332
```

Request Body：

```json
{
  "jsonrpc": "2.0",
  "method": "getblockcount",
  "params":[],
  "id": 1
}
```

After sending the request, you will get the following response：

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": 909122
}
```

## Test tools

You can use the Chrome extension in Postman to facilitate the test (Installation of the Chrome extension requires Internet connection). A test screenshot is shown below:

![image](../../../assets/api_3.jpg)

## Other

[C# JSON-RPC Command List](https://github.com/chenzhitong/CSharp-JSON-RPC/blob/master/json_rpc/Program.cs)

