# Understanding Risk

## Risk Types

### Liquidation Risk
Positions are liquidated when health factor drops below 1.09. This results in loss of collateral. Monitor health factor and maintain adequate buffer.

### Interest Rate Risk
Borrowing rates vary based on utilization. High demand can increase rates, affecting profitability. Consider rate changes in strategy planning.

### Impermanent Loss
Liquidity provision strategies face IL risk when asset prices diverge. Use correlated assets or stable pairs to minimize impact.

### Smart Contract Risk
While audited, smart contracts may contain undiscovered vulnerabilities. Start with small positions and diversify across strategies.

## Risk by Leverage

| Leverage | Risk Level | Recommended For |
|----------|------------|----------------|
| 2-3x | Low | Beginners |
| 4-6x | Medium | Experienced users |
| 7-10x | High | Advanced traders |
| 11-15x | Very High | Expert users only |

## Health Factor

Health Factor = (Collateral Value × LTV) / Borrowed Value

- **>1.5**: Safe
- **1.2-1.5**: Monitor closely
- **1.09-1.2**: High risk
- **<1.09**: Liquidation

## Risk Mitigation

1. **Use appropriate leverage** for your experience level
2. **Diversify** across multiple strategies
3. **Set alerts** for health factor changes
4. **Maintain buffer** collateral
5. **Understand** strategies before executing
6. **Start small** and scale gradually

## Liquidation Process

When health factor drops below 1.09:
1. Position becomes eligible for liquidation
2. Liquidator repays debt
3. Liquidator receives collateral + 5% bonus
4. Remaining collateral returns to user

To avoid liquidation:
- Add more collateral
- Partially repay debt
- Close position before reaching threshold