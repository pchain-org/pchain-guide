.. _Client Validator:

=======================
How to Become Validator
=======================

Before you vote to become validator, make sure you have done things below: 

- sync and run pchain 
- have an address and consensus keys
- have at least 100k PI on your address

You can choose to apply candidates first so you can let other delegate to you. This is an option, not neccessity.

Pchain have 12 epochs per year, and in each epoch there are 4 phases.

+------------+--------------------------------------+------------------------------+
| Phase      | Block Number                         | What you can do              | 
+============+======================================+==============================+
| 0% ~ 75%   | start_block ~ vote_start_block - 1   | apply candidates and delegate| 
+------------+--------------------------------------+------------------------------+
| 75% ~ 85%  | vote_start_block ~ vote_end_block    | vote                         |
+------------+--------------------------------------+------------------------------+
| 85% ~ 95%  | reveal_start_block ~ reveal_end_block| reveal vote                  |
+------------+--------------------------------------+------------------------------+
| 95% ~ 100% | reveal_end_block + 1 ~ end_block     | check next epoch's info      |
+------------+--------------------------------------+------------------------------+

You can check the current stage by our `Monitor <https://monitor.pchain.org>`_, our by RPC `tdm_getEpoch <https://github.com/pchain-org/pchain/wiki/JSON-RPC#tdm_getEpoch>`_.

Now you can prepare the parameters will used during vote and reveal vote, you should have:

- address 
- consensus public key   //contains in priv_validator.json
- consensus private key  //contains in priv_validator.json
- amount           //should be at least 100k PI and equal or larger than total_depositBalance + total_proxiedBalance
- salt             

If you are not sure what amount should set, you can check your full balance by RPC `eth_getFullBalance <https://github.com/pchain-org/pchain/wiki/JSON-RPC#eth_getFullBalance>`_.

Note: you can also do the vote and reveal vote by PIWallet, it will make this process much easier.

>>>>>>>>>>>>>>>>>>
Generate vote hash
>>>>>>>>>>>>>>>>>>

Suppose you have a priv_validator.json look like this:
::
	{
        "address": "4CACBCBF218679DCC9574A90A2061BCA4A8D8B6C",
        "consensus_priv_key": [
                4,
                "D8AF52E355CD070ED3401800CBC920B6E94F3C49B42808C3049BF7BDB1FA3B19"
        ],
        "consensus_pub_key": [
                4,
                "085586D41F70435700850E19B7DE54B3E793C5EC4C6EC502D19030EF4F2122823E5A765E56CBA7B4C57E50561F77B022313C39895CA303F3C95D7B7282412F334778B95ACE046A79AEA4DB148334527250C8895AC5DB80459BF5D367236B59AF2DB5C0254E30A6D8CD1FA10AB8A5D872F5EBD312D3160D3E4DD496973BDC75E0"
        ]
	}
And you are voting for main chain's validator, which means the chainid is "pchain" (And the child chian's id is child_0).
First, attach to pchain's console
::
	pchain attach yourdatadir/chainid/pchain.ipc
In this case, the command should be
::
	pchain attach yourdatadir/pchain/pchain.ipc
and then type your paremeters to generate the vote hash:
::
	var address = "4CACBCBF218679DCC9574A90A2061BCA4A8D8B6C"; 
	var pubkey = "085586D41F70435700850E19B7DE54B3E793C5EC4C6EC502D19030EF4F2122823E5A765E56CBA7B4C57E50561F77B022313C39895CA303F3C95D7B7282412F334778B95ACE046A79AEA4DB148334527250C8895AC5DB80459BF5D367236B59AF2DB5C0254E30A6D8CD1FA10AB8A5D872F5EBD312D3160D3E4DD496973BDC75E0"; 
	var amount = "0x152d02c7e14af7000000"; 
	var salt = "ilovepchain"; //this string can be whatever you like
	web3.getVoteHash(address,pubkey,amount,salt);
	//"0x4dcb9f6e059051c58cc06ee0c038af4bffc18e85983540a72012bce56d2c37ec"
