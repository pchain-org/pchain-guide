.. _Client Validator zh:

=======================
如何成为验证节点
=======================

在投票竞标之前，请先确定已完成以下准备工作：

- 同步并运行pchain
- 持有一个账户地址和共识公私钥
- 账户地址下至少有100K 数量的PI

您也可以选择先申请成为Candidate,让更多人委托给您，增加投票中标的机率。

PCHAIN主网以12个epoch为1年，每一个epoch中分为4个阶段：

+------------+--------------------------------------+------------------------------+
| 阶段       | 块高度                                | 你能做什么                    | 
+============+======================================+==============================+
| 0% ~ 75%   | start_block ~ vote_start_block - 1   | 申请成为候选人和委托           | 
+------------+--------------------------------------+------------------------------+
| 75% ~ 85%  | vote_start_block ~ vote_end_block    | 投暗标                        |
+------------+--------------------------------------+------------------------------+
| 85% ~ 95%  | reveal_start_block ~ reveal_end_block| 投明标                        |
+------------+--------------------------------------+------------------------------+
| 95% ~ 100% | reveal_end_block + 1 ~ end_block     | 查看下一个epoch的信息          |
+------------+--------------------------------------+------------------------------+

您可以通过monitor来查看目前epoch的阶段情况 `Monitor <https://monitor.pchain.org>`_。

现在，您可以准备以下几个将会在投票和揭标阶段使用到的参数。
- 账户地址
- 公钥 //存放在 priv_validator.json
- 私钥 //存放在 priv_validator.json
- 至少100K 数量的PI //total_depositProxiedBalance+total_proxiedBalance-total_pendingRefundBalance
- salt
          

如果你不确定可投票的PI数量，可以通过RPC eth_getFullBalance 查看fullbalance。 RPC `eth_getFullBalance <https://github.com/pchain-org/pchain/wiki/JSON-RPC#eth_getFullBalance>`_.

注意：您也可以通过PIWALLET来完成投票和揭标，过程相对会比较简单。

>>>>>>>>>>>>>>>>>>
生成暗标hash
>>>>>>>>>>>>>>>>>>

假如你有这样的一个priv_validator.json
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
如果您是在主链上参与竞标，则chainid为‘pchain’,若在子链1上参与竞标，则chainid为‘child_0’。

首先，请先前往pchain的控制台。
::
	pchain attach yourdatadir/chainid/pchain.ipc
在本例中, 指令为:
::
	pchain attach yourdatadir/pchain/pchain.ipc
然后，请输入以下参数来创建投票hash:
::
	var address = "4CACBCBF218679DCC9574A90A2061BCA4A8D8B6C"; 
	var pubkey = "085586D41F70435700850E19B7DE54B3E793C5EC4C6EC502D19030EF4F2122823E5A765E56CBA7B4C57E50561F77B022313C39895CA303F3C95D7B7282412F334778B95ACE046A79AEA4DB148334527250C8895AC5DB80459BF5D367236B59AF2DB5C0254E30A6D8CD1FA10AB8A5D872F5EBD312D3160D3E4DD496973BDC75E0"; 
	var amount = "0x152d02c7e14af7000000";  
	var salt = "ilovepchain"; //this string can be whatever you like
	web3.getVoteHash(address,pubkey,amount,salt);
	//"0x4dcb9f6e059051c58cc06ee0c038af4bffc18e85983540a72012bce56d2c37ec"
现在你获得了暗标hash“0x4dcb9f6e059051c58cc06ee0c038af4bffc18e85983540a72012bce56d2c37ec”
注意: 这里的数量是十六进制的，如果您不知道如何转化成十六进制，我们建议您通过PIWALLET来完成竞标的全部操作。


注意: 1gwei = 1000000000wei = 0x3B9ACA00

>>>>>>
投暗标
>>>>>>
你可以用此RPC投暗标 `RPC tdm_voteNextEpoch <https://github.com/pchain-org/pchain/wiki/JSON-RPC#tdm_votenextepoch>`_.
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"tdm_voteNextEpoch","params":["address", "vote hash"],"id":1}' localhost:6969/chainid
在本例中, 指令为:
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"tdm_voteNextEpoch","params":["0x4CACBCBF218679DCC9574A90A2061BCA4A8D8B6C", "0x4dcb9f6e059051c58cc06ee0c038af4bffc18e85983540a72012bce56d2c37ec"],"id":1}' localhost:6969/pchain
请记住所返回的hash值并且等到主网进入明标阶段。

注意：您可以在投票阶段进行几次的投票操作，最终系统将会以最后一次为准。

>>>>>>>>>>>
投明标
>>>>>>>>>>>
在揭标之前，你需要通过你的私钥创建一个签名，你可以通过RPC chain_signAddress来完成。`RPC chain_signAddress <https://github.com/pchain-org/pchain/wiki/JSON-RPC#chain_signAddress>`_. 
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"chain_signAddress","params":["address", "consensus private key"],"id":1}' localhost:6969/pchain
在本例中, 指令为:
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"chain_signAddress","params":["0x4CACBCBF218679DCC9574A90A2061BCA4A8D8B6C", "0xD8AF52E355CD070ED3401800CBC920B6E94F3C49B42808C3049BF7BDB1FA3B19"],"id":1}' localhost:6969/pchain
	//"0x1214608bcdf2e464b2d37d19b1b671482253e275d33079264045253fbb18689385ac0d5b4128d0c593211588deafd9ea2507b4858bdd42aaef3999045c0407ae"
记录返回的hash.

现在你可以用此RPC来投明标 `RPC tdm_revealvote <https://github.com/pchain-org/pchain/wiki/JSON-RPC#tdm_revealvote>`_.
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"tdm_revealVote","params":["address", "consensus public key", "amount", "salt", "signature"],"id":1}' localhost:6969/chainid
在本例中, 指令为:
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"tdm_revealVote","params":["0x4CACBCBF218679DCC9574A90A2061BCA4A8D8B6C", "085586D41F70435700850E19B7DE54B3E793C5EC4C6EC502D19030EF4F2122823E5A765E56CBA7B4C57E50561F77B022313C39895CA303F3C95D7B7282412F334778B95ACE046A79AEA4DB148334527250C8895AC5DB80459BF5D367236B59AF2DB5C0254E30A6D8CD1FA10AB8A5D872F5EBD312D3160D3E4DD496973BDC75E0", "0x152d02c7e14af7000000", "ilovepchain", "0x1214608bcdf2e464b2d37d19b1b671482253e275d33079264045253fbb18689385ac0d5b4128d0c593211588deafd9ea2507b4858bdd42aaef3999045c0407ae"],"id":1}' localhost:6969/pchain
请记住返回的hash值，等待epoch进入到最后一个阶段。

>>>>>>>>
查看结果
>>>>>>>>
您可以通过RPC tdm_getnextepochvalidators 来查看自己是否成功竞标成为下个Epoch的共识节点 `RPC tdm_getnextepochvalidators <https://github.com/pchain-org/pchain/wiki/JSON-RPC#tdm_getnextepochvalidators>`_.
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"tdm_getNextEpochValidators","params":[],"id":1}' localhost:6969/chainid
在本例中, 指令为:
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"tdm_getNextEpochValidators","params":[],"id":1}' localhost:6969/pchain

>>>>>>>>>>>>>>>>>>>>>
如何退出验证节点
>>>>>>>>>>>>>>>>>>>>>

如果您不再继续作为一个共识节点，您可以自行退出。退出过程同样需要参与上述的投票和揭标，其中需将PI数量设置为0。如果您本身还是Candidate身份，那么还请先取消Candidate。