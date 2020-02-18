.. _Sync child chain zh:

========================
同步并运行子链
========================

PCHAIN目前有一条子链1，用户可参与挖矿。参与方式和参与主链的挖矿机制是一样的。但是在参与之前，需要先完成子链1 的同步和运行。

同时在开始运行子链之前，请先完成主链的同步与运行。

首先，你要获得子链的配置文件（`config file <https://github.com/pchain-org/pchain/releases/download/v1.0.01/child_0_config.tar.gz>`_），一共有3个文件：
:: 
	ubuntu@ip-172-31-12-155:~/child_0_config$ ls
	eth_genesis.json  genesis.json  run.sh
2个JSON 文件需要复制粘贴到你的数据目录下（yourdatadir/.pchain/child_0/）, 您要自建一个child_0的目录。
::
	mkdir -p yourdatadir/.pchain/child_0/
	cp ~/child_0_config/*.json yourdatadir/.pchain/child_0/
然后，您需要将子链初始化
::
	pchain --datadir=yourdatadir init yourdatadir/child_0/eth_genesis.json child_0
输出的结果如下:
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
完成后，您通过flag-childChain=child_0重新启动并运行pchain ,以此来同步子链。

您可以再检查下您的数据目录结构
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


