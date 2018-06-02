MultiCryptoCoins RPC Lib by TypeScript for Node.js

## Supports

* Bitcoin(core 0.16+)
* Ethereum(geth 1.8.0+) and ERC20
* DKKToken

## TODO Supports

* [ ] Bitcoin Cash
* [ ] LiteCoin
* [ ] EOS

## Install

```shell
# PRE-REQUIRED: Node.js 8.x && NPM 5.6+
npm install wallet-rpc --save
```

## Usage

### CommonJS

```js
const { bitcoin, ethereum, dkktoken } = require("wallet-rpc");
// get rpc and rpc methods by this
const { rpc: btcRpc, mtd: btcMtd } = bitcoin;
// the default rpc port of bitcoin is 8332
// so this param is optional
const defaultPort = 8332;
const btcClient = new btcRpc("username", "password", "ip", defaultPort);
// the default rpc of geth has no username and no password
// if you config the proxy you can pass them to constructor.
// the param order is ip-port-username-password
const ethClient = new ethereum.rpc("ip");
btcClient
  .getTxInfo("txid")
  .then(txInfo => console.log)
  .catch(console.log);
// ...
// BulkCall see flow
```

### TypeScript

```typescript
import { bitcoin, ethereum, dkktoken } from "wallet-rpc";
const { rpc: btcRpc, mtd: btcMtd } = bitcoin;
const defaultPort = 8332;
const btcClient = new btcRpc("username", "password", "ip", defaultPort);

// Bulk Call
btcClient
  // your can set generic
  // and return `type[]`
  // the types can import from defined/*.d.ts
  .bulkRpcExec<string>([{
    id: 0,
    jsonrpc: "2.0",
    method: btcMtd.block.hash
    params: [0]
  },{
    id: 1,
    jsonrpc: "2.0",
    method: btcMtd.block.hash
    params: [1]
  }])
  .then(console.log)
  .catch(console.log);

// also can Bulk call by this
btcClient.BulkAdd(btcMtd.block.hash, [0], 0);
btcClient.BulkAdd(btcMtd.block.hash, [1], 1);
btcClient.BulkCall();
```

### API

* [Bitcoin API](./types/bitcoin/rpc.d.ts)
* [Ethereum API and Util func](./types/ethereum/rpc.d.ts)
* [DKKToken API](./types/dkktoken/rpc.d.ts)

## Feedback

* [issue](https://github.com/isLishude/wallet-rpc/issues)
