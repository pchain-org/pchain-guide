==============
Full Balance
==============

-------------------------------------------------------------
1. Where can I find the node’s balance info and reward info 
-------------------------------------------------------------
You can go to PIwallet/ PIscan under “fullbalance” tag, or via call for the FullBalance RPC.

-------------------------------------------------------------
2. What’s the meaning of each balance type there ?
-------------------------------------------------------------
**balance**: The total unlocked amount.
This balance also call free balance, means you can do anything on PCHAIN with this balance e.g transfer, delegate, vote,etc. Your transaction Gas Fee (gas price * used gas) will be deduct from this balance. 

**delegateBalance**: The total amount you delegate to other address(es).
If you send delegate transaction to other address, the delegate amount will be locked from balance to this delegate balance. If you delegate to multiple address, this field will sum each delegation amount. For detailed delegate balance, you can go to PIwallet/ PIscan to check. 

**depositBalance**: The staking amount you vote from your balance for Validator.
If you want to become a validator, after you vote/reveal vote, your staking amount will be locked from balance field to this deposit balance.

**depositProxiedBalance**: The total amount that others delegate to you (You applied as a Candidate) and you vote for validator with these delegation amount. 
After 75% block height, the delegators are not able to revoke their delegation. 

**pendingRefundBalance**: The total pending refund amount when delegator revoke delegation.
Delegators revoke the delegate amount to you which is the part of total staking amount in current epoch before 75% block height. This pending refund balance will return to the delegators’ balance when the current epoch ends.

**proxiedBalance**: The total balance that other people delegate their balance amount to you. 
Before voting, delegators can also revoke their delegation. After becoming validator, proxied balance will move to the deposit proxied balance.

**rewardBalance**: The reward amount which will unlock to the free balance in next epochs.
After each epoch reach its end, the reward balance will unlock 1/12 to your balance field for free to use. 
