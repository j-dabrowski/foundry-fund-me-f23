# Foundry Fund Me – F23

**A decentralized crowdfunding smart contract built using the Foundry toolkit and Chainlink oracles.**

This project was developed as part of the Cyfrin Foundry Course and covers the full lifecycle of smart contract development: writing, testing, deployment, gas analysis, and interaction through the CLI.

---

## Foundry Toolkit

Foundry is a blazing fast, portable, and modular toolkit for Ethereum application development written in Rust.

It includes:

- **Forge**: Ethereum testing framework
- **Cast**: CLI for interacting with contracts and the blockchain
- **Anvil**: Local testnet node
- **Chisel**: Solidity REPL

Documentation: https://book.getfoundry.sh/

---

## 🧰 Features

- Chainlink-integrated minimum funding
- Custom deployment and interaction scripts
- Local, forked, and testnet testing
- Gas snapshotting and analysis
- Cast-based CLI contract interaction
- Storage inspection and layout viewing

---

## 🔧 Setup

```bash
forge init
forge install smartcontractkit/chainlink-brownie-contracts@1.3.0 --no-commit
```

### Add remappings to `foundry.toml`:

```toml
remappings = [
    "@chainlink/contracts/=lib/chainlink-brownie-contracts/contracts/"
]
```

Then:

```bash
forge build
```

---

## 🧪 Testing

```bash
forge test
forge test -vv
```

### Types of Tests

1. **Unit**: Single function/module
2. **Integration**: Internal components
3. **Forked**: Real-world simulation with `--fork-url`
4. **Staging**: Live testnet behavior without production impact

### Example – Chainlink Price Feed Test (Forked)

```bash
source .env
forge test --match-test testPriceFeedVersionIsAccurate -vvv --fork-url $SEPOLIA_RPC_URL
```

Ensure `.env` is in `.gitignore`.

---

## 🏗 Deployment

### Local (Anvil)

**Terminal 1**

```bash
anvil
```

**Terminal 2**

```bash
forge script script/DeployFundMe.s.sol --rpc-url http://127.0.0.1:8545 --broadcast --account defaultKey --sender <deployer_address> --password-file .password
```

### Arbitrum Sepolia (Testnet)

Set your environment variables in `.env`:

```env
SEPOLIA_RPC_URL=https://arb-sepolia.g.alchemy.com/v2/your-api-key
```

Then:

```bash
source .env
forge script script/DeployFundMe.s.sol --rpc-url $SEPOLIA_RPC_URL --broadcast --account metaKey --sender <your_public_address> --password-file .password
```

Example deployed contract:  
https://sepolia.arbiscan.io/tx/0x40d9adfced95a9fdc018641d2ad595c12da82a6d71115b6c17c7b8627cc3f3ce

---

## 🧮 Interacting via Cast

### Send a Transaction

```bash
cast send <contract_address> "store(uint256)" 123 --rpc-url http://127.0.0.1:8545 --account defaultKey --password-file .password
```

### Call a Function

```bash
cast call <contract_address> "retrieve()"
cast --to-base <hex_output> dec
```

---

## 🛠 Utilities

### Format Code

```bash
forge fmt
```

### Gas Snapshots

```solidity
uint256 gasStart = gasleft();
vm.txGasPrice(1 gwei);
fundMe.withdraw();
uint256 gasUsed = (gasStart - gasleft()) * tx.gasprice;
console.log(gasUsed);
```

```bash
forge snapshot --match-test testWithdrawWithASingleFunder -vv
```

---

## 🧬 Storage Inspection

### View Storage Layout

```bash
forge inspect FundMe storageLayout
```

### Inspect Deployed Contract Storage

```bash
cast storage <contract_address> <slot_index>
cast --to-base <hex_output> dec
```

---

## 🔐 Wallet Setup with Cast

```bash
cast wallet import <wallet_name> --interactive
cast wallet list
```

Use `--account <wallet_name>` and `--password-file .password` to safely hide private keys.

⚠️ **Security Tip**:  
Run `history -c` to clear terminal history after importing or using private keys.

---

## License

MIT License. Use and adapt freely.
