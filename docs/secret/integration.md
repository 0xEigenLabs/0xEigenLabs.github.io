## Integration with your DApps

It's easy to integrate DApps with EigenSecret via [SecretSDK](https://0xeigenlabs.github.io/eigen-secret/classes/sdk.SecretSDK.html). To initialize the SecretSDK instance, you need ,

```
user: ethers.Signer = <your address>
const signature = await signEOASignature(user, rawMessage, user.address, timestamp);
const ctx = new Context(
  alias,
  user.address,
  rawMessage,
  timestamp,
  signature
);
const contractJson = require(defaultContractFile);

let secretSDK = await SecretSDK.initSDKFromAccount(
    ctx, defaultServerEndpoint, password, user, contractJson, defaultCircuitPath, defaultContractABI
);
```
The password is to encrypt your L2 account currently, but will be deprecated and replaced by Google Drive, or external TSS key service to host in the next version.


The SecretSDK provides quite simple account and transaction interface.

* Account: the [create](https://0xeigenlabs.github.io/eigen-secret/classes/sdk.SecretSDK.html#createAccount), [migrate](https://0xeigenlabs.github.io/eigen-secret/classes/sdk.SecretSDK.html#migrateAccount) and [update](https://0xeigenlabs.github.io/eigen-secret/classes/sdk.SecretSDK.html#updateAccount) interface are used to create a new L2 account, change account key and change signing key correspondingly.
* Transaction: the [deposit](https://0xeigenlabs.github.io/eigen-secret/classes/sdk.SecretSDK.html#deposit), [send](https://0xeigenlabs.github.io/eigen-secret/classes/sdk.SecretSDK.html#send) and [withdraw](https://0xeigenlabs.github.io/eigen-secret/classes/sdk.SecretSDK.html#withdraw) are used to send asset from L1 to L2, L2 to L2 and L2 to L1 correspondingly.

Check out [tasks](https://github.com/0xEigenLabs/eigen-secret/tree/main/tasks) and learn how to use the interfaces.
