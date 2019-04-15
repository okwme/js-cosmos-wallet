# Javascript cosmos wallet library

Created using [typescript-library-starter](https://github.com/alexjoverm/typescript-library-starter).

Example Usage:
```javascript

const axios = require('axios')
const {
  // createCosmosAddress,
  sign,
  // createSignature,
  // createSignMessage,
  generateWalletFromSeed,
  // generateSeed,
  // generateWallet,
  createSignedTx
  // createBroadcastBody
} = require('js-cosmos-wallet')

async submitTransaction(tx) {
  const wallet = generateWalletFromSeed(process.env.MNEMONIC)
  let requestMetadata = await getMetadata()
  requestMetadata.chain_id = process.env.CHAIN_ID
  tx = createSignedTx(tx, sign(tx, wallet, requestMetadata))
  let body = {
    tx,
    return: 'block'
  }
  // send tx
  return await axios
    .post(
      restEndpoint + '/txs',
      body
    )
}

async function getMetadata () {
  let response = await axios.get(restEndpoint + '/auth/accounts/' + process.env.ADDRESS)
  return response.data.value
}

```
