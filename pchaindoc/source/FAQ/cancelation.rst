===================================
Cancel node/ Candidate / delegation
===================================

-------------------------------------------------------------
As a candidate, can I update the commission fee?
-------------------------------------------------------------
Candidate can update commission fee via cancel candidate first and then reapply for it with the new commission fee. But once you cancel, all the delegation will return to delegators’ balance.

-------------------------------------------------------------
How to cancel candidate?
-------------------------------------------------------------
:ref:`How to cancel candidate<cancelcandidate>`
 
-------------------------------------------------------------
How to cancel node to unlock the staking amount?
-------------------------------------------------------------
After epoch reaches 75% height, you need to participate in the voting and revealing vote and set the staking amount to 0. 
For more information please refers to :ref:`Wallet Validator<How to become validator by PIWallet>` and :ref:`Client Validator<How to become validator by RPC>`
Once cancellation succeed, the staking amount will be unlocked to your balance when the current epoch ends.

-------------------------------------------------------------
How to cancel delegation ?
-------------------------------------------------------------
Before the epoch reaches 75% height, you can cancel delegation. Guidance: :ref:`How to cancel delegation<canceldelegation>`

If your candidate is the validator in current epoch，the delegated amount will be unlocked to your balance when the epoch ends.
If not, then the delegated amount will be unlocked to your balance immediately.

-------------------------------------------------------------
Error: cancel amount greater than your Proxied Balance
-------------------------------------------------------------

This error occured because you are cancel more PI than you deposit. Please copy your candidate's address and go to `PIScan <https://piscan.pchain.org/fullBalance.html>`_ to check your candidate's fullbalance. Find your address in your candidate's Proxied detail, there are 3 value which we supposed is 
::
	ProxiedBalance 	A PI
	DepositProxiedBalance 	B PI
	PendingRefundBalance 	C PI

The amount you cancel should lower or equal than A+B-C.

-------------------------------------------------------------
Error:delegation amount must be greater or equal to 1000PI
-------------------------------------------------------------

This error occured because you are cancel invalid amount.Please copy your candidate's address and go to `PIScan <https://piscan.pchain.org/fullBalance.html>`_ to check your candidate's fullbalance. Find your address in your candidate's Proxied detail, there are 3 value which we supposed is 
::
	ProxiedBalance 	A PI
	DepositProxiedBalance 	B PI
	PendingRefundBalance 	C PI

If you don't wanna cancel all your deposit, the amount you cancel should be lower or equal than A+B-C-1000. If you wanna cancel all your deposit, the amount you cancel must be equal to A+B-C.
