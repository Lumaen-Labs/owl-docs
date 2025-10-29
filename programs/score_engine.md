### Score Engine

Responsible for:

* Maintaining user credit scores
* Storing last update timestamp
* Enforcing decay over time

**Account Structure:**

```rust
#[account]
pub struct ScoreAccount {
    pub value: u64,
    pub last_updated: i64,
    pub user: Pubkey,
}
```

**Instruction Example:**

```rust
pub fn update_score(ctx: Context<UpdateScore>, new_score: u64) -> Result<()> {
    let score = &mut ctx.accounts.score;
    require!(new_score <= 1000, ScoreError::InvalidScore);
    score.value = new_score;
    score.last_updated = Clock::get()?.unix_timestamp;
    Ok(())
}
```

---