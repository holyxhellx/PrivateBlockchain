# PrivateBlockchain (MAC-terminal)
This is a test environment for a Private Blockchain using get

- Create genesis.json file:
vi /genesis.json

- Insert values (save: ecs + :wp):
{ "nonce": "0x0000000000000042", 
  "timestamp": "0x0", 
  "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000", 
  "extraData": "0x0", 
  "gasLimit": "0x8000000", 
  "difficulty": "0x400", 
  "mixhash": "0x0000000000000000000000000000000000000000000000000000000000000000", 
  "coinbase": "0x3333333333333333333333333333333333333333", 
  "alloc": { 
  }
}


This is the 1. node/blockchain
- Initialise the 1. node:
geth --datadir ../PrivateBlockchain/node1 init ../PrivateBlockchain/genesis.json

- Start the 1. node:
geth --datadir ../PrivateBlockchain/node1 --networkid 1234 console 2>console.log

- Create Account if you need to have a miner (password use: 12345)
personal.addAccount()


This is the 2. node/blockchain
- Initialise the 2. node:
geth --datadir ../PrivateBlockchain/node2 init ../PrivateBlockchain/genesis.json

- Start on a different port and specify networkid:
geth --datadir ../PrivateBlockchain/node2 --port 30304 --nodiscover --networkid 1234 console 2>console.log

- Collect the admin.nodeInfo "enode" from the 2. node and copy it to admin.addPeer([enode]) into the 1. node.

# Valuable API keys in "geth":
Miner start/stop
- miner.start([number])  ,   miner.stop()

Get miner id:
- eth.getBlock(eth.blockNumber).miner  
returns: personalAccountId (inspect by personal.listAccounts)

Get miner balance:
- eth.getBalance(eth.getBlock(eth.blockNumber).miner)
returns: personalAccoint

- admin.nodeInfo, admin.peers, admin.addPeer
- personal.newAccount
- eth.blockNumber, eth.getBlock([number]), eth.gethBalance([account adress])

# The underlying database inspection - Require both nodes running in terminal
Start-path: blockchain (node1/geth/chaindata)

1. node:
eth.getBlock([number])
- get hashValue

2. node:
eth.getBlock([number])
- get hashValue 

The hashVaules will be the same, even though the underlying file inspection showed difference.
