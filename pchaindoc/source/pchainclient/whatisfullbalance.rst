.. _What is FullBalance:

===================
What is FullBalance
===================

Beside the normal Balance of each Account, PCHAIN design a list of Balance Amount for multipurpose reason, therefore we have the following RPC to allow you to view the overall balance under your account, you can also check your FullBalance on `PIScan <https://piscan.pchain.org/fullBalance.html>`_ for an easier way.

FullBalance RPC
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"eth_getFullBalance","params":["0x f92f0b506feb77693c51507eeea62c74869ff0f0", "0x175393", true],"id":1}'

Javascript Console
::
	pi.getFullBalance("0xf92f0b506feb77693c51507eeea62c74869ff0f0", "0x175393", true)
Sample Result (JSON Format)
::
	{
	    "jsonrpc": "2.0",
	    "id": 1,
	    "result": {
	        "balance": "0x1e4d26a8ca73c5c0e89c",
	        "proxied_detail": {
	            "0x29c6aaa742c98000f56b022bfdc68ac18070e0ab": {
	                "ProxiedBalance": "0x0",
	                "DepositProxiedBalance": "0x3017f94f218b846c4000",
	                "PendingRefundBalance": "0x0"
	            },
	            "0x4e8d522e7d95690bb44f7c589067cf06ba3b4e34": {
	                "ProxiedBalance": "0x0",
	                "DepositProxiedBalance": "0x7c35cd23913e1218a78c",
	                "PendingRefundBalance": "0x0"
	            },
	            "0x5078ffa5b2ea521a77c5069dd77fa88c3526a0d0": {
	                "ProxiedBalance": "0x0",
	                "DepositProxiedBalance": "0x567d0352bf3c82d00000",
	                "PendingRefundBalance": "0x0"
	            },
	            "0x6a3c07fa2b7ed2d0a7d0151d123e0f0cdffa3dbb": {
	                "ProxiedBalance": "0x0",
	                "DepositProxiedBalance": "0x4870d737ed0ee3724000",
	                "PendingRefundBalance": "0x0"
	            },
	            "0x75e4dbb9f429d6a3475e4f84a87ed8e4be748f6b": {
	                "ProxiedBalance": "0x0",
	                "DepositProxiedBalance": "0x34f0184982338e8a0000",
	                "PendingRefundBalance": "0x0"
	            },
	            "0x981d9cd05117a9d84437958863374a9bc78ac988": {
	                "ProxiedBalance": "0x0",
	                "DepositProxiedBalance": "0x23ee4727743b014c33d4",
	                "PendingRefundBalance": "0x0"
	            },
	            "0xac7ab60e2f28b137be99a9f960f0d01af01faad5": {
	                "ProxiedBalance": "0x0",
	                "DepositProxiedBalance": "0x1163ab378be4bf762000",
	                "PendingRefundBalance": "0x0"
	            },
	            "0xb0534db09a8ad1fd6ee2e3ad6889a26799926ad8": {
	                "ProxiedBalance": "0x0",
	                "DepositProxiedBalance": "0x3b984991099043475706",
	                "PendingRefundBalance": "0x0"
	            },
	            "0xc72f78ab2334a0a8acdbdc53c71186b07ee7580d": {
	                "ProxiedBalance": "0x0",
	                "DepositProxiedBalance": "0x3daaa47c278b400adaaa",
	                "PendingRefundBalance": "0x0"
	            },
	            "0xe4da810f56e27ba24364621da2b0c3b571355f65": {
	                "ProxiedBalance": "0x0",
	                "DepositProxiedBalance": "0x1ad994e1723d21600000",
	                "PendingRefundBalance": "0x0"
	            }
	        },
	        "reward_detail": {
	            "epoch_10": "0x38a4c99380b8546d96",
	            "epoch_11": "0x38a4c99380b85511bb",
	            "epoch_12": "0x28d7ce6d4796e16115",
	            "epoch_13": "0xd20fa530790c92286",
	            "epoch_2": "0x38a4c99380b854aeb8",
	            "epoch_3": "0x38a4c99380b8546d96",
	            "epoch_4": "0x38a4c99380b8546d96",
	            "epoch_5": "0x38a4c99380b8546d96",
	            "epoch_6": "0x38a4c99380b8546d96",
	            "epoch_7": "0x38a4c99380b8546d96",
	            "epoch_8": "0x38a4c99380b8546d96",
	            "epoch_9": "0x38a4c99380b8546d96"
	        },
	        "total_delegateBalance": "0x0",
	        "total_depositBalance": "0x784757798f05f3000000",
	        "total_depositProxiedBalance": "0x2499a2e9484c0f0c5ad10",
	        "total_pendingRefundBalance": "0x0",
	        "total_proxiedBalance": "0x0",
	        "total_rewardBalance": "0x26c68a883565af7b0be"
	    }
	}

Detail of FullBalance
(natural unit: wei, 1 PI = 1,000,000,000,000,000,000 or 10^18 natural units)

1.	balance
This balance also call free balance, means you can do anything on PCHAIN with this balance, (transfer, delegate, vote), your transaction Gas Fee (gas price * used gas) will be deduct from this balance
	
2.	total_delegateBalance
The total delegate balance amount. If you send delegate transaction to other address, the delegate amount will be moved from balance field to this delegate balance. If you delegate to multiple address, this field will sum the total delegation amount, you won’t able to see the detail of delegation on blockchain level, (for save storage reason, keep the on-chain data as minimum as possible), for detail delegate balance, you may need wallet or 3rd party dapp.

3.	total_depositBalance
The total staking balance amount, from you own address. If you want to become a validator, after you sending the hash/reveal vote, your staking amount will be locked from balance field to this deposit balance.
	
4.	total_proxiedBalance
The total balance that other address delegate their balance amount to your address. The balance takes no effect until you vote become a validator, it will move to the deposit proxied balance. Before that, the other address also able to revoke their delegation.
For detail of each proxied balance, see proxied_detail field

5.	total_depositProxiedBalance
The total balance that other address delegate their balance amount to your address and become the part of total staking. Other address can not revoke their delegation until epoch reach its end.
For detail of each deposit proxied balance, see proxied_detail field

6.	total_pendingRefundBalance
The total balance that other address delegate their balance amount to your address and wait for refund when other address revokes their delegation. The balance will refund when epoch reach its end.
For detail of each pending refund balance, see proxied_detail field

7.	total_rewardBalance
The total balance that will reward to address in the future, after each epoch reach its end, the reward balance of epoch will move to your balance field for free to use.
Every time when the address produces a new Block, this address will be considered as the recipient of the reward. Below is how the reward being calculated

| For Main Chain:
20% of block reward goes to Child Chain Foundation Address 0x991cf3cee2a55d06f9c7ba511bee3fad45a1bda7
80% of block reward belongs to the miner. If the block miner has delegation from other address, deduct the commission fee first if any, then the remaining rewards will be distributed by proportion.

| For Child Chain:
The Block Reward, setup by Child Chain Owner, belongs to the miner. If the reward pool (address 0x000000000000000000000000000000000000064) doesn’t has sufficient balance, then no reward to miner.
If the block miner has delegation from other address, deduct the commission fee first if any, then the remaining rewards will be distributed by proportion.

After each address receive their reward, the reward will be divided into 12 pieces, and allocate to 12 epochs. At each epoch ends, the reward will be move to free balance.

For detail of each reward balance, see reward_detail field

Example (Main Chain)
::
	Block Reward = 100 wei
	Miner reward = 100 * 80% = 80 wei
	If the miner has delegation, Miner self delegation 50% staking, Other Account 50% staking, commission percentage 10%
	Then, commission fee = 80 * 10% = 8 wei
	Other Account reward = (80 – 8) * 50% = 36 wei
	Miner reward = (80 – 8) * 50% + 8 = 44 wei

	Miner Reward divide into 12 epochs = 44 / 12 = 3
	From Epoch 0 – 10 = 3 wei each
	Epoch 11 = 11 wei (remaining reward)


