# Set your own Node URLs

We recommend you to use your own JSON RPC URLs, especially for production: this will improve availability of service and will lower the load on our public nodes.

## Pass node URLs on init

```typescript
const options: ResolversParams = {
  redefined: {
      node: "https://evm.node.io/123abc",
  },
  unstoppable: {
      mainnetNode: "https://evm2.node.io/123abc",
      polygonMainnetNode: "https://evm-polygon.node.io/123abc",
  },
  ens: {
    node: "https://evm.node.io/123abc",
  },
  sid: {
    bscNode: "https://bsc.node.io/123abc",
    arbitrumOneNode: "https://arb.node.io/123abc",
  },
  bonfida: {
    cluster: "https://rpc.ankr.com/solana",
  },
  lens: {
    apiUrl: "https://api.lens.dev", // current lens api
  },
}

const resolver = new RedefinedResolver({
      resolvers: RedefinedResolver.createDefaultResolvers(options)
});
```
