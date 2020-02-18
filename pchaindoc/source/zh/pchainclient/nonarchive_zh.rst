=================
压缩PCHAIN的旧数据
=================

PCHAIN主网已于12月26日8点19分区块高度为9,383,000时成功硬分叉升级。
此次升级再次优化了Data Reduction,可进一步减少至少50% 以上的新增存储数据。对于之前所产生的旧数据，节点用户可根据以下步骤操作删减。


1. 更新到最新版pchain（v1.2.0以上）
::
	cd ~/pchain/
	./bin/pchain version
	1.2.0
如果版本低于1.2.0，请从 `Release <https://github.com/pchain-org/pchain/releases>`_下载。将压缩包中的ochain替换至~/pchain/bin/下，然后取消crontab脚本
::
	crontab -e
选择你熟悉的编译器，你会看到如下内容:
::
	*/10 * * * * ~/pchain/scripts/updatefile.sh > ~/pchain/scripts/update.log
	*/2 * * * * ~/pchain/scripts/monitor.sh > ~/pchain/scripts/monitor.log
执行crontab -e 然后将文件中的内容用‘#’注释掉，保存之后退出

2. 导出链数据

在pchain运行的情况下，进入console，执行admin.exportChain(“filename”)导出对应主/子链的全部区块信息
导出的文件会生成在启动pchain的目录下
 
若需导出主链，则连接到主链的console后执行admin.exportChain(“filename”)
若需导出子链，则连接到子链的console后执行admin.exportChain(“filename”)
 
导出所需时间大概在10分钟左右

3. 删除文件

先将pchain进程杀死
::
	sudo killall pchain
删除Datadir目录下除pchain/priv_validator.json, pchain/keystore, child_0/priv_validator.json, child_0/keystore, child_0/eth_genesis.json, child_0/genesis.json 以外的所有文件和文件夹。

删除后的目录结构是：
::
	datadir/
        -pchain/
                -priv_validator.json
                -keystore/
        -child_0/(if you are not running child chain, please ignore this directory)
                -genesis.json
		-eth_genesis.json
                -priv_validator.json
                -keystore/

4. 导入链数据

用以下命令启动pchain:
::
	./pchain --datadir=~/pchain/.pchain --gcmode=full --verbosity=0 --childChain=child_0 --maxpeers=0
Then attach to console, run admin.importChain("filename") to import chain data.

这一步可能需要超过10个小时的时间, 请耐心等待。

如果同时跑主链和子链，一定要先导入主链再导入子链。 在导入子链数据前，需要先初始化子链。
::
	./bin/pchain --datadir=~/pchain/.pchain init ~/pchain/.pchain/child_0/eth_genesis.json child_0

这一步完成后，你本地的数据只会保留最新128个块的状态。

5. 重启pchain

以上四步完成以后，请用以下命令重启pchain:
::
	~/pchain/bin/pchain --datadir=~/pchain/.pchain --rpc --rpcapi=eth,web3,admin,tdm,miner,personal,chain,txpool,del --gcmode=full --verbosity=0 --childChain=child_0 > /dev/null 2>&1 &
你也可以直接使用v1.2.0版本里的run.sh去启动pchain。





