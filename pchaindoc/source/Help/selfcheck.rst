==============================
Check node status step by step
==============================

.. image:: ../_static/Help/nodecheck.png

1.How to check if your node is still running?

Attach to your server, and run command
::
	ps ax|grep pchain

if it returns a string such as
::
	 6931 pts/0    Rl     0:01 /home/ubuntu/pchain/bin/pchain --datadir=~/pchain/.pchain --rpc --rpcapi=eth,web3,admin,tdm,miner,personal,chain,txpool,del --gcmode=archive --verbosity=0 --prune

your pchain is still running. If not, please run
::
	sudo ./pchain/run.sh

2.How to check if your node is caught up to the latest block?

if you wanna check main chain:
::
	cd ~/pchain
	sudo ./bin/pchain attach .pchain/pchain/pchain.ipc
	pi.blockNumber

if you wanna check child chain:
::
	cd ~/pchain
	sudo ./bin/pchain attach .pchain/child_0/pchain.ipc
	pi.blockNumber
it will return the latest block on your node, and then to check if the height is same as our `Monitor <https://monitor.pchain.org>`_.

3.How to check pchain's version?
::
	cd ~/pchain
	./bin/pchain version
it will return the version of pchain, you can check the latest version on our `github <https://github.com/pchain-org/pchain/releases>`_.

Note: if the version of pchain is different from the version in file "~/pchain/version", plz delete the file, the auto-update script will update pchain 10 mins later.

4.How to check if your node is syncing?
if you wanna check main chain:
::
	cd ~/pchain
	sudo ./bin/pchain attach .pchain/pchain/pchain.ipc
	pi.syncing

if you wanna check child chain:
::
	cd ~/pchain
	sudo ./bin/pchain attach .pchain/child_0/pchain.ipc
	pi.syncing

if it return true, your node is syncing now. Also you can type "pi.blockNumber" every min to check if the height is growing continiously. If so, your node is syncing.

5.How to check if my node is validating blocks?

| Go to `piscan <https://piscan.pchain.org/miner.html>`_, enter your address and search, you can check the last block you validated. Usually the last block you validate should be several mins ago. 

6.How to collect logs?

Set verbosity=3 in file "run.sh" and restart pchain, there will be a "log" folder under the same directory you run the "run.sh".