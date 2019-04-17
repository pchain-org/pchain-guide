================================
How to deploy contract on pchain
================================

.. toctree::
   :maxdepth: 2

| We recommand use `online compiler <https://ethereum.github.io/browser-solidity/#optimize=false&version=soljson-v0.5.7+commit.6da8b019.js>`_ to compile smart contract.

| If you wanna testing your smart contract, it's better to deploy it on testnet first. You can  `run PCHAIN testnet <https://github.com/pchain-org/pchain/wiki/How-to-sync-and-run-pchain's-testnet>`_ first.
| You can Get `free tPI <https://testnet.pchain.org/vfaucet.html>`_ from our testnet.

-------
Compile
-------

Copy your code into it.

.. image:: ../_static/contract/contract.png

Click **Details** button.

.. image:: ../_static/contract/compile.png

Copy the Byte Code and ABI/JSON Interface

.. image:: ../_static/contract/bytecode.png

-------
Deploy
-------
| Note: You can only deploy smart contract on child chain.

| Enter contract page

.. image:: ../_static/contract/contractpage.png

Copy your byte code and click ‘Contract--Deploy Contract’ button.

.. image:: ../_static/contract/deploy.png

Enter your password and send the transaction.

.. image:: ../_static/contract/maketransaction.png

Wait for the contract address return and copy the address.

.. image:: ../_static/contract/address.png

----------------------
Interact with Contract
----------------------

Click ‘Contract--Interact with Contract’ button, copy your ABI/JSON Interface into it and click **Access** button.

.. image:: ../_static/contract/abi.png



