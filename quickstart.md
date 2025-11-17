# Quick Start

## System Support
- Linux
- Windows

## Installation

You can either compile from source or use the precompiled binaries

Download links:

| Linux | Windows |
| --- | --- |
| [v1.0.0](https://github.com/mosalut/dsysb/releases/download/v1.0.0/dist_linux_x86_64-v1.0.0.tar.gz) | [v1.0.0](https://github.com/mosalut/dsysb/releases/download/v1.0.0/dist_windows_x86_64-v1.0.0.rar) |
  

_If you download from sources other than the official link, you may get tampered files_

Unzip the downloaded package

- __dsysb__：The main program，Responsible for communicating with other nodes, validating incoming data, and reading/writing to the local data

- __dsysbminer__：Mining program ，un this if you want to mine.

- __dsysbcmd__：Command program，Used to interact with both __dsysb__ and __dsysbminer__ 

- __config__：Configuration file

- __removedatabase__：__Linux__ ，only script that clears blockchain data from the node to prevent accidental wallet deletion，Not needed for__windows__ 

## Starting dsysb

Navigate to the extracted directory and run:

```bash
$ ./dsysb [-network_id=0] -remote_host=<ip:port>
```

\-network\_id specifies which network to join, supporting values 0 – 16
- 0: __Mainnet__ not yet online at the time of writing; default
- 1 - 15: __Testnet__ at present, only testnet 1 is available，others reserved
- 16: __DEVNet__ for developers

_\-remote\_host_，specifies a known node to connect to，Usually, you can join the DSYSB network via the _remote\_hosts_ list in the configuration file.If this list is empty, you must specify a node using -remote_host to join the network.

For more parameters for __dsysb__ , see here(#)

## Starting dsysbminer
If you wish to mine, with __dsysb__ running, open another terminal in the same directory and run:

```bash
$ ./dsysbminer
```

This starts the mining process in the background, but mining won't actually begin until controlled via dsysbcmd to start, stop, pause, or resume.

## Using dsysbcmd

with __dsysb__ running, open another terminal in the same directory and run:

#### Display blockchain height

```bash
$ ./dsysbcmd getindex
```

#### Generate wallet address

```bash
$ ./dsysbcmd newaddresses // If first time, creates wallet database wallet.db
```

#### List addresses

```bash
$ ./dsysbcmd getaddresses // Lists all wallet addresses for the current node
```

#### Start mining

```bash
$ ./dsysbcmd start <wallet address>
```

_start_ requires a miner’s wallet address


#### Stop mining

```bash
$ ./dsysbcmd stop 
```

#### Pause mining

```bash
$ ./dsysbcmd pause
```

#### Resume mining

```bash
$ ./dsysbcmd recover 
```

If you have sufficient DSB or other assets from mining or transfers, you can send them to others.


#### Transfer transaction

```bash
$ ./dsysbcmd createrawtransaction transfer '{"from":"<sender address>","to":"<receiver address>","hier":"<inherit address>","amount":<amount>,"bytePrice":<byte price>}'

$ ./dsysbcmd createrawtransaction transfer '{"from":"D892kxbavZUUmj5DHoVCJAFUWsWMeJCGQY","to":"DBwz7C6u6ggHJXnERzWt2co8yT5gTFtBw5","hier":"<inherit address>","amount":10000000,"bytePrice":10}'
```

- When you run the above command, it outputs the raw transaction data --the binary representation of that transaction.
- _createrawtransaction_  specifies that you want to create a transaction. It can be shortened to _create_
- In the command, the content enclosed in single quotes is, in fact, a JSON data object
- In the command, all options or parameters outside of the JSON are written in lowercase. All JSON field names use the camelCase naming convention, such as bytePrice.
- Field order in JSON does not matter. JSON parsers will correctly interpret the data regardless of the sequence.
- All numerical inputs and outputs in the command are expressed in satoshis --the smallest unit of Bitcoin，amount: total value to be transferred, in satoshis. bytePrice: fee rate per byte, in satoshis.
- _transfer_ indicates that the transaction type is a fund transfer.
- Each transaction requires a _bytePrice_ field, which specifies the price per byte the sender is willing to pay for the transaction.
- If the _JSON_ data does not include an _assetId_ ，field, the transaction will transfer __DSB__ by default. Otherwise, it will transfer the specified asset.

```bash
	bytePrice × transaction size (bytes) = fee
```

- Every transaction requires a _hier_ address. In __DSYSB__, this is called the inheritance address, which is used to inherit all assets from another address. It functions similarly to a change address in __bitcoin__, helping to avoid continued use of wallet addresses whose public keys have been exposed. In some cases, the security of a given wallet address may not be important — for example, if you frequently use the same wallet address to publish tasks, and the address holds only a small amount of _DSB_or other assets. For convenience, if the hier field is omitted in the JSON payload, the system will automatically use the value from the _from_ field as the _hier_ address：

```bash
// hier = from
$ ./dsysbcmd createrawtransaction transfer '{"from":"<sender address>","to":"<receiver address>","to","amount":<amount>,"bytePrice":<byte Price>}'

// hier = from
$ ./dsysbcmd createrawtransaction transfer '{"from":"D892kxbavZUUmj5DHoVCJAFUWsWMeJCGQY","to":"DBwz7C6u6ggHJXnERzWt2co8yT5gTFtBw5","amount":10000000,"bytePrice":10}'
```

miners will sort the transactions in the mempool in descending order based on the fee per byte, and then package them into a block.

#### Decode the Transaction

```bash
$ ./dsysbcmd decoderawtransaction <transaction data>
```

- _decoderawtransaction_ can be shortened to_decode_
- The output will contain details such as the_txid_of the transaction.
- At this stage, the signature information will all be 0

#### Sign the Transaction

```bash
$ ./dsysbcmd signrawtransaction <transaction data>
```

- _signrawtransaction_ can be shortened to_sign_
- It will display the signed transaction data

If you now use _decoderawtransaction_ to decode the signed transaction data, you will see that the _signature_ field already contains a non-zero value.  

```bash
$ ./dsysbcmd decode <signed_transaction_data>
```

Note: When copying transaction data, make sure not to include spaces, line breaks, or other extra characters.

Finally, we send the signed transaction data to the main program. If the main program validates it successfully, it will broadcast the transaction to the network, and other nodes will receive and verify it.

```bash
$ ./dsysbcmd sendrawtransaction <signed_transaction_data>
```

- _sendrawtransaction_ can be shortened to _send_

If no output appears at this point, you have successfully sent a transaction.

Now, let’s proceed to create an asset.

#### Create an Asset Transaction

```bash
$ ./dsysbcmd create create '{"name":"<5-10 letters or digits>","symbol":"<3-5 letters or digits>","decimals":<number of decimal places>,"totalSupply":<total supply>,"from":"<creator_wallet_address>","price":<unit price per block>,"blocks":<lifespan in blocks>,"bytePrice":20}'

$ ./dsysbcmd create create '{"name":"aaaaaa","symbol":"AAA","decimals":8,"totalSupply":1000000000000000,"price":10,"blocks":10000,"from":"D892kxbavZUUmj5DHoVCJAFUWsWMeJCGQY","bytePrice":1}'
```

-The first _create_  is the shortened form of _createrawtransaction_ ，The second _create_ specifies that the transaction type is "create asset".
- From the asset's field values, an _assetId_ can be calculated，If an_assetId_ already exists on the blockchain, it means an identical asset has already been created, and the new creation request will fail.
- If no restriction is placed on asset lifespan, many unused or forgotten assets would remain on the chain forever, occupying space and becoming blockchain "garbage".
- _blocks_  defines the lifespan of the asset, measured in blocks，blocks: 10,000 means that starting from the asset's inclusion on the chain, after 10,000 blocks, it will expire unless someone chooses to extend its lifespan. Historical records of the asset will still remain in earlier blocks even after it expires.
- _price_ represents the payment per block for maintaining the asset's lifespan,creating the asset requires both a transaction fee for miners and a lifespan payment in _DSB_,Each time a block is produced, the miner who records it receives the asset’s price as a reward — and this can happen up to 10,000 times (based on the asset’s blocks value).
The asset creator does not pay the full lifespan fee all at once during creation.
At creation time, no blocks have yet been consumed, so the miner who includes the asset creation transaction does not receive any lifespan fee at that moment.
Only subsequent block producers receive the ongoing life-cycle rewards.
- _price_  also sets a minimum fee threshold，Any _bytePrice_ used for transferring_transfer_ this asset must be greater than or equal to the asset's _price_,When extending asset lifespan via _extension_ , the same_price_is applied.
- After the asset is created, the _from_ address (the creator) will initially hold the asset’s totalSupply, as defined in the_JSON_data.

Then, use _signrawtransaction_ and _sendrawtransaction_ to broadcast this transaction.
After a transaction enters the transaction pool, it is not immediately packaged into a block, because the main program is still waiting for more transactions to accumulate in the pool.
When your miner program successfully mines a block, the main node will then package the current transactions in the pool into a new block.A maximum of 511 transactions can be included, since one additional slot is reserved for the coinbase (mining reward) transaction, making a total of 512 transactions per block.
Any remaining transactions will be deferred to later blocks.
After the new block is packaged, it is not instantly added to the blockchain.
The miner program still needs to mine (compute) it — this follows the standard Proof of Work __PoW__ process, which we won’t go into detail here.

Therefore, when you see the miner program displaying that it is currently mining block #10, and you send a transaction at that time, that transaction will be included in block #11 once it is mined.

When block #11 is successfully mined, the miner program will show that it has moved on to block #12, which makes it appear as if your transaction was delayed by one block (from 10 → 12).

Once the asset creation transaction is successfully confirmed on-chain, you can then view and verify it.

#### List Assets

```bash
$ ./dsysbcmd getassets
```

- The _getassets_ command lists all on-chain assets and their corresponding _assetId_ values.

#### View an Asset

```bash
$ ./dsysbcmd getasset <assetId>
```

- The _getassets_ command displays detailed information about a specific asset.

#### View an On-Chain Transaction

```bash
$ ./dsysbcmd gettransaction <txid>
```

#### List Transactions in the Pool

```bash
$ ./dsysbcmd listtransactionpool
```

- _listtransactionpool_ command can be abbreviated as _listtxpool_.
- Once transactions in the pool are packaged into a block, they will be removed from the pool.

#### Asset Transfer

```bash
$ ./dsysbcmd createrawtransaction transfer '{"from":"<sender_address>","to":"<receiver_address>","assetId":<assetId>,"amount":<amoun>,"bytePrice":<byte_price>}'

$ ./dsysbcmd createrawtransaction transfer '{"from":"D892kxbavZUUmj5DHoVCJAFUWsWMeJCGQY","to":"DBwz7C6u6ggHJXnERzWt2co8yT5gTFtBw5","assetId":"121639f97c3b296b67edc208948e4d041bd4755f7a98274d6284d152be4af679","amount":10000000,"bytePrice":10}'
```

- After creating a raw transaction, you must also execute _signrawtransaction_，_sendrawtransaction_ then wait for approximately two blocks for confirmation.

#### All Transaction Types

- _coinbase_: Mining reward
- _create_: Create an asset
- _transfer_: A transfer is a basic blockchain transaction used to move digital assets from one address to another.
- _exchange_: Asset swap
- _deploy_: Deploy a task
- _call_: Call a task
- _extension_: Extend the lifespan of an asset or task

Transactions not mentioned in the Quick Start guide are described in detail in the full tutorial.
