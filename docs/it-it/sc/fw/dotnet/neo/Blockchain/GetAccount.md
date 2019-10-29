# Metodo (byte[]) Blockchain.GetAccount 

Restituisce un account (indirizzo) basato sull'hash dello scripthash del contratto.

Namespace: [Neo.SmartContract.Framework.Services.Neo](../../neo.md)

Assembly: Neo.SmartContract.Framework

## Sintassi

```c#
public static extern Neo.SmartContract.Framework.Services.Neo.Account GetAccount(byte[] script_hash)
```

Parametri: Scripthash come array di byte di lunghezza 20.

Valore restituito: [Account](../Account.md).

## Esempio

```c#
public class Contract1: FunctionCode
{
    public static void Main()
    {
        byte[] scriptHash = {36, 23, 241, 177, 228, 54, 109, 223, 27, 237, 139, 54, 207, 38, 132, 101, 172, 3, 10, 73};
        Account acc = Blockchain.GetAccount(scriptHash);
    }
}
```
The scripthash can be obtained in advanced and passed as a parameter into smart contracts. The following code uses the SDK to convert an address into scripthash.

```c#
Static void Main(string[] args)
{
    byte[] scriptHash = Neo.Wallets.Wallet.ToScriptHash("AK4if54jXjSiJBs6jkfZjxAastauJtjjse").ToArray();
}
```



[Indietro](../Blockchain.md)
