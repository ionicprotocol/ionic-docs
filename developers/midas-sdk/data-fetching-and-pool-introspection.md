---
description: >-
  Whether it be to create a custom dashboard, or just finding out what current
  positions look like, fetching pool information might be the first and foremost
  task that most developers will want to use
---

# Data Fetching & Pool Introspection

Initialisation always works the same way -- pick a chain and a provider, and create the Fuse object

```typescript
// Initialisation always works the same way -- 
// pick a chain and a provider, and create the Fuse object

const sdk = new IonicSdk(provider, chainId);
```

### `fetchFusePoolData`

**Arguments:**

* `poolId: string`
* `address?: string`

**Returns:**

* `Promise<FusePoolData>`

The `poolId` is the canonical pool index, retrievable via the UI. E.g. https://app.ionic.money/56/pool/1 -> `poolId = 1`

The `address` is the address of a pool user, e.g. someone that has provided liquidity, or borrowed assets. If passed, the function will returned detailed information about the user's balances.

```typescript
const fusePoolData = await sdk.fetchFusePoolData("1", "0x111...")

fusePoolData.assets.map((a) => console.log(a.underlyingSymbol));

>>> "2brl", "WBNB", "ETH", "BUSD"
```

This returns a `Promise` of [`FusePoolData`](api-reference-typing-and-interfaces.md#fusepooldata). Check out the type definition for more information about the data contained in it.

### `fetchPools`

**Arguments:**

* `filter: string | null`
* `options: { from: string })`

**Returns:**

* `Promise<FusePoolData[]>`

Returns an array of fuse pools, given a specific filter. Filters can be:

```typescript
"created-pools" | "verified-pools" | "unverified-pools"
```

Passing the `{ from: address }` will return the detailed balances of the address provided

### `fetchPoolsManual`

* `verification: boolean`
* `options: { from: string }`

**Returns:**

* `Promise<(FusePoolData | null)[] | undefined>`

Slightly optimised data fetching function for expensive calculations that handles failures gracefully in case of using less efficient RPC endpoints
