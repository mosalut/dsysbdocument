## 0. Conventions
- This book mentions references to __bitcoin__ or some other cryptocurrencies. Direct jump links are provided without repetition.
- The smallest unit in this book remains consistent with __bitcoin__ (__satoshi__).
- All "transactions" or "tx" in this book refer to operations, not financial trades.

## 1. Introduction
__DSYSB__ (_Decentral System Blockchain_) is a decentralized cryptocurrency system based on blockchain. It is similar to __bitcoin__ and also uses __Ethereum__’s account model. __DSYSB__ centers around decentralized asset operations. Fungible assets can be seen as currencies, and a currency with a total supply of 1 can be considered an asset (like an _NFT_).

### DSB
_DSB_ is the native system token on the __DSYSB__ chain, similar to ETH on __Ethereum__. Its unit is _DSB_, and the smallest unit is _satoshi_, with 1 _DSB_ = 100,000,000 _satoshi_.

### Asset token
_Asset_ tokens are also denominated in _DSB_. The smallest unit depends on its _decimals_ field.

If _decimals_ = 1, then 1 _DSB_ = 10 _satoshi_.

If _decimals_ = 2, then 1 _DSB_ = 100 _satoshi_, and so on.

### Differences between DSYSB and Bitcoin：
1. __Bitcoin__ is a cryptocurrency. __DSYSB__ is a system that natively supports coin issuance and transfer without relying on smart contracts.
2. __Bitcoin__ uses _UTXO_. __DSYSB__ uses an account model.
3. __Bitcoin__ supports multi-input and multi-output transfers. __DSYSB__ supports only one sender and one recipient per transfer transaction. (__DSYSB__ uses tasks to simulate multi-party transactions)

### Differences between DSYSB and Ethereum：
1. __Ethereum__ uses smart contracts. __DSYSB__ uses tasks.
2. __Ethereum__'s tokens (_ERC20_, _ERC721_) are variables in contracts. __DSYSB__ uses assets directly; fungible assets are cryptocurrencies and do not require contracts.
3. Token transfers on __Ethereum__ require contract function calls. __DSYSB__ uses direct commands for all asset transfers.

## 2. Consensus and Proof of Work
Proof of Work (_PoW_) was introduced in __bitcoin__. Here are additional details.

Nodes attempt to compute a value that meets a target difficulty to earn rewards. Since the final value cannot be reverse-engineered, it proves computational work.
This process, called mining, is a point of synchronization across the network. However, due to the _Byzantine Generals Problem_, forks may occur.
DSYSB follows __bitcoin__’s rule: a transaction is irreversible after 6 confirmations.

### How it Works
- _Problem Complexity_: Miners must find a hash meeting certain criteria (e.g., leading zeros) by hashing the block header.
- _Competition_: All miners compete to find a valid hash. The winner adds the next block.
- _Reward_: The successful miner earns crypto and transaction fees.

### Difficulty Adjustment
To maintain stability, __DSYSB__ adjusts difficulty every 1024 blocks to target a 10-minute block time.
See: [__bitcoin__ whitepaper](https://bitcoin.org/bitcoin.pdf)

## 3. Account Model
__DSYSB__ uses __Ethereum__’s account model.

### Model Components
- __Balance__: Native token balances are stored as unsigned 64-bit integers.
- __Custom Assets__: Accounts may hold multiple assets, each with a unique hex ID and balance.
- __Replay Protection__: Each account has a nonce to track transaction count for uniqueness.

Serialization is used for storage and transfer, and deserialization restores the account object. Byte arrays store the balance, each asset’s ID and balance, and nonce in little-endian order.

SHA-256 hashes accounts for integrity and uniqueness, preventing tampering.

## 4. Cryptographic Algorithm
Elliptic Curve Cryptography (_ECC_) is a public key system offering high security with shorter keys (e.g., 256-bit _ECC_ ≈ 3072-bit RSA). It is ideal for limited-resource devices and supports digital signatures, key exchange, and identity verification.

See：[__bitcoin__ whitepaper](https://bitcoin.org/bitcoin.pdf)

## 5. Block Structure
This model aims to store and verify decentralized asset transactions using efficient block headers and bodies.

### Block Header and Body
- __Header__: Includes previous hash, current hash, state root, transaction root, difficulty, timestamp, and nonce.
- __Body__: Contains transaction sets and execution support.

Compared to bitcoin, DSYSB adds a state root and transaction root for improved scalability and complexity support. Headers and bodies are serialized for storage and parsing using little-endian byte order.

Blocks can be queried by index over HTTP to retrieve data.

## 6. Transactions
_Transactions_ define how digital assets are handled and provide methods for hashing, encoding, decoding, computing, verifying, and string representation.

### Transaction Types
- _coinbase_: Rewards miners for maintaining the network. Fees are added to the amount.
- _create_: Issues new assets. Users buy how many blocks the asset can survive. If it expires with no extension, it disappears. In order to prevent the chain from being occupied by garbage, __DSYSB__ believes that if an asset does have value, someone must pay attention to its use. Therefore, when an asset is released, it is necessary to "buy" how many blocks it can be used in the future. If this amount is used up and no one is willing to continue the asset, then the asset will disappear on the chain! This is a very important feature, please be aware of it.
- _transfer_: Transfers existing assets or __DSB__ between users with specified sender, receiver, and amount.
- _exchange_: Atomic swaps between two parties within one transaction.
- _deploy_: Publishes a task (like a simplified smart contract). No calls or permissions exist between tasks. The sender funds the task.
- _call_: Executes a task, possibly changing variables or triggering transfers.
- _extension_: Extends the lifetime (block count) of an asset or a task.

### Fee
TODO

## 7. Wallet Address
Wallet generation, signing, and verification follow __bitcoin__’s method. __DSYSB__ addresses are base58-encoded and always 34 characters starting with _D_.
