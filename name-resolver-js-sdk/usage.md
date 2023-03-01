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
        network: "eth",
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
        network: "eth",
        from: "ens"
    ]
}*/

// resolve Unstoppable names
const unstoppableResult = await resolver.resolve("nick.crypto");
/* result: {
    [
        address: "0x16d94b922bF11981DBa2C4A6cAEd9938F00d5d0C",
        network: "eth",
        from: "unstoppable"
    ]
}*/
```

That is it!

## Recommended config for Production use

Each supported domain system is hosted on some blockhain, and lib needs corresponding JSON RPC nodes in order to resolve names.

Our lib comes with all necessary node URLs built-in, but we strongly recommend specifying your own JSON RPC node URLs in order to provide best availability of service.&#x20;

Please follow [set-your-own-node-urls.md](set-your-own-node-urls.md "mention") documentation.