Now you get the vote hash "0x4dcb9f6e059051c58cc06ee0c038af4bffc18e85983540a72012bce56d2c37ec". Notice the amount is in hex, if you don't know how to convert dec to hex, we suggest you do this by PIWallet, which will be much easier.

>>>>>
Vote
>>>>>
You can vote by `RPC tdm_voteNextEpoch <https://github.com/pchain-org/pchain/wiki/JSON-RPC#tdm_votenextepoch>`_.
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"tdm_voteNextEpoch","params":["address", "vote hash"],"id":1}' localhost:6969/chainid
In this case, the command should be:
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"tdm_voteNextEpoch","params":["0x4CACBCBF218679DCC9574A90A2061BCA4A8D8B6C", "0x4dcb9f6e059051c58cc06ee0c038af4bffc18e85983540a72012bce56d2c37ec"],"id":1}' localhost:6969/pchain
Remember the return hash and wait for pchain enter reveal vote duration.

>>>>>>>>>>>
Reveal Vote
>>>>>>>>>>>
Before reveal vote, you need to generate a signature sign by your consensus private key. You can generate it by `RPC chain_signAddress <https://github.com/pchain-org/pchain/wiki/JSON-RPC#chain_signAddress>`_. 
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"chain_signAddress","params":["address", "consensus private key"],"id":1}' localhost:6969/pchain
In this case, the command should be:
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"chain_signAddress","params":["0x4CACBCBF218679DCC9574A90A2061BCA4A8D8B6C", "0xD8AF52E355CD070ED3401800CBC920B6E94F3C49B42808C3049BF7BDB1FA3B19"],"id":1}' localhost:6969/pchain
	//"0x1214608bcdf2e464b2d37d19b1b671482253e275d33079264045253fbb18689385ac0d5b4128d0c593211588deafd9ea2507b4858bdd42aaef3999045c0407ae"
Remember the return hash.

Note: you can vote many times during vote phase, the last one will prevail.

Now you can vote by `RPC tdm_revealvote <https://github.com/pchain-org/pchain/wiki/JSON-RPC#tdm_revealvote>`_.
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"tdm_revealVote","params":["address", "consensus public key", "amount", "salt", "signature"],"id":1}' localhost:6969/chainid
In this case, the command should be:
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"tdm_revealVote","params":["0x4CACBCBF218679DCC9574A90A2061BCA4A8D8B6C", "085586D41F70435700850E19B7DE54B3E793C5EC4C6EC502D19030EF4F2122823E5A765E56CBA7B4C57E50561F77B022313C39895CA303F3C95D7B7282412F334778B95ACE046A79AEA4DB148334527250C8895AC5DB80459BF5D367236B59AF2DB5C0254E30A6D8CD1FA10AB8A5D872F5EBD312D3160D3E4DD496973BDC75E0", "0x152d02c7e14af7000000", "ilovepchain", "0x1214608bcdf2e464b2d37d19b1b671482253e275d33079264045253fbb18689385ac0d5b4128d0c593211588deafd9ea2507b4858bdd42aaef3999045c0407ae"],"id":1}' localhost:6969/pchain
Remember the return hash and wait for pchain enter the last phase.

>>>>>>
Check
>>>>>>
Now you can check if you can become the next epoch's validator by `RPC tdm_getnextepochvalidators <https://github.com/pchain-org/pchain/wiki/JSON-RPC#tdm_getnextepochvalidators>`_.
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"tdm_getNextEpochValidators","params":[],"id":1}' localhost:6969/chainid
In this case, the command should be 
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"tdm_getNextEpochValidators","params":[],"id":1}' localhost:6969/pchain

>>>>>>>>>>>>>>>>>>>>>
How to quit validator
>>>>>>>>>>>>>>>>>>>>>

If you no longer want to be a validator, you can quit by yourself, the process is the same as above, just set the amount to 0. If you are also a candidate, you should cancel candidate first.