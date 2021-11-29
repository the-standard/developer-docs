# 🈸 Application Manager

Manages applications developed by 3rd parties to plug into the protocol. Applications have to be approved to be able to be selected from the Smart Vault interface. However applications in general do NOT need approval to be available for users since its decentralised system. The DAO however will vote on applications or other modules to be used in or with strategies to offer the users of the protocol a wide range of services.&#x20;

### Possible applications

* Directly swapping of currencies
* Bridge between blockchains
* Staking mechanisms
* DeFi products like future contracts etc.&#x20;

## Functions

In reality we need to deploy an application manager per application. Application managers need to be approved by the DAO and deployed by the Governor.

* `SetApplicationState`
* `GetApplicationState`
* `SetApplicationParameters`
* `GetApplicationParameters`
* `SetApplicationType`
* `GetApplicationType`

## States

A State is just a flag to prevent old dApps that might be not maintained or incompatible to be linked to protocol activities which might lead to the loss of funds for the end-user or the DAO.

* `Active`
* `Inactive`
* `Deprecated (Not encouraged, use at your own risk)`

## Parameters

Technically any parameters necessary for the dApp to work within the system or be compatible.

* Name
* Developer
* Blockchain
* Description
* URL
* Compatibilities
* Version
* Functions
  * Read
  * Write
*

## Type

Based on the blockchain model that is leveraged, decentralised applications can be classified into three categories:

* **Type 1:**\
  These dApps have their own blockchain, for example, Bitcoin. Other alternative cryptocurrencies with their own blockchain also fall under this category.
* **Type 2:**\
  This breed of dApps leverages the blockchain of Type 1 apps. These decentralized apps are protocols and have tokens necessary for their functioning. The Omni Protocol is the best example of a Type 2 applications. Omni is a distributed trading platform developed on top of the Bitcoin blockchain as a ‘layer’ to facilitate ‘peerless, trustless, and effortless’ exchange of assets or value between parties without involving middlemen.
* **Type 3:**\
  Type 3 dApps use the protocol of the Type 2 application. The SAFE Network (Secure Access for Everyone) is an example of a Type 3 dApp. It is a decentralized data storage and communications network that replaces data centers and servers with the additional computing resources of its users. It is an autonomous data network that enables the creation of censorship-resistant websites and applications. It leverages the Omni Protocol for issuing SafeCoins that are then used to allow for its functional aspects.









