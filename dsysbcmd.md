# Interactive Command Program
_dsysbcmd_ can interact with dsysb and dsysbminer through commands.

Usage format:

```bash
$ ./dsysbcmd option param1 param2 paramn...
```

### setconnnum
Set the maximum number of P2P connections

parameter:
- Number of connections


### listnodes
List connected nodes.


### listaddresses/getaddresses
List wallet addresses of this node.


### newaddress
Generate a new wallet address


### validateaddress
Validate a wallet address


### exportwallet
Export a wallet address

parameter:
-wallet address


### importwallet
Import a wallet private key

parameter:
- Wallet private key


### createrawtransaction / create
Create a transaction

parameter:
- Transaction type
1. create: Create an asset
2. transfer: A transfer is a basic blockchain transaction used to move digital assets from one address to another.
3. exchange: Exchange assets
4. deploy: Deploy a task
5. call: Call a task
6. extension: Extend the lifecycle of an asset or task
- JSON  string  Example:
```bash
./dsysb createrawtransaction '{"axid":"0xa....","type":"transfer","from":addressF,"to":addressTo,"Amount":100,"assetId":id}' returns a rawtransaction.
```

[JSON field details](json_zh.md)


### decoderawtransaction / decode
Decode a transaction

parameter:
- Transaction raw data string 


### signrawtransaction / sign
Sign a transaction

parameter:
- Transaction raw data string


### sendrawtransaction / send
Send a transaction

parameter:
- Signed transaction raw data string


### getaccount
View account information

parameter:
- Wallet address


### getassets
List assets


### getasset
View asset details.

parameter: 
- Asset ID


### gettasks
List tasks


### gettask
View task details

parameter:
- Task ID


### getstate
View global on-chain state


### getblockchain
View the entire blockchain

parameter:
- Number of blocks to display (optional; default is 10)


### getblockbyindex
Get block details by height

parameter:
- Block height


### getblockbyhash
Get block details by hash

parameter:
- HASH


### gettransaction
Search and display transactions from the most recent n blocks

parameter:
- TXID
- n


### gettxinpool
Search and display a transaction from the transaction pool

parameter:
- TXID


### listtransactionpool / listtxpool
List all transactions in the transaction pool


### getbalance
View balance

parameter:
- Wallet address


### getassetbalance
View asset balance

parameter:
- Wallet address
- Asset ID


### broadcast
Broadcast a message

parameter:
- Message content


### start
Start mining

parameter:
-Wallet address to be used for mining
- Miner program port (optional; default is 8569)


### stop
Stop mining

parameter:
- Miner program port (optional; default is 8569)



### pause
Stop mining

parameter:
- Miner program port (optional; default is 8569)


### recover
Resume mining

parameter:
- Port number to resume the miner program (optional, default is 8569) 


### atbs
Wallet address to byte array

parameter:
- Wallet address


### nidtbs: Asset id or task id to bytes
Convert asset ID or task ID into a byte array

parameter:
- Asset ID or task ID


### help
This document


# 5. Common Issues

1. Failed to send transaction data: If a user creates a transaction and, after decoding, finds the nonce value to be 0，sending will fail. The user must first participate in mining, then re-create and send the transaction.

2. Miner program failed to start: This may be due to issues with the user's dsysb program.

3. Failed to create a personal asset: If the user's total asset amount is less than the required amount in satoshis, creation will fail, possibly without specific error logs.

4. Special characters cause creation failure: Personal asset creation will fail if special characters are used.

5. Incorrect transaction encoding/decoding: If an incorrect transaction is encoded or decoded，`decoderawtransaction` will return an error. Verify the accuracy of transaction data.

6. Special characters cause data corruption: Using certain special characters in asset creation may corrupt data; use English letters for naming.

7. Transfer failed: Transfers will fail if `from` and `to` addresses are the same.

8. Block search failed: Searching will fail if the input block does not exist or is less than 0 .

9. Block search by hash failed: Searching will fail if the provided hash is incorrect.

10. Duplicate asset creation failed: Attempting to create an identical asset will fail.

11. Level DB Not Found: This error means the corresponding key was not found in the database.
