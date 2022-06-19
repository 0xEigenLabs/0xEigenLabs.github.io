# Stealth Address
What is anonymity? In the context of blockchains, anonymity means the ability for parties to exchange data without disclosing any off-chain identity information or other transactions they have done. 

Stealth Address is a privacy protection technique for receivers of cryptocurrencies that provides strong anonymity for transaction receivers and enables them to receive unlinkable payments in practice. Stealth address requires the sender to create random one-time addresses for every transaction on behalf of the recipient so that different payments made to the same payee are unlinkable.

If Alice wants to initiate an anonymous payment to Bob, what do they need to do?

First, Bob needs to provide Alice with the public key to his address. Bob can select **Copy Public Key** from the address of **My Account**, and tell Alice the public key.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/stealth_address/0.png" width="75%" height="75%">

When Alice knows Bob's public key, Alice needs to enter the **Send** page and click the button **Hide**, indicating that an anonymous payment will be initiated, then enter Bob's public key, and click **Send**. The difference from ordinary transfers is that it no longer receives Bob's address, but Bob's public key.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/stealth_address/1.png" width="75%" height="75%">

When Bob receives an anonymous payment transaction, there will be an additional record on the **Stealth Address** page, He can click **Unhide** to export the stealth address as a normal address.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/stealth_address/2.png" width="75%" height="75%">

After clicking the button **Unhide**, the prompt of **Unhide Submitted** will appear.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/stealth_address/3.png" width="75%" height="75%">

After the submission is successful, the button **Unhide** will become **Unhided**, indicating that it has been exported as a normal address.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/stealth_address/4.png" width="75%" height="75%">

If everything goes well, Bob can see a newly generated address in **My Account**, and then He can use this stealth address like a normal address.

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/usage/stealth_address/5.png" width="75%" height="75%">