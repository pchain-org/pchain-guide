.. _Token Swap:

==========
Token Swap
==========

The official token swap from ERC 20 to native PI has finished on March 31st 2020! 

There are two methods to complete the token swap: Exchange Swap and PIwallet Swap

Currently, 4 exchanges (Bibox, Gate.io, Bithumb, Upbit) support native PI, the other exchange（Bittrex Global）still support the ERC 20 PI. Thus, if your ERC 20 PI tokens are in the exchange, then you need to withdraw all the ERC 20 PI first.

If your ERC 20 PI tokens are in the ERC 20 wallet, e.g. MEW, Imtoken or cold wallet, please make sure that you keep its private key and/or keystore file well before token swap via PIwallet. If not, then you have to transfer the ERC 20 PI tokens to new ERC 20 address which can be created on PIwallet. (:ref:`Create account on PIwallet<Create or import account>`)

- Exchange Swap
Bithumb supports the PCHAIN swap. You can deposit ERC 20 PI to Bithumb account and they will be swapped automatically.
Details: https://support.bithumb.pro/hc/en-us/articles/360033820673-Bithumb-Global-PI-Listing-Jul-31-2019

- PIwallet Swap
PIwallet only support native PI, and the address created on PIwallet is compatible with ERC 20 address. 

Please read the reminders before you start PIwallet swap.

1. Update PCHAIN Wallet to the latest version. Click `here <https://github.com/pchain-org/wallet/releases>`_ to download PIwallet.
2. Ensure that you keep the private key and/or keystore file of the ERC20 PI address well. 
3. Ensure there is a minimum amount of ETH (recommend 0.00036 ether which is 6 gwei*60,000) in your ERC20 PI address to cover the gas fee.
4. After you send the swap transaction, you will receive your native PI within 2 business days at most.
5. The swap need to get 12 blocks confirmation in Ethereum so the swap may take dozens of minutes.

Step 1: Open the PIwallet and click ‘Token Swap’ tab.

.. image:: ../_static/tokenswap/tokenswap0.png

Step 2: Import your ERC20 PI address to PCHAIN wallet.

	**Notice:** If you don't wanna import your current ERC20 address' private key or keystore to PIWallet, you can creat an ethereum address by MEW or imToken and tranfer all ERC20 PI to this new address and then do the token swap.

	Option1: Click ‘Import Private Key ’, fill out its private key. Set password and repeat it. Then click ‘Import’ to confirm. 
	Noticed: Please keep the password well by yourself.   

	.. image:: ../_static/tokenswap/tokenswap1.png

	It will show your ERC20 PI address and your ERC20 PI balance there. 

	.. image:: ../_static/tokenswap/tokenswap2.png

	Option 2: Click ‘Import Keystore’, ‘select keystore file’ from your computer.

	.. image:: ../_static/tokenswap/tokenswap3.png

	.. image:: ../_static/tokenswap/tokenswap4.png

	Enter its password and click ‘Import’.

	.. image:: ../_static/tokenswap/tokenswap5.png

	And you will see the ERC20 PI address and ERC20 PI balance there.

	.. image:: ../_static/tokenswap/tokenswap6.png

Step 3: Confirm your native PI address.
The default native PI address below is your ERC20 PI address after importing. 

.. image:: ../_static/tokenswap/tokenswap7.png

If you want to use new address to receive native PI, then click ‘Create Wallet’. Set the password and repeat it. Click ‘Create’ to confirm.

.. image:: ../_static/tokenswap/tokenswap8.png

Step 4: Fill out the amount that you want to swap. Then Click ‘Token Swap’ .
Enter the password and click ‘Confirm’ to continue. Please ensure there is enough ETH in your ERC20 PI address to cover gas fee. 

.. image:: ../_static/tokenswap/tokenswap9.png

Confirm the swap info. Then click ‘Send Transaction’. It will go to Etherscan automatically, and please be patient to wait for the transaction to succeed.

.. image:: ../_static/tokenswap/tokenswap10.png

.. image:: ../_static/tokenswap/tokenswap11.png

Noticed: If the Etherscan page shows ‘pending’ status or ‘unable to locate this transaction Hash’  status for a long time (e.g. more than 1 hour ), **you can resend with the same amount and greater gas fee. If nonce is same with the former transaction’s, then your former swap transaction will be dropped and replaced by this new one.**

.. image:: ../_static/tokenswap/tokenswap12.png

Step 5: Click ‘Wallet’ tab to check your balance.

.. image:: ../_static/tokenswap/tokenswap13.png

Welcome to :ref:`stake on PCHAIN as Validator<Staking>`! 
