# API Reference, Typing & Interfaces

## Interfaces

#### `FusePoolData`

```typescript
interface FusePoolData {
  id: number;
  assets: NativePricedFuseAsset[];
  creator: string;
  comptroller: string;
  name: string;
  totalLiquidityNative: number;
  totalAvailableLiquidityNative: number;
  totalSuppliedNative: number;
  totalBorrowedNative: number;
  totalSupplyBalanceNative: number;
  totalBorrowBalanceNative: number;
  blockPosted: BigNumber;
  timestampPosted: BigNumber;
  underlyingTokens: string[];
  underlyingSymbols: string[];
  whitelistedAdmin: boolean;
  utilization: number;
}
```

#### `NativePricedFuseAsset`

```typescript
interface NativePricedFuseAsset extends FuseAsset {
  supplyBalanceNative: number;
  borrowBalanceNative: number;

  totalSupplyNative: number;
  totalBorrowNative: number;

  liquidityNative: number;
  utilization: number;
}
```

#### `FuseAsset`

```typescript
interface FuseAsset {
  cToken: string;
  plugin?: MarketPluginConfig;

  borrowBalance: BigNumber;
  supplyBalance: BigNumber;
  liquidity: BigNumber;

  membership: boolean;

  underlyingName: string;
  underlyingSymbol: string;
  underlyingToken: string;
  underlyingDecimals: BigNumber;
  underlyingPrice: BigNumber;
  underlyingBalance: BigNumber;

  collateralFactor: BigNumber;
  reserveFactor: BigNumber;

  adminFee: BigNumber;
  fuseFee: BigNumber;

  borrowRatePerBlock: BigNumber;
  supplyRatePerBlock: BigNumber;

  totalBorrow: BigNumber;
  totalSupply: BigNumber;

  isBorrowPaused: boolean;
  isSupplyPaused: boolean;
}
```

#### PluginData

```
interface PluginData { 
    market: string;
    name: string;
    strategy?: string; 
}
```

## Types

#### `SupportedAsset`

```typescript
type SupportedAsset = {
  symbol: string;
  underlying: string;
  name: string;
  decimals: number;
  disabled?: boolean;
  oracle?: OracleTypes;
  simplePriceOracleAssetPrice?: BigNumber;
};
```

#### `ChainAddresses`

```typescript
type ChainAddresses = {
  W_TOKEN: string;
  W_TOKEN_USD_CHAINLINK_PRICE_FEED: string;
  UNISWAP_V2_ROUTER: string;
  UNISWAP_V2_FACTORY: string;
  PAIR_INIT_HASH: string;
};
```

#### `ChainParams`

```typescript
type ChainParams = {
  blocksPerYear: BigNumber;
  cgId: string;
};
```

#### **`DeployedPlugins`**

```typescript
type DeployedPlugins = { 
    [pluginAddress: string]: PluginData; 
};
```

#### `MarketPluginConfig`

```typescript
type MarketPluginConfig = StandardPluginConfig | RewardsPluginConfig;

interface AbstractPluginConfig {
  cTokenContract: DelegateContractName;
  strategyName: string;
  strategyCode: string;
  strategyAddress: string;
}

interface StandardPluginConfig extends AbstractPluginConfig {
  cTokenContract: DelegateContractName.CErc20PluginDelegate;
}

type RewardFlywheel = {
  address: string;
  rewardToken: string;
};

interface RewardsPluginConfig extends AbstractPluginConfig {
  cTokenContract: DelegateContractName.CErc20PluginRewardsDelegate;
  flywheels: RewardFlywheel[];
}
```

#### `ChainDeployment`, `OracleConfig`, `IrmConfig`

```typescript
type ChainDeployment = {
  [contractName: string]: {
    abi: any;
    address: string;
  };
};
type OracleConfig = IrmConfig = ChainDeployment;
```

#### **`Artifact`**

```typescript
export type Artifact = {
  abi: Array<object>;
  bytecode: {
    object: string;
    sourceMap: string;
  };
  deployedBytecode: {
    object: string;
    sourceMap: string;
  };
};
```

#### `ChainLiquidationConfig`

```typescript
export type ChainLiquidationConfig = {
  SUPPORTED_OUTPUT_CURRENCIES: Array<string>;
  SUPPORTED_INPUT_CURRENCIES: Array<string>;
  LIQUIDATION_STRATEGY: LiquidationStrategy;
  MINIMUM_PROFIT_NATIVE: BigNumber;
  LIQUIDATION_INTERVAL_SECONDS: number;
};
```

#### **`LiquidatablePool`,** `EncodedLiquidationTx`

```typescript
export type EncodedLiquidationTx = {
  method: string;
  args: Array<any>;
  value: BigNumber;
};

export type LiquidatablePool = {
  comptroller: string;
  liquidations: EncodedLiquidationTx[];
};
```

#### `FlywheelMarketRewardsInfo`

```typescript
type FlywheelMarketRewardsInfo = {
  market: string;
  underlyingPrice?: BigNumber;
  rewardsInfo: {
    rewardToken: string;
    flywheel: string;
    rewardSpeedPerSecondPerToken?: BigNumber;
    rewardTokenPrice?: BigNumber;
    formattedAPR?: BigNumber;
  }[];
};
```

## **Enums**

#### `IrmTypes`

```typescript
enum IrmTypes {
  JumpRateModel = "JumpRateModel",
  WhitePaperRateModel = "WhitePaperRateModel",
  AnkrBNBInterestRateModel = "AnkrBNBInterestRateModel",
}
```

#### OracleTypes

```typescript
enum OracleTypes {
  ChainlinkPriceOracleV2 = "ChainlinkPriceOracleV2",
  CurveLpTokenPriceOracleNoRegistry = "CurveLpTokenPriceOracleNoRegistry",
  DiaPriceOracle = "DiaPriceOracle",
  FixedNativePriceOracle = "FixedNativePriceOracle",
  FluxPriceOracle = "FluxPriceOracle",
  MasterPriceOracle = "MasterPriceOracle",
  SimplePriceOracle = "SimplePriceOracle",
  UniswapLpTokenPriceOracle = "UniswapLpTokenPriceOracle",
  UniswapTwapPriceOracleV2 = "UniswapTwapPriceOracleV2",
  AnkrBNBcPriceOracle = "AnkrBNBcPriceOracle",
}
```

#### `LiquidationStrategy`

```typescript
export enum LiquidationStrategy {
  DEFAULT = "DEFAULT",
  UNISWAP = "UNISWAP",  // uses flash swaps
}
```
