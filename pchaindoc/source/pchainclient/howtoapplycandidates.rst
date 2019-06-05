.. _Client Candidate:

=======================
How to Apply Candidates
=======================

Before you apply candidates, make sure you have done things bellow: 

- sync and run pchain 
- have an address and consensus keys
- have at least 10k PI on your address

Pchain have 12 epochs per year, and in each epoch there are 4 phases. You can apply candidates during the first phase.

+------------+--------------------------------------+------------------------------+
| Phase      | Block Number                         | What you can do              | 
+============+======================================+==============================+
| 0% ~ 75%   | start_block ~ vote_start_block - 1   | apply candidates and delegate| 
+------------+--------------------------------------+------------------------------+
| 75% ~ 85%  | vote_start_block ~ vote_end_block    | vote                         |
+------------+--------------------------------------+------------------------------+
| 85% ~ 95%  | reveal_start_block ~ reveal_end_block| reveal vote                  |
+------------+--------------------------------------+------------------------------+
| 95% ~ 100% | reveal_end_block + 1 ~ end_block     | check next epoch's info      |
+------------+--------------------------------------+------------------------------+

You can check the current stage by our `Monitor <https://monitor.pchain.org>`_, our by RPC `tdm_getEpoch <https://github.com/pchain-org/pchain/wiki/JSON-RPC#tdm_getEpoch>`_.

Now you can prepare the parameters will used after, you should have:

- address 
- security deposit  //amount of the security deposit PAI (minimum 1k PI)
- commission  // the commission fee percentage of each Block Reward be charged from delegator, when Candidate become a Validator (between 0 - 100)

Note: you can also apply candidates by PIWallet, it will make this process much easier.

>>>>>>>>>>>>>>>>>>>>>
Apply candidates
>>>>>>>>>>>>>>>>>>>>>

Now you can apply candidates by RPC `del_applycandidate <https://github.com/pchain-org/pchain/wiki/JSON-RPC#del_applycandidate>`_.
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"del_applyCandidate","params":["address", "security deposit", commission],"id":1}' localhost:6969/chainid
After this you can check by RPC `del_checkcandidate <https://github.com/pchain-org/pchain/wiki/JSON-RPC#del_checkcandidate>`_.

**Importantly Noticed**: Please go to `Join Candidate List <https://pchain.org/joinCandidate>`_ to submit your introduction. Once your submission has been validated, you will be publicly listed on Recommended Candidates on PIWALLET. Detailed information increases your chances of convincing Delegators to support your candidacy.

.. _Client Cancel Candidate:

>>>>>>>>>>>>>>>>>>>>>
Cancel candidates
>>>>>>>>>>>>>>>>>>>>>

Once you apply candidate successfully, you can cancel it via calling for RPC or PCHAIN wallet before the Epoch reaches 75%.
1) Canceling your submission after selected to be Validator: your staked PI will be unlocked and all the delegated tokens you received will be automatically returned to each delegator.once the Epoch reaches 100% height.
2) Canceling your submission after you failed being elected Validator: the cancelation will be effective immediately since there are no Validator duties to be completed, your staked PI will be unlocked, and all the delegated tokens you received automatically returned to each delegator balance. 

If you no longer want to be a validator, you can cancel by RPC `del_cancelcandidate <https://github.com/pchain-org/pchain/wiki/JSON-RPC#del_cancelcandidate>`_.
::
	curl -X POST -H "Content-Type:application/json" --data '{"jsonrpc":"2.0","method":"del_cancelCandidate","params":["address"],"id":1}' localhost:6969/chainid
