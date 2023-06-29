---
description: Access all the addresses, contract interfaces, and chain configurations
---

# Chain Configuration and Addresses

Being the interface to a cross-chain protocol, the `MidasSdk` is configured to seamlessly work across chains, and allows developers to introspect each chain's available infrastructure, as well as the deployed contracts in that chain.

These values are directly available via the instantiated SDK, for the selected chain with which the SDK is instantiated.

E.g.:

```typescript
import { MidasSdk } from '@midas-capital/sdk';
import { ethers } from "ethers";

const chainId = 56;  // for BSC mainnet
const provider = new ethers.providers.JsonRpcProvider('<YOUR-ENDPOINT-HERE>')

const sdk = new MidasSdk(provider, chainId);

console.log(sdk.oracles)
>>> ["FixedNativePriceOracle", "MasterPriceOracle", "ChainlinkPriceOracleV2", "CurveLpTokenPriceOracleNoRegistry", "UniswapLpTokenPriceOracle", "UniswapTwapPriceOracleV2"]
```

Here's an overview of the available properties of `MidasSdk`:

```typescript
MidasSdk.provider         // the passed in provider
MidasSdk.chainId          // the passed in chain id 
MidasSdk.supportedAssets
MidasSdk.chainDeployment
MidasSdk.contracts 
MidasSdk.artifacts
MidasSdk.irms
MidasSdk.availableIrms
MidasSdk.oracles
MidasSdk.availableOracles
MidasSdk.chainSpecificAddresses
MidasSdk.chainSpecificParams
MidasSdk.deployedPlugins
```

### `MidasSdk.supportedAssets`

**Type:**  Array of [`SupportedAsset`](api-reference-typing-and-interfaces.md#supportedasset)

Returns an array of the supported assets for Midas Protocol given a specific chain.&#x20;

E.g.:

```typescript
console.log(sdk.supportedAssets)
>>> 
[
  {
    symbol: 'WBNB',
    underlying: '0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c',
    name: 'Wrapped Binance Network Token',
    decimals: 18,
    oracle: 'FixedNativePriceOracle'
  },
  {
    symbol: 'BUSD',
    underlying: '0xe9e7CEA3DedcA5984780Bafc599bD69ADd087D56',
    name: 'Binance USD',
    decimals: 18,
    oracle: 'ChainlinkPriceOracleV2'
  },
  {
    symbol: 'BTCB',
    underlying: '0x7130d2A12B9BCbFAe4f2634d864A1Ee1Ce3Ead9c',
    name: 'Binance BTC',
    decimals: 18,
    oracle: 'ChainlinkPriceOracleV2'
  },
  ...
```

### `MidasSdk.irms`

**Type:** [`IrmConfig`](api-reference-typing-and-interfaces.md#chaindeployment-oracleconfig-irmconfig)

Returns an object mapping IRM contract names to their deployment specification, i.e., its address and ABI.

### `MidasSdk.availableIrms`

**Type:** `Array<`[`IrmTypes`](api-reference-typing-and-interfaces.md#irmtypes)`>`

Returns an array of the supported IRMs for a specific chain.

### `MidasSdk.oracles`

**Type:** [`OracleConfig`](api-reference-typing-and-interfaces.md#chaindeployment-oracleconfig-irmconfig)

Returns an object mapping oracle contract names to their deployment specification, i.e., its address and ABI.&#x20;

### `MidasSdk.availableOracles`

**Type:** `Array<`[`OracleTypes`](api-reference-typing-and-interfaces.md#oracletypes)`>`

Returns an array of the supported Oracles for a specific chain

### `MidasSdk.chainSpecificAddresses`

**Type:** [`ChainAddresses`](api-reference-typing-and-interfaces.md#chainaddresses)

This object contains a set of addresses for infra specific to this chain. The chain's Native Wrapped Token address, and the main Uniswap-like router and factory addresses are amongst them. Widely used within the SDK.

### `MidasSdk.chainSpecificParams`

**Type:** [`ChainParams`](api-reference-typing-and-interfaces.md#chainparams)

A few chain-specific parameters, such as the Blocks Per Year and the coingecko ID for the chain's native token.

### `MidasSdk.deployedPlugins`

**Type**: [**`DeployedPlugins`**](api-reference-typing-and-interfaces.md#deployedplugins)

Object containing the address, names, and strategies for the ERC4626 plugins deployed in a specific chain.

### `MidasSdk.contracts`

Set of already instantiated  [`ethers.Contract`](https://docs.ethers.io/v5/api/contract/contract/#Contract) for the core Midas Protocol contracts that are widely used across the SDK. The functionality of these contracts is mostly wrapped by other SDK functions, so these are unlikely to be widely used by developers. They are given however as instantiated contracts for ease of access from the SDK's codebase.&#x20;

**Type:**  `[contractName: string]: ethers.Contract]`

The main contracts are the following:

* `FuseFeeDistributor`: the "admin" contract, in charge of collecting protocol fees, and of performing admin functionality over the protocol
* `FusePoolDirectory`: a registry contract in charge of keeping track of deployed pools
* `FusePoolLens`: introspection module for querying Midas Pool's data at different levels of aggregation
* `FusePoolLensSecondary`: secondary introspection module, in charge of querying a specific pool's information
* `FuseSafeLiquidator`: the contract in charge of performing the liquidations on Fuse Pools

### `MidasSdk.artifacts`

**Type:** object containing as keys the Contract Name, and as object an [`Artifact`](api-reference-typing-and-interfaces.md#artifact) type. Once more, this is provided as a shorthand for other SDK functions.

E.g, to instantiate a cToken as an `ethers.Contract`, the following code is used:

```
const assetContract = new Contract(
    assetAddress, 
    this.artifacts.CTokenInterface.abi, 
    this.provider
);
```

### `MidasSdk.chainDeployment`

**Type:** [`ChainDeployment`](api-reference-typing-and-interfaces.md#chaindeployment)

Returns all the contract ABIs and addresses for the Midas Protocol's deployment in a given chain.

E.g.:

```typescript
console.log(sdk.chainDeployment.Comptroller)
>>> 
{
  address: '0x713B66c31833FF5E70123701a7368A2d28ea6485',
  abi: [
    {
      inputs: [Array],
      stateMutability: 'nonpayable',
      type: 'constructor'
    },
    {
      anonymous: false,
      inputs: [Array],
      name: 'ActionPaused',
      type: 'event'
    },
     ...
}
```

