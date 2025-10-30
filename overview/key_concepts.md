# Key Concepts

## Leverage

**Leverage** multiplies your buying power. With 10x leverage, $100 controls $1,000 worth of assets.

### Leverage Tiers
- 2x - Conservative
- 5x - Moderate  
- 7x - Aggressive
- 10x - Maximum

Higher leverage = Higher potential returns AND higher risk

## Health Factor

**Health Factor** measures how safe your position is:
```
Health Factor = (Collateral Value × LTV) / Borrowed Value
```

- **> 1.5**: Very Safe 🟢
- **1.2 - 1.5**: Safe 🟡
- **1.09 - 1.2**: Risky 🟠
- **< 1.09**: Liquidation Zone 🔴

## Liquidation

When Health Factor drops below 1.09:
1. Position becomes eligible for liquidation
2. Liquidators repay your debt
3. They receive your collateral + 5% bonus
4. Remaining collateral (if any) returns to you

## Interest Rates

### Supply APY
- Based on utilization of the lending pool
- Higher utilization = Higher APY for lenders

### Borrow APR
- Variable rate based on pool utilization
- Typically 10-25% annually
- Paid continuously, not at maturity

## Supported Protocols

Borrowed funds can be deployed to:

**DEXs**: Jupiter, Orca, Raydium
**Perps**: Drift, Mango, Zeta
**Yield**: Kamino, Tulip, Francium
**Options**: PsyOptions, Zeta

More integrations added regularly.