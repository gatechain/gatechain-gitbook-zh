# How to Become a GateChain Validator

A validator node is responsible for participating in the network consensus and block production. By becoming a validator, you can contribute to the network's security and earn rewards through POS mining.

To upgrade your full node to a validator node and participate in POS mining, follow these steps:

1. Create a regular account:
```bash
gatecli account create
```

2. Create a consensus account based on the regular account:
```bash
gatecli con-account create [account address] --chain-id mainnet
```

3. Initiate the "consensus account online" transaction:
```bash
gatecli con-account online \
--from [sender account] \
--pubkey [sender account public key] \
--moniker [name] \
--commission-max-change-rate [maximum daily commission rate change] \
--commission-max-rate [maximum commission rate] \
--commission-rate [commission rate] \
--chain-id mainnet
```

After completing these steps, your node will begin participating in GateChain's consensus process. Please ensure your machine operates normally with stable network connectivity.
