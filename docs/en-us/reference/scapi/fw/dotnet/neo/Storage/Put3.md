# Storage.Put Method (StorageContext, string, byte[])

Inserts a given value to the given key in the persistent store.

Namespace: [Neo.SmartContract.Framework.Services.Neo](../../neo.md)

Assembly: Neo.SmartContract.Framework

## Syntax

```c#
public extern void Put(Neo.SmartContract.Framework.Services.Neo.StorageContext context, string key, byte[] value)
```

Parameters:

Context: Storage context as a [StorageContext](../StorageContext.md).

Key: Key as a string.

Value: Value as a byte array.

Return value: void.

## Example

```c#
public class Contract1: FunctionCode
{
     public static void Main()
     {
         String key = "key";
         byte[] value = new byte[] {1};
         Storage.Put(Storage.CurrentContext, key, value);
     }
}
```



[Back](../Storage.md)
