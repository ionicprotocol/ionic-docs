---
description: >-
  The Ionic SDK is a chain-agnostic toolkit to interact with the Ionic Protocol,
  enabling developers to seamlessly integrate isolated pools into their own
  applications
---

# Ionic SDK

### Quickstart

**Installation**

```bash
npm i --save @ionicprotocol/sdk ethers 
```

Depending on your machine configuration, you may also need this:

```bash
npm install -D tslib @types/node
```

**Usage**

```typescript
import { ethers } from "ethers";
import { IonicSdk } from '@ionicprotocol/sdk';


const chainId = 56;  // for BSC mainnet
const provider = new ethers.providers.JsonRpcProvider('<YOUR-ENDPOINT-HERE>')

const ionic = new IonicSdk(provider, chainId);
```

The `IonicSdk` object provides access to all the functionality needed to query, manage & interact with pools created via our protocol. See the next sections to get an overview of the possibilities it enables.

To get a sense of how the `ionic-sdk` is used in a real-life, full-fledged web application, check out the latest section, [Putting It All Together](putting-it-all-together.md).
