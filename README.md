# Blueshift Anchor Escrow
<img width="745" height="838" alt="Screenshot 2026-02-25 at 7 09 51 PM" src="https://github.com/user-attachments/assets/0b23c981-a73e-42ae-971a-96ccd4e0182c" />

Token escrow program on Solana using Anchor. Allows peer-to-peer SPL token swaps without intermediaries.

## Overview

Maker deposits Token A into escrow vault and specifies how much Token B they want. Taker provides Token B and gets Token A. Maker can refund anytime if deal doesn't happen.

## Instructions

### make
Creates escrow and deposits tokens.

Parameters:
- `seed: u64` - Unique ID for the escrow
- `receive: u64` - Amount of Token B wanted
- `amount: u64` - Amount of Token A to deposit

### take
Completes the swap. Transfers Token B from taker to maker, Token A from vault to taker. Closes vault and escrow accounts.

### refund
Cancels escrow. Returns deposited tokens to maker and closes accounts.

## State

```rust
pub struct Escrow {
    pub seed: u64,
    pub maker: Pubkey,
    pub mint_a: Pubkey,
    pub mint_b: Pubkey,
    pub receive: u64,
    pub bump: u8,
}
```

## Setup

```bash
yarn install
anchor build
anchor test
```

## Deploy

```bash
anchor deploy
```

Update program ID in `Anchor.toml` and `lib.rs` after deployment.

## Project Structure

```
programs/blueshift_anchor_escrow/src/
├── lib.rs
├── state.rs
├── errors.rs
└── instructions/
    ├── make.rs
    ├── take.rs
    └── refund.rs
```

## Notes

- Uses PDA vaults for security
- Compatible with Token-2022
- Rent returned to maker on close
- Supports multiple escrows per maker via seed parameter

Program ID: `HfKrsayizJgU275W9doH5uW3k55Q8XF4nAoHqrhRnU8t`
