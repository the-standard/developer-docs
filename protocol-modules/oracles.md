# Oracles

{% hint style="info" %}
**Please read about oracles here **[**https://ethereum.org/en/developers/docs/oracles/**](https://ethereum.org/en/developers/docs/oracles/)****
{% endhint %}

**The Standard Oracle Implementation**

The Standard will use the Uniswap v3 TWAP oracles as this has been proven to be a solid source of data for price discovery.

As Uniswap offers good on-chain data the standard protocol also will need the data from from off-chain sources for gold/silver/oil or any asset that the DAO seems worthy to be a good hedge against inflation. For this reason we also use the data from [https://data.chain.link/](https://data.chain.link)

Potentially tokenised indices can be used as collateral as well.

## General Oracle Implementation



![Oracle structure](<../.gitbook/assets/image (2).png>)

**TWAP**

The time-weighted price algorithm (TWAP) is quite simple: the price **P** multiplied by how long it lasts **T **is continuously added to** **a cumulative value **C**.

For example,

* when timestamp = 0 & ETH price = 3000: C = 0 (initialisation)
* when timestamp = 200 & ETH price = 3200: C = `0 + 3000 * (200 — 0) = 600,000`
* when timestamp = 250 & ETH price = 3150: C = `600,000` + `3200 * (250 — 200)` = `760,000`

The TWAP between time (0, 250) is `(760,000 — 0) / (250 — 0) = 3,040`, which satisfies that price 3000 lasts for `4/5` of the time and price 3200 lasts for `1/5`: `3000 * 4 / 5 + 3200 / 5 = 3,040`.



