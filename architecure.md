## 1. System Architecture

Each component of the protocol serves a distinct function, yet all operate in sync through the `core_router`:

```
              ┌────────────────────────────┐
              │        zkTLS Proofs        │
              └────────────┬───────────────┘
                           │
                Off-chain Verifier & Oracle
                           │
              ┌────────────▼───────────────┐
              │        Core Router         │
              ├────────────┬───────────────┤
              │            │               │
       ┌──────▼─────┐ ┌────▼────┐ ┌────────▼────────┐
       │ ScoreEngine│ │CreditPool│ │RestakeRegistry │
       └─────────────┘ └─────────┘ └────────────────┘
                            │
                       ┌─────▼──────┐
                       │Liquidation │
                       └────────────┘
```

**Key Ideas:**

* **Core Router**: Central dispatcher, entry point for all Solana instructions.
* **Score Engine**: Manages borrower reputation, updated via zkTLS verifications.
* **Credit Pool**: Handles loans, repayments, and health factor computation.
* **Restake Registry**: Maps validator restaked capital to protocol pools.
* **Liquidation Engine**: Triggers liquidations when positions go under threshold.

---

## 2. Credit Flow Overview

### Borrower Lifecycle

1. **Registration:** User initializes a `UserAccount` via `core_router`.
2. **Score Proof Submission:** Off-chain zkTLS verifier submits score updates using a signed transaction.
3. **Borrow Request:** Borrower submits `borrow` instruction specifying amount and asset.
4. **Loan Evaluation:** `CreditPool` checks score and available liquidity.
5. **Fund Disbursement:** Approved loans transfer from pool vault PDA to borrower.
6. **Repayment:** Borrower repays loan + interest.
7. **Score Adjustment:** Repayments feed back into score engine.

---

## 3. Liquidation Engine

Monitors health factor and liquidates unhealthy positions.

```rust
pub fn check_liquidation(ctx: Context<Check>) -> Result<()> {
    let hf = compute_health_factor(ctx);
    if hf < 1.0 {
        trigger_liquidation(ctx)?;
    }
    Ok(())
}
```

---

## 4. Score Verification Flow (zkTLS + Oracle Adapter)

Owl Finance uses zkTLS proofs to verify off-chain data authenticity:

1. User connects to an off-chain zkTLS verifier (like Opacity).
2. The verifier fetches authenticated data (e.g., trading history, repayment logs).
3. A **zk proof** is generated asserting validity.
4. Proof data is submitted on-chain via `core_router`.

```rust
// pseudo-code snippet
let proof_data = generate_zk_proof(user_activity);
core_router.update_score_with_proof(proof_data)?;
```

---

## 5. Program Accounts

| Account           | Type | Description                               |
| ----------------- | ---- | ----------------------------------------- |
| `UserAccount`     | PDA  | User profile with loan + score references |
| `ScoreAccount`    | PDA  | Borrower’s score state                    |
| `CreditPool`      | PDA  | Asset pool (USDC, USDT, etc.)             |
| `RestakeRegistry` | PDA  | Validator collateral record               |
| `LoanAccount`     | PDA  | Active loan metadata                      |

---

## 6. Instruction Reference

| Instruction    | Description                   | Parameters              |
| -------------- | ----------------------------- | ----------------------- |
| `init_user`    | Initializes a user account    | -                       |
| `update_score` | Updates user score            | `new_score: u64`        |
| `borrow`       | Issues a loan                 | `amount: u64`           |
| `repay`        | Repays loan                   | `amount: u64`           |
| `restake`      | Registers validator’s restake | `validator_key: Pubkey` |
| `liquidate`    | Liquidates unhealthy position | `user: Pubkey`          |

---

## 7. Risk Engine

Dynamic parameters:

* `BaseLTV` = 0.4
* `MaxLTV` = 0.8
* `ScoreMultiplier` adjusts linearly between 0–1
* Decay: score reduces 5% every 7 days of inactivity

Future addition: score volatility coefficient based on protocol usage variance.

---
