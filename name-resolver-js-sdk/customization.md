# Customization

## Reference

```typescript
export type EnsParams = { node: string };
export type UnstoppableParams = { mainnetNode?: string, polygonMainnetNode?: string };
export type RedefinedParams = { node?: string, allowDefaultEvmResolves?: boolean };
export type SidParams = { bscNode: string, arbitrumOneNode: string };
export type BonfidaParams = { cluster: string };
export type LensParams = { apiUrl: string };

export type ResolversParams = {
    redefined?: RedefinedParams,
    unstoppable?: UnstoppableParams,
    ens?: EnsParams,
    sid?: SidParams,
    bonfida?: BonfidaParams,
    lens?: LensParams,
}
```

## Set you own Nodes

Documented [here.](set-your-own-node-urls.md)

## Init with params

```typescript
const resolver = new RedefinedResolver({
      resolvers: RedefinedResolver.createDefaultResolvers({
        // specify only params that you want to change
        redefined: {
          node: "https://evm.node.io/123",
          allowDefaultEvmResolves: false
        },
        // uncomment if you want to specify params for ens, otherwise defaults used
        // ens: { node: "https://evm.node.io/123abc" }
      })
});
```
