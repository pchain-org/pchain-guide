===================================
Cancel node/ Candidate / delegation
===================================

1. As a candidate, can I update the commission fee?
Candidate can update commission fee via cancel candidate first and then reapply for it with the new commission fee. But once you cancel, all the delegation will return to delegators’ balance.

2. How to cancel candidate?
:ref:`cancelcandidate<How to cancel candidate>`
 
3. How to cancel node to unlock the staking amount via PIWallet?
After epoch reaches 75% height, you need to participate in the voting and revealing vote and set the staking amount to 0. 
For more information please refers to :ref:`How to become validator by PIWallet <Wallet Validator>` and :ref:`How to become validator by RPC <Client Validator>`
Once cancellation succeed, the staking amount will be unlocked to your balance when the current epoch ends.

4. How to cancel delegation ?
Before the epoch reaches 75% height, you can cancel delegation via PIwallet. Guidance: :ref:`canceldelegation<How to cancel delegation>`
If you are the technical peopl, you can cancellation via RPC: https://pchaindoc.readthedocs.io/en/latest/FAQ/canceldelegation.html

If your candidate is the validator in current epoch，the delegated amount will be unlocked to your balance when the epoch ends.
If not, then the delegated amount will be unlocked to your balance immediately.
