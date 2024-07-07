# Governance

Provides a DAO which can be used to upgrade modules of multisig wallet, or any other actions (comming soon in the future).

A Governance Proposal can be created by any user who have enough a special ERC20 token (now the token is called `GovernanceToken`). The `GovernanceToken` is used to count votings, one token one voting. Besides all ERC20 methods supporting, the `GovernanceToken` supports:

- **Delegation**. You can delegate the votings to someone (including yourself) without transfering them
- **Checkpoints Recording**. To prevent users from cheating, the voting number for a user is determined by the start time of each proposal. So any user can't gain their votings by any actions. The checkpoints are recorded on the chain to implement this function

The proposal should incorporate feedback from the Consensus Check and is accompanied by executable onchain code. In our test environment, in order to submit an on-chain Governance proposal, a delegate must have a minimum balance of 0.2m `GovernanceToken`. The voting period lasts 1 hour and a majority vote with a 4m `GovernanceToken` yes-vote threshold wins.

If a proposal wins, it can be queued by anyone. Another 0.5h delay is need to let people know that the proposal is going to be executed. Then the proposal can be executed, of course, by any one.

## Delegate

A user can delegate votes to the delegatee, self or any other address. Users can delegate to 1 address at a time, and the number of votes added to the delegatee's vote count is equivalent to the balance of `GovernanceToken` in the user's account. Votes are delegated from the current block and onward, until the sender delegates again, or transfers their `GovernanceToken`.

If a user want to create proposal or vote, he/she **must delegate to someone**, either himself/herself or someone else. So a user should firstly enter the `Delegate` page.
For example, the one who want to delegate `GovernanceToken` to himself/herself, firstly enter the **Delegate** page, it will show us the current delegation:

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/delegate_overview.png" width="75%" height="75%">

A user can edit the current delegate address by click _Edit_ Button:

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/delegate_edit.png" width="75%" height="75%">

Delegate to _Self_:

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/delegate_self.png" width="75%" height="75%">

Or _Cancel_:

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/delegate_cancel.png" width="75%" height="75%">

Of course, a third address can be input in the text box. If you want to submit the delegation address, just click the _Submit_ button, because it will call a contract, you should confirm it:

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/delegate_submit.png" width="75%" height="75%">

## Proposals

Any one could see all the proposals:

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/proposal_overview.png" width="75%" height="75%">


There're several kinds of status for proposals:
  - *Pending*: The proposal is just created, a short time is delayed before users can vote
  - *Active*: The proposal is active for voting now
  - *Canceled*: The proposal has been canceled
  - *Defeated*: The proposal is defeated, which means most people votes for **No** or the quorum is not satisfied
  - *Succeeded*: The proposal wins most **Yes** votes and satisfies the quorum, thus the proposal could now be queued
  - *Queued*: The proposal now is queued, after the queued time is up, it should be executed by anyone
  - *Executed*: The proposal has been executed
  - *Expired*: The proposal does not execute on a given time (now 14 ays) after queued, the proposal can't be executed then


Each proposal could show details if you choose one. If a proposal is *Active*, it means that you can vote **Yes** or **No** on it. The votings you can vote is shown on the page:

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/vote_overview.png" width="75%" height="75%">

For example, you can vote for "Yes" and then submit:

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/vote_submit.png" width="75%" height="75%">

If the transaction is confirmed on the chain:

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/vote_submit_on_chain.png" width="75%" height="75%">

The vote result of the current proposal will be shown (the votings from you will be highlight):

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/vote_display_vote_information.png" width="75%" height="75%">

If you want to create a proposal, you should have enough `GovernanceToken`:

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/create_proposal_add_information.png" width="75%" height="75%">

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/create_proposal_submit.png" width="75%" height="75%">

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/create_proposal_submit_success.png" width="75%" height="75%">

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/create_proposal_submit_on_the_chain.png" width="75%" height="75%">

## Queue

If a proposal satisfy all the conditions below:

- The vote for the proposal last enough time (currently for test, we set a shorter time with 1 hour)
- More **Yes** votings than **No**
- The **Yes** votings is greater than the quorum (currently 4M `GovernanceToken`)

Then the proposal could be queued by anyone:

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/queue.png" width="75%" height="75%">

The time when the proposal can be executed will be shown if queued:

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/queue_on_chain.png" width="75%" height="75%">

## Execute

After several hours (currently 0.5h), the proposal which is queued before could be executed by anyone:

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/execute.png" width="75%" height="75%">

If the proposal is successfully executed, the status of the proposal will become **Executed**:

<img src="https://github.com/0xEigenLabs/0xeigenlabs.github.io/raw/main/docs/images/governance/queue_on_chain.png" width="75%" height="75%">

Gloria! The proposal is finally executed! By the governance DAO!
