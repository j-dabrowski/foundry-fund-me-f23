## Foundry

**Foundry is a blazing fast, portable and modular toolkit for Ethereum application development written in Rust.**

Foundry consists of:

- **Forge**: Ethereum testing framework (like Truffle, Hardhat and DappTools).
- **Cast**: Swiss army knife for interacting with EVM smart contracts, sending transactions and getting chain data.
- **Anvil**: Local Ethereum node, akin to Ganache, Hardhat Network.
- **Chisel**: Fast, utilitarian, and verbose solidity REPL.

## Documentation

https://book.getfoundry.sh/

## Usage

### Build

In root fir of the project folder:
forge init
forge install smartcontractkit/chainlink-brownie-contracts@1.3.0 --no-commit

Add remappings to foundry.toml (so .sol files can reference the chainlnk-brownie-contracts)
Insert:
remappings = [
"@chainlink/contracts/=lib/chainlink-brownie-contracts/contracts/",
]

Build the project
forge build

```shell
$ forge build
```

### Test

```shell
$ forge test
```

forge test -vv
number of v's specifies verbosity of logging.
i.e. if console has been imported to the test file, and console logs used, -vv should show their output in the terminal output.

What can we do to work with addresses outside our system? (E.g. price feed contracts)
Types of tests:

1. Unit

- Testing a specific part of our code

2. Integration

- Testing how our code works with other parts of our code

3. Forked

- Testing our code on a simulated real environment

4. Staging

### Format

```shell
$ forge fmt
```

### Gas Snapshots

```shell
$ forge snapshot
```

### Anvil

```shell
$ anvil
```

### Deploy

```shell
$ forge script script/Counter.s.sol:CounterScript --rpc-url <your_rpc_url> --private-key <your_private_key>
```

### Cast

```shell
$ cast <subcommand>
```

### Help

```shell
$ forge --help
$ anvil --help
$ cast --help
```
