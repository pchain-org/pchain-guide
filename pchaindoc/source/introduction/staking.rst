.. _Staking:

========
Staking
========

| Welcome to PCHAIN staking.
PCHAIN is the 1st native EVM multichain enables the interoperability of child chain and main chain. Making large scale blockchain application possible.
We welcome more PCHAIN community members to run on PCHAIN and jointly make the mainnet stable with PCHAIN innovative PDBFT consensus algorithm, which can greatly reduce communication cost from N^2 to N comparing with traditional BFT algorithm and effectively reduce the centralization problem as the number of nodes is limited. Meanwhile, PCHAIN adopts Dynamic Bidding including voting and revealing vote and it enables the validator election more fair and secure in epoch switch. For the non-technicals, you can delegate PI via Safe Delegation, effectively avoiding the risk of evil by candidates. 
PCHAIN wallet has been released. It will help you participate in Validator competition more easier and quickly. Meanwhile, PCHAIN staking mechanism is the same on main chain and child chain.

Let’s check the details below.

-----------------------------
Who can get POS mining reward
-----------------------------

Before you staking on PCHAIN, please confirm which way you would like to take to participate in PoS Mining. 

- Bidder
PCHAIN holders with a minimum of 100K+ PI and the required configuration set-up are directly eligible to vote for validator. Dynamic staking ranking at each voting round will then determine if selected to be a next Epoch Validator.

- Candidate
If PCHAIN holders want to get the supports from delegation, they should be with a minimum of 10k PI and the required configuration set-up, and should apply for candidate first. Then they can compete against bidders for the validator via voting. Dynamic staking ranking at each voting round will then determine if selected to be a next Epoch Validator.

- Delegator 
PCHAIN holders with a minimum of 1K PI can delegate PI to candidate(s). Once his candidate succeed in voting for validator, he will get his PoS Mining reward based on his delegation percentage.

We will introduce how to do those step by step.

-----------
Preparation
-----------

Currently, you can swap native PI via :ref:`token swap on PIWallet<Token Swap>`.


-------------------
Delegation
-------------------

First, we will introduce how to delegate to other candidates, since this is the easiest way to get staking reward and don't request any technical background. All you need to do is

- :ref:`Install PIWallet<PIWallet>`
- :ref:`Create or import account to PIWallet<Create or import account>`
- Have at least 1k PI on your address
- :ref:`Go to delegate <How to delegate>` (You can delegate on both chain or one chain)

Once your candidate succeed in voting for validator, then you will get PoS Mining reward during next Epoch.

--------------------
Bidding
--------------------

Before we introduce how to bid, you must know that become a validator is a very interesting but complex thing. If you do not have any technical background or are new to blockchain, we recommend you to delegate to other candidate(s). Since once you become validator, you have to spend some time to monitor your node and even send your node's log to our team sometimes. But if you are determined to become pchain's validator, we will help you as much as we can.

You must have done things below before bidding on any chains:

Stake on main chain:

- :ref:`Installed pchain<Installation>`
- :ref:`Sync main chain` to the latest height (you can check by `Monitor <http://monitor.pchain.org/>`_)
- :ref:`Create Your Account`

Stake on child chain or both chains:

- :ref:`Installed pchain<Installation>`
- :ref:`Sync main chain` to the latest height (you can check by `Monitor <http://monitor.pchain.org/>`_)
- :ref:`Create Your Account`
- :ref:`Sync child chain` to the latest height (you can check by `Monitor <http://monitor.pchain.org/>`_)

Now you have 2 options to stake:

- Become validator as bidder
- Become validator as candidate

The advantage to apply candidate is you can earn the commission fee from delegators and the delegators' staking will make you more competitive, but once you got delegators, you have the responsibility to keep your node healthy cause the delegators will take attention to their reward.

So we will first introduce how to apply candidates, you can skip this section if you don't wanna apply one.

>>>>>>>>>>>>>>>>>>>>>>
How to apply candidate
>>>>>>>>>>>>>>>>>>>>>>

After you installed and synced pchain mainnet, you should also have at least 10k PI on your account. We provide 2 ways to apply candidate:

- :ref:`Apply candidate by PIWallet<Wallet Candidate>`
- :ref:`Apply candidate by RPC<Client Candidate>`

| **Notice:**
| You can do this on both chain, the RPC URL on main chain and child chain is different:
| Main chain: 	http://yourip:6969/pchain
| Child chain:	http://yourip:6969/child_0

>>>>>>>>>>>>>>>>>>>>>>>
How to become validator
>>>>>>>>>>>>>>>>>>>>>>>

After you installed and synced pchain mainnet, you should also have at least 100k PI on your account. We provide 2 ways to apply candidate:

- :ref:`Bid for validator by PIWallet<Wallet Validator>`
- :ref:`Bid for validator by RPC<Client Validator>`

| **Notice:**
| You can do this on both chain, the RPC URL on main chain and child chain is different:
| Main chain: 	http://yourip:6969/pchain
| Child chain:	http://yourip:6969/child_0

-----------------
Cancel delegation
-----------------

Once you delegate successfully, you can cancel it before the Epoch reaches 75%. We provide 2 ways to cancel candidate:

- :ref:`Cancel delegation by PIWallet<Wallet Cancel Delegation>`
- :ref:`Cancel delegation by RPC<Client Cancel Delegation>`

1) If your candidate is validator in current Epoch, the cancelation will be effective immediately. Your PI will be automatically unlocked to your balance when the current Epoch reaches 100%.

2) If your candidate is not validator in current Epoch, then the cancelation will take effect immediately and your PI will be automatically unlocked to your balance.


------------------
Cancel candidate
------------------

Once you apply candidate successfully, you can cancel it before the Epoch reaches 75%. We provide 2 ways to cancel candidate:

- :ref:`Cancel candidate by PIWallet<Wallet Cancel Candidate>`
- :ref:`Cancel candidate by RPC<Client Cancel Candidate>`

| **Notice:**
| You can do this on both chain, the RPC URL on main chain and child chain is different:
| Main chain: 	http://yourip:6969/pchain
| Child chain:	http://yourip:6969/child_0

1) Canceling your submission after selected to be Validator: your staked PI will be unlocked and all the delegated tokens you received will be automatically returned to each delegator once the Epoch reaches 100% height.
2) Canceling your submission after you failed being elected Validator: the cancelation will be effective immediately since there are no Validator duties to be completed, your staked PI will be unlocked, and all the delegated tokens you received automatically returned to each delegator balance.



------------------
Check your balance
------------------

There are 7 balance on PCHAIN. You can check it on PIWallet FullBalance page or `PIScan <https://piscan.pchain.org/>`_ .

Description of the various balance below： 

1) balance: total unlocked amount in current Epoch.
2) delegateBalance:  total amount you delegate to other address(es).
3) depositBalance:  total staked amount for Validator bidding.
4) depositProxiedBalance:  the delegated amount that you staked for Validator bidding.
5) pendingRefundBalance: total pending refund amount which will be return to delegators at the end of Current Epoch.
6) proxiedBalance:  total delegated amount from other address(es).
7) rewardBalance:  total pending reward amount, it will be unlocked 1/12 at the end of each Epoch.

For more detail, please check :ref:`What is FullBalance<What is FullBalance>`.



