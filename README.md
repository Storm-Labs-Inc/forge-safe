# forge-safe: Gnosis Safe batch builder

Forge Safe lets Forge users build Gnosis Safe batch transactions using Forge scripting in Solidity. Forge Safe builds a collection of encoded transactions, then sends them to the Gnosis [Safe Transaction Service](https://github.com/safe-global/safe-transaction-service) uses [surl](https://github.com/memester-xyz/surl).

The goal of this tool is to allow users to quickly build, validate and version control complex Safe batches as code.

Inspired by [ape-safe](https://github.com/banteg/ape-safe) and Olymsig

## Supported Chains

Supports Mainnet, Goerli, Arbitrum, Optimism, Binance Smart Chain, Gnosis Chain, Polygon, zkSync, zkEVM, Base, Celo, Avalanche, Blastchain (unofficial), Sepolia, and Aurora currently. If you'd like more to be supported, please make a PR.

The official chains supported by Gnosis Safe API can be found [here](https://docs.safe.global/advanced/api-supported-networks).
List of multisend contract addresses can be found [here](https://docs.safe.global/advanced/smart-account-supported-networks/v1.3.0).

## Installation

`forge install ind-igo/forge-safe`

## Usage

Steps:

1. In your .env file
   - Set `WALLET_TYPE` with `local`, `ledger`, `trezor`, or `account` depending on your wallet
   - If `WALLET_TYPE` is `local`:
     - Set `PRIVATE_KEY` with your private key
   - If `WALLET_TYPE` is `ledger` or `trezor`:
     - Set `MNEMONIC_INDEX` with the index of the mnemonic
   - If `WALLET_TYPE` is `account`:
     - Set `ACCOUNT_NAME` with the name of the account saved in the forge cast wallet

2. Import `BatchScript.sol` into your Forge script
3. Call `addToBatch()` for each encoded call
4. After all encoded txs have been added, call `executeBatch()` with your Safe address and whether to send the transaction
5. Sign the batch data
6. ???
7. Profit

```js
import {BatchScript} from "forge-safe/BatchScript.sol";

...

function run(bool send_) public {
        string memory gm = "gm";
        address greeter = 0x1111;

        bytes memory txn = abi.encodeWithSelector(
            Greeter.greet.selector,
            gm
        );
        addToBatch(greeter, 0, txn);

        executeBatch(safe, send_);
}
```
