How to become validator
=========================

First of all, make sure you have bls' key for consensus, the information is included in file `priv_validator.json`. Here is an example.

.. code-block:: json

	{
	        "address": "50CA5341DFE4B07C41854FF79BDB8AB4E11C996D",
	        "consensus_priv_key": [
	                4,
	                "E0F8749A59EEF72347DDB1947A00292BD9D18D32B7C637692B98133A9A9D06D4"
	        ],
	        "consensus_pub_key": [
	                4,
	                "0939AD7B1543A37FB2803325EE6C385424D31E0A6A48B2913F425FE3ACBB56301282406B98C389D2D8DE95BB354ABAEF0C3CE7D4D985BE178B3B889B1859874D77C7EEB09146C1B66106FFB803D2884C0102B62A0FEF02D57B33AC286B41BD1183FDB55C8F25FA29859C4A370C9A19F077AB335D905CAB7E4E097C6BF31D3C5C"
	        ]
	}

EPOCH is the update cycle of the Validator, which is about 30 days on mainnet.

To become a Pchain's validator, you can participate by voting. The voting is divided into two phases: Vote and Reveal Vote.

You can view epoch's information on wallet `Epoch` page.

.. image:: ../../_static/wallet/localnode/epoch.png

You should vote during vote duration (when block height higher than vote_start_block and lower than vote_end_block) and reveal during revealduration (when block height higher than reveal_start_block and lower than reveal_end_block).

====
Vote
====
Click the **Vote Next Epoch** button and fill the information

.. image:: ../../_static/wallet/localnode/vote.png

| From: 	the address to receive mining reward 
| PubKey:	bls public key included in priv_validator.json
| Amount: 	the amount(pi) you wanna deposit
| Salt:		can be whatever you want

If you vote success, the wallet will return a transaction hash

.. image:: ../../_static/wallet/localnode/votehash.png

===========
Reveal Vote
===========
Click the **Reveal Vote** button and fill the information

.. image:: ../../_static/wallet/localnode/reveal.png

| From, PubKey, Amount and Salt must be the same with the value you set on vote.
| BLS Private Key: bls private key included in priv_validator.json

If you vote success, the wallet will return a transaction hash

.. image:: ../../_static/wallet/localnode/revealhash.png
