================
Installation
================

This tutorial is going to use pre-built binaries. For you to get started as quickly as possible this is the best option. Building from source is an option, but will set you back an hour or more and you may encounter build errors.

------
Ubuntu
------
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

- Install from release
Install latest pchain from release, the latest version can be find from `here <https://github.com/pchain-org/pchain/releases>`_.

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







