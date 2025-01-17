# hello-foundry

https://github.com/foundry-rs/foundry

https://book.getfoundry.sh/

## Basic

-   [x] Install

```shell
curl -L https://foundry.paradigm.xyz | bash
foundryup
```

-   [x] Init

```shell
forge init
```

-   [x] Basic commands

```shell
forge build
forge test
forge test --match-path test/HelloWorld -vvvv
```

---

-   [x] Test
    -   counter app
    -   test setup, ok, fail
    -   match
    -   verbose
    -   gas report

```shell
forge test --match-path test/Counter.t.sol -vvv --gas-report
```

---

-   [x] Solidity version and optimizer settings

https://github.com/foundry-rs/foundry/tree/master/config

---

-   [x] Remapping

```shell
forge remappings
forge install rari-capital/solmate
forge update lib/solmate
forge remove solmate

npm i @openzeppelin/contracts
```

---

-   [x] Formatter

```shell
forge fmt
```

---

---

-   [x] console (Counter, test, log int)

```shell
forge test --match-path test/Console.t.sol -vv
```

## Intermediate

---

-   [x] Test auth
-   [x] Test error
    -   `vm.expectRevert`
    -   `require` error message
    -   custom error
    -   label assertions
-   [x] Test event (expectEmit)
-   [x] Test time (`Auction.sol`)
-   [x] Test send eth (`Wallet.sol`) - hoax, deal
-   [x] Test signature

## Advanced

-   [x] mainnet fork

```shell
forge test --fork-url $FORK_URL --match-path test/Fork.t.sol -vvv
```

-   [x] main fork deal (whale)

```shell
forge test --fork-url $FORK_URL --match-path test/Whale.t.sol -vvv
```

TODO: need working example for (mainnet - opt)

-   [ ] crosschain fork

-   [x] Fuzzing (assume, bound)

```shell
forge test --match-path test/Fuzz.t.sol
```

-   [x] Invariant

```shell
# Open testing
forge test --match-path test/invariants/Invariant_0.t.sol -vvv
forge test --match-path test/invariants/Invariant_1.t.sol -vvv
# Handler
forge test --match-path test/invariants/Invariant_2.t.sol -vvv
# Actor management
forge test --match-path test/invariants/Invariant_3.t.sol -vvv
```

-   [ ] FFI

```shell
forge test --match-path test/FFI.t.sol --ffi -vvv

```

-   [ ] Differential testing

```shell
# virtual env
python3 -m pip install --user virtualenv
virtualenv -p python3 venv
source venv/bin/activate

pip install eth-abi
```

```shell
FOUNDRY_FUZZ_RUNS=100 forge test --match-path test/DifferentialTest.t.sol --ffi -vvv
```

## Misc

-   forge geiger

-   [ ] Vyper

https://github.com/0xKitsune/Foundry-Vyper

0. Install vyper

```shell
# virtual env
python3 -m pip install --user virtualenv
virtualenv -p python3 venv
source venv/bin/activate

pip3 install vyper==0.3.7

# Check installation
vyper --version
```

1. Put Vyper contract inside `vyper_contracts`
2. Declare Solidity interface inside `src`
3. Copy & paste `lib/utils/VyperDeployer.sol`
4. Write test

-   [ ] print vyper

```
print("HERE", convert(123, uint256), hardhat_compat=True)
```

```shell
forge test --match-path test/Vyper.t.sol --ffi
```

-   [ ] ignore error code

```
ignored_error_codes = ["license", "unused-param", "unused-var"]
```

-   [ ] Forge geiger

```shell
forge geiger
```

# TODO:

-   chisel?
-   debugger?
-   forge snapshot?
-   script?

# deploy 
forge create --rpc-url "ENTER_YOUR_RPC_HERE" --mnemonic "FOR_USING_UNLOCKED_ACCOUNTS" src/Counter.sol:Counter

forge create --rpc-url "https://rpc.dev.buildbear.io/unfair-taun-we-75f9829e" --mnemonic "picture length bitter bid lizard bid custom fork resource evidence dress cup" src/Counter.sol:Counter

# verfiy
ETHERSCAN_API_KEY="verifyContract" forge verify-contract --chain-id ENTER_CHAIN_ID --constructor-args "ENTER_ARGS" --verifier-url "https://rpc.buildbear.io/verify/etherscan/ENTER_TESTNET_NAME" CONTRACT_ADDRESS src/Counter.sol:Counter

ETHERSCAN_API_KEY="verifyContract" forge verify-contract --chain-id 1 --verifier-url "https://rpc.buildbear.io/verify/etherscan/unfair-taun-we-75f9829e" 0xfad47B8F3524923Cf2c9D64923A91fA9ae137954 src/Counter.sol:Counter

# testing 

forge test --fork-url https://eth.llamarpc.com --ffi