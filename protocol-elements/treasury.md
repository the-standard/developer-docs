# 💰 Treasury

The `Treasury` contract accumulates all the Management fees sent from the collateral manager. It's an intermediate contract that can convert between different tokens, currently normalising all rewards into TST or ETH, depending on the strategy&#x20;

* `toStaking()`, sending part of the fees to DAO Vault holders.
* `toGovernance()`, sending part of the fees to the multi-sig to cover gas costs and other expenses.
