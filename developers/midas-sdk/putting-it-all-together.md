---
description: >-
  In this guide, we'll showcase how to get the most of the SDK in a real-life
  project
---

# Putting It All Together

While this guide is a work-in-progress, we have a full-fledged react-based/[wagmi](https://github.com/wagmi-dev/wagmi) web-app that showcases how to make use of the SDK. You can find it here: [`midas-starter`](https://github.com/Midas-Protocol/midas-starter)&#x20;

### **SDK instantiation**&#x20;

```typescript
// Context
export interface SDKContextData {
  sdk: MidasSdk;
  address: string;
  disconnect: () => void;
  currentChain: Chain & {
    unsupported?: boolean | undefined;
  };
  chains: Chain[];
}

export const SDKContext = createContext<SDKContextData | undefined>(undefined);

// Hook
export function useSDK() {
  const context = useContext(SDKContext);

  if (context === undefined) {
    throw new Error(`useSDK must be used within a SDKProvider`);
  }
  return context;
}


...

const { sdk, address, currentChain } = useSDK();
```

[Source code](https://github.com/Midas-Protocol/midas-starter/blob/master/src/context/SDKContext.tsx)

### **Pool Creation**

```typescript
  const { sdk, address, currentChain } = useSDK();
  const deployResult = await sdk.deployPool(
    poolName,
    whitelistedAddresses.length !== 0,
    bigCloseFactor,
    bigLiquidationIncentive,
    oracle,
    { reporter },
    { from: address },
    whitelistedAddresses
);
```

[Source code](https://github.com/Midas-Protocol/midas-starter/blob/master/src/components/sdk/CreatePool.tsx#L80-L89)

### Fetching Assets

```typescript
  const { sdk, address, currentChain } = useSDK();
  
  const { data: allPools } = useQuery(
    ['allPools', address, currentChain.id],
    async () => {
      return await sdk.fetchPoolsManual({
        verification: false,
        options: {
          from: address,
        },
      });
    },
    { cacheTime: Infinity, staleTime: Infinity, enabled: !!address && !!currentChain.id }
  );
```

[Source code](https://github.com/Midas-Protocol/midas-starter/blob/master/src/components/sdk/PoolsList.tsx)
