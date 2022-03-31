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
When the owner's key of the your multisig wallet is lost or stolen (in extreme cases such as the crash of the Multisig Wallet key escrow service), it can be recovered by the following steps.


#### Preparation
1. You need to log in your eigen account;
2. You need another safe account to replace the old owner of your multisig wallets by `Import` or `Create`, as to the tutorial [here](https://ieigen.github.io/#/docs/usage/Account).
3. Click recover wallet of left bar and eneter the Eigen account of the smart contract wallet you want to recover，and choose its blockchain addresses.

#### Steps

1. For new owner, click the `Recover Wallet`, and choose the wallet you want to recover.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/recovery/recovery-choose-wallet.png" width="75%" height="75%">

2. Step1, the new owner need click button `Start` to invite at least 50% + signers to sign for your recovery. A single recovery will expire in 48 hours. Please restart the recovery if it's timeout.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/recovery/recovery-step1.png" width="75%" height="75%">

3. For Signers of your wallet, enter `My Wallet`, and switch to tab `I am The Signer`, and find the wallet which allows you to `Confirm recovery`

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image046.png" width="75%" height="75%">

sign the request as below.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image047.png" width="75%" height="75%">

4. When more than 1/2 signers agree your recovery request, you need one of them to submit the recovery.

If more than 1/2 signers signs, the last one who sign the recovery will be notified automatically to submit the recovery transaction. If he/she does not confirm in time, any signer who signed the recovery  can click "Confirm" and then submit the transaction.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image048.png" width="75%" height="75%">

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/image049.png" width="75%" height="75%">

After this, the Step 2 will be completed automatically if the recovery triggered successfully.

5. Step 3, the new owner click `confirm`, and submit the replacement transaction, and if the transaction success, the new owner will replace the old owner and ownes the multisig wallet.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/recovery/recovery-owner-step3.png" width="75%" height="75%">

6. If you want to cancel the recovery, or the timeout is reached, you can `cancel` the recovery.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/recovery/recovery-cancel.png" width="75%" height="75%">

