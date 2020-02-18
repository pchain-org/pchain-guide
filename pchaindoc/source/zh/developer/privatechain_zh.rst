=======================
用pchain搭建私链
=======================

| 备注：以下例子的步骤全都在privatetest文件夹下进行，例子中的datadir为privatetest/.pchain，pchain的可执行文件放在了privatetest/bin/下
| 注意：若不指定datadir，则默认~/.pchain为datadir，若指定了datadir，请保持所有指令的datadir一致

1. 生成eth_genesis.json
运行此步骤pchain会为用户生成一个随机地址的keystore和priv_validator.json，并用此随机地址生成eth_genesis.json.eth_genesis.json中是创世块的信息，包含了创世块中地址的初始余额和抵押。

命令：
::	
	ubuntu@ip-172-31-11-28:~/privatetest$ ./bin/pchain --datadir=.pchain init_eth_genesis "{10000000000000000000000000000,1000000000000000000000000}" //大括号中的第一个参数是该随机地址的初始余额，第二个参数是该随即地址的初始抵押
	INFO [01-13|06:28:16.284] this is init_eth_genesis
	INFO [01-13|06:28:17.386] createPriValidators                      account:=0x5C1Fac44C7827e55364543744556c13392c883a5 pwd:=pchain
	ubuntu@ip-172-31-11-28:~/privatetest$ cd .pchain/
	ubuntu@ip-172-31-11-28:~/privatetest/.pchain$ cd pchain/
	ubuntu@ip-172-31-11-28:~/privatetest/.pchain/pchain$ ls //可以看到.pchain/pchain目录下生成了priv_validator.json和eth_genesis.json
	data  eth_genesis.json  keystore  priv_validator.json
	ubuntu@ip-172-31-11-28:~/privatetest/.pchain/pchain$ cat priv_validator.json
	{
	    "address": "5C1FAC44C7827E55364543744556C13392C883A5",
	    "consensus_priv_key": [
	            4,
	            "C2AAB7E0D1C636133EB49AECCC9A390FD70AD615BAD2BDB6A8D2352F504DE682"
	    ],
	    "consensus_pub_key": [
	            4,
	            "6BA273E17A86146DA9A27B591F01724ABADC4F67EB8DFCAF70EF9A6CC858222D1EEAC8600842F5EA05A153B946479FA25A4C2410E78D002EED2F8736B003E1AA4F55311D1160C415DC21BEAC0994D4903A97A14731610F02F88CF2403B470EC98786B99230CC90771C9C63C92929C15280A8C23BD4280E22F77A26907E47140A"
	    ]
	}
	ubuntu@ip-172-31-11-28:~/privatetest/.pchain/pchain$ ll keystore/ //可以看到keystore文件夹下生成的存储了私钥的加密文件，此加密文件的默认密码是“pchain”
	total 16
	drwx------ 2 ubuntu ubuntu 4096 Jan 13 06:28 ./
	drwx------ 4 ubuntu ubuntu 4096 Jan 13 06:28 ../
	-rw------- 1 ubuntu ubuntu  491 Jan 13 06:28 UTC--2020-01-13T06-28-16.285283099Z--5c1fac44c7827e55364543744556c13392c883a5

2. 生成genesis.json
运行此步骤pchain会根据第1步中生成的eth_genesis.json来生成genesis.json，该文件包含了pchain运行时初始的共识信息

命令：
::
	ubuntu@ip-172-31-11-28:~/privatetest$ ./bin/pchain --datadir=.pchain init .pchain/pchain/eth_genesis.json
	INFO [01-13|06:32:21.112] init_eth_blockchain 0 with dbPath: .pchain/pchain/geth/chaindata
	INFO [01-13|06:32:21.112] Allocated cache and file handles         database=.pchain/pchain/geth/chaindata cache=16.78mB handles=16
	INFO [01-13|06:32:21.125] init_eth_blockchain 1
	INFO [01-13|06:32:21.125] init_eth_blockchain 2
	INFO [01-13|06:32:21.127] Writing custom genesis block
	INFO [01-13|06:32:21.127] Persisted trie from memory database      nodes=1 size=305.00B time=49.064µs gcnodes=0 gcsize=0.00B gctime=0s livenodes=1 livesize=0.00B
	INFO [01-13|06:32:21.127] init_eth_blockchain end
	INFO [01-13|06:32:21.127] successfully wrote genesis block and/or chain rule set: 665d8a99cdd69faf209bdb6a92efd498bf1a99e3b195b6d10478d393f02229f1
	INFO [01-13|06:32:21.127] Database closed                          database=.pchain/pchain/geth/chaindata
	INFO [01-13|06:32:21.128] checkAccount(), coinbase is 0000000000000000000000000000000000000000
	INFO [01-13|06:32:21.128] checkAccount(), address is 5c1fac44c7827e55364543744556c13392c883a5, balance is 10000000000000000000000000000, amount is 1000000000000000000000000
	ubuntu@ip-172-31-11-28:~/privatetest$ cd .pchain/pchain/
	ubuntu@ip-172-31-11-28:~/privatetest/.pchain/pchain$ ls //可以看到genesis.json已经生成
	data  eth_genesis.json  genesis.json  geth  keystore  priv_validator.json
	ubuntu@ip-172-31-11-28:~/privatetest/.pchain/pchain$ cat genesis.json //可以看到genesis.json中的validator与第一步中的地址对应
	{
	        "chain_id": "pchain",
	        "consensus": "pos",
	        "genesis_time": "2020-01-13T06:32:21.128149875Z",
	        "reward_scheme": {
	                "total_reward": "0xfb0c9ff7abf3b85f800000",
	                "reward_first_year": "0x1f6193fef57e770bf00000",
	                "epoch_no_per_year": "0xc",
	                "total_year": "0x17"
	        },
	        "current_epoch": {
	                "number": "0x0",
	                "reward_per_block": "0x10ed3d42c506b2bf",
	                "start_block": "0x0",
	                "end_block": "0xa0668",
	                "validators": [
	                        {
	                                "address": "0x5c1fac44c7827e55364543744556c13392c883a5",
	                                "pub_key": "0x6BA273E17A86146DA9A27B591F01724ABADC4F67EB8DFCAF70EF9A6CC858222D1EEAC8600842F5EA05A153B946479FA25A4C2410E78D002EED2F8736B003E1AA4F55311D1160C415DC21BEAC0994D4903A97A14731610F02F88CF2403B470EC98786B99230CC90771C9C63C92929C15280A8C23BD4280E22F77A26907E47140A",
	                                "amount": "0xd3c21bcecceda1000000",
	                                "name": "",
	                                "epoch": "0x0"
	                        }
	                ]
	        }
	}

3. 启动pchain
编辑一个pchain启动脚本，将下面的内容复制到run.sh中，保存后退出。此文件应存放在privatetest目录下，注意networkid不要填写小于3的数字，否则将连接到pchain主网。
::
	#!/bin/bash
	~/privatetest/bin/pchain --datadir=~/privatetest/.pchain --rpc --rpcapi=eth,web3,admin,tdm,miner,personal,chain,txpool,del --gcmode=full --verbosity=0 --networkid=200 > /dev/null 2>&1 &

然后运行该脚本。

4. 连接至pchain的console
确认pchain启动以后，可以连接到pchain的console查看出块情况。
命令：
::
	ubuntu@ip-172-31-11-28:~/privatetest$ ./bin/pchain attach .pchain/pchain/pchain.ipc
	Welcome to the Pchain JavaScript console!

	instance: pchain/linux-amd64/go1.10.3
	coinbase: 0x5c1fac44c7827e55364543744556c13392c883a5
	at block: 20 (Mon, 13 Jan 2020 06:35:22 UTC)
	 datadir: /home/ubuntu/privatetest/.pchain/pchain
	 modules: admin:1.0 chain:1.0 debug:1.0 del:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 pi:1.0 rpc:1.0 tdm:1.0 txpool:1.0 web3:1.0

	> eth.blockNumber
	24
	> eth.blockNumber
	26
	> eth.blockNumber
	28

如果看到blockNumber不断增长，说明pchain正在正常出块，可以进行后续操作。
