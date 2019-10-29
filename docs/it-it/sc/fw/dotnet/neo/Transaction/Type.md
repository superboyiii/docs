# Proprietà Transaction.Type

Restituisce il tipo di transazione.

Namespace: [Neo.SmartContract.Framework.Services.Neo](../../neo.md)

Assembly: Neo.SmartContract.Framework

## Sintassi

```c#
public extern byte Type {get;}
```

Valore dell'attributo: Tipo di transazione come byte.

Tipi:

```c#
// consensus transaction, special transaction for allocating byte charges
MinerTransaction = 0x00,
//Special transactions for the distribution of assets
IssueTransaction = 0x01,
// special deals for the distribution of small coins
ClaimTransaction = 0x02,
//Special transaction for registration as a book of candidates
EnrollmentTransaction = 0x20,
//Special transactions for asset registration
RegisterTransaction = 0x40,
// contract transaction, which is the most commonly used deal
ContractTransaction = 0x80,
// commissioned by the transaction
AgencyTransaction = 0xb0,
// issue a deal with a smart contract
PublishTransaction = 0xd0,
// Invoke smart contract transactions
InvocationTransaction = 0xd1
```



[Indietro](../Transaction.md)
