# Transaction Types
There are several different types of transactions on NEO, each with a different purpose and different properties. Some previously used transaction types are now deprecated or removed from the network, so these should not be used when creating new transactions on the MainNet.

| Byte   | Name                    | Status       | Transaction fee | Description                                             |
|--------|-------------------------|--------------|-----------------|---------------------------------------------------------|
| `0x00` | `MinerTransaction`      | *Active*     | `0`             | First transaction in a block to distribute network fees |
| `0x01` | `IssueTransaction`      | *Deprecated* | `500`           | Issue assets from a registered native asset             |
| `0x02` | `ClaimTransaction`      | *Active*     | `0`             | Claim GAS from unclaimed transaction outputs            |
| `0x20` | `EnrollmentTransaction` | *Deprecated* | `1000`          | Enroll a new consensus node candidate                   |
| `0x24` | `VotingTransaction`     | *Removed*    | `0`             | Vote for consensus node candidates                      |
| `0x40` | `RegisterTransaction`   | *Deprecated* | `10000`         | Register a new native asset on the blockchain           |
| `0x80` | `ContractTransaction`   | *Active*     | `0`             | Common transaction to transfer assets                   |
| `0x90` | `StateTransaction`      | *Active*     | `0`             | Voting and registering for a consensus node candidate   |
| `0xb0` | `AgencyTransaction`     | *Removed*    | `0`             | Place orders on the blockchain                          |
| `0xd0` | `PublishTransaction`    | *Deprecated* | `500`           | Publish a smart contract to the blockchain              |
| `0xd1` | `InvocationTransaction` | *Active*     | `0`             | Invoke a smart contract on the blockchain               |

### MinerTransaction
The first transaction in a block. It is generated by the active consensus node for a given consensus round, and will collect and distribute all the network fees in that block.

#### Additional attributes for a MinerTransaction:

| Field   | Type   | Description                                       |
|---------|--------|---------------------------------------------------|
| `nonce` | uint32 | Random number to make the transaction hash unique |

Example:

```javascript
{
   "txid":"0xdbf3ad80e483c56b996fcc1264384f87a86a889d3cc2c79888200d347923f6c6",
   "size":70,
   "type":"MinerTransaction",
   "version":0,
   "attributes":[

   ],
   "vout":[
      {
         "n":0,
         "asset":"0x602c79718b16e442de58778e148d0b1084e3b2dffd5de6b7b16cee7969282de7",
         "value":"0.001",
         "address":"AWHX6wX5mEJ4Vwg7uBcqESeq3NggtNFhzD"
      }
   ],
   "vin":[

   ],
   "sys_fee":"0",
   "net_fee":"0",
   "scripts":[

   ],
   "nonce":960164232
}
```

### ClaimTransaction
Claim GAS from unclaimed transaction outputs

#### Additional attributes for a ClaimTransaction:

| Field    | Type  | Description                                          |
|----------|-------|------------------------------------------------------|
| `claims` | array | References to spent outputs in previous transactions |

#### Claims
A `claim` is a reference to a spent [`output`](2-Structure_of_NEO_transactions.md#outputs) (only for the NEO asset) in a previous transaction. Each transaction can have up to 65536 claim references. Each claim reference in the array of claims has a set of required attributes.

| Field  | Type    | Description                                    |
|--------|---------|------------------------------------------------|
| `txid` | uint256 | The transaction hash of the referenced output  |
| `vout` | uint16  | The index of the outputs array to use as input |

Once an output from a previous transaction is used as a claim reference, it will be considered `claimed` and cannot be used anymore in any future claims. The amount of GAS that can be claimed will be calculated by the total GAS distribution in all blocks while the referenced NEO asset was in the respective contract address.

Example:

```javascript
{
   "txid":"0x30f90c7df4c02984bcdc11abd68ffef01557eed3ccadc1b653ab918842ecdfcc",
   "size":237,
   "type":"ClaimTransaction",
   "version":0,
   "attributes":[

   ],
   "vout":[
      {
         "n":0,
         "asset":"0x602c79718b16e442de58778e148d0b1084e3b2dffd5de6b7b16cee7969282de7",
         "value":"0.03326015",
         "address":"ANAP9Afv5WxJzgw5j5Q3zrY71QWMAwhZHg"
      }
   ],
   "vin":[

   ],
   "sys_fee":"0",
   "net_fee":"0",
   "scripts":[
      {
         "invocation":"40da65923fbfb60ee9f94882e1df1d11dfefa1eae89cb989ec6e27007108c4d7db4e134ce9be5636436fae1209bb44c308f8b9eef3dcbc73d1a0132b8dab9f07de",
         "verification":"210282606b2b58cbbeb25890d35e5b7480089fa726e5f625fdb3193a2677b3a6ebf6ac"
      }
   ],
   "claims":[
      {
         "txid":"0x84d91a7641f038a03a7e93ddfd0d7f546aba3b4494dd4d7981552abdf2890593",
         "vout":0
      },
      {
         "txid":"0x3c256425d2f650572fdcef7101cfb845bd668170e3fbc5b55ef10bd4d8b6ac1a",
         "vout":0
      }
   ]
}
```

### ContractTransaction
Common transaction to transfer assets. The `ContractTransaction` is used to send NEO or GAS to another contract address.

#### Additional attributes for a ContractTransaction:
There are no additional attributes required.

Example:

```javascript
{
   "txid":"0x3d5b91a488a12ec091fff743b1670c008cc1962f3aa98e760981016685e9c668",
   "size":211,
   "type":"ContractTransaction",
   "version":0,
   "attributes":[
      {
         "usage":255,
         "data":"6e656f2d6f6e65"
      }
   ],
   "vout":[
      {
         "n":0,
         "asset":"0xc56f33fc6ecfcd0c225c4ab356fee59390af8560be0e930faebe74a6daff7c9b",
         "value":"12",
         "address":"ATNjqV62Azg3yLw4Tfc6yhKyUCSsqjQ6iA"
      }
   ],
   "vin":[
      {
         "txid":"0xdd5fb8bfac04742788e1d0a73307d1eeb87d098165eb248d481fb84448742003",
         "vout":0
      }
   ],
   "sys_fee":"0",
   "net_fee":"0",
   "scripts":[
      {
         "invocation":"407eea3ba920b48973e7f3d5d4e532fe3011d02da3e75daaa20f310c3248ed49a97f5dad0a28178c9473b52ed04c8fa2ffe2f49eb8e6e4a8ed5968d4a507283c86",
         "verification":"21029d910eb93122578d0ddf0443f96f4cdece42a7e4e404ae047a75734c1aa4738eac"
      }
   ]
}
```

### StateTransaction
Voting and registering for a consensus node candidate. 

#### Additional attributes for a StateTransaction:

| Field         | Type  | Description           |
|---------------|-------|-----------------------|
| `descriptors` | array | State descriptor list |

#### Descriptors
A `descriptor` contains voting information. It can be used to apply as a consensus node or to vote for a consensus node candidate.

| Field   | Type   | Description                          |
|---------|--------|--------------------------------------|
| `type`  | uint8  | State descriptor type                |
| `key`   | byte   | Contract script hash or public key   |
| `field` | string | State field to update                |
| `value` | byte   | Updated value for the state field    |

#### Type
The state descriptor type can be either `0x40` for `Account` or `0x48` for `Validator`. If this type is set to account, then the descriptor can be used to update votes. If this type is set to validator, then it is used to update the registration state as a consensus node candidate.

#### Key
The key is either the 20 byte script hash of the voting contract if `Type` is `Account`, or the 33 byte public key of the validator if `Type` is `Validator`.

#### Field
The state field to update. This is either `Registered` to set validator request or `Votes` to set account votes.

#### Value
Updated value for the state field. If a validator wants to register to be a consensus node candidate then he can set the `Registered` field to the value `True` or cancel a registration by setting `Registered` to `False`. If an account wants to vote for consensus nodes he can set an array of public keys to vote for.

Example:

```javascript
{
   "txid":"0x7031bbc63b5087ed1e84a7a6f02a4b5c7a998c800862f0b5d1e745128bdd152f",
   "size":271,
   "type":"StateTransaction",
   "version":0,
   "attributes":[

   ],
   "vout":[

   ],
   "vin":[

   ],
   "sys_fee":"0",
   "net_fee":"0",
   "scripts":[
      {
         "invocation":"40f74883a23083f9a236b01aec3eb016e4611ac23cf3036addf8957460917bad4bb968cbbb93e321da368e11da77defca0342299dd8806e9953c0def13c6b348f4",
         "verification":"21034278b37db70b6c59b1e68a34569b77c5470ed50b9a1176b0d2da1b1b601ae86cac"
      }
   ],
   "descriptors":[
      {
         "type":"Account",
         "key":"ce47912d51b7ed8a24a77f97f2cb6ef9a0e0bf0d",
         "field":"Votes",
         "value":"04024c7b7fb6c310fccf1ba33b082519d82964ea93868d676662d4a59ad548df0e7d02aaec38470f6aad0042c6e877cfd8087d2676b0f516fddd362801b9bd3936399e02ca0e27697b9c248f6f16e085fd0061e26f44da85b58ee835c110caa5ec3ba55402df48f60e8f3e01c48ff40b9b7f1310d7a8b2a193188befe1c2e3df740e895093"
      }
   ]
}
```

### InvocationTransaction
Invoke or deploy a smart contract on the blockchain. 

#### Additional attributes for a InvocationTransaction:

| Field    | Type  | Description                                  |
|----------|-------|----------------------------------------------|
| `script` | byte  | Script to be executed by the virtual machine |

#### Script
The `script` is the AVM bytecode to be executed. This can be a stand-alone script, an invocation of an already deployed smart contract using the `AppCall` opcode, or the deployment of a new smart contract through the use of the `Neo.Contract.Create` instruction.

Example:

```javascript
{
   "txid":"0x1ae96d64e4d88a31f21f8a05a5370600efb3a7aa55e6fec6057f895f5ba91c16",
   "size":231,
   "type":"InvocationTransaction",
   "version":1,
   "attributes":[

   ],
   "vout":[
      {
         "n":0,
         "asset":"0x602c79718b16e442de58778e148d0b1084e3b2dffd5de6b7b16cee7969282de7",
         "value":"1011.92212",
         "address":"ALEN8KC46GLaadRxaWdvYBUhdokT3RhxPC"
      }
   ],
   "vin":[
      {
         "txid":"0x33b241c922c7178c1fc50c0bf104ab729a851b77c2073be842c69712ceac2118",
         "vout":0
      }
   ],
   "sys_fee":"0",
   "net_fee":"0.0001",
   "scripts":[
      {
         "invocation":"401ba0d3ba2751842cca57c562ad31617cec8187fe0fa894ca71e0a1dfb29f87e6753615528336be273a7ef90601c9ba1b7719beaa0cc5113ec4dc11e5b52b68a0",
         "verification":"2103ed613933d4745622e7c626275c5e74dac1a595d07a9ada02b31104ebb6330aa2ac"
      }
   ],
   "script":"00c104696e69746771496142de066bd6b7a2d6a166dc47a543d1c0ba"
}
```

## Registering assets (deprecated)
NEO supports the registration of native (UTXO) assets on the blockchain with the `RegisterTransaction` and `IssueTransaction` transaction types. NEO and GAS are both examples of these native assets. For digital asset registration it is more common now to use a (NEP-5 compatible) smart contract. Using a smart contract is more scalable and flexible than using native assets. The new token smart contract may be deployed to the blockchain with an [InvocationTransaction](#InvocationTransaction).

## What's next?

[Transaction Fees](4-NEO_transaction_fees.md)
