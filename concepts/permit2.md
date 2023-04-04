---
description: Transaction Approval
---

# Permit2

In traditional on-chain transactions, approvals are required _prior_ to a token transfer.  This is required for all transactions types in which an ERC-20 is transferred out of an EOA or contract account.  While this is not explicitly mentioned in the sections that follow, it should be common knowledge for many who have used web3 or smart contracts.

Optionally, traders can approve token transfers using the [Permit2](https://github.com/dragonfly-xyz/useful-solidity-patterns/tree/main/patterns/permit2) contract from Uniswap instead of needing a separate approval transaction for each collateral & option. The permit signature can be passed into **each pool function** bypassing separate approval transactions. More information about Permit2 can be found on Uniswaps documentation [here](https://docs.uniswap.org/contracts/permit2/overview). A brief overview of how Permit2 works and what its benefits can be found [here](https://etherworld.co/2023/02/01/uniswap-permit2/).&#x20;

While we encourage users to adopt this methodology of approving transactions, it is completely optional.
