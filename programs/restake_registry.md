### Restake Registry

Tracks validator restaked collateral used to secure protocol-level debt.

**Purpose:**

* Register validators participating in protocol restaking
* Record total restaked JitoSOL
* Manage slashing or insurance triggers

```rust
#[account]
pub struct RestakeRegistry {
    pub validator_key: Pubkey,
    pub restaked_amount: u64,
    pub slashed: bool,
}
```

---