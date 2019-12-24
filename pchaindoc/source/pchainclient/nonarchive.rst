=================
Data Reduction
=================

1. Ensure your pchain version is later than v1.2.0
::
	cd ~/pchain/
	./bin/pchain version
	1.2.0
If not, please update from our `Release <https://github.com/pchain-org/pchain/releases>`_. Then, stop monitor and auto-update scripts.
::
	crontab -e
Open it with your familiar editor, you will see something like this:
::
	*/10 * * * * ~/pchain/scripts/updatefile.sh > ~/pchain/scripts/update.log
	*/2 * * * * ~/pchain/scripts/monitor.sh > ~/pchain/scripts/monitor.log
Comment out this two line with symbol '#', and save file.

2. Export chain data

While pchain is running, attach to the console, and run admin.exportChain("filename") to export the chain data. Chain data will be exported under the same directory where you started pchain.

If you wanna export main chain's data, attach to main chain's console and run admin.exportChain("filename").
If you wanna export child chain's data, attach to child chain's console and run admin.exportChain("filename").

This step may take around 10 mins, please be patient.

3. Delete files

Kill pchain first.
::
	sudo killall pchain
Delete all files and directories under ~/pchain/.pchain except pchain/priv_validator.json, pchain/keystore, child_0/priv_validator.json, child_0/keystore, child_0/eth_genesis.json, child_0/genesis.json.

Your datadir should be like this after you delete files:
::
	datadir/
        -pchain/
                -priv_validator.json
                -keystore/
        -child_0/(if you are not running child chain, please ignore this directory)
                -genesis.json
		-eth_genesis.json
                -priv_validator.json
                -keystore/

4. Import chain data

Start pchain with command below:
::
	./pchain --datadir=~/pchain/.pchain --gcmode=full --verbosity=0 --childChain=child_0 --maxpeers=0
Then attach to console, run admin.importChain("filename") to import chain data.

This step may take more than 10 hours, please be patient.

Note: If you are running both main chain and child chain, you must import main chain first. Before import child chain's data, please init child chain first. 
::
	./bin/pchain --datadir=~/pchain/.pchain init ~/pchain/.pchain/child_0/eth_genesis.json child_0

After this step, your local database will store only 128 blocks' state instead of all of the state.

5.Restart pchain

After step 4 finished, please restart pchain with command below:
::
	~/pchain/bin/pchain --datadir=~/pchain/.pchain --rpc --rpcapi=eth,web3,admin,tdm,miner,personal,chain,txpool,del --gcmode=full --verbosity=0 --childChain=child_0 > /dev/null 2>&1 &
You can also use run.sh in the v1.2.0 release to run pchain.





