.. _Wallet Validator zh:

=========================
如何成为验证节点
=========================

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

您可以通过monitor来查看目前epoch的阶段情况。 `Monitor <https://monitor.pchain.org>`_。

现在，您可以准备以下几个将会在投票和揭标阶段使用到的参数。
- 账户地址
- 公钥 //存放在 priv_validator.json
- 私钥 //存放在 priv_validator.json
- 至少100K 数量的PI //total_depositProxiedBalance+total_proxiedBalance-total_pendingRefundBalance
- salt
          

如果你不确定可投票的PI数量，可以通过RPC eth_getFullBalance 查看fullbalance。 RPC `eth_getFullBalance <https://github.com/pchain-org/pchain/wiki/JSON-RPC#eth_getFullBalance>`_.      

首先，请确认该账户您有对应的公钥和私钥，一般可以在priv_validator.json.文件中找到。（若您没有，可通过创建一个新账户地址:ref:`Create Your Account`来获取）。举例如下：

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


------
投暗标
------
请点击‘Epoch–Vote Next Epoch’ 并填写相关信息

.. image:: ../../_static/wallet/localnode/vote.png

| From: 获取挖矿奖励的账户地址
| PubKey: 在priv_validator.json文件中的共识公钥
| Amount: 您计划抵押的PI数量（抵押数量需大于等于total_depositProxiedBalance+total_proxiedBalance)
| Salt: 任何参数

若您投票成功，将会返回一个交易hash。
上述4个所设置的参数请务必保存记录下来。


.. image:: ../../_static/wallet/localnode/votehash.png

-----------
投明标
-----------
请点击“Epoch–Reveal Vote”,并填写相关信息

.. image:: ../../../_static/wallet/localnode/reveal.png

From, PubKey, Amount 以及 Salt 必须与您在投票时所设置的参数一致。
BLS Private Key: 在 priv_validator.json 中的共识私钥。
如果您投票成功，将会返回一个交易hash.

.. image:: ../../../_static/wallet/localnode/revealhash.png
