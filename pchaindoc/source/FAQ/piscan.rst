==================
PIScan
==================

-------------------------------------------------------------
1. What’s the PIscan
-------------------------------------------------------------
That’s block explorer which allows you to search, view and analyze PCHAIN data like blocks, transactions, validators, etc.

| PIscan：https://piscan.pchain.org

-------------------------------------------------------------
2. How to ensure if the transaction succeed or not?
-------------------------------------------------------------
Option1: Go to https://piscan.pchain.org “explorer” page, search with the transaction hash. If it returns transaction details, it succeed. Sometimes it may delay due to the mainnet speed. Then please retry later.
Option2: Go to console, enter pi.getTransactionReceipt(“hash”) , if status=”0x1”, it means success. 