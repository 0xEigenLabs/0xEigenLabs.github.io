# Secret Usage Instructions Document

Version: 1.0


## Register ang Login
Open https://secret.ieigen.com/，click the “Connect Wallet”, and log in with your Google account.

![image001](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image001.png)

Select the corresponding Google Email account to log in and complete the authorization. 

![image002](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image002.png)

After logging in, you need to set a 6-digit password (including at least uppercase and lowercase letters, numbers and special symbols)

![image003](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image003.png)

After setting the fund password, go to the Overview page

![image004](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image004.png)

## Overview
Include: Home, History, Approval management. The Home page displays the asset fluctuation curve under the wallet, where All Assets represents the asset list and the number of assets corresponding to the current address;

![image005](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image005.png)



The History page displays the transaction history corresponding to the current wallet address. Click the Multisig Wallet button to filter the transaction history corresponding to the Multisig Wallet.

![image006](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image006.png)

Approval page: View the approved agreement and provide an entry to cancel the approval

## Send
Send assets to corresponding addresses by selecting different networks. Among them, the recipient address asset can choose the Multisig Wallet address.

![image007](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image007.png)

You can choose the Multisig Wallet address.

![image008](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image008.png)

## Exchange
By choosing different networks, you can exchange different assets. Currently PROTOCOL supports UniswapV2 and UniswapV3.

![image009](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image009.png)

## Tools
Provides rich tool components, including: Create Secret, Recover Secret, Co-Workers.

### Create Secret
"Create" implements key backup for the current account address; "Import" means importing a mnemonic or private key for the current account address.

![image010](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image010.png)

Click "Create" to enter the process of creating a key backup. Set the backup name and description and click the "Next" button.

![image011](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image011.png)

Download Google's "Authenticator" in the app market, scan the following QR code, and fill in the 6-digit verification code in "Authenticator". After clicking the "Next" button, the 2FA verification is completed. Then click the "Send Email" button to enter the social recovery process. Click the "Next" button.

![image012](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image012.png)

![image013](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image013.png)

![image014](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image014.png)



Select at least 2 friends, and the key shard will be sent to the selected friends by email. If you lose the key, you can complete the recovery key operation through "Tools-Recover Secret".

![image015](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image015.png)


Click the "Confirm" button, and click "Authorize" - "Continue" to confirm the authorization.

![image016](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image016.png)

![image017](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image017.png)

![image018](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image018.png)

![image019](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image019.png)



Then click the "Send Email" button to complete the email sending of the key fragment.

![image020](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image020.png)

### Recover Secret
Recover lost keys.Select any backup you want to restore and click "Recovery".

![image021](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image021.png)

Enter the 6-digit verification code corresponding to Google's "Authenticator". (If you lose the "Authenticator", click "Forget QR Secret ?" in the lower right corner to share the verification code by creating a new key backup).

![image022](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image022.png)

Paste the key fragment received by your friend's email, and click "Confim" to complete the key recovery.

![image023](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image023.png)

### Co-Workers
Add friend relationships by searching your friend's Google mailbox. This friend list can be used to select mailboxes for creating key shards.

![image024](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image024.png)

## Multisig Wallet
Multisig Wallet offers multiple features including social recovery, multi-signature transactions, payment limits, locking and unlocking, and more, preventing users’ funds from being lost or stolen.

### My Wallet
Refers to the Multisig Wallet corresponding to the current account, including "I am The Owner" and "I am The Signer"

![image025](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image025.png)

Click “Setting”,  set up the Payment Limit or Security settings.  For Payment Limit, you can limit the maximal payment amount for each transaction by Max per transaction, and maximal total payment each day by Max per day.  If the transaction amount  exceed the value of Max per day or total amount of the day  exceeds the value of Max per day, multi-signature mechanism will be triggered, and you need the N/2 signers to jointly sign for you to complete the transaction.  Now the Limitation can only take effect on ETH payment. 

For the Security, you can set up the Lock expiry and Recover expiry.  The lock expiry can be used to freeze the wallet,  and then  the wallet can not transfer or add new signers.  The recovery expiry is  used to limit the expiry of triggering recovery, only when you execute the recovery before the expiry,  the recovery can be completed.  If it expires, you need to trigger the recovery again.

![image026](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image026.png)

![image027](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image027.png)




"I am The Owner" is the list of Multisig Wallets owned by this account address. Click "Detail" to add Signer or delete Signer.

![image028](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image028.png)

"I am The Signer" is the Multisig Wallet list of this account as Signer. Click the "Freeze" button to freeze the wallet.

![image029](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image029.png)


Click "Confirm", and it will display "Frozen". At this time, the wallet cannot be transferred out. To unfreeze the wallet, you can restore it through Multisig Wallet-Recover Wallet. Note: When the number of Signers is greater than or equal to 1/2, the wallet will be frozen and take effect.

![image030](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image030.png)

![image031](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image031.png)

### Create Wallet
Create an entry for Multisig Wallet.Set the wallet name, click the "Add another signer" button to add a Singer, which can support "Google mailbox, ENS, address" to search and add. Please note that the Signer must be a user who has registered with Secret, please add at least one Signer.

![image032](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image032.png)

Click "Create", then click "Confirm" to sign.

![image033](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image033.png)

![image034](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image034.png)

![image035](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image035.png)


Wait for the transaction to complete, and "Create Successfully" appears to complete the wallet creation process.

![image036](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image036.png)


### Recover Wallet
When the Multisig Wallet corresponding to the user's current address is lost (in extreme cases such as the crash of the Multisig Wallet key escrow service), it can be recovered by the following steps.

Click on the avatar-Import Account in the upper right corner to import any other address of your own.

![image037](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image037.png)

Enter the 6-digit password you set earlier.

![image038](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image038.png)

You can choose mnemonic or private key to import.

![image039](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image039.png)

Switch to the newly imported address.

![image040](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image040.png)

Click Multisig Wallet-Recover Wallet, select the wallet to be recovered, and click the "Recovery" button.

![image041](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image041.png)

Confirm the wallet information to be restored and click "Confirm".

![image042](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image042.png)

Notify Signer to perform the recovery operation (Signer click "Confirm Recover" in Multisig Wallet-My Wallet-I am The Signer, and then sign again. Please refer to step 4 for details).

![image043](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image043.png)

After waiting for the signer greater than or equal to 1/2 to confirm, click the "Confirm" button, and then sign to complete the recovery operation. At this time, the Owner address of the wallet is changed to the address that currently initiates the recovery.

![image044](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image044.png)

![image045](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image045.png)

### Recovery operation performed by Signer
Signer clicks "Confirm Recover" in Multisig Wallet-My Wallet-I am The Signer

![image046](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image046.png)



Click to sign

![image047](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image047.png)

If the signer is the last signer (greater than or equal to 1/2 the number of signers to restore the wallet), you need to confirm the restoration, click "Confirm" and then sign.

![image048](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image048.png)

![image049](https://github.com/ieigen/ieigen/raw/main/docs/images/usage/image049.png)

