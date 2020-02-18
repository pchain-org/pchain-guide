===============
PMetamask(中文)
===============

PMetamask是一个插件钱包

------------
安装
------------
首先，下载PMetamask安装包。然后打开Chrome并输入Chrome://extensions/进入扩展页面。 `下载地址 <https://github.com/pchain-org/pmetamask/releases/download/v0.0.1/Pmetamask-chrome-0.0.1.zip>`_.

.. image:: ../../_static/pmatemask/chromeextension.png

切换到资源管理器右上角的Developer模式，并将PMetamask安装包拖动到其中以安装插件。

.. image:: ../../_static/pmatemask/developermode.png

根据PMetamask的指南创建或导入地址后，您可以看到如下内容:

.. image:: ../../_static/pmatemask/pmetamaskehello.png

PCHAIN的smart contract只能部署在子链上我们选择PCHAIN testnet上的子链1来部署smart contract。`获取免费的tPI <https://testnet.pchain.org/vfaucet.html>`_.

.. image:: ../../_static/pmatemask/choosenetwork.png

-------------------------------
连接 Remix 和 PMetamask
-------------------------------
保持PMetamask打开，打开Remix【http://remix.ethereum.org】页面如下:

.. image:: ../../_static/pmatemask/remix.png

在Remix的“运行”菜单下，选择环境为“注入Web3”:

.. image:: ../../_static/pmatemask/selectenv.png

在弹出的PMetamask通知对话框中单击“连接”

.. image:: ../../_static/pmatemask/connecttometamask.png

之后，PMetamask中的默认帐户地址将自动显示在“account”字段中。

.. image:: ../../_static/pmatemask/shownaddress.png

-----------------------------------------
部署和调用智能合约
-----------------------------------------
在Remix中编写好智能合约，比如：
::
	pragma solidity ^ 0.4.23 ;
	contract PCHAINTest{
	    
	  uint public value = 0;
	  function inc(uint v) public {
	    value += v;
	  }
	}

选择要编译的版本(这里我们以0.4.23版本为例)：

.. image:: ../../_static/pmatemask/selectversion.png

编译智能合约

.. image:: ../../_static/pmatemask/compile.png

点击“运行”菜单下的“部署”按钮来部署刚刚编译好的智能合约

.. image:: ../../_static/pmatemask/deploy.png

点击“部署”按钮后，点击PMetamask通知对话框中的“确认”按钮:

.. image:: ../../_static/pmatemask/confirm.png

成功部署后，可以调试合约

.. image:: ../../_static/pmatemask/interact1.png

.. image:: ../../_static/pmatemask/interact2.png

| 如果有操作需要花费精力，您可能需要在弹出的PMetamask对话框中或直接在PMetamask中进行确认。
| 如果交易失败，您可以尝试重新发送它或根据返回的错误更改GAS费用。

