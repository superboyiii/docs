# getwalletheight 方法

获取当前钱包索引高度。

> [!Note]
>
> 此方法由插件提供，需要安装 [RpcWallet](https://github.com/neo-project/neo-plugins/releases) 插件才可以调用。

## 调用示例

请求正文：

```json
{
  "jsonrpc": "2.0",
  "method": "getwalletheight",
  "params": [],
  "id": 1
}
```

响应正文：

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": 2713183
}
```

