.. _Installation:

================
Installation
================

This tutorial is going to use pre-built binaries. For you to get started as quickly as possible this is the best option. Building from source is an option, but will set you back an hour or more and you may encounter build errors. If you insist building from source, please go to our `github page <https://github.com/pchain-org/pchain>`_.

Here is our system :ref:`system requirement <Requirement>` and you should open port 30308 tcp&udp for pchain's p2p network.

------
Ubuntu
------

- Install from AWS Marketplace
You can install from :ref:`AWS Marketplace <AWS>`

- Install from release
If you wanna become validator, we recommend you to install from release, the latest version can be find from `here <https://github.com/pchain-org/pchain/releases>`_. And we have a step by step `guide <https://github.com/pchain-org/pchain/wiki/Install-pchain-from-release>`_  to help you install pchain from release and will help you set up auto-upgrade scripts.

- Install from PPA
You can follow the steps bellow to install pchain from PPA:
::
	sudo apt update
	sudo apt upgrade
	sudo apt install software-properties-common
	sudo add-apt-repository -y ppa:pchainorg/pchain
	sudo apt update
	sudo apt install pchain

You should now be able to check the different options and commands with 'pchain --help'.
Upgrade the latest version of 'pchain'
::
	sudo apt update
	sudo apt dist-upgrade

---------
Mac OS X
---------
You can use our Homebrew tap to install pchain. If you don't have Homebrew, install it first

Then run the following commands to add the tap and install pchain:
::
	brew tap pchain-org/pchain
	brew install pchain

Upgrade the latest version of 'pchain'
::
	brew upgrade pchain

You should now be able to check the different options and commands with 'pchain --help'.

-------------------
Docker Quick Start
-------------------

One of the quickest ways to get Pchain up and running on your machine is by using Docker:
::
	docker run -d --name pchain-node -v ~/pchain/.pchain:/.pchain \
           -p 6969:6969 -p 30308:30308 \
           pchain/client-go --datadir=/.pchain

This will start pchain just as the above command does. It will also create a persistent volume in your home directory for saving your blockchain as well as map the default ports.

Do not forget --rpcaddr=0.0.0.0 --rpc --rpcapi=eth,web3,admin,tdm,miner,personal,chain,txpool,del, if you want to access RPC from other containers and/or hosts. By default, pchain binds to the local interface and RPC endpoints is not accessible from the outside.






