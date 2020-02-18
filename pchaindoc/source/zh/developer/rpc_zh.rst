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

To talk to an pchain node from inside a JavaScript application use the `pweb3 <https://github.com/pchain-org/pweb3>`_ library, which gives a convenient interface for the RPC methods. See the `JavaScript API <https://github.com/pchain-org/pweb3/wiki/JavaScript-API>`_ for more.

---------------
Java API
---------------

To talk to an pchain node from inside a Java application use the `pweb3j <https://github.com/pchain-org/pweb3j>`_ library.

---------------
JSON RPC URL
---------------

Default JSON RPC URL

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
How To Open RPC 
------------------

You can start pchain with flag --rpc
::
	pchain --rpc
After this, if you wanna check main chain's current block number, the command will look like this:
::	
	curl -X POST --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}' localhost:6969/pchain
Or if you wanna check child chain's current block number, the command will look like this:
::	
	curl -X POST --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}' localhost:6969/child_0
You can also send request by `Postman <https://www.getpostman.com/>`_, you will need to start pchain with flag "--rpc --rpcaddr=0.0.0.0". But remember open your rpc to remote hosts is very dangerous if you keep your account unlocking.  

You can check our api list from `here <https://github.com/pchain-org/pchain/wiki/JSON-RPC>`_.



