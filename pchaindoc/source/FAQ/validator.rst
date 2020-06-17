.. _Faqvalidator:

================================
Flow and FAQ of become validator
================================

.. image:: ../_static/Help/validator.png

For more information please refers to :ref:`How to become validator by PIWallet <Wallet Validator>` and :ref:`How to become validator by RPC <Client Validator>`. There are some FAQ below:

---------------------------------------------------------------------
1. Where to find the exact time to participate in staking correctly?
---------------------------------------------------------------------

You can check stage on our `Monitor <https://monitor.pchain.org>`_. There are four stage in one epoch.

+------------+--------------------------------------+------------------------------+
| Stage      | Block Number                         | What you can do              | 
+============+======================================+==============================+
| 0% ~ 75%   | start_block ~ vote_start_block - 1   | apply candidates and delegate| 
+------------+--------------------------------------+------------------------------+
| 75% ~ 85%  | vote_start_block ~ vote_end_block    | vote                         |
+------------+--------------------------------------+------------------------------+
| 85% ~ 95%  | reveal_start_block ~ reveal_end_block| reveal vote                  |
+------------+--------------------------------------+------------------------------+
| 95% ~ 100% | reveal_end_block + 1 ~ end_block     | check next epoch's info      |
+------------+--------------------------------------+------------------------------+

-------------------------------------------------------------
2. The detailed operation to become validator via PIwallet
-------------------------------------------------------------
:ref:`How to become validator by PIWallet <Wallet Validator>`

-------------------------------------------------------------
3. The detailed operation to become validator via RPC
-------------------------------------------------------------
:ref:`How to become validator by RPC <Client Validator>`

-------------------------------------------------------------
4.Must I apply candidate?
-------------------------------------------------------------

No, you can compete validator by yourself. But if you apply candidate, you can get other's deposit, which will make you more competitive.

-------------------------------------------------------------
5.How many PI should I deposit while vote stage?
-------------------------------------------------------------

The amount you deposit should be at least 100k PI and equal or larger than total_depositProxiedBalance+total_proxiedBalance-total_pendingRefundBalance. And the deposit number should be the same while reveal vote stage.

-------------------------------------------------------------
6.How many PI is needed to be elected for Validator node?
-------------------------------------------------------------

There is no a guaranteed amount, the number of new validator node depends on how many native PI voted and reveal voted. If your deposit amount ranking is ahead of No.(number of current epoch's validator + number of next epoch's new bidders / 2 ), then you will be next epoch's validator. You can also check via tdm.getNextEpochValidators() to see if you are in the validator list.

e.g currently we have 79 validator nodes on main chain, and we got 5 Candidate nodes who participated in voting and revealing voting now, then the threshold ranking will be 79 + 5 / 2 = 81, which means the system will elect 81 Validator nodes for Next epoch based on each voting amount ranking.

-------------------------------------------------------------
7.How do I know if I can be next epoch’s validator or not?
-------------------------------------------------------------
If your deposit amount ranking is ahead of No.(number of current epoch’s validator + number of next epoch’s new bidders / 2 ), then you will be next epoch’s validator. You can also check via tdm.getNextEpochValidators() to see if you are in the validator list.

-------------------------------------------------------------
8.What is the minimun amount should I enter when I vote?
-------------------------------------------------------------

The amount should be at least 100k PI and equal or larger than total_depositProxiedBalance+total_proxiedBalance-total_pendingRefundBalance.

------------------------------------------------------------------------
9.As validator, should I do the vote and the reveal vote for each epoch?
------------------------------------------------------------------------
If you wanna keep the same deposit amount in next epoch, you don’t need to proceed it again. Otherwise you should participate in this process.

e.g 
your current deposit amount is A
the deposit amount you wanna add is B
then you should set the amount to A+B during vote and reveal vote

-------------------------------------------------------------
10.Can I update the commission fee as a candidate?
-------------------------------------------------------------
You need to cancel candidate first and then reapply candidate node (Noted that once you cancel，the delegation amount you received will return to delegators). After reapply, you can check on PIWallet if you are on the candidate list. If not, just wait for couple hours for PIWallet to refresh the commission fee.




