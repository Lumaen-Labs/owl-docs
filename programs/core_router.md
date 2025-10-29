### Core Router

Central Solana program responsible for routing all user instructions to respective modules.

```rust
#[derive(Accounts)]
pub struct Route<'info> {
    #[account(mut)]
    pub authority: Signer<'info>,
    pub system_program: Program<'info, System>,
}

pub fn route_instruction(ctx: Context<Route>, action: Action, data: Vec<u8>) -> Result<()> {
    match action {
        Action::UpdateScore => invoke_score_update(ctx, data),
        Action::Borrow => invoke_borrow(ctx, data),
        Action::Repay => invoke_repay(ctx, data),
        Action::Restake => invoke_restake(ctx, data),
    }
}
```

**Purpose:** keeps modularity — future modules (insurance, governance) can be plugged in without redeploying everything.

---