====================
Sync and Run Testnet
====================

After you install pchain on your computer, you can run 
::
	pchain --testnet

to sync testnet's block and transactions, you should see some outputs look like this:
::
	INFO [05-23|09:22:04.736] Starting PChain...
	INFO [05-23|09:22:04.737] PChain supports large scale block-chain applications with multi-chain
	INFO [05-23|09:22:04.738] Create peer-to-peer node                 instance=pchain/linux-amd64/go1.11.4
	INFO [05-23|09:22:04.738] ethereum.MakeSystemNode
	INFO [05-23|09:22:04.740] Allocated cache and file handles         database=/home/ubuntu/.pchain/testnet/geth/chaindata cache=768 handles=512
	INFO [05-23|09:22:04.748] Writing default main-net genesis block
	INFO [05-23|09:22:04.749] Persisted trie from memory database      nodes=11 size=3.35kB time=47.682µs gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
	INFO [05-23|09:22:04.749] Initialised chain configuration          config="{PChainId: testnet ChainID: 98411113441374360242664033072086975431386585974419604025805951356851497696398 Homestead: 0 DAO: <nil> DAOSupport: false EIP150: 0 EIP155: 0 EIP158: 0 Byzantium: 0 Constantinople: <nil> Engine: tendermint}"
	INFO [05-23|09:22:04.762] Tendermint (backend) Protocol, add logic here
	INFO [05-23|09:22:04.762] Initialising Ethereum protocol           versions=[64] network=2
	INFO [05-23|09:22:04.762] Loaded most recent local header          number=0 hash=b92288…40abe6 td=1024
	INFO [05-23|09:22:04.762] Loaded most recent local full block      number=0 hash=b92288…40abe6 td=1024
	INFO [05-23|09:22:04.762] Loaded most recent local fast block      number=0 hash=b92288…40abe6 td=1024
	INFO [05-23|09:22:04.762] Regenerated local transaction journal    transactions=0 accounts=0
	INFO [05-23|09:22:04.762] Tendermint (backend) SetBroadcaster: 0xc0002302d0
	INFO [05-23|09:22:04.762] Tendermint (backend) Protocol, add logic here
	INFO [05-23|09:22:04.764] Allocated cache and file handles         database=/home/ubuntu/.pchain/tx3cache               cache=16  handles=16
	INFO [05-23|09:22:04.766] Starting P2P networking
	INFO [05-23|09:22:06.901] UDP listener up                          self=enode://7b3f6226995c73acfb9f792b8aa73e8c2b1eb35656c9cd7d8c9287c34c0241c34c595d3bb6c7d0b0b7678bf5df0d1e8693bc735bd4a2311e50bd7f4a5d80fd7c@[::]:30308
	INFO [05-23|09:22:06.902] Start Chain: testnet
	INFO [05-23|09:22:06.902] StartChain()->utils.StartNode(stack)
	INFO [05-23|09:22:06.907] IPC endpoint opened                      url=/home/ubuntu/.pchain/testnet/pchain.ipc
	INFO [05-23|09:22:06.907] Before Load Child Chains, childChainIds is [child_0], len is 1
	INFO [05-23|09:22:06.908] Number of Child Chain to be load - 0
	INFO [05-23|09:22:06.908] Start to Load Child Chain - map[]
	INFO [05-23|09:22:06.908] RLPx listener up                         self=enode://7b3f6226995c73acfb9f792b8aa73e8c2b1eb35656c9cd7d8c9287c34c0241c34c595d3bb6c7d0b0b7678bf5df0d1e8693bc735bd4a2311e50bd7f4a5d80fd7c@[::]:30308
	INFO [05-23|09:22:16.908] Block synchronisation started
	...

| It means the pchain running on your computer starts to sync.
If you wanna run it backend, you can run with this command
::
	(./pchain --testnet --verbosity=0 &)
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
		-testnet/
			-data/  
			-geth/  
			-pchain.ipc  
			-keystore/             
