# StorageContext.EntryContract 列挙値

コントラクトのエントリポイント（コントラクト呼び出しチェーンの開始ポイント）の、ストレージコンテキストです。

> [!警告]
> 注意: バージョン2.0で廃止予定です。

名前空間: [Neo.SmartContract.Framework.Services.Neo](../../neo.md)

アセンブリ: Neo.SmartContract.Framework

## 構文

```c#
public enum StorageContext: byte
{
     Current = 1,
     CallingContract = 2,
     EntryContract = 4
}
```

列挙値: 4



[戻る](../StorageContext.md)
