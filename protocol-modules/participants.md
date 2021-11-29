# 🧑💻 Participants

## Defintion

A participant can be a human, smart contract(s) or computer system. These can interact with Smart Vaults or respective smart contracts individually. Even though it is possible to interact individually with all smart contracts deployed to the system, we highly encourage for end users to rely on the Smart Vault interface to manage all interactions within the Standard protocol.

## Participant types

Current user types acknowledged by the the protocol

### User (End-User)

A user is someone who uses the Standard Protocol and the [Smart Vaults ](smart-vault.md)to generate a stable coin backed by inflation proof assets. For this a user would need to use interfaces provided to them. A user can select different strategies within the protocol to generate these.

Basic functions

* Deposits funds into vaults, to receive Stable Currency tokens, through calling `deposit()`;
* Withdraws funds from smart vaults, by depositing (effectively burning) Stable Currency tokens tokens into smart vaults and receiving the corresponding deposit token amount back in return, through calling `withdraw()`. If the vault does not have enough funds to handle the withdrawal, this triggers a cascading `withdraw()` call via the `Controller` to the Strategy to liquidate enough funds to process the withdrawal.

Advanced functions

* Exchange funds within the smart vault via `swap()` using attached swapping mechanisms. These swaps can be facilitated only if the smart vault has enough funds to cover the fee and a buffer to avoid liquidation while the operation is running.  This allows to the user to swap locked in funds to another potentially more stable asset.
* `InitialSwap()` can only be used on the initial deposit (generation) of the Smart Vault. When doing the initial deposit the collateral can be swapped to another before it goes into the smart vault and the Stable Currency Token is generated.

{% hint style="info" %}
Advanced functionality can only be used when the market provides the liquidity and the user pays potentially more fees to cover the swap fees and slippage. It can still be beneficial for the user in the long run to avoid swapping via other mechanism.
{% endhint %}

### DAO Member

Any owner of the Standard Token (TST) is a member of the Standard DAO. There are two possible ways to interact with the Dao and benefit from owning the Standard Token:&#x20;

#### 1. Dao Vault Staking

If TST holder want to earn a reward for participating, a DAO member must send their funds to a DAO Vault. a DAO Vault is a special smart vault with two functionalities (possible more to come).

1. The amount of TST staked in the DAO Vault will determine the amount of fee share this vault will receive from the protocol. Fees are paid by users in form of TST.
2. Voting (Since voting is currently happening through [Snapshot.org](https://snapshot.org/#/).) is currently a WIP. Voting will later be enabled within the Smart Vault System / The Standard DAO website. For now please use below strategy if you want to vote on proposals.

#### 2. Owning TST in compatible wallet

If you hold TST you can use your TST to vote on DAO specific topics or propose topics to vote on. Please be active in our Discord if you want to know more. In general voting is commenced through

[Snapshot.org](https://snapshot.org/#/)

Following list compatible wallets (there are more but these are the most popular ones).

* [Metamask](https://metamask.io)
* [MyEtherwallet](https://www.myetherwallet.com)
* [Eidoo](https://eidoo.io)
* [Argent](https://www.argent.xyz)

## Governor

A Governor can deploy a strategy previously voted on the DAO. Governors get rewarded for deploying the different elements that are voted on into the core

{% content-ref url="core.md" %}
[core.md](core.md)
{% endcontent-ref %}

#### What is the governor able to deploy?

The governor deploys a set of rules voted in by the DAO, these rules are broken down into smart contracts by the development team:

* [Strategies](strategies.md)
* Token Contracts
* Applications
* Stability Fees
* Liquidation Parameters

In an optimal world strategies are deployed automatically after being voted on by the DAO. We are constantly perusing the fully decentralisation of the system.

## Auditor

The designated Auditors job is to do a pre-audit of asset custodians, vaulting facilities, documents and more to ensure the principles of the protocol are followed. The Auditor gets highly rewarded for the job. To become an auditor you must be voted in by the DAO.&#x20;

## Master Custodian

The mater custodian is a bot that calls contract functions. It queries the appropriate strategies and updates the Smart Vaults accordingly.&#x20;

## Asset Custodian

### **Independent Custodians**

Independent Custodians are tokenised asset providers who have issued their own asset backed tokens.\
\
It is the responsibility of The Standard DAO to set the security standards and audit the physical vaulting facilities of independent custodians. Once the DAO’s security criteria have been met, the protocol will onboard independent custodian tokens that can be used as collateral in Smart Vaults.

Asset backed tokens will be enabled using strategies that the DAO is voting on.

{% content-ref url="strategies.md" %}
[strategies.md](strategies.md)
{% endcontent-ref %}

### **Native Custodians**

Native custodians are usually precious metals dealers or asset vaulting providers who are experts in securing and dealing with hard assets. Such custodians have legal contracts with The Standard DAO to ensure compliance with its custodian security framework. Users can access their vaulted assets balances via The Standard Protocol platform.&#x20;

A Native Custodian uses The Standard Protocol to tokenise the assets within the platform. These tokens cannot be withdrawn from the platform. Instead they provide a secure accounting mechanism between the Smart Vaults and the hard asset custodians.&#x20;

#### **Tokenizing Assets**

The `Native Custodian Framework` Protocol has built-in functions that enable native custodians to tokenise their assets. Each native custodian is subject to a first time and periodical audit by the Standard DAO. Audit protocols might change, depending on the vote of the DAO.

## **Oracles**

Oracles are data feeds that connect Ethereum to off-chain, real-world information so that you can query data in your smart contracts. For example, prediction market dapps use oracles to settle payments based on events. A prediction market may ask you to bet your ETH on who will become the next president of the United States. They'll use an oracle to confirm the outcome and payout to the winners.

The Standard will use multiple oracles, [read more in the oracle section.](../protocol-elements/oracles.md)

## 3rd Party apps/modules (dApps)

As a protocol 3rd party apps can use it to generate soft hard pegged or any other currencies either using strategies or develop other compatible dApps on our platform.\










