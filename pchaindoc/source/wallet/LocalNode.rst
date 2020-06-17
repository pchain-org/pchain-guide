.. _Local Node Mode:

Local Node Mode
===============

Before using the local node mode of PIWallet, make sure you have done things bellow:

- :ref:`Installed pchain<Installation>`
- Sync to the latest height (you can check by `Monitor <http://monitor.pchain.org/>`_)
- :ref:`Create Your Account`
- opened rpc (run pchain with flag `--rpc --rpcapi=eth,web3,admin,debug,tdm,miner,personal,chain,txpool,del --rpcaddr=0.0.0.0`)
- opened rpc port to your local ip 
- transport keystore file to your datadir

Important: 
Pchain RPC's default port is 6969, remember open your port 6969 **ONLY** to your local ip and **DO NOT** keep your account unlock for long time (the keystore file should be copied to datadir/CHIAN_ID/keystore/ if you wanna send **any** transaction under local node mode)!!! 

First, set the RPC URL in wallet. The RPC URL is http://yourserverip:rpcport/chainid, so suppose you are running pchain on a machine which ip is 111.222.333.444, and you open rpc with pchain default rpc port, and you wanna interact with main chain, the RPC URL should be http://111.222.333.444:6969/pchain. If you wanna interact with child chain which chain id is child_0, the RPC URL should be http://111.222.333.444:6969/child_0.

.. image:: ../_static/wallet/localnode/seturl.jpg

After this, PIWallet will read the chain state to wallet.

Note: If you wanna send any transation by local node mode, you should transport your keystore to teh machine which running pchain, and your datadir should look like this:
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

   localnode/Epoch
   localnode/Candidate