# chain-registry

<p align="center" width="100%">
    <img height="90" src="https://user-images.githubusercontent.com/545047/190171475-b416f99e-2831-4786-9ba3-a7ff4d95b0d3.svg" />
</p>

<p align="center" width="100%">
  
  <a href="https://github.com/cosmology-tech/chain-registry/actions/workflows/run-tests.yml">
    <img height="20" src="https://github.com/cosmology-tech/chain-registry/actions/workflows/run-tests.yml/badge.svg" />
  </a>
   <a href="https://github.com/cosmology-tech/chain-registry/blob/main/LICENSE"><img height="20" src="https://img.shields.io/badge/license-MIT-blue.svg"></a>
   <a href="https://www.npmjs.com/package/chain-registry"><img height="20" src="https://img.shields.io/npm/dt/chain-registry"></a>
   <a href="https://www.npmjs.com/package/chain-registry"><img height="20" src="https://img.shields.io/github/package-json/v/cosmology-tech/chain-registry?filename=packages%2Fchain-registry%2Fpackage.json"></a>
</p>

The npm package for the Official Cosmos [chain registry](https://github.com/cosmos/chain-registry)


```
npm install chain-registry
```

A unified store of chains info, assets, asset lists, and IBC channels for the Cosmos ecosystem. Get everything from token symbols, logos, and IBC denominations for all assets you want to support in your application.

## example

Fetch data from chain-registry:

```js
import { assets, chains, ibc } from 'chain-registry';

const assetList = assets.find(({chain_name})=>chain_name==='osmosis');

console.log(assetList);
```

will output:

```js
{
  '$schema': '../assetlist.schema.json',
  chain_name: 'osmosis',
  assets: [
    {
      description: 'The native token of Osmosis',
      denom_units: [Array],
      base: 'uosmo',
      name: 'Osmosis',
      display: 'osmo',
      symbol: 'OSMO',
      logo_URIs: [Object],
      coingecko_id: 'osmosis'
    },
    {
      denom_units: [Array],
      base: 'uion',
      name: 'Ion',
      display: 'ion',
      symbol: 'ION',
      logo_URIs: [Object],
      coingecko_id: 'ion'
    }
  ]
}
```

Dynamically fetch data:

```js
import { ChainRegistryClient } from '@chain-registry/client';

// create an instance of ChainRegistryClient by passing in the chain names
const client = new ChainRegistryClient({
  chainNames: [
    'osmosis',
    'juno',
    'stargaze'
  ]
});

// chain info, assets and ibc data will be downloaded dynamically by invoking fetchUrls method
await client.fetchUrls();
// get chain data
const chain = client.getChain('osmosis');
// get asset list
const assetList = client.getChainAssetList('osmosis');
// get ibc data
const ibcData = client.getChainIbcData('osmosis);
// get asset list (including ibc assets)
const generatedAssetList = client.getGeneratedAssetLists('osmosis);

```


## packages

#### [chain-registry](packages/chain-registry)

An npm module for the Official `chain-registry` for the Cosmos ⚛️

#### [@chain-registry/client](packages/client)

A Client for `chain-registry` that allows you to dynamically fetch data.

#### [@chain-registry/types](packages/types)

Types for `chain-registry`.

#### [@chain-registry/keplr](packages/keplr)

Keplr integration for the chain-registry returning keplr's `ChainInfo` type from `@chain-registry/types` `Chain` type.

#### [@chain-registry/assets](packages/assets)

Asset lists for the Cosmos ⚛️

#### [@chain-registry/osmosis](packages/osmosis)

Chain Registry info for Osmosis, including asset lists.

#### [@chain-registry/juno](packages/juno)

Chain Registry info for Juno, including asset lists.

#### [@chain-registry/utils](packages/utils)

Utility functions for `chain-registry`.

## Developing

Checkout the repository and bootstrap the yarn workspace:

```sh
# Clone the repo.
git clone https://github.com/cosmology-tech/chain-registry
yarn
yarn bootstrap
```
### Building

```sh
yarn build
```

### Publishing

First, `cd` into the root folder of the project:

```sh
cd /your/path/to/chain-registry
```

Second, update the git submodules:

```sh
git submodule update --remote
```

Third, generate the code (this takes a bit since it does some linting):

```sh
yarn codegen
```

Finally, commit and publish the code!

```sh
git commit -am "new registry updates"
lerna publish
```

## Related

Checkout these related projects:

* [@cosmwasm/ts-codegen](https://github.com/CosmWasm/ts-codegen) for generated CosmWasm contract Typescript classes
* [@cosmology/telescope](https://github.com/cosmology-tech/telescope) a "babel for the Cosmos", Telescope is a TypeScript Transpiler for Cosmos Protobufs.
* [chain-registry](https://github.com/cosmology-tech/chain-registry) an npm module for the official Cosmos chain-registry.
* [cosmos-kit](https://github.com/cosmology-tech/cosmos-kit) A wallet connector for the Cosmos ⚛️
* [create-cosmos-app](https://github.com/cosmology-tech/create-cosmos-app) set up a modern Cosmos app by running one command.
* [starship](https://github.com/cosmology-tech/starship) a k8s-based unified development environment for Cosmos Ecosystem

## Credits

🛠 Built by Cosmology — if you like our tools, please consider delegating to [our validator ⚛️](https://cosmology.tech/validator)
