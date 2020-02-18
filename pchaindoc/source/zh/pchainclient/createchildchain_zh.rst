===========================
创建你自己的子链
===========================

在创建子链之前，请确保您已完成以下事项：

- 同步并运行pchain 主网
- 至少有一个账户地址以及对应的共识公私钥
- 账户地址中至少有200K数量的PI


以下是关于存储您账户和共识公私钥的priv_validator.json 例子：
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

请注意：请不要使用同一个账户地址来创建多个子链。

>>>>>>>>>>>>>>>>>>
创建子链
>>>>>>>>>>>>>>>>>>

假设您所要创建的子链ID是mychain,并且以一个共识节点和100K数量的PI来启动运行子链。

您可以通过RPC chain_createChildChain来创建子链。`RPC chain_createChildChain <https://github.com/pchain-org/pchain/wiki/JSON-RPC-chain_createchildchain>`_.
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"chain_createChildChain","params":["from","chainId", "minValidators", "minDepositAmount", "startBlock","endBlock"],"id":1}' localhost:6969/pchain
在本例中, rpc指令为:
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"chain_createChildChain","params":["0x4CACBCBF218679DCC9574A90A2061BCA4A8D8B6C","mychain", "0x1", "0x152D02C7E14AF6800000", "0x32","0x7D0"],"id":1}' localhost:6969/pchain

您可以设置一个很小的起始区块参数，以及一个较大的结束区块参数。您的账户将会抵押100K至子链上。如果您没有完成第二步，那么一旦主链达到结束区块高度，抵押数量将会返回至您的账户地址。

请注意：这仅仅是第一步，您必须完成第二步操作，才能正式启动链。

>>>>>>>>>>>>>>>>
加入子链
>>>>>>>>>>>>>>>>

在您加入子链之前，你需要使用私钥通过RPC chain_signAddress创建一个签名 `RPC chain_signAddress <https://github.com/pchain-org/pchain/wiki/JSON-RPC-chain_signAddress>`_. 
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"chain_signAddress","params":["address", "consensus private key"],"id":1}' localhost:6969/pchain
在本例中, rpc指令为:
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"chain_signAddress","params":["0x4CACBCBF218679DCC9574A90A2061BCA4A8D8B6C", "0xD8AF52E355CD070ED3401800CBC920B6E94F3C49B42808C3049BF7BDB1FA3B19"],"id":1}' localhost:6969/pchain
	//"0x1214608bcdf2e464b2d37d19b1b671482253e275d33079264045253fbb18689385ac0d5b4128d0c593211588deafd9ea2507b4858bdd42aaef3999045c0407ae"
记录返回的hash.

现在，以1个共识节点为例的情况下，您需要一个共识节点以100K抵押数量来加入该子链，并启动运行，您可以通过RPC chain_joinChildChain来加入子链。 `RPC chain_joinChildChain <https://github.com/pchain-org/pchain/wiki/JSON-RPC-chain_joinchildchain>`_.
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"chain_createChildChain","params":["from","pubkey", "chainId", "depositAmount", "signature"],"id":1}' localhost:6969/pchain
在本例中, rpc指令为:
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"chain_createChildChain","params":["0x4CACBCBF218679DCC9574A90A2061BCA4A8D8B6C","085586D41F70435700850E19B7DE54B3E793C5EC4C6EC502D19030EF4F2122823E5A765E56CBA7B4C57E50561F77B022313C39895CA303F3C95D7B7282412F334778B95ACE046A79AEA4DB148334527250C8895AC5DB80459BF5D367236B59AF2DB5C0254E30A6D8CD1FA10AB8A5D872F5EBD312D3160D3E4DD496973BDC75E0", "mychain", "0x152D02C7E14AF6800000", "0x1214608bcdf2e464b2d37d19b1b671482253e275d33079264045253fbb18689385ac0d5b4128d0c593211588deafd9ea2507b4858bdd42aaef3999045c0407ae"],"id":1}' localhost:6969/pchain

在该笔交易完成打包且主链达到起始区块高度后，您的子链就会启动。

>>>>>>
检查
>>>>>>

一旦您的子链启动后，会在datadir/.pchain/下生成一个以chain id为名的文件目录。如datadir/.pchain/mychain。您可以通过命令行进入其控制台。
::
	./bin/pchain attach .pchain/mychain/pchain.ipc


