# APIs

## RPC API

Connecting to parachain nodes:

* **Kintsugi (by Kintsugi Labs)**: `wss://api-kusama.interlay.io/parachain`
* **Kintsugi (by OnFinality)**: `wss://kintsugi.api.onfinality.io/public-ws`
* **Testnet**: `wss://api.interlay.io/parachain`

## Asset API

### Overview of assets

| Asset    | CURRENCY_ID | CURRENCY_INDEX | DECIMALS |
|----------|-------------|----------------|----------|
| DOT      | DOT         | 0              | 10       |
| interBTC | INTERBTC    | 1              | 8        |
| INTR     | INTR        | 2              | 10       |
| KSM      | KSM         | 10             | 12       |
| kBTC     | KBTC        | 11             | 8        |
| KINT     | KINT        | 12             | 12       |

?> For any newly added assets, please refer to the [on-chain implementation](https://github.com/interlay/interbtc/blob/master/primitives/src/lib.rs#L472). We will not update the currency id or index of already published assets.

### Querying account balances

Returns the `amount` of tokens in the smallest denomination.

```js
api.query.tokens.accounts('address', {Token: CURRENCY_ID})
```

### Transferring tokens extrinsic

Transfers an `amount` of tokens in the smallest denomination.

```js
api.tx.tokens.transfer('address', {Token: CURRENCY_ID}, amount)
```

### Implementation notes

All assets in Kintsugi and Interlay networks are implemented using [orml](https://github.com/open-web3-stack/open-runtime-module-library).

- Asset implementation: [orml-tokens](https://github.com/open-web3-stack/open-runtime-module-library/tree/master/tokens)
- Cross-chain transfer implementation (XCM): [orml-xtokens](https://github.com/open-web3-stack/open-runtime-module-library/tree/master/xtokens)

?> Querying the `system` account is not supported on Kintsugi or Interlay. Please use the API methods described above to achieve transfers.

