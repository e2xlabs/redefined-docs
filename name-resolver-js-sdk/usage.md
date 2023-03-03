# Usage

## Installation

```bash
npm i @redefined/name-resolver-js
```

or download the lib from NPM registry manually: [https://www.npmjs.com/package/@redefined/name-resolver-js](https://www.npmjs.com/package/@redefined/name-resolver-js)

## Usage

```typescript
// initialize resolver
const resolver = new RedefinedResolver();

// resolve redefined names
const emailResult = await resolver.resolve("ik@e2xlabs.com");
/* result: {
    [
        address: "0x6BdfC9Fb0102ddEFc2C7eb44cf62e96356D55d04",
        network: "evm",
        from: "redefined"
    ], [
        address: "0x6BdfC9Fb0102ddEFc2C7eb44cf62e96356D55d04",
        network: "zil",
        from: "redefined"
    ]
}*/
const nicknameResult = await resolver.resolve("gigachadivan");
/* result: {
    [
        address: "GsYPSWAbXw4YsSEeowuTf7nqjExVxKS5tS1Yy9WwFAPG",
        network: "sol",
        from: "redefined"
    ]
}*/

// resolve ENS names
const ensResult = await resolver.resolve("ivan.eth");
/* result: {
    [
        address: "0x25428d29a6FA3629ff401c6DADe418B19CB2D615",
        network: "evm",
        from: "ens"
    ]
}*/

// resolve Unstoppable names
const unstoppableResult = await resolver.resolve("nick.crypto");
/* result: {
    [
        address: "0x16d94b922bF11981DBa2C4A6cAEd9938F00d5d0C",
        network: "evm",
        from: "unstoppable"
    ]
}*/

// resolve specific network
const zilResult = await resolver.resolve("ik@e2xlabs.com", ["zil"]);
/* result: {
    [
        address: "0x6BdfC9Fb0102ddEFc2C7eb44cf62e96356D55d04",
        network: "zil",
        from: "redefined"
    ]
}*/
const bscFromUnstoppable = await resolver.resolve("nick.crypto", ["bsc"]);
/* result: {
    [
        address: "0x16d94b922bF11981DBa2C4A6cAEd9938F00d5d0C",
        network: "evm",
        from: "unstoppable"
    ]
}*/
```

## Priorties of resolution of EVM-compatible

For example, you want to get a BSC or Polygon address, but there is no special mapping for them, we will fall back to default EVM mapping.

1. If we do not find the address in the desired network, but find EVM, then we will give you EVM
2. If we find the address in the desired network + EVM, then we will give you only the address in the desired network
3. If desired network is not specified, we will return all known results

```typescript
resolve.resolve("domain", ["eth"]);
// We found [{ address: "0x", network: "eth", from:"redefined" }, { address: "0x", network: "evm", from:"redefined" }]
// You receive [{ address: "0x", network: "eth", from:"redefined" }]

resolve.resolve("domain", ["eth"]);
// We found [{ address: "0x", network: "bsc", from:"redefined" }, { address: "0x", network: "evm", from:"redefined" }]
// You receive [{ address: "0x", network: "evm, from:"redefined" }]

resolve.resolve("domain");
// We found [{ address: "0x", network: "bsc", from:"redefined" }, { address: "0x", network: "evm", from:"redefined" }]
// You receive [{ address: "0x", network: "bsc, from:"redefined" }, { address: "0x", network: "evm", from:"redefined" }]
```

## Recommended config for Production use

Each supported domain system is hosted on some blockhain, and lib needs corresponding JSON RPC nodes in order to resolve names.

Our lib comes with all necessary node URLs built-in, but we strongly recommend specifying your own JSON RPC node URLs in order to provide best availability of service.&#x20;

Please follow [set-your-own-node-urls.md](set-your-own-node-urls.md "mention") documentation.
