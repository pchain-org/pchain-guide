===========
JSON RPC
===========

-------------------
Pchain JSON RPC API
-------------------

`JSON <http://json.org/>`_ 是一种轻量级的数据交换格式。它可以表示数字、字符串、有序的值序列和名称/值对的集合。
`JSON RPC <http://www.jsonrpc.org/specification>`_ 是一个无状态的、轻量级的远程过程调用(RPC)协议。该规范主要定义了几个数据结构及其处理规则。它与传输无关，因为这些概念可以在相同的流程中、在套接字上、在HTTP上或在许多不同的消息传递环境中使用。它使用JSON (`RFC 4627 <http://www.ietf.org/rfc/rfc4627.txt>`_)作为数据格式。

---------------
JavaScript API
---------------

要从JavaScript应用程序内部与pchain节点通信，可以使用`pweb3 < https://github.com/pchorg/pweb3>`_ library，它为RPC方法提供了一个方便的接口。有关更多信息，请参见 `JavaScript API < https://github.com/pchorg/pweb3/wiki/javascript-api >`_。


---------------
Java API
---------------

要从Java应用程序内部与pchain节点通信，可以使用 `pweb3j <https://github.com/pchain-org/pweb3j>`_ library.

---------------
JSON RPC URL
---------------

默认JSON RPC URL

+--------------+---------------+------------------------------------+
| Chain Name   | Chain Id      | Default Datadir Directory          | 
+==============+===============+====================================+
| Main Chain   | pchain        | http://localhost:6969/pchain       | 
+--------------+---------------+------------------------------------+
| Child Chain 1| child_0       | http://localhost:6969/child_0      | 
+--------------+---------------+------------------------------------+
| Your Chain   | your_chain_id | http://localhost:6969/your_chain_id|
+--------------+---------------+------------------------------------+

------------------
如何开启RPC连接 
------------------

你可以在启动命令行中加上 --rpc 来开启RPC连接
::
	pchain --rpc
假如你想查看主链现在的高度，可以使用这样的命令:
::	
	curl -X POST --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}' localhost:6969/pchain
假如你想查看子链现在的高度，可以使用这样的命令::
::	
	curl -X POST --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}' localhost:6969/child_0
你也可以用`Postman <https://www.getpostman.com/>`_ 发送请求, 但你需要先将 "--rpc --rpcaddr=0.0.0.0" 加入到启动的命令中。 

你可以在github上查看我们的RPC接口列表 `RPC List <https://github.com/pchain-org/pchain/wiki/JSON-RPC>`_.



