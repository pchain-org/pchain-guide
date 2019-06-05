.. _Create Your Account:

===================
Create Your Account
===================

After running pchain, sooner or later you will want to create your own account. 
If you wanna 

- transfer PI
- delegate
- create a child chain
- deploy smart contrat
- interact with smart contract

you will only need to generate an address.
:: 
	pchain --datadir=yourdatadir account new
This command will generate a keystore file under your datadir, the file name usually start with "UTC". We suggest you to keep this file on your local computer or import it to PIWallet.

If you wanna also

- become a validator to mining
- apply candidates

you will also need to generate bls keys for mining.
:: 
	pchain --datadir=yourdatadir gen_priv_validator youraddress
This command will generate a priv_validator.json file under your datadir. This file should copy to the datadir/chainid/ if you wanna mining, and after that you should **restart** pchain.

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
			-priv_validator.json  
			-keystore/          

If you also running child chain and would like to mining on both main chain and child chain, your datadir's structure should look like this:
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




