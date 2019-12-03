===========================
Create your own child chain
===========================

Before you create your own child chain, make sure you have done things below: 

- sync and run pchain 
- have at least one address and one consensus keys
- have at least 200k PI on your address

Here is an example of priv_validator.json which stores your address and consensus keys:
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

Notice: Dont create different child chain with same address.

>>>>>>>>>>>>>>>>>>
create child chain
>>>>>>>>>>>>>>>>>>

Suppose you are gonna create a child chain which chain id is "mychain", and you want your child chain start with one validator with minimun deposit 100k PI.

You can create child chain by `RPC chain_createChildChain <https://github.com/pchain-org/pchain/wiki/JSON-RPC#chain_createchildchain>`_.
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"chain_createChildChain","params":["from","chainId", "minValidators", "minDepositAmount", "startBlock","endBlock"],"id":1}' localhost:6969/pchain
In this case, the command should be:
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"chain_createChildChain","params":["0x4CACBCBF218679DCC9574A90A2061BCA4A8D8B6C","mychain", "0x1", "0x152D02C7E14AF6800000", "0x32","0x7D0"],"id":1}' localhost:6969/pchain

You can set parameter startBlock very small and set parameter endBlock very big to make sure you wont miss it. After this your account will deposit 100k PI on child chain. If you didnt finish second step, the deposit will be back to your account once main chain reachs the "endBlock" height.

Note: This is only the first step, you need to finish the second step or the chain wont start.

>>>>>>>>>>>>>>>>
Join Child Chain
>>>>>>>>>>>>>>>>

Before you join child chain, you need to generate a signature signed by your consensus private key. You can generate it by `RPC chain_signAddress <https://github.com/pchain-org/pchain/wiki/JSON-RPC#chain_signAddress>`_. 
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"chain_signAddress","params":["address", "consensus private key"],"id":1}' localhost:6969/pchain
In this case, the command should be:
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"chain_signAddress","params":["0x4CACBCBF218679DCC9574A90A2061BCA4A8D8B6C", "0xD8AF52E355CD070ED3401800CBC920B6E94F3C49B42808C3049BF7BDB1FA3B19"],"id":1}' localhost:6969/pchain
	//"0x1214608bcdf2e464b2d37d19b1b671482253e275d33079264045253fbb18689385ac0d5b4128d0c593211588deafd9ea2507b4858bdd42aaef3999045c0407ae"
Remember the return hash.

Now you need to join child chain, in this example, you need at least one validator with at least 100k PI deposit to let your child chain start.
You can join child chain by `RPC chain_joinChildChain <https://github.com/pchain-org/pchain/wiki/JSON-RPC#chain_joinchildchain>`_.
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"chain_createChildChain","params":["from","pubkey", "chainId", "depositAmount", "signature"],"id":1}' localhost:6969/pchain
In this case, the command should be:
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"chain_createChildChain","params":["0x4CACBCBF218679DCC9574A90A2061BCA4A8D8B6C","085586D41F70435700850E19B7DE54B3E793C5EC4C6EC502D19030EF4F2122823E5A765E56CBA7B4C57E50561F77B022313C39895CA303F3C95D7B7282412F334778B95ACE046A79AEA4DB148334527250C8895AC5DB80459BF5D367236B59AF2DB5C0254E30A6D8CD1FA10AB8A5D872F5EBD312D3160D3E4DD496973BDC75E0", "mychain", "0x152D02C7E14AF6800000", "0x1214608bcdf2e464b2d37d19b1b671482253e275d33079264045253fbb18689385ac0d5b4128d0c593211588deafd9ea2507b4858bdd42aaef3999045c0407ae"],"id":1}' localhost:6969/pchain

After this transaction been packed and main chain reachs "startBlock" height, your chain will be start.

>>>>>>
Check
>>>>>>

Once your chain started, you will find a directory named with chain id under datadir/.pchain/, in this case, it should be datadir/.pchain/mychain, you can attach to it's console by command
::
	./bin/pchain attach .pchain/mychain/pchain.ipc


