# Strategies

### Introduction

A Strategy is a smart contract that reflects the current strategy of the Standard Protocol to handle the issuance of Stable currency tokens generated by the users and Smart Vaults respectively. The DAO will set the rules and vote on different aspects.

There are two types of strategies.

## Global Strategy

A global strategy will affect all smart vaults and is used by all `collateral managers` at the same time. Global strategies are used by smart vaults. Use cases are.

1. Stability Fee&#x20;
2. Network Fee
3. Ratio Stability Fee / Network Fee

## Local Strategy

A local strategy is by definition a single instance of smart vault. Local Strategies take global strategies into account overwriting however if necessary the parameters of certain function.

A `LocalStrategy` contract needs to be deployed for each colleteral/stablecoin/smart vault. Only DAO approved strategies can be deployed and only DAO approved tokens can be used as colletoral&#x20;



## Functions

The following functions can only be called by an address having the `Governor Role`, which means the DAO or the multisig if not yet revoked.

#### updateStrategyDebtRatio

```javascript
function updateStrategyDebtRatio(address strategy, uint256 _debtRatio)  external;
```

Modifies the portion of the debt dedicated to the funds a strategy has access to.

The update has to be such that the `debtRatio` does not exceeds the 100% threshold as the manager cannot lend collateral that it does not own.

Parameters:

* `strategy`: The address of the Strategy
* `_debtRatio`: The share of the total assets that the `strategy` has access to

#### setStrategyEmergencyExit

```javascript
function setStrategyEmergencyExit(address strategy) external;
```

Triggers an emergency exit for a strategy and then harvests it to fetch all the funds

#### addStrategy

```javascript
function addStrategy(address strategy, uint256 _debtRatio) external;
```

Implements the new `strategy` for the `PoolManager`. Multiple checks are made such that the contract must not already belong to the `PoolManager` but also that the tokens considered are consistent in both `strategy` and `PoolManager` contracts.

Parameters:

* `strategy`: The address of the Strategy to add
* `_debtRatio`: The share of the total assets that the `strategy` has access to

#### revokeStrategy

```javascript
function revokeStrategy(address strategy) external;
```

Revokes the `Strategy` from `PoolManager` strategies. The normal way to revoke a strategy should go through in order:

1. `strategy.debtRatio` is set to 0.
2. `strategy.harvest()` has been called enough time to recover all capital gain/losses and the initial capital.
3. `revokeStrategy()` is called .

Parameters:

* `strategy`: The address of the Strategy to revoke

#### withdrawFromStrategy

```javascript
function withdrawFromStrategy(IStrategy strategy, uint256 amount) external;
```

Withdraws a given amount from a Strategy. It may not recover `amount` from the strategy, as we may not be able to withdraw from the lending protocol the full amount. In this last case we only update the parameters by setting the loss as the gap between what has been asked and what has been returned.

Parameters:

* `strategy`: The address of the Strategy
* `amount`: The amount to withdraw

### Strategy-Only Functions

The following functions can only be called by a `Strategy` or will only make sense if they are called by one of them. They are used by the strategies related to this `PoolManager` to either query information from the `PoolManager` or transmits information to it.

#### creditAvailable

```javascript
function creditAvailable() external returns(uint256);
```

Tells a strategy how much it can borrow from this `PoolManager`. Since this function is a view function, there is no need to have an access control logic.

#### debtOutstanding

```javascript
function debtOutstanding() external returns(uint256);
```

Tells a strategy how much it owes to this `PoolManager`

#### report

```javascript
function report(uint256 gain, uint256 loss, uint256 debtPayment) external;
```

Reports the gains or losses made by a strategy. This is the main contact point where the strategy interacts with the `PoolManager.` The strategy reports back what it has free, then the `PoolManager` contract "decides" whether to take some back or give it more. Note that the most it can take is `gain + _debtPayment`, and the most it can give is all of the remaining reserves. Anything outside of those bounds is abnormal behavior.

Parameters:

* `gain`: Amount strategy has realized as a gain on its investment since its last report, and is free to be given back to `PoolManager` as earnings
* `loss`: Amount strategy has realized as a loss on its investment since its last report, and should be accounted for on the `PoolManager`'s balance sheet. The loss will reduce the `debtRatio`. The next time the strategy will harvest, it will pay back the debt in an attempt to adjust to the new debt limit.
* `debtPayment`: Amount strategy has made available to cover outstanding debt
