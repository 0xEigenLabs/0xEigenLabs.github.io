## Multisig Wallet
Multisig Wallet offers multiple features including social recovery, multi-signature transactions, payment limits, locking and unlocking, and more, preventing users’ funds from being lost or stolen.

### My Wallet
Refers to the Multisig Wallet corresponding to the current account, including "I am The Owner" and "I am The Signer"

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image025.png" width="75%" height="75%">

Click “Setting”,  set up the Payment Limit or Security settings.  For Payment Limit, you can limit the maximal payment amount for each transaction by Max per transaction, and maximal total payment each day by Max per day.  If the transaction amount  exceed the value of Max per day or total amount of the day  exceeds the value of Max per day, multi-signature mechanism will be triggered, and you need the N/2 signers to jointly sign for you to complete the transaction.  Now the Limitation can only take effect on ETH payment. 

For the Security, you can set up the Lock expiry and Recover expiry.  The lock expiry can be used to freeze the wallet,  and then  the wallet can not transfer or add new signers.  The recovery expiry is  used to limit the expiry of triggering recovery, only when you execute the recovery before the expiry,  the recovery can be completed.  If it expires, you need to trigger the recovery again.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image026.png" width="75%" height="75%">

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image027.png" width="75%" height="75%">




"I am The Owner" is the list of Multisig Wallets owned by this account address. Click "Detail" to add Signer or delete Signer.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image028.png" width="75%" height="75%">

"I am The Signer" is the Multisig Wallet list of this account as Signer. Click the "Freeze" button to freeze the wallet.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image029.png" width="75%" height="75%">


Click "Confirm", and it will display "Frozen". At this time, the wallet cannot be transferred out. To unfreeze the wallet, you can restore it through Multisig Wallet-Recover Wallet. Note: When the number of Signers is greater than or equal to 1/2, the wallet will be frozen and take effect.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image030.png" width="75%" height="75%">

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image031.png" width="75%" height="75%">

### Create Wallet
Create an entry for Multisig Wallet.Set the wallet name, click the "Add another signer" button to add a Singer, which can support "Google mailbox, ENS, address" to search and add. Please note that the Signer must be a user who has registered with Secret, please add at least one Signer.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image032.png" width="75%" height="75%">

Click "Create", then click "Confirm" to sign.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image033.png" width="75%" height="75%">

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image034.png" width="75%" height="75%">

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image035.png" width="75%" height="75%">


Wait for the transaction to complete, and "Create Successfully" appears to complete the wallet creation process.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image036.png" width="75%" height="75%">


### Recover Wallet
When the Multisig Wallet corresponding to the user's current address is lost (in extreme cases such as the crash of the Multisig Wallet key escrow service), it can be recovered by the following steps.

Click on the avatar-Import Account in the upper right corner to import any other address of your own.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image037.png" width="75%" height="75%">

Enter the 6-digit password you set earlier.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image038.png" width="75%" height="75%">

You can choose mnemonic or private key to import.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image039.png" width="75%" height="75%">

Switch to the newly imported address.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image040.png" width="75%" height="75%">

Click Multisig Wallet-Recover Wallet, select the wallet to be recovered, and click the "Recovery" button.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image041.png" width="75%" height="75%">

Confirm the wallet information to be restored and click "Confirm".

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image042.png" width="75%" height="75%">

Notify Signer to perform the recovery operation (Signer click "Confirm Recover" in Multisig Wallet-My Wallet-I am The Signer, and then sign again. Please refer to step 4 for details).

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image043.png" width="75%" height="75%">

After waiting for the signer greater than or equal to 1/2 to confirm, click the "Confirm" button, and then sign to complete the recovery operation. At this time, the Owner address of the wallet is changed to the address that currently initiates the recovery.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image044.png" width="75%" height="75%">

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image045.png" width="75%" height="75%">

### Recovery operation performed by Signer
Signer clicks "Confirm Recover" in Multisig Wallet-My Wallet-I am The Signer

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image046.png" width="75%" height="75%">



Click to sign

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image047.png" width="75%" height="75%">

If the signer is the last signer (greater than or equal to 1/2 the number of signers to restore the wallet), you need to confirm the restoration, click "Confirm" and then sign.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image048.png" width="75%" height="75%">

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image049.png" width="75%" height="75%">

