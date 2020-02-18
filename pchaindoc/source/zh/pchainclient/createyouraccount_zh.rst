.. _Create Your Account zh:

===================
创建账户
===================

在运行了PCHAIN之后，您可以创建自己的账户，同时您还可以：

- 转账
- 委托
- 创建子链
- 部署智能合约
- 与智能合约交互

您可以通过以下命令创建账户地址：
:: 
	pchain --datadir=yourdatadir account new

如果你还想

- 成为验证节点挖矿
- 申请成为候选人

你还需要生成bls公私钥对：
:: 
	pchain --datadir=yourdatadir gen_priv_validator youraddress
这个命令会在您的数据目录下自动创建一个pri_validator.json文件。如果您想要挖矿，则需讲该文件复制粘贴到datadir/childid/。然后请重新启动PCHAIN.

最后，请检查下您的数据目录结构：
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
			-priv_validator.json  
			-keystore/          

如果你想在紫莲和主链上同时挖矿，你的目录结构应该是这样的：
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
			-priv_validator.json  
			-keystore/ 
		-child_0/
			-data/  
			-geth/  
			-pchain.ipc
			-priv_validator.json 
			-keystore/ 




