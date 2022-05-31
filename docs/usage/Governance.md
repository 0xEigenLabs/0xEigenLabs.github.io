# Governance
Provides a DAO which can be used to upgrade modules of multisig wallet, or any other actions (comming soon in the future).

A Governance Proposal can be created by any user who have enough a special ERC20 token (now the token is called `GovernanceToken`). The proposal should incorporate feedback from the Consensus Check and is accompanied by executable on-chain code. In our test environment, in order to submit an on-chain Governance proposal, a delegate must have a minimum balance of 0.2m `GovernanceToken`. The voting period lasts 1 hour and a majority vote with a 4m `GovernanceToken` yes-vote threshold wins.

If a proposal wins, it can be queued by anyone. Another 0.5h delay is need to let people know that the proposal is going to be executed. Then the proposal can be executed, of course, by any one.

## Delegate
A user can delegate votes to the delegatee, self or any other address. Users can delegate to 1 address at a time, and the number of votes added to the delegatee's vote count is equivalent to the balance of `GovernanceToken` in the user's account. Votes are delegated from the current block and onward, until the sender delegates again, or transfers their `GovernanceToken`.

If a user want to create proposal or vote, he/she **must delegate to someone**, either himself/herself or someone else. So a user should firstly enter the `Delegate` page.
For example, the one who want to delegate `GovernanceToken` to himself/herself, firstly enter the **Delegate** page, it will show us the current delegation:
<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/governance/delegate_overview.png" width="75%" height="75%">

A user can edit the current delegate address by click *Edit* Button:
<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/governance/delegate_edit.png" width="75%" height="75%">

Delegate to *Self*:
<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/governance/delegate_self.png" width="75%" height="75%">

Or *Cancel*:
<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/governance/delegate_cancel.png" width="75%" height="75%">

Of course, a third address can be input in the text box. If you want to submit the delegation address, just click the *Submit* button, because it will call a contract, you should confirm it:

<img src="https://github.com/ieigen/ieigen.github.io/raw/main/docs/images/governance/delegate_submit.png" width="75%" height="75%">