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
/* {
    response: [
        {
            address: "0x6BdfC9Fb0102ddEFc2C7eb44cf62e96356D55d04",
            network: "evm",
            from: "redefined-email"
        }, {
            address: "0x6BdfC9Fb0102ddEFc2C7eb44cf62e96356D55d04",
            network: "bsc",
            from: "redefined-email"
        }
    ],
    errors: [
        {
            vendor: "ens",
            error: "Invalid domain",
        },
    ],
}*/
const nicknameResult = await resolver.resolve("gigachadivan");
/* {
    response: [{
        address: "GsYPSWAbXw4YsSEeowuTf7nqjExVxKS5tS1Yy9WwFAPG",
        network: "sol",
        from: "redefined-username"
    }],
    errors: [],
}*/

// resolve ENS names
const ensResult = await resolver.resolve("ivan.eth");
/* {
    response: [{
        address: "0x25428d29a6FA3629ff401c6DADe418B19CB2D615",
        network: "evm",
        from: "ens"
    }],
    errors: [
        {
            vendor: "redefiend-email",
            error: "Domain is not registered",
        },
    ],
}*/

// resolve Unstoppable names
const unstoppableResult = await resolver.resolve("nick.crypto");
/* {
    response: [{
        address: "0x16d94b922bF11981DBa2C4A6cAEd9938F00d5d0C",
        network: "evm",
        from: "unstoppable"
    }],
    errors: [],
}*/

// resolve specific network
const ethResult = await resolver.resolve("ik@e2xlabs.com", ["eth"]);
/* {
    response: [{
        address: "0x6BdfC9Fb0102ddEFc2C7eb44cf62e96356D55d04",
        network: "eth",
        from: "redefined-email"
    }],
    errors: [],
}*/
const bscFromUnstoppable = await resolver.resolve("nick.crypto", ["bsc"]);
/* {
    response: [{
        address: "0x16d94b922bF11981DBa2C4A6cAEd9938F00d5d0C",
        network: "evm",
        from: "unstoppable"
    }],
    errors: [],
}*/
const solFromBonfida = await resolver.resolve("example", ["sol"]);
/* {
    response: [{
        address: "CiJscHNjYEa6z61bXuYnxLGoLyMiY3mf8vjcx97Dcmxg",
        network: "sol",
        from: "bonfida"
    }],
    errors: [],
}*/
const bscFromSid = await resolver.resolve("nick.bnb");
/*
  {
    response: [{ address: "0xf88353e6b33d1f9f6f325dbcbb697ddd0be3bd5c", network: "bsc", from: "sid", }],
    errors: [],
  }
*/

const arbOneFromSid = await resolver.resolve("nick.arb");
/*
  {
    response: [{ address: "0xf88353e6b33d1f9f6f325dbcbb697ddd0be3bd5c", network: "arbitrum-one", from: "sid", }],
    errors: [],
  }
*/

const arbNovaFromSid = await resolver.resolve("nick.arb");
/*
  {
    response: [{ address: "0xf88353e6b33d1f9f6f325dbcbb697ddd0be3bd5c", network: "arbitrum-nova", from: "sid", }],
    errors: [],
  }
*/

const evmFromLens = await resolver.resolve("aaveaave.lens");
/* {
    response: [{
        address: "0xD4478D18E203c418A1Fd1d89f6518eD9819Ff348",
        network: "evm",
        from: "lens"
    }],
    errors: [],
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
