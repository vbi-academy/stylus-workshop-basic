# Challenge: Simple Storage Contract

Compile and deploy your first smart contract. The goal is to implement the smart contract on the testnet. 


## Prerequisites
Before starting, ensure you have the following installed:
* Node.js (version 18.17 or higher)
* Yarn – A package manager alternative to npm
* Git – For cloning repositories and managing source code
* WSL (for Windows users) – Either Ubuntu or Debian is fine
* Docker – Used to pull and run the Stylus build environment
* Curl – Used to download the Rust installation script

###  Install Rust (includes rustc, rustup, and cargo)

> Note for Windows users: You must run the command below inside a WSL terminal (do not run it from PowerShell or Command Prompt)

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source ~/.bashrc  # or restart your terminal
```
### 📦 install cargo-stylus:
```bash
cargo install cargo-stylus
```

If you’re using Ubuntu and encounter errors related to pkg-config, run the following commands to install the necessary dependencies:
```
sudo apt update
sudo apt install pkg-config
sudo apt install libssl-dev
sudo apt install build-essential
```

Foundry – An essential toolkit for smart contract development:
```
curl -L https://foundry.paradigm.xyz | bash

```

After installing Foundry, you’ll need to configure your environment variables to use command-line tools like forge, cast, etc. Add the following path to your shell configuration file (.bashrc, .zshrc, or whichever shell you’re using):

```
export PATH="$HOME/.foundry/bin:$PATH"
```
```
source ~/.bashrc 
# or 
source ~/.zshrc
```

To check versions of other related tools, you can run the following:
```
cargo stylus --version
//cargo --version
//rustup --version
//rustc --version
//cast --version
//forge --version
```


# Start the local devnode in Docker:
```
docker pull offchainlabs/cargo-stylus-base:0.6.1
```

Then Install your devnode
```
git clone https://github.com/OffchainLabs/nitro-devnode.git
cd nitro-devnode
```
```
./run-dev-node.sh
```

# Challenge Setup
Use the `cargo-stylus` command to create a new project:
```
cargo stylus new simple_storage
cd simple_storage
```

Open the `src/lib.rs` file and replace the content with the following code:


```rust
// Allow `cargo stylus export-abi` to generate a main function.
#![cfg_attr(not(feature = "export-abi"), no_main)]
extern crate alloc;

/// Use an efficient WASM allocator.
#[global_allocator]
static ALLOC: mini_alloc::MiniAlloc = mini_alloc::MiniAlloc::INIT;

/// Import items from the SDK. The prelude contains common traits and macros.
use stylus_sdk::{alloy_primitives::U256, prelude::*};

// Define some persistent storage using the Solidity ABI.
// `Storage` will be the entrypoint.
sol_storage! {
    #[entrypoint]
    pub struct Storage {
        uint256 value;
    }
}

/// Declare that `Storage` is a contract with the following external methods.
#[external]
impl Storage {
    /// Gets the value from storage.
    pub fn get_value(&self) -> U256 {
        self.value.get()
    }

    /// Sets a value in storage to a user-specified value.
    pub fn set_value(&mut self, new_value: U256) {
        self.value.set(new_value);
    }

    /// Multiplies the stored value by a user-specified value.
    pub fn mul_value(&mut self, multiplier: U256) {
        self.value.set(multiplier * self.value.get());
    }

    /// Adds a user-specified value to the stored value.
    pub fn add_value(&mut self, increment: U256) {
        self.value.set(increment + self.value.get());
    }

    /// Increments `value` and updates its value in storage.
    pub fn increment(&mut self) {
        let value = self.value.get();
        self.set_value(value + U256::from(1));
    }
}
```

# Deploying and Testing the Contract

## Check the Contract:

```
cargo stylus check --endpoint https://sepolia-rollup.arbitrum.io/rpc
```

Ensure you have a valid private key saved in a file (e.g., `private_key.txt`). The file should contain only the private key without any extra characters or spaces.

```
cargo stylus deploy --private-key-path=/path/to/private_key.txt --endpoint https://sepolia-rollup.arbitrum.io/rpc 
```




Fill your contract address to `readme` file.

statement. The address your contract gets deployed to will likely differ, so take note of that address. Select it and copy it to your clipboard.




# Interacting with your contract in CLI 

We'll set up a `.env` file with a few variables to avoid repetitive typing in the console:

```
RPC_URL=https://sepolia-rollup.arbitrum.io/rpc
STYLUS_CONTRACT_ADDRESS=
PRIV_KEY=
```



We'll now use cast, which was installed as part of our Foundry CLI suite, to call the contract. Later we'll send a transaction to the contract. The difference between call and send is that call costs no gas, so it can only be used to invoke read-only functions.

```bash
cast call --rpc-url $RPC_URL --private-key $PRIV_KEY $STYLUS_CONTRACT_ADDRESS "number()(uint256)"
```

Which should return:

```
0
```

We’re passing two flags in the command
* `--rpc-url` is the address of the Stylus chain we deployed to,
* `--private-key` is your private key, which belongs to the address 


Let's try incrementing it! This time, we'll invoke the send command.

```bash
cast send --rpc-url $RPC_URL --private-key $PRIV_KEY $STYLUS_CONTRACT_ADDRESS "increment()"
```

Which will display something like:

```
blockHash 0xb4087ada199419ca7e07a442059dc10b4cf0ef3709fcb906b8ecac9eff570136
...
```

Our transaction went through successfully and we even received a `transactionHash` and detailed logs in the CLI.


To show how to pass arguments with `cast`, let’s try setting the counter to `19` using the set_number function. But instead of calling it as set_number, we use setNumber — this is the camelCase style that matches Solidity’s naming. Using this format helps make Rust and Solidity contracts work better together.

```
cast send --rpc-url $RPC_URL --private-key $PRIV_KEY $STYLUS_CONTRACT_ADDRESS "setNumber(uint256)()" 19
```


 Now, let's check our work:

```bash
cast call --rpc-url $RPC_URL --private-key $PRIV_KEY $STYLUS_CONTRACT_ADDRESS "number()(uint256)"
 ```

It will show:

```
19
```




