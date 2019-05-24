========================
Sync and Run Child Chain
========================

Pchain have one child chain now and you can join to mining, the process is same with join the main chain's validators. But at first you need to sync and run child chain.

Before you start to sync child chain, make sure you have install pchain and sync main chain.

First, you need to get child chain's `config file <https://github.com/pchain-org/pchain/releases/download/v1.0.01/child_0_config.tar.gz>`_. There are three files in it :
:: 
	ubuntu@ip-172-31-12-155:~/child_0_config$ ls
	eth_genesis.json  genesis.json  run.sh
The two json file should copy to yourdatadir/.pchain/child_0/, you need to make the directory child_0 yourself.
::
	mkdir -p yourdatadir/.pchain/child_0/
	cp ~/child_0_config/*.json yourdatadir/.pchain/child_0/
Then you need to initialize child chain
::
	pchain --datadir=yourdatadir init yourdatadir/child_0/eth_genesis.json child_0
You will see some output look like this:
::
	INFO [05-23|10:12:51.743] init_eth_blockchain 0 with dbPath: .pchain/child_0/geth/chaindata
	INFO [05-23|10:12:51.743] Allocated cache and file handles         database=.pchain/child_0/geth/chaindata cache=16 handles=16
	INFO [05-23|10:12:51.748] init_eth_blockchain 1
	INFO [05-23|10:12:51.748] init_eth_blockchain 2
	INFO [05-23|10:12:51.748] Writing custom genesis block
	INFO [05-23|10:12:51.749] Persisted trie from memory database      nodes=8 size=2.68kB time=54.136µs gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
	INFO [05-23|10:12:51.749] init_eth_blockchain end
	INFO [05-23|10:12:51.749] successfully wrote genesis block and/or chain rule set: 0bb3cd96500c814d39901c120ec2a78385781a58ce5bd6ed1a272b4ee5cb8435
	INFO [05-23|10:12:51.749] Database closed                          database=.pchain/child_0/geth/chaindata
	INFO [05-23|10:12:51.750] priv_validator_file not exist, probably you are running in non-mining mode
After this you should restart pchain and run pchain with flag --childChain=child_0 to sync child chain.

Now please check your datadir's structure:
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
			-priv_validator.json //you may not have this file now  
			-keystore/ 
		-child_0/
			-data/  
			-geth/  
			-pchain.ipc
			-priv_validator.json //you may not have this file now 
			-keystore/ 


