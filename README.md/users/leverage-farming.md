---
cover: ../.gitbook/assets/WhatsApp Image 2025-10-29 at 15.00.02.jpeg
coverY: 0
---

# 🧑‍🌾 leverage farming

Leverage farming uses borrowed capital to amplify yield farming returns. Instead of farming with only your capital, borrow additional funds to increase position size and yields.

### Strategy Comparison

{% columns %}
{% column width="50%" %}
**Traditional Farming**

* Capital: $1,000
* APY: 20%
* Annual return: $200
{% endcolumn %}

{% column width="50%" valign="middle" %}
**5x Leverage Farming**

* Capital: $1,000
* Borrowed: $4,000
* Total position: $5,000
* Yield: 20% on $5,000 = $1,000
* Interest: 15% on $4,000 = $600
* Net return: $400 (40% ROI)
{% endcolumn %}
{% endcolumns %}



#### Integrated Protocols

* Concentrated and standard liquidity pools
* Standard AMM and concentrated liquidity
* &#x20;Automated vault strategies
* Auto-compounding vaults

### ROI Calculation

{% code title="" %}
```
Net APY = (Farm APY × Leverage) - (Borrow APR × (Leverage - 1))
```
{% endcode %}

Example with 5x leverage:

* Farm APY: 30%
* Borrow APR: 15%
* Net APY = (30% × 5) - (15% × 4) = 90%

### Safety Guidelines

{% stepper %}
{% step %}
### Start conservatively

Begin with lower leverage (2–3x).
{% endstep %}

{% step %}
### Prefer stable pairs

Use stable pairs to minimize impermanent loss.
{% endstep %}

{% step %}
### Risk controls

Set stop-loss orders.
{% endstep %}

{% step %}
### Monitoring

Monitor positions regularly.
{% endstep %}

{% step %}
### Maintain buffer

Keep buffer collateral.
{% endstep %}
{% endstepper %}

