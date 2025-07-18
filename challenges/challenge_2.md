# Assignment: ERC20 token smart contract

> Launching ERC20 tokens on Arbitrum using stylus

In this challenge, you'll learn how to build and deploy a custom ERC-20 token smart contract using Rust and Stylus. The ERC-20 token standard is one of the most widely used standards for creating fungible tokens on Ethereum and EVM-compatible chains.

With Stylus, you can implement ERC-20 tokens in Rust compiled to WebAssembly (Wasm) while benefiting from low gas costs and memory safety.

# Contract Overview
This Stylus-based ERC-20 contract includes the following core features:


Token metadata: name, symbol, and decimals
Token state: balances and allowances
Functions: transfer, approve, transfer_from, mint, balance_of, and allowance

```
#[storage]
struct Storage {
    name: String,
    symbol: String,
    decimals: u8,
    total_supply: u128,
    balances: Map
}
```

* name: Full name of the token
* symbol: Short ticker symbol (e.g., "TKN")
* decimals: Number of decimal places (usually 18)
* total_supply: Total tokens minted
* balances: Mapping from address to token balance
* allowances: Mapping from (owner, spender) to allowed amount




