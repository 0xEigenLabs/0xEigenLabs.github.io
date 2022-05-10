## Multisig Wallet
Multisig Wallet offers multiple features including social recovery, multi-signature transactions, payment limits, locking and unlocking, and more, preventing users’ funds from being lost or stolen.

### My Wallet

Check out your Multisig Wallet from the top-left popup menu after login as below.
<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/multisig/multisig-overview.png" width="75%" height="75%">


### Signers

When you switch to Multisig Wallet，the "Signers" is the list of these account addresses to protect your Multisig Wallet. Click "Detail" to add Signer or delete Signer.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/multisig/signers.png" width="75%" height="75%">

When you switch to Account, the 'Signers' is the list of Multisig Wallet who you protect.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/multisig/account-signer.png" width="75%" height="75%">

Click the "Freeze" button if you want to freeze the wallet.
<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/multisig/account-signer-detail.png" width="75%" height="75%">

Click "Confirm", and it will display "Frozen". At this time, the wallet cannot be transferred out. To unfreeze the wallet, you can restore it through Multisig Wallet-Recover Wallet. Note: When the number of Signers is greater than or equal to 1/2, the wallet will be frozen and take effect.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/multisig/freeze.png" width="75%" height="75%">

### Create Wallet
You can click Create Wallet in Multisig Wallet on the left column to create a multi-signature contract wallet.
The specific process will be divided into the following steps.：
（You can refer to the detailed description below to complete the operation）
1. Set smart contract wallet name
2. Enter the user's Eigen account and select the blockchain address you want to add as signer
3. Complete the creation of smart contract wallet

You can click About Eight Multi Signature Wallet to view the detailed description of the wallet.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/create_wallet/intro.png" width="75%" height="75%">

#### Step1:
Set the name of the wallet in set wallet name and enter the payment password to confirm this operation.
Creating a wallet requires gas fee. Please ensure that the account gas fee is sufficient in advance. After payment, you can proceed to the next step.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/create_wallet/step1.png" width="75%" height="75%">

After the payment is completed, the transaction will be confirmed and wait for the transaction to be completed automatically.
<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/create_wallet/step1_done.png" width="75%" height="75%">


#### Step2:
Click Add signer to add users. You need to add at least one signer to complete the wallet creation.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/create_wallet/step2.png" width="75%" height="75%">

After entering the user's Eigen account, select one of his blockchain addresses as the signer. (a person may have multiple blockchain addresses. Please select his commonly used blockchain address as the signer)
<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/create_wallet/step2_1.png" width="75%" height="75%">

After selection, click confirm to confirm.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/create_wallet/step2_2.png" width="75%" height="75%">

After paying the certification gas fee, you can complete the creation of smart contract wallet.
<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/create_wallet/step2_done.png" width="75%" height="75%">


#### Step3:
After the creation is successful, you can view the smart contract wallet you have created in My Wallet.
<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/create_wallet/step3.png" width="75%" height="75%">


### Recover Wallet
When the owner's key of the your multisig wallet is lost or stolen (in extreme cases such as the crash of the Multisig Wallet key escrow service), it can be recovered by the following steps.


#### Preparation
1. You need to log in your eigen account;
2. You need another safe account to replace the old owner of your multisig wallets by `Import` or `Create`, as to the tutorial [here](https://ieigen.github.io/#/docs/usage/Account).
3. Click recover wallet of left bar and eneter the Eigen account of the smart contract wallet you want to recover，and choose its blockchain addresses.

#### Steps

1. For new owner, click the `Recover Wallet`, and choose the wallet you want to recover.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/recovery/recovery-choose-wallet.png" width="75%" height="75%">
<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/recovery/recovery-choose-wallet2.png" width="75%" height="75%">

2. Step1, the new owner need click button `Start` to invite at least 50% + signers to sign for your recovery. A single recovery will expire in 48 hours. Please restart the recovery if it's timeout.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/recovery/recovery-step1.png" width="75%" height="75%">

3. For Signers of your wallet, enter `My Wallet`, find the wallet and `Confirm recovery` to sign for the recovery.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/recovery/signer_confirm.png" width="75%" height="75%">

sign the request as below.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/recovery/sign_recovery.png" width="75%" height="75%">

4. When more than 1/2 signers agree your recovery request, you need one of them to submit the recovery.

If more than 1/2 signers signs, the last one who sign the recovery will be notified automatically to submit the recovery transaction. If he/she does not confirm in time, any signer who signed the recovery  can click "Confirm" and then submit the transaction.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/recovery/sign_confirm.png" width="75%" height="75%">

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/recovery/sign_confirm2.png" width="75%" height="75%">

After this, the Step 2 will be completed automatically if the recovery triggered successfully.

5. Step 3, the new owner click `confirm`, and submit the replacement transaction, and if the transaction success, the new owner will replace the old owner and ownes the multisig wallet.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/recovery/recovery-owner-step3.png" width="75%" height="75%">

6. If you want to cancel the recovery, or the timeout is reached, you can `cancel` the recovery.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/recovery/recovery-cancel.png" width="75%" height="75%">

### Setting

Click “Setting”,  set up the Payment Limit or Security settings.  For Payment Limit, you can limit the maximal payment amount for each transaction by Max per transaction, and maximal total payment each day by Max per day.  If the transaction amount  exceed the value of Max per day or total amount of the day  exceeds the value of Max per day, multi-signature mechanism will be triggered, and you need the N/2 signers to jointly sign for you to complete the transaction.  Now the Limitation can only take effect on ETH payment. 

For the Security, you can set up the Lock expiry and Recover expiry.  The lock expiry can be used to freeze the wallet,  and then  the wallet can not transfer or add new signers.  The recovery expiry is  used to limit the expiry of triggering recovery, only when you execute the recovery before the expiry,  the recovery can be completed.  If it expires, you need to trigger the recovery again.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/multisig/setting.png" width="75%" height="75%">


