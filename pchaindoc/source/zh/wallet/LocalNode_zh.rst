.. _Local Node Mode zh:

Local Node Mode
===============

在使用PIWallet的本地local node mode之前，请确保您已完成以下操作：
 
- 安装了pchain :ref:`Installed pchain<Installation zh>`
- 同步到最新高度（您可以通过监视器monitor检查）(`Monitor <http://monitor.pchain.org/>`_)
- 已创建帐户地址 :ref:`Create Your Account zh`
- 已打开RPC (run pchain with flag `--rpc --rpcapi=eth,web3,admin,debug,tdm,miner,personal,chain,txpool,del --rpcaddr=0.0.0.0`)
- 开放您本地IP的rpc端口
- 将keystore文件传输到您的数据目录

请注意：Pchain RPC的默认端口是6969，因此只需将6969端口开放给您的本地IP即可。请不要将您的账户长时间处于解锁状态（如果您想在local node 模式下发送交易，请将keystore文件应该复制到datadir / CHIAN_ID / keystore /）！

首先，在钱包中设置RPC URL。RPC URL是 http://yourserverip:rpcport/chainid, 因此若你在一台ip为111.222.333.444的机器上运行pchain，用pchain默认的rpc端口打开rpc，此时与主链RPC进行交互的URL应为： http://111.222.333.444:6969/pchain。
若您想与链ID为child_0的子链进行交互，则RPC URL应为http://111.222.333.444:6969/child_0。

.. image:: ../../_static/wallet/localnode/seturl.jpg

之后，PIwallet 会读链上的状态。

注意： 若您想通过local node 模式进行转账交易，请将keystore 传输至运行pchain 的机器上，且您的数据目录应类似于：

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
			-keystore/   //you should put your keystore file under here
		-child_0/
			-data/  
			-geth/  
			-pchain.ipc
			-priv_validator.json 
			-keystore/	 //you should put your keystore file under here

.. toctree::
   :maxdepth: 1
   :caption: Contents:

   localnode/Epoch_zh