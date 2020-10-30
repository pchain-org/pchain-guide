====================
Delegation
====================

-------------------------------------------------------------
1. How many PI should I delegate to one candidate node?
-------------------------------------------------------------
You need to delegate at least 1K PI to one candidate.

-------------------------------------------------------------
2. When can I delegate token?
-------------------------------------------------------------
You can delegate PI before the epoch reaches 75% height. 

--------------------------------------------------------------------------------------------------------------------------
3. I have sent tx to delegate PI, why does the Tx status still show “pending” under the PIWallet delegate tag? 
--------------------------------------------------------------------------------------------------------------------------
When your candidate elected for next epoch validator successfully, then this Tx status will change to success, which also means you will start to get pos mining reward.

-------------------------------------------------------------
4. What does “Delegated to ** elected candidate node” mean?
-------------------------------------------------------------
It means the the number of your candidate which became the validator in current epoch. 

-------------------------------------------------------------
5. Can I delegate more to the same candidate?
-------------------------------------------------------------
Yes. You can delegate again before the epoch reaches 75% block height.

-------------------------------------------------------------
6. After delegation, when can I get the reward?
-------------------------------------------------------------
If the candidate you delegate to elected to be the next epoch validator successfully, then you will get the reward when the new epoch starts.

-------------------------------------------------------------
7.Error: cancel amount greater than your Proxied Balance
-------------------------------------------------------------
This error occured because the PI amount you are cancelling is greater than you delegated. Please copy your candidate's address and go to `PIScan <https://piscan.pchain.org/fullBalance.html>`_ to check your candidate's fullbalance. Find your address in your candidate's Proxied detail, there are 3 value which we supposed is 
::
	ProxiedBalance 	A PI
	DepositProxiedBalance 	B PI
	PendingRefundBalance 	C PI

The amount you cancel should lower or equal than A+B-C.

-------------------------------------------------------------
8.Error:delegation amount must be greater or equal to 1000PI
-------------------------------------------------------------
This error occured because you are cancel invalid amount.Please copy your candidate's address and go to `PIScan <https://piscan.pchain.org/fullBalance.html>`_ to check your candidate's fullbalance. Find your address in your candidate's Proxied detail, there are 3 value which we supposed is 
::
	ProxiedBalance 	A PI
	DepositProxiedBalance 	B PI
	PendingRefundBalance 	C PI

If you don't wanna cancel all your delegation, the amount you cancel should be lower or equal than A+B-C-1000. If you wanna cancel all your delegation, the amount you cancel must be equal to A+B-C.

-------------------------------------------------------------
9.Error: Replacement transaction underpriced
-------------------------------------------------------------
This error occured becaused the former transaction you made before are in processing. Suggest you to wait for a moment and retry. But if you wanna make this new transaction to cover the former one, you can increase the gas fee. 

------------------------------------------------------------------------------------------
10. I didn't get delegation tx hash, how can I ensure if my delegation is successful?
------------------------------------------------------------------------------------------
You can check the delegation history in PIwallet "Delegate" page, or go to 'Wallet" page to check the account balance if it decreased.

---------------------------------------------------------------------------------------------------------------
11. Why did my delegation hash/ Cancellation hash fail?/ Why did it return "can't delegate now"/ "Can't cancel now"?
---------------------------------------------------------------------------------------------------------------
After the chain reached 75% block height, you'r not allowed to delegate or cancel delegation. Then, pls retry when next epoch starts.



