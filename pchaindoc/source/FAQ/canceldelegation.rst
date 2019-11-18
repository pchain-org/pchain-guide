=================
Cancel Delegation
=================

-------------------------------------------------------------
1.Error: cancel amount greater than your Proxied Balance
-------------------------------------------------------------

This error occured because you are cancel more PI than you deposit. Please copy your candidate's address and go to `PIScan <https://piscan.pchain.org/fullBalance.html>`_ to check your candidate's fullbalance. Find your address in your candidate's Proxied detail, there are 3 value which we supposed is 
::
	ProxiedBalance 	A PI
	DepositProxiedBalance 	B PI
	PendingRefundBalance 	C PI

The amount you cancel should lower or equal than A+B-C.

-------------------------------------------------------------
2.Error:delegation amount must be greater or equal to 1000PI
-------------------------------------------------------------

This error occured because you are cancel invalid amount.Please copy your candidate's address and go to `PIScan <https://piscan.pchain.org/fullBalance.html>`_ to check your candidate's fullbalance. Find your address in your candidate's Proxied detail, there are 3 value which we supposed is 
::
	ProxiedBalance 	A PI
	DepositProxiedBalance 	B PI
	PendingRefundBalance 	C PI

If you don't wanna cancel all your deposit, the amount you cancel should be lower or equal than A+B-C-1000. If you wanna cancel all your deposit, the amount you cancel must be equal to A+B-C.
