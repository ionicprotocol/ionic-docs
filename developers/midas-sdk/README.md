---
description: >-
  The Midas SDK is a chain-agnostic toolkit to interact with the Midas Protocol,
  enabling developers to seamlessly integrate permissionless pools into their
  own applications
---

# Midas SDK

### Quickstart

**Installation**

```bash
npm i --save @midas-capital/sdk ethers 
```

Depending on your machine configuration, you may also need this:

```bash
npm install -D tslib @types/node
```

**Usage**

```typescript
import { ethers } from "ethers";
import { MidasSdk } from '@midas-capital/sdk';


const chainId = 56;  // for BSC mainnet
const provider = new ethers.providers.JsonRpcProvider('<YOUR-ENDPOINT-HERE>')

const midas = new MidasSdk(provider, chainId);
```

The `MidasSdk` object provides access to all the functionality needed to query, manage & interact with pools created via our protocol. See the next sections to get an overview of the possibilities it enables.

To get a sense of how the `midas-sdk` is used in a real-life, full-fledged web application, check out the latest section, [Putting It All Together](putting-it-all-together.md).
