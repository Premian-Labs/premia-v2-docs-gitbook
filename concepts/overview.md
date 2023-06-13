---
description: Transaction Approval
---

# Overview

The following sections outline some of the technical concepts and core functionality within the ecosystem.  This section is intended for all user types. Where possible, corresponding inputs and function calls are provided.  For a complete list of function calls available, please reference [contracts](broken-reference).&#x20;

#### Permit2&#x20;

{% hint style="warning" %}
Section Under Construction as Permit2 is Currently Pending Removal
{% endhint %}

In traditional on-chain token transfers, users must approve a transfer amount _prior_ to a token transfer.  While this is not explicitly mentioned in the sections that follow, it should be common knowledge for many who have used web3 or smart contracts.

Optionally, traders can approve token transfers using the [Permit2](https://github.com/dragonfly-xyz/useful-solidity-patterns/tree/main/patterns/permit2) contract from Uniswap instead of needing a separate approval transaction for each collateral & option. The permit signature can be passed into **each pool function** bypassing separate approval transactions. More information about Permit2 can be found on Uniswap documentation [here](https://docs.uniswap.org/contracts/permit2/overview). A brief overview of how Permit2 works and what its benefits can be found [here](https://etherworld.co/2023/02/01/uniswap-permit2/).&#x20;

{% hint style="info" %}
While we encourage users to adopt this methodology of approving transactions, it is completely optional.  Standard approval methods are still supported.&#x20;
{% endhint %}
