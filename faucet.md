#  Connecting Stylus Testnets and Getting Test Tokens from Faucets

Before deploying a Stylus smart contract, you need to connect your wallet to the appropriate Stylus testnet and acquire some test tokens for gas fees. Stylus currently runs on Arbitrum's Wasm-compatible testnets which support contracts compiled to WebAssembly (Wasm) via Rust.

# Stylus Testnet RPC Details

To connect MetaMask or any compatible wallet to the Stylus testnet, manually add the following network configuration:
```
Network Name: Stylus Testnet
New RPC URL: https://stylus-testnet.arbitrum.io/rpc
Chain ID: 23011913
Currency Symbol: ETH
Block Explorer URL: https://stylus-explorer.arbitrum.io
```

After adding this configuration to your wallet, you’ll be able to send transactions, deploy contracts, and interact with the Stylus chain just like you would on Ethereum.

# Getting Test Tokens

To pay for deployment and transaction fees on the Stylus testnet, you’ll need some testnet ETH and ARB tokens. 


You can go to one of these faucets, claim your Sepolia Eth (SepETH). Then bridge it from Ethereum Sepolia to Arbitrum Sepolia using the official Arbitrum bridge: https://bridge.arbitrum.io/. 


Sepolia👇
https://sepoliafaucet.com/ 
https://arbitrum.faucet.dev/ (*)
https://www.infura.io/faucet/sepolia
https://sepolia-faucet.pk910.de/ 

Or you can claim ETH Sepolia directly to Arbitrum Sepolia.

Sepolia and Arbitrum Sepolia👇
https://arbitrum.faucet.dev/ 
https://faucet.quicknode.com/arbitrum/sepolia
https://www.l2faucet.com/arbitrum 

Or you can get some USDC on Arb Sepolia/Sepolia from Circle’s faucet👇
https://faucet.circle.com/







# Verifying Connection
Once you've connected to the Stylus testnet and received your test tokens, you can verify the connection by running a simple transaction or viewing your account on the Stylus block explorer.

# 📝 Notes
The Stylus testnet may be reset periodically as it is still in active development.
Test tokens have no real-world value and are only meant for experimentation.


# Remix IDE for Stylus
The most popular web-based IDE supporting the development, compilation, deployment, and interaction of Arbitrum Stylus contracts.: https://docs.welldonestudio.io/code/arbitrum-stylus/



# 📌 Summary
Connecting to the Stylus testnet and funding your wallet with test ETH and ARB tokens is the first step in deploying and testing your Rust-based smart contracts. This setup mirrors a production environment and prepares you for hands-on development on Arbitrum’s Stylus platform.



