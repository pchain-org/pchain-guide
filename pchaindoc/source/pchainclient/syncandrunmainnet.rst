.. _Sync main chain:

====================
Sync and Run Mainnet
====================

After you install pchain on your computer, you can run 
::
	pchain

to sync mainnet's block and transactions, you should see some outputs look like this:
::
	INFO [05-21|09:47:41.666] Starting PChain...
	INFO [05-21|09:47:41.666] PChain supports large scale block-chain applications with multi-chain
	INFO [05-21|09:47:41.667] Create peer-to-peer node                 instance=pchain/linux-amd64/go1.11.4
	INFO [05-21|09:47:41.667] ethereum.MakeSystemNode
	INFO [05-21|09:47:41.669] Allocated cache and file handles         database=/home/ubuntu/.pchain/pchain/geth/chaindata cache=768 handles=512
	INFO [05-21|09:47:41.692] Writing default main-net genesis block
	INFO [05-21|09:47:41.704] Persisted trie from memory database      nodes=182 size=48.66kB time=1.1982ms gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
	INFO [05-21|09:47:41.705] Initialised chain configuration          config="{PChainId: pchain ChainID: 24160843454325667600331855523506733810605584168331177014437733538279768116753 Homestead: 0 DAO: <nil> DAOSupport: false EIP150: 0 EIP155: 0 EIP158: 0 Byzantium: 0 Constantinople: <nil> Engine: tendermint}"
	INFO [05-21|09:47:41.720] Tendermint (backend) Protocol, add logic here
	INFO [05-21|09:47:41.720] Initialising Ethereum protocol           versions=[64] network=1
	INFO [05-21|09:47:41.720] Loaded most recent local header          number=0 hash=c6ade9…f2f8c3 td=1024
	INFO [05-21|09:47:41.720] Loaded most recent local full block      number=0 hash=c6ade9…f2f8c3 td=1024
	INFO [05-21|09:47:41.720] Loaded most recent local fast block      number=0 hash=c6ade9…f2f8c3 td=1024
	INFO [05-21|09:47:41.721] Regenerated local transaction journal    transactions=0 accounts=0
	INFO [05-21|09:47:41.721] Tendermint (backend) SetBroadcaster: 0xc0001e22d0
	INFO [05-21|09:47:41.721] Tendermint (backend) Protocol, add logic here
	INFO [05-21|09:47:41.732] Allocated cache and file handles         database=/home/ubuntu/.pchain/tx3cache              cache=16  handles=16
	INFO [05-21|09:47:41.737] Starting P2P networking
	INFO [05-21|09:47:43.846] UDP listener up                          self=enode://7b3f6226995c73acfb9f792b8aa73e8c2b1eb35656c9cd7d8c9287c34c0241c34c595d3bb6c7d0b0b7678bf5df0d1e8693bc735bd4a2311e50bd7f4a5d80fd7c@[::]:30308
	INFO [05-21|09:47:43.846] Start Chain: pchain
	INFO [05-21|09:47:43.846] StartChain()->utils.StartNode(stack)
	INFO [05-21|09:47:43.849] RLPx listener up                         self=enode://7b3f6226995c73acfb9f792b8aa73e8c2b1eb35656c9cd7d8c9287c34c0241c34c595d3bb6c7d0b0b7678bf5df0d1e8693bc735bd4a2311e50bd7f4a5d80fd7c@[::]:30308
	INFO [05-21|09:47:43.851] IPC endpoint opened                      url=/home/ubuntu/.pchain/pchain/pchain.ipc
	INFO [05-21|09:47:43.851] Before Load Child Chains, childChainIds is [], len is 0
	INFO [05-21|09:47:43.851] Number of Child Chain to be load - 0
	INFO [05-21|09:47:43.851] Start to Load Child Chain - map[]
	INFO [05-21|09:47:45.011] Block synchronisation started
	...

| It means the pchain running on your computer starts to sync.
If you wanna run it backend, you can run with this command
::
	(./pchain --verbosity=0 &)
After start pchain, it will create a directory to store blockchain data under default datadir directory.


+------------+--------------------------+
| Platform   | Default Datadir Directory| 
+============+==========================+
| Linux      | ~/.pchain                | 
+------------+--------------------------+
| Mac        | ~/Library/Pchain         |
+------------+--------------------------+
| Windows    | %APPDATA%\Pchain         |
+------------+--------------------------+

You can also set datadir to wherever you like by flag --datadir. 

The datadir's structure will look like this:
::
	datadir/
		-chaininfo.db/    
		-config.toml  
		-nodekey    
		-nodes/    
		-tx3cache/
		-pchain/
			-data/  
			-geth/  
			-pchain.ipc 
			-priv_validator.json  //you may not have this file now
			-keystore/             
