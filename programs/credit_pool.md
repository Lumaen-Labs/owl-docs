### Credit Pool

Handles liquidity, loan issuance, and repayment.

**Account Layout:**

```rust
#[account]
pub struct CreditPool {
    pub asset_mint: Pubkey,
    pub total_liquidity: u64,
    pub borrowed: u64,
    pub interest_rate: u64,
}
```

**Borrow Flow:**

```rust
pub fn borrow(ctx: Context<Borrow>, amount: u64) -> Result<()> {
    let user_score = ctx.accounts.score.value;
    require!(user_score > MIN_SCORE, CreditError::LowScore);

    let loan_limit = compute_ltv(user_score);
    require!(amount <= loan_limit, CreditError::ExceedsLimit);

    transfer_from_pool(ctx, amount)?;
    Ok(())
}
```

---