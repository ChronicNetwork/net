# Gentx process:  v1.1

This document describes the steps needed to create a Gentx for v1.1 of Chronic Chain. Patience by everyone was very much appreciated while this scenario was being mitigated.

It is encouraged for new validator operators who were not connected prior to the network upgrade height to **NOT participate in this process** until after consensus resumes. 

Links:

> **v1.1 Genesis: [https://raw.githubusercontent.com/ChronicNetwork/net/main/mainnet/v1.1/genesis.json](https://raw.githubusercontent.com/ChronicNetwork/net/main/mainnet/v1.1/genesis.json)
Gentxs Location: [https://github.com/ChronicNetwork/net/tree/main/gentx/v1.1%20gentxs](https://github.com/ChronicNetwork/net/tree/main/gentx/v1.1%20gentxs)
Exported Balances: [https://raw.githubusercontent.com/ChronicNetwork/net/main/accounts/exported-accounts-v1.1.md](https://raw.githubusercontent.com/ChronicNetwork/net/main/accounts/exported-accounts-v1.1.md)**
> 

****

### Steps:

### 1. Spin up a new node with chtd v1.1 binary installed [[link](https://github.com/ChronicNetwork/cht)].

Follow the steps located in the readme.md , until you are able to confirm your chtd binary to be `v1.1.0`.

### 2. Next, Import Previous Validator Wallet to node.

This will ensure that your validator will have an active balance when consensus will resume. 
A list of the total supply distribution between wallets can be found here [[link](https://raw.githubusercontent.com/ChronicNetwork/net/main/accounts/exported-accounts-v1.1.md)].

### 3. Create Gentx.

We encourage all participating validators to self-delegate just 1 CHT when creating a gentx initially

```jsx
chtd gentx <key_name> 1000000ucht —chain-id morocco-1

```

### 4. Push Gentx to github [[link](https://github.com/ChronicNetwork/net/tree/main/gentx/v1.1%20gentxs)].

Once enough validators have submitted their gentx, the new genesis file for v1.1 will be compiled and made available, containing all gentxs as well as an expected genesis time height.

Details will continue to be provided, regarding how preparations for this migration took place, why it did & when it will actually happen. For any questions about this process, please bring them to the validator channel in the discord.

Immense thanks to all for providing value to this community, very exciting times ahead for Chronic Chain as a whole!
