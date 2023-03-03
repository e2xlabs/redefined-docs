# Add your own Custom Resolver

You can implement your own resolver service and add pass it to `RedefinedResolver`.

## Step 1. Extend ResolverService class

Please see github for sources: [https://github.com/e2xlabs/redefined-name-resolver-js/blob/master/src/services/resolvers/resolver.service.ts](https://github.com/e2xlabs/redefined-name-resolver-js/blob/master/src/services/resolvers/resolver.service.ts)

```typescript
export abstract class ResolverService {
    abstract vendor: ResolverVendor;
    abstract resolve(domain: string, options?: ResolverServiceOptions, networks?: string[]): Promise<Account[]>;
}
```

Example:

```typescript
export class KeyValueResolverService extends ResolverService {

    vendor: ResolverVendor = "keyvalue"
    
    registry = {
        "ivan": "0x1",
        "stepan": "0x2",
        "andrey": "0x3",
    }

    async resolve(domain: string, { throwErrorOnInvalidDomain }: ResolverServiceOptions = defaultResolverServiceOptions): Promise<Account[]> {
        const address = registry[domain];
        return address ? [{ address, network: "evm", from: this.vendor }] : [];
    }
}
```

## Step 2. Register your ResolverService in RedefinedResolver

Initialize `RedefinedResolver` with your `ResolverService` only:

```typescript
const resolver = new RedefinedResolver({
      resolvers: [new KeyValueResolverService()]
});
```

Or combine it with existing built-in resolver services:

```typescript
const resolver = new RedefinedResolver({
      resolvers: [
            ...RedefinedResolver.createRedefinedResolvers(),
            new KeyValueResolverService(),
      ]
});
```

## Contribute!

Open a pull request with your new `ResolverService` in our [GitHub](https://github.com/e2xlabs/redefined-name-resolver-js) and help the community!
