# Sky OP Bridges Deployment Validation


This report is given for the following contract addresses.

```js
unichain_bridge: 
{
  "escrow": "0x1196F688C585D3E5C895Ef8954FFB0dCDAfc566A",
  "l1Bridge": "0xDF0535a4C96c9Cd8921d8FeC92A7680b281681d2",
  "l1BridgeImp": "0x8A925ccFd5F7f46332E2D719A916f8b4a643599F",
  "l1GovRelay": "0xb383070Cf9F4f01C3a2cfD0ef6da4BC057b429b7",
  "l2Bridge": "0xa13152006D0216Fe4627a0D3B006087A6a55D752",
  "l2BridgeImp": "0xd78292C12707CF28E8EB7bf06fA774D1044C2dF5",
  "l2BridgeSpell": "0x32760698c87834c02ED9AFF2d4FC3e16c029B936",
  "l2GovRelay": "0x3510a7F16F549EcD0Ef018DE0B3c2ad7c742990f",
  "l2Usds": "0x7E10036Acc4B56d4dFCa3b77810356CE52313F9C",
  "l2UsdsImp": "0x8fb6EF2dA06a6957fC84C2C55bb195837fB7DBa9"
}
optimism_bridge:
{
  "l1Bridge": "0x3d25B7d486caE1810374d37A48BCf0963c9B8057",
  "l1BridgeImp": "0xA50adBad34c1e9786979bD44220F8fd46e43A6B0",
  "l2Bridge": "0x8F41DBF6b8498561Ce1d73AF16CD9C0d8eE20ba6",
  "l2BridgeImp": "0xc2702C859016db756149716cc4d2B7D7A436CF04",
  "l2BridgeSpell": "0x99892216eD34e8FD924A1dBC758ceE61a9109409",
  "l2Usds": "0x4F13a96EC5C4Cf34e442b46Bbd98a0791F20edC3",
  "l2UsdsImp": "0x2A3541003B34f34833a82F194e4dC69a7a39B057"
}
Unichain:
{
  "sUsds": "0xA06b10Db9F390990364A3984C04FaDf1c13691b5",
  "sUsdsImp": "0x15c2A564b987470FAFCaB0B036029532bd168E10"
}
Optimism:
{
  "sUsds": "0xb5B2dc7fd34C249F4be7fB1fCea07950784229e0",
  "sUsdsImp": "0x6f0888DDA6a5E35451D5bE0fABb20171715788B3"
}
```


## Code validation

All deployed contracts listed above have been validated against the code at the following commits:

- [op-token-bridge](https://github.com/makerdao/op-token-bridge/tree/82918f4853d50c6520dac53fdb70a42fd4ce671b): `82918f4853d50c6520dac53fdb70a42fd4ce671b`
- susds: [susds](https://github.com/makerdao/sdai/tree/dfc7f41cb7599afcb0f0eb1ddaadbf9dd4015dce): `dfc7f41cb7599afcb0f0eb1ddaadbf9dd4015dce`
- usds: [usds](https://github.com/makerdao/usds/tree/d65551dbc11cfe1afcc4718ab790663b99d766af): `d65551dbc11cfe1afcc4718ab790663b99d766af`

## Initialization validation

### ETH - Unichain bridge - Escrow (`0x1196F688C585D3E5C895Ef8954FFB0dCDAfc566A`)

**Code:** [op-token-bridge/src/Escrow.sol](https://github.com/makerdao/op-token-bridge/blob/82918f4853d50c6520dac53fdb70a42fd4ce671b/src/Escrow.sol)

**Immutables:** N/A

**Relevant State:**
1. `wards[0xbe8e3e3618f7474f8cb1d074a26affef007e98fb] = true` - [`MCD_PAUSE_PROXY`](https://chainlog.sky.money/api/mainnet/active.json)



### ETH - Unichain bridge - L1 Token Bridge (`0xDF0535a4C96c9Cd8921d8FeC92A7680b281681d2`)

**Code:** 
1. Proxy `0xDF0535a4C96c9Cd8921d8FeC92A7680b281681d2`: [op-token-bridge/lib/**/ERC1967Proxy.sol](https://github.com/makerdao/op-token-bridge/tree/82918f4853d50c6520dac53fdb70a42fd4ce671b/lib/)
2. Implementation `0x8A925ccFd5F7f46332E2D719A916f8b4a643599F`: [op-token-bridge/src/L1TokenBridge.sol](https://github.com/makerdao/op-token-bridge/blob/82918f4853d50c6520dac53fdb70a42fd4ce671b/src/L1TokenBridge.sol)

**Immutables:**
1. `implementation.otherBridge = 0xa13152006D0216Fe4627a0D3B006087A6a55D752` - Matches "Unichain - Unichain Bridge - L2 Token Bridge"
2. `implementation.messenger = 0x9A3D64E386C18Cb1d6d5179a9596A4B5736e98A6` - [`L1CrossDomainMessengerProxy`](https://docs.unichain.org/docs/technical-information/contract-addresses)

**Relevant State:**
1. `implementation = 0x8a925ccfd5f7f46332e2d719a916f8b4a643599f` - Matches expected implementation contract.
1. `wards[0xbe8e3e3618f7474f8cb1d074a26affef007e98fb] = true` - [`MCD_PAUSE_PROXY`](https://chainlog.sky.money/api/mainnet/active.json)

### ETH - Unichain bridge - L1 Gov Relay (`0xb383070Cf9F4f01C3a2cfD0ef6da4BC057b429b7`)

**Code:** [op-token-bridge/src/L1GovernanceRelay.sol](https://github.com/makerdao/op-token-bridge/blob/82918f4853d50c6520dac53fdb70a42fd4ce671b/src/L1GovernanceRelay.sol)

**Immutables:**
1. `l2GovernanceRelay = 0x3510a7f16f549ecd0ef018de0b3c2ad7c742990f` - Matches "Unichain - Unichain Bridge - L2 Gov Relay"
2. `messenger = 0x9a3d64e386c18cb1d6d5179a9596a4b5736e98a6` - [`L1CrossDomainMessengerProxy`](https://docs.unichain.org/docs/technical-information/contract-addresses)

**Relevant State:**
1. `wards[0xbe8e3e3618f7474f8cb1d074a26affef007e98fb] = true` - [`MCD_PAUSE_PROXY`](https://chainlog.sky.money/api/mainnet/active.json)

### Unichain - Unichain bridge - L2 Token Bridge (`0xa13152006D0216Fe4627a0D3B006087A6a55D752`)

**Code:** 
1. Proxy `0xa13152006D0216Fe4627a0D3B006087A6a55D752`: [op-token-bridge/lib/**/ERC1967Proxy.sol](https://github.com/makerdao/op-token-bridge/tree/82918f4853d50c6520dac53fdb70a42fd4ce671b/lib/)
2. Implementation `0xd78292C12707CF28E8EB7bf06fA774D1044C2dF5`: [op-token-bridge/src/L2TokenBridge.sol](https://github.com/makerdao/op-token-bridge/blob/82918f4853d50c6520dac53fdb70a42fd4ce671b/src/L2TokenBridge.sol)

**Immutables:**
1. `implementation.otherBridge = 0xDF0535a4C96c9Cd8921d8FeC92A7680b281681d2` - Matches "Ethereum - Unichain Bridge - L1 Token Bridge"
2. `implementation.messenger = 0x4200000000000000000000000000000000000007` - [`L2CrossDomainMessengerProxy`](https://docs.unichain.org/docs/technical-information/contract-addresses) ⚠️ Not listed in [Unichain docs](https://docs.unichain.org/docs/technical-information/contract-addresses) but matches standard `L2CrossDomainMessenger` address for OP chains and implementation contract points to `L2CrossDomainMessenger` contract.

**Relevant State:**
1. `implementation = 0xd78292c12707cf28e8eb7bf06fa774d1044c2df5` - Matches expected implementation contract.
2. `wards[0x3510a7f16f549ecd0ef018de0b3c2ad7c742990f] = true` - Matches "Unichain - Unichain Bridge - L2 Gov Relay"


### Unichain - Unichain bridge - L2 Bridge Spell (`0x32760698c87834c02ED9AFF2d4FC3e16c029B936`)

**Code:** [op-token-bridge/deploy/L2TokenBridgeSpell.sol](https://github.com/makerdao/op-token-bridge/blob/82918f4853d50c6520dac53fdb70a42fd4ce671b/deploy/L2TokenBridgeSpell.sol)

**Immutables:**
1. `l2Bridge = 0xa13152006d0216fe4627a0d3b006087a6a55d752` - Matches "Unichain - Unichain Bridge - L2 Token Bridge"

**Relevant State:** N/A


### Unichain - Unichain bridge - L2 Gov Relay (`0x3510a7F16F549EcD0Ef018DE0B3c2ad7c742990f`)

**Code:** [op-token-bridge/src/L2GovernanceRelay.sol](https://github.com/makerdao/op-token-bridge/blob/82918f4853d50c6520dac53fdb70a42fd4ce671b/src/L2GovernanceRelay.sol)

**Immutables:**
1. `l1GovernanceRelay = 0xb383070cf9f4f01c3a2cfd0ef6da4bc057b429b7` - Matches "ETH - Unichain bridge - L1 Gov Relay"
2. `messenger = 0x4200000000000000000000000000000000000007` ⚠️ Not listed in [Unichain docs](https://docs.unichain.org/docs/technical-information/contract-addresses) but matches standard `L2CrossDomainMessenger` address for OP chains and implementation contract points to `L2CrossDomainMessenger` contract.

**Relevant State:** N/A


### Unichain - L2 USDS (`0x7E10036Acc4B56d4dFCa3b77810356CE52313F9C`)

**Code:** 
1. Proxy `0x7E10036Acc4B56d4dFCa3b77810356CE52313F9C`: [usds/lib/**/ERC1967Proxy.sol](https://github.com/makerdao/usds/tree/d65551dbc11cfe1afcc4718ab790663b99d766af/lib/)
2. Implementation `0x8fb6ef2da06a6957fc84c2c55bb195837fb7dba9`: [usds/src/Usds.sol](https://github.com/makerdao/usds/blob/d65551dbc11cfe1afcc4718ab790663b99d766af/src/Usds.sol)

**Immutables:** N/A

**Relevant State:**
1. `implementation = 0x8fb6ef2da06a6957fc84c2c55bb195837fb7dba9` - Matches expected implementation contract.
2. `wards[0x3510a7f16f549ecd0ef018de0b3c2ad7c742990f] = true` - Matches "Unichain - Unichain Bridge - L2 Gov Relay"
3. `totalSupply = 0`



























### ETH - Optimism bridge - L1 Token Bridge (`0x3d25b7d486cae1810374d37a48bcf0963c9b8057`)

**Code:** 
1. Proxy `0x3d25b7d486cae1810374d37a48bcf0963c9b8057`: [op-token-bridge/lib/**/ERC1967Proxy.sol](https://github.com/makerdao/op-token-bridge/tree/82918f4853d50c6520dac53fdb70a42fd4ce671b/lib/)
2. Implementation `0xa50adbad34c1e9786979bd44220f8fd46e43a6b0`: [op-token-bridge/src/L1TokenBridge.sol](https://github.com/makerdao/op-token-bridge/blob/82918f4853d50c6520dac53fdb70a42fd4ce671b/src/L1TokenBridge.sol)

**Immutables:**
1. `implementation.otherBridge = 0x8F41DBF6b8498561Ce1d73AF16CD9C0d8eE20ba6` - Matches "Optimism - Optimism Bridge - L2 Token Bridge"
2. `implementation.messenger = 0x25ace71c97B33Cc4729CF772ae268934F7ab5fA1` - [`L1CrossDomainMessengerProxy`](https://docs.optimism.io/superchain/addresses)

**Relevant State:**
1. `implementation = 0xa50adbad34c1e9786979bd44220f8fd46e43a6b0` - Matches expected implementation contract.
1. `wards[0xbe8e3e3618f7474f8cb1d074a26affef007e98fb] = true` - [`MCD_PAUSE_PROXY`](https://chainlog.sky.money/api/mainnet/active.json)






# Verifying the DV-files yourself

### Validation commands

Check out the git repositories at the mentioned commits:

```bash
git submodule init .
git submodule update .
# print checked out commits, should match above
git submodule status
```

### Install Deployment Verification Tool

We are using the Deployment Verification Tool from ChainSecurity, which is designed to verify deployed contracts. You can find it [here](https://github.com/ChainSecurity/deployment_validation). We used the version from the following commit: [4c804e4bb984024857c71aa6c2fe279999201105](https://github.com/ChainSecurity/deployment_validation/commit/4c804e4bb984024857c71aa6c2fe279999201105).

### Create Validation File

Copy the following into a file named `.dv_config.json` in the root directory of this repository:

```bash
{
  "rpc_urls": {
    "1": "ETH_RPC_URL",
    "10": "OP_RPC_URL",
    "130": "UNI_RPC_URL"
  },
  "dvf_storage": "./dvf",
  "trusted_signers": [],
  "etherscan_global": {
    "api_url": "https://api.etherscan.io/v2/api",
    "api_key": "ETHERSCAN_API_KEY"
  },
  "etherscan_chain_configs": {},
  "blockscout_global": null,
  "blockscout_chain_configs": {},
  "max_blocks_per_event_query": 9999,
  "web3_timeout": 700,
  "signer": null
}
```

You have to replace the placeholder values with your own. If you do not know from where to get RPCs that support debug_traceTransaction or trace_transaction, check [here](https://github.com/mario-eth/deployment_validation?tab=readme-ov-file#dvf-creation). Furthermore, you have to replace `ETHERSCAN_API_KEY` with your own Etherscan API key.

-------- 

### DV-file creation THIS WILL NEED TO BE DELETED IN THE FINAL COMMIT, this is just for bootstraping the dv files



At the following blocks
- Ethereum: [22488821](https://etherscan.io/block/22488821): May-15-2025 01:29:47 PM +UTC
- Optimism: [135858527](https://optimistic.etherscan.io/block/135858527): May-15-2025 01:30:31 PM +UTC
- Unichain: [16567310](https://uniscan.xyz/block/16567310) May-15-2025 01:27:49 PM +UTC

#### Step 1 create the dv files 
```bash
dv init --project ./projects/op-token-bridge --address 0x1196F688C585D3E5C895Ef8954FFB0dCDAfc566A --contractname Escrow escrow_unichain.dvf.json --chainid 1 --initblock 22488821

dv init --project ./projects/op-token-bridge --address 0xDF0535a4C96c9Cd8921d8FeC92A7680b281681d2 --contractname ERC1967Proxy --implementation L1TokenBridge l1Bridge_unichain.dvf.json --chainid 1 --initblock 22488821

dv init --project ./projects/op-token-bridge --address 0xb383070Cf9F4f01C3a2cfD0ef6da4BC057b429b7 --contractname L1GovernanceRelay l1GovRelay_unichain.dvf.json --chainid 1 --initblock 22488821

dv init --project ./projects/op-token-bridge --address 0xa13152006D0216Fe4627a0D3B006087A6a55D752 --contractname ERC1967Proxy --implementation L2TokenBridge l2Bridge_unichain.dvf.json --chainid 130 --initblock 16567310

dv init --project ./projects/op-token-bridge --address 0x32760698c87834c02ED9AFF2d4FC3e16c029B936 --contractname L2TokenBridgeSpell l2BridgeSpell_unichain.dvf.json --chainid 130 --initblock 16567310

dv init --project ./projects/op-token-bridge --address 0x3510a7F16F549EcD0Ef018DE0B3c2ad7c742990f --contractname L2GovernanceRelay l2GovRelay_unichain.dvf.json --chainid 130 --initblock 16567310

dv init --project ./projects/usds --address 0x7E10036Acc4B56d4dFCa3b77810356CE52313F9C --contractname ERC1967Proxy --implementation Usds l2Usds_unichain.dvf.json --chainid 130 --initblock 16567310

dv init --project ./projects/op-token-bridge --address 0x3d25B7d486caE1810374d37A48BCf0963c9B8057 --contractname ERC1967Proxy --implementation L1TokenBridge l1Bridge_op.dvf.json --chainid 1 --initblock 22488821

dv init --project ./projects/op-token-bridge --address 0x8F41DBF6b8498561Ce1d73AF16CD9C0d8eE20ba6 --contractname ERC1967Proxy --implementation L2TokenBridge l2Bridge_op.dvf.json --chainid 10 --initblock 135858527

dv init --project ./projects/op-token-bridge --address 0x99892216eD34e8FD924A1dBC758ceE61a9109409 --contractname L2TokenBridgeSpell l2BridgeSpell_op.dvf.json --chainid 10 --initblock 135858527

dv init --project ./projects/usds --address 0x4F13a96EC5C4Cf34e442b46Bbd98a0791F20edC3 --contractname ERC1967Proxy --implementation Usds l2Usds_op.dvf.json --chainid 10 --initblock 135858527

dv init --project ./projects/susds --address 0xA06b10Db9F390990364A3984C04FaDf1c13691b5 --contractname ERC1967Proxy --implementation SUsds sUsds_unichain.dvf.json --chainid 130 --initblock 16567310

dv init --project ./projects/susds --address 0x15c2A564b987470FAFCaB0B036029532bd168E10 --contractname SUsds sUsds_impl_unichain.dvf.json --chainid 130 --initblock 16567310

dv init --project ./projects/susds --address 0xb5B2dc7fd34C249F4be7fB1fCea07950784229e0 --contractname ERC1967Proxy --implementation SUsds sUsds_op.dvf.json --chainid 10 --initblock 135858527

dv init --project ./projects/susds --address 0x6f0888DDA6a5E35451D5bE0fABb20171715788B3 --contractname SUsds sUsds_impl_op.dvf.json --chainid 10 --initblock 135858527
```

> Note: need to run `dv id <dvf>` after changing the dvf files. 
-----

#### Validate the DV-files

At the following blocks:

- Ethereum: [22488821](https://etherscan.io/block/22488821): May-15-2025 01:29:47 PM +UTC
- Optimism: [135858527](https://optimistic.etherscan.io/block/135858527): May-15-2025 01:30:31 PM +UTC
- Unichain: [16567310](https://uniscan.xyz/block/16567310) May-15-2025 01:27:49 PM +UTC

> TODO: use `dv validate` instead of `dv init`

##### Unichain Bridge

```bash
# validate escrow_unichain.dvf.json for unichain_bridge => escrow
dv --config .dv_config.json validate dvf/escrow_unichain.dvf.json --allowuntrusted --validationblock 22488821

# validate l1Bridge_unichain.dvf.json for unichain_bridge => l1Bridge
dv --config .dv_config.json validate dvf/l1Bridge_unichain.dvf.json --allowuntrusted --validationblock 22488821

# validate l1GovRelay_unichain.dvf.json for unichain_bridge => l1GovRelay
dv --config .dv_config.json validate dvf/l1GovRelay_unichain.dvf.json --allowuntrusted --validationblock 22488821

# validate l2Bridge_unichain.dvf.json for unichain_bridge => l2Bridge
dv --config .dv_config.json validate dvf/l2Bridge_unichain.dvf.json --allowuntrusted --validationblock 16567310

# validate l2BridgeSpell_unichain.dvf.json for unichain_bridge => l2BridgeSpell
dv --config .dv_config.json validate dvf/l2BridgeSpell_unichain.dvf.json --allowuntrusted --validationblock 16567310

# validate l2GovRelay_unichain.dvf.json for unichain_bridge => l2GovRelay
dv --config .dv_config.json validate dvf/l2GovRelay_unichain.dvf.json --allowuntrusted --validationblock 16567310

# validate l2Usds_unichain.dvf.json for unichain_bridge => l2Usds
dv --config .dv_config.json validate dvf/l2Usds_unichain.dvf.json --allowuntrusted --validationblock 16567310
```

##### Optimism Bridge

```bash
# validate l1Bridge_op.dvf.json for optimism_bridge => l1Bridge
dv --config .dv_config.json validate dvf/l1Bridge_op.dvf.json --allowuntrusted --validationblock 22488821

# validate l2Bridge_op.dvf.json for optimism_bridge => l2Bridge
dv --config .dv_config.json validate dvf/l2Bridge_op.dvf.json --allowuntrusted --validationblock 135858527

# validate l2BridgeSpell_op.dvf.json for optimism_bridge => l2BridgeSpell
dv --config .dv_config.json validate dvf/l2BridgeSpell_op.dvf.json --allowuntrusted --validationblock 135858527

# validate l2Usds_op.dvf.json for optimism_bridge => l2Usds
dv --config .dv_config.json validate dvf/l2Usds_op.dvf.json --allowuntrusted --validationblock 135858527
```

##### Susds

```bash
# validate sUsds_unichain.dvf.json for susds => sUsds (unichain)
dv --config .dv_config.json validate dvf/sUsds_unichain.dvf.json --allowuntrusted --validationblock 16567310

# validate sUsds_op.dvf.json for susds => sUsds (optimism)
dv --config .dv_config.json validate dvf/sUsds_op.dvf.json --allowuntrusted --validationblock 135858527
```
