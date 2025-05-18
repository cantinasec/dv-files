# Sky OP Bridges Deployment Validation

## Summary

The deployments along with proper initialization have been validated for the following contract addresses.
Details can be found in the subsequent sections.

```json
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
Optimism bridge:
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

All deployed contracts listed above have been validated against the code at the following commits using [ChainSecurity's Deployment Validation Tool](https://github.com/ChainSecurity/deployment_validation).

- [op-token-bridge](https://github.com/makerdao/op-token-bridge/tree/0f935505c0dc74ce3db2a9998320a56119321814): `0f935505c0dc74ce3db2a9998320a56119321814`, corresponds to [Cantina 2024-10-23 report](https://github.com/makerdao/op-token-bridge/blob/82918f4853d50c6520dac53fdb70a42fd4ce671b/audit/20241023-cantina-report-review-makerdao-op-token-bridge.pdf) when compiled with the compiler options specified [here](https://github.com/makerdao/op-token-bridge/commit/82918f4853d50c6520dac53fdb70a42fd4ce671b)
- [susds](https://github.com/makerdao/sdai/tree/e1d160aba17e95e8cec3d6bf50f310fbed9f28d6): `e1d160aba17e95e8cec3d6bf50f310fbed9f28d6`, corresponds to [Cantina 2024-09-26 report](https://github.com/makerdao/sdai/blob/dfc7f41cb7599afcb0f0eb1ddaadbf9dd4015dce/audit/20240926-cantina-report-maker-susds.pdf)
- [usds](https://github.com/makerdao/usds/tree/45bf759ba046b66dd115842ee8b9205a64e7bab6): `45bf759ba046b66dd115842ee8b9205a64e7bab6`, corresponds to [Cantina 2024-09-26 report](https://github.com/makerdao/usds/blob/d65551dbc11cfe1afcc4718ab790663b99d766af/audit/20240926-cantina-report-review-makerdao-usds.pdf)


## Initialization validation

The state and emitted events have been manually inspected and compared against expected values.

The initialization validation was performed at the following blocks:

- Ethereum: [22488821](https://etherscan.io/block/22488821): May-15-2025 01:29:47 PM +UTC
- Optimism: [135858527](https://optimistic.etherscan.io/block/135858527): May-15-2025 01:30:31 PM +UTC
- Unichain: [16567310](https://uniscan.xyz/block/16567310) May-15-2025 01:27:49 PM +UTC

### Ethereum - Unichain bridge - Escrow (`0x1196F688C585D3E5C895Ef8954FFB0dCDAfc566A`)

**Code:** [op-token-bridge/src/Escrow.sol](https://github.com/makerdao/op-token-bridge/blob/0f935505c0dc74ce3db2a9998320a56119321814/src/Escrow.sol)

**Immutables:** N/A

**Relevant State:**
1. `wards[0xbe8e3e3618f7474f8cb1d074a26affef007e98fb] = true` - [`MCD_PAUSE_PROXY`](https://chainlog.sky.money/api/mainnet/active.json)

---

### Ethereum - Unichain bridge - L1 Token Bridge (`0xDF0535a4C96c9Cd8921d8FeC92A7680b281681d2`)

**Code:** 
1. Proxy `0xDF0535a4C96c9Cd8921d8FeC92A7680b281681d2`: [op-token-bridge/lib/**/ERC1967Proxy.sol](https://github.com/makerdao/op-token-bridge/tree/0f935505c0dc74ce3db2a9998320a56119321814/lib/)
2. Implementation `0x8A925ccFd5F7f46332E2D719A916f8b4a643599F`: [op-token-bridge/src/L1TokenBridge.sol](https://github.com/makerdao/op-token-bridge/blob/0f935505c0dc74ce3db2a9998320a56119321814/src/L1TokenBridge.sol)

**Immutables:**
1. `implementation.otherBridge = 0xa13152006D0216Fe4627a0D3B006087A6a55D752` - Matches "Unichain - L2 Token Bridge"
2. `implementation.messenger = 0x9A3D64E386C18Cb1d6d5179a9596A4B5736e98A6` - [`L1CrossDomainMessengerProxy`](https://docs.unichain.org/docs/technical-information/contract-addresses)

**Relevant State:**
1. `implementation = 0x8a925ccfd5f7f46332e2d719a916f8b4a643599f` - Matches expected implementation contract.
2. `wards[0xbe8e3e3618f7474f8cb1d074a26affef007e98fb] = true` - [`MCD_PAUSE_PROXY`](https://chainlog.sky.money/api/mainnet/active.json)
3. `escrow = 0x0`
    > ⚠️ Escrow has **not** been set to the deployed Escrow contract yet.

---

### Ethereum - Unichain bridge - L1 Gov Relay (`0xb383070Cf9F4f01C3a2cfD0ef6da4BC057b429b7`)

**Code:** [op-token-bridge/src/L1GovernanceRelay.sol](https://github.com/makerdao/op-token-bridge/blob/0f935505c0dc74ce3db2a9998320a56119321814/src/L1GovernanceRelay.sol)

**Immutables:**
1. `l2GovernanceRelay = 0x3510a7f16f549ecd0ef018de0b3c2ad7c742990f` - Matches "Unichain - L2 Gov Relay"
2. `messenger = 0x9a3d64e386c18cb1d6d5179a9596a4b5736e98a6` - [`L1CrossDomainMessengerProxy`](https://docs.unichain.org/docs/technical-information/contract-addresses)

**Relevant State:**
1. `wards[0xbe8e3e3618f7474f8cb1d074a26affef007e98fb] = true` - [`MCD_PAUSE_PROXY`](https://chainlog.sky.money/api/mainnet/active.json)

---

### Unichain - L2 Token Bridge (`0xa13152006D0216Fe4627a0D3B006087A6a55D752`)

**Code:** 
1. Proxy `0xa13152006D0216Fe4627a0D3B006087A6a55D752`: [op-token-bridge/lib/**/ERC1967Proxy.sol](https://github.com/makerdao/op-token-bridge/tree/0f935505c0dc74ce3db2a9998320a56119321814/lib/)
2. Implementation `0xd78292C12707CF28E8EB7bf06fA774D1044C2dF5`: [op-token-bridge/src/L2TokenBridge.sol](https://github.com/makerdao/op-token-bridge/blob/0f935505c0dc74ce3db2a9998320a56119321814/src/L2TokenBridge.sol)

**Immutables:**
1. `implementation.otherBridge = 0xDF0535a4C96c9Cd8921d8FeC92A7680b281681d2` - Matches "Ethereum - Unichain Bridge - L1 Token Bridge"
2. `implementation.messenger = 0x4200000000000000000000000000000000000007` - [`L2CrossDomainMessengerProxy`](https://docs.unichain.org/docs/technical-information/contract-addresses)
    > ⚠️ Not listed in [Unichain docs](https://docs.unichain.org/docs/technical-information/contract-addresses) but matches standard `L2CrossDomainMessenger` address for OP chains and implementation contract points to `L2CrossDomainMessenger` contract.

**Relevant State:**
1. `implementation = 0xd78292c12707cf28e8eb7bf06fa774d1044c2df5` - Matches expected implementation contract.
2. `wards[0x3510a7f16f549ecd0ef018de0b3c2ad7c742990f] = true` - Matches "Unichain - L2 Gov Relay"

---

### Unichain - L2 Bridge Spell (`0x32760698c87834c02ED9AFF2d4FC3e16c029B936`)

**Code:** [op-token-bridge/deploy/L2TokenBridgeSpell.sol](https://github.com/makerdao/op-token-bridge/blob/0f935505c0dc74ce3db2a9998320a56119321814/deploy/L2TokenBridgeSpell.sol)

**Immutables:**
1. `l2Bridge = 0xa13152006d0216fe4627a0d3b006087a6a55d752` - Matches "Unichain - L2 Token Bridge"

**Relevant State:** N/A

---

### Unichain - L2 Gov Relay (`0x3510a7F16F549EcD0Ef018DE0B3c2ad7c742990f`)

**Code:** [op-token-bridge/src/L2GovernanceRelay.sol](https://github.com/makerdao/op-token-bridge/blob/0f935505c0dc74ce3db2a9998320a56119321814/src/L2GovernanceRelay.sol)

**Immutables:**
1. `l1GovernanceRelay = 0xb383070cf9f4f01c3a2cfd0ef6da4bc057b429b7` - Matches "Ethereum - Unichain bridge - L1 Gov Relay"
2. `messenger = 0x4200000000000000000000000000000000000007`
    > ⚠️ Not listed in [Unichain docs](https://docs.unichain.org/docs/technical-information/contract-addresses) but matches standard `L2CrossDomainMessenger` address for OP chains and implementation contract points to `L2CrossDomainMessenger` contract.

**Relevant State:** N/A

---

### Unichain - L2 USDS (`0x7E10036Acc4B56d4dFCa3b77810356CE52313F9C`)

**Code:** 
1. Proxy `0x7E10036Acc4B56d4dFCa3b77810356CE52313F9C`: [usds/lib/**/ERC1967Proxy.sol](https://github.com/makerdao/usds/tree/45bf759ba046b66dd115842ee8b9205a64e7bab6/lib/)
2. Implementation `0x8fb6ef2da06a6957fc84c2c55bb195837fb7dba9`: [usds/src/Usds.sol](https://github.com/makerdao/usds/blob/45bf759ba046b66dd115842ee8b9205a64e7bab6/src/Usds.sol)

**Immutables:** N/A

**Relevant State:**
1. `implementation = 0x8fb6ef2da06a6957fc84c2c55bb195837fb7dba9` - Matches expected implementation contract.
2. `wards[0x3510a7f16f549ecd0ef018de0b3c2ad7c742990f] = true` - Matches "Unichain - L2 Gov Relay"
3. `totalSupply = 0`

---

### Unichain - sUSDS (`0xA06b10Db9F390990364A3984C04FaDf1c13691b5`)

**Code:** 
1. Proxy `0xA06b10Db9F390990364A3984C04FaDf1c13691b5`: [sdai/lib/**/ERC1967Proxy.sol](https://github.com/makerdao/sdai/tree/e1d160aba17e95e8cec3d6bf50f310fbed9f28d6/lib)
2. Implementation `0x15c2A564b987470FAFCaB0B036029532bd168E10`: [sdai/src/l2/SUsds.sol](https://github.com/makerdao/sdai/tree/e1d160aba17e95e8cec3d6bf50f310fbed9f28d6/src/l2/SUsds.sol)

**Immutables:** N/A

**Relevant State:**
1. `implementation = 0x15c2a564b987470fafcab0b036029532bd168e10` - Matches expected implementation contract.
2. `wards[0x3510a7f16f549ecd0ef018de0b3c2ad7c742990f] = true` - Matches "Unichain - L2 Gov Relay"
3. `totalSupply = 0`

---

### Ethereum - Optimism bridge - L1 Token Bridge (`0x3d25b7d486cae1810374d37a48bcf0963c9b8057`)

**Code:** 
1. Proxy `0x3d25b7d486cae1810374d37a48bcf0963c9b8057`: [op-token-bridge/lib/**/ERC1967Proxy.sol](https://github.com/makerdao/op-token-bridge/tree/0f935505c0dc74ce3db2a9998320a56119321814/lib/)
2. Implementation `0xa50adbad34c1e9786979bd44220f8fd46e43a6b0`: [op-token-bridge/src/L1TokenBridge.sol](https://github.com/makerdao/op-token-bridge/blob/0f935505c0dc74ce3db2a9998320a56119321814/src/L1TokenBridge.sol)

**Immutables:**
1. `implementation.otherBridge = 0x8F41DBF6b8498561Ce1d73AF16CD9C0d8eE20ba6` - Matches "Optimism - L2 Token Bridge"
2. `implementation.messenger = 0x25ace71c97B33Cc4729CF772ae268934F7ab5fA1` - [`L1CrossDomainMessengerProxy`](https://docs.optimism.io/superchain/addresses)

**Relevant State:**
1. `implementation = 0xa50adbad34c1e9786979bd44220f8fd46e43a6b0` - Matches expected implementation contract.
2. `wards[0xbe8e3e3618f7474f8cb1d074a26affef007e98fb] = true` - [`MCD_PAUSE_PROXY`](https://chainlog.sky.money/api/mainnet/active.json)
3. `escrow = 0x0`
    > ⚠️ Escrow has **not** been set to the deployed Escrow contract yet.

---

### Optimism - L2 Token Bridge (`0x8F41DBF6b8498561Ce1d73AF16CD9C0d8eE20ba6`)

**Code:** 
1. Proxy `0x8F41DBF6b8498561Ce1d73AF16CD9C0d8eE20ba6`: [op-token-bridge/lib/**/ERC1967Proxy.sol](https://github.com/makerdao/op-token-bridge/tree/0f935505c0dc74ce3db2a9998320a56119321814/lib/)
2. Implementation `0xc2702C859016db756149716cc4d2B7D7A436CF04`: [op-token-bridge/src/L2TokenBridge.sol](https://github.com/makerdao/op-token-bridge/blob/0f935505c0dc74ce3db2a9998320a56119321814/src/L2TokenBridge.sol)

**Immutables:**
1. `implementation.otherBridge = 0x3d25B7d486caE1810374d37A48BCf0963c9B8057` - Matches "Ethereum - Optimism bridge - L1 Token Bridge"
2. `implementation.messenger = 0x4200000000000000000000000000000000000007` - [`L2CrossDomainMessenger`](https://docs.optimism.io/stack/smart-contracts#l2crossdomainmessenger).

**Relevant State:**
1. `implementation = 0xc2702C859016db756149716cc4d2B7D7A436CF04` - Matches expected implementation contract.
2. `wards[0x10e6593cdda8c58a1d0f14c5164b376352a55f2f] = true` - Matches `l2GovRelay` for Optimism, verified as being the `l2GovernanceRelay` value on the Optimism `L1GovernanceRelay` [`0x09B354CDA89203BB7B3131CC728dFa06ab09Ae2F`](https://etherscan.io/address/0x09B354CDA89203BB7B3131CC728dFa06ab09Ae2F#readContract#F1) on Ethereum which can be verified from [chainlog.sky.money](https://chainlog.sky.money/api/mainnet/active.json)

---

### Optimism - L2 Bridge Spell (`0x99892216eD34e8FD924A1dBC758ceE61a9109409`)

**Code:** [op-token-bridge/deploy/L2TokenBridgeSpell.sol](https://github.com/makerdao/op-token-bridge/blob/0f935505c0dc74ce3db2a9998320a56119321814/deploy/L2TokenBridgeSpell.sol)

**Immutables:**
1. `l2Bridge = 0x8F41DBF6b8498561Ce1d73AF16CD9C0d8eE20ba6` - Matches "Optimism - L2 Token Bridge"

**Relevant State:** N/A

---

### Optimism - L2 USDS (`0x4F13a96EC5C4Cf34e442b46Bbd98a0791F20edC3`)

**Code:** 
1. Proxy `0x4F13a96EC5C4Cf34e442b46Bbd98a0791F20edC3`: [usds/lib/**/ERC1967Proxy.sol](https://github.com/makerdao/usds/tree/45bf759ba046b66dd115842ee8b9205a64e7bab6/lib/)
2. Implementation `0x2A3541003B34f34833a82F194e4dC69a7a39B057`: [usds/src/Usds.sol](https://github.com/makerdao/usds/blob/45bf759ba046b66dd115842ee8b9205a64e7bab6/src/Usds.sol)

**Immutables:** N/A

**Relevant State:**
1. `implementation = 0x2A3541003B34f34833a82F194e4dC69a7a39B057` - Matches expected implementation contract.
2. `wards[0x10e6593cdda8c58a1d0f14c5164b376352a55f2f] = true` - Matches `l2GovRelay` for Optimism, verified as being the `l2GovernanceRelay` value on the Optimism `L1GovernanceRelay` [`0x09B354CDA89203BB7B3131CC728dFa06ab09Ae2F`](https://etherscan.io/address/0x09B354CDA89203BB7B3131CC728dFa06ab09Ae2F#readContract#F1) on Ethereum which can be verified from [chainlog.sky.money](https://chainlog.sky.money/api/mainnet/active.json)
3. `totalSupply = 0`

---

### Optimism - L2 sUSDS (`0xb5B2dc7fd34C249F4be7fB1fCea07950784229e0`)

**Code:** 
1. Proxy `0xb5B2dc7fd34C249F4be7fB1fCea07950784229e0`: [sdai/lib/**/ERC1967Proxy.sol](https://github.com/makerdao/sdai/tree/e1d160aba17e95e8cec3d6bf50f310fbed9f28d6/lib)
2. Implementation `0x6f0888DDA6a5E35451D5bE0fABb20171715788B3`: [sdai/src/l2/SUsds.sol](https://github.com/makerdao/sdai/tree/e1d160aba17e95e8cec3d6bf50f310fbed9f28d6/src/l2/SUsds.sol)

**Immutables:** N/A

**Relevant State:**
1. `implementation = 0x6f0888DDA6a5E35451D5bE0fABb20171715788B3` - Matches expected implementation contract.
2. `wards[0x10e6593cdda8c58a1d0f14c5164b376352a55f2f] = true` - Matches `l2GovRelay` for Optimism, verified as being the `l2GovernanceRelay` value on the Optimism `L1GovernanceRelay` [`0x09B354CDA89203BB7B3131CC728dFa06ab09Ae2F`](https://etherscan.io/address/0x09B354CDA89203BB7B3131CC728dFa06ab09Ae2F#readContract#F1) on Ethereum which can be verified from [chainlog.sky.money](https://chainlog.sky.money/api/mainnet/active.json)
3. `totalSupply = 0`





# Validating the DV-files using DV tool

Anyone can perform the validation themselves using the `.dvf` files in this repository.

## Clone projects

The projects with the contracts are installed as submodules at the mentioned commits:

```bash
git submodule init .
git submodule update .
# print checked out commits, should match above
git submodule status
```

## Install Deployment Verification Tool

The [Deployment Verification Tool](https://github.com/ChainSecurity/deployment_validation) from ChainSecurity is used to verify the deployed contracts.
The version used for this validation can be found at the following commit: [4c804e4bb984024857c71aa6c2fe279999201105](https://github.com/ChainSecurity/deployment_validation/commit/4c804e4bb984024857c71aa6c2fe279999201105).

## Create DV config

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

You have to replace the placeholder values with your own.
If you do not know from where to get RPCs that support debug_traceTransaction or trace_transaction, check [here](https://github.com/mario-eth/deployment_validation?tab=readme-ov-file#dvf-creation).
Furthermore, you have to replace `ETHERSCAN_API_KEY` with your own Etherscan API key.

## Validate the DV-files

The contracts have been validated at the blocks mentioned above.

### Unichain Bridge

```bash
# validate escrow_unichain.dvf.json for unichain_bridge => escrow
dv validate dvf/escrow_unichain.dvf.json --allowuntrusted --validationblock 22488821

# validate l1Bridge_unichain.dvf.json for unichain_bridge => l1Bridge
dv validate dvf/l1Bridge_unichain.dvf.json --allowuntrusted --validationblock 22488821
dv validate dvf/l1Bridge_unichain.impl.dvf.json --allowuntrusted --validationblock 22488821

# validate l1GovRelay_unichain.dvf.json for unichain_bridge => l1GovRelay
dv validate dvf/l1GovRelay_unichain.dvf.json --allowuntrusted --validationblock 22488821

# validate l2Bridge_unichain.dvf.json for unichain_bridge => l2Bridge
dv validate dvf/l2Bridge_unichain.dvf.json --allowuntrusted --validationblock 16567310
dv validate dvf/l2Bridge_unichain.impl.dvf.json --allowuntrusted --validationblock 16567310

# validate l2BridgeSpell_unichain.dvf.json for unichain_bridge => l2BridgeSpell
dv validate dvf/l2BridgeSpell_unichain.dvf.json --allowuntrusted --validationblock 16567310

# validate l2GovRelay_unichain.dvf.json for unichain_bridge => l2GovRelay
dv validate dvf/l2GovRelay_unichain.dvf.json --allowuntrusted --validationblock 16567310

# validate l2Usds_unichain.dvf.json for unichain_bridge => l2Usds
dv validate dvf/l2Usds_unichain.dvf.json --allowuntrusted --validationblock 16567310
dv validate dvf/l2Usds_unichain.impl.dvf.json --allowuntrusted --validationblock 16567310
```

### Optimism Bridge

```bash
# validate l1Bridge_op.dvf.json for optimism_bridge => l1Bridge
dv validate dvf/l1Bridge_op.dvf.json --allowuntrusted --validationblock 22488821
dv validate dvf/l1Bridge_op.impl.dvf.json --allowuntrusted --validationblock 22488821

# validate l2Bridge_op.dvf.json for optimism_bridge => l2Bridge
dv validate dvf/l2Bridge_op.dvf.json --allowuntrusted --validationblock 135858527
dv validate dvf/l2Bridge_op.impl.dvf.json --allowuntrusted --validationblock 135858527

# validate l2BridgeSpell_op.dvf.json for optimism_bridge => l2BridgeSpell
dv validate dvf/l2BridgeSpell_op.dvf.json --allowuntrusted --validationblock 135858527

# validate l2Usds_op.dvf.json for optimism_bridge => l2Usds
dv validate dvf/l2Usds_op.dvf.json --allowuntrusted --validationblock 135858527
dv validate dvf/l2Usds_op.impl.dvf.json --allowuntrusted --validationblock 135858527
```

### Susds

```bash
# validate sUsds_unichain.dvf.json for susds => sUsds (unichain)
dv validate dvf/sUsds_unichain.dvf.json --allowuntrusted --validationblock 16567310
dv validate dvf/sUsds_unichain.impl.dvf.json --allowuntrusted --validationblock 16567310

# validate sUsds_op.dvf.json for susds => sUsds (optimism)
dv validate dvf/sUsds_op.dvf.json --allowuntrusted --validationblock 135858527
dv validate dvf/sUsds_op.impl.dvf.json --allowuntrusted --validationblock 135858527
```


<details>
<summary><strong>Initial dv-files creation<strong></summary>

```bash
dv init --project ./projects/op-token-bridge --address 0x1196F688C585D3E5C895Ef8954FFB0dCDAfc566A --contractname Escrow escrow_unichain.dvf.json --chainid 1 --initblock 22488821

dv init --project ./projects/op-token-bridge --address 0xDF0535a4C96c9Cd8921d8FeC92A7680b281681d2 --contractname ERC1967Proxy --implementation L1TokenBridge l1Bridge_unichain.dvf.json --chainid 1 --initblock 22488821

dv init --project ./projects/op-token-bridge --address 0x8A925ccFd5F7f46332E2D719A916f8b4a643599F --contractname L1TokenBridge l1Bridge_unichain.impl.dvf.json --chainid 1 --initblock 22488821

dv init --project ./projects/op-token-bridge --address 0xb383070Cf9F4f01C3a2cfD0ef6da4BC057b429b7 --contractname L1GovernanceRelay l1GovRelay_unichain.dvf.json --chainid 1 --initblock 22488821

dv init --project ./projects/op-token-bridge --address 0xa13152006D0216Fe4627a0D3B006087A6a55D752 --contractname ERC1967Proxy --implementation L2TokenBridge l2Bridge_unichain.dvf.json --chainid 130 --initblock 16567310

dv init --project ./projects/op-token-bridge --address 0xd78292C12707CF28E8EB7bf06fA774D1044C2dF5 --contractname L2TokenBridge l2Bridge_unichain.impl.dvf.json --chainid 130 --initblock 16567310

dv init --project ./projects/op-token-bridge --address 0x32760698c87834c02ED9AFF2d4FC3e16c029B936 --contractname L2TokenBridgeSpell l2BridgeSpell_unichain.dvf.json --chainid 130 --initblock 16567310

dv init --project ./projects/op-token-bridge --address 0x3510a7F16F549EcD0Ef018DE0B3c2ad7c742990f --contractname L2GovernanceRelay l2GovRelay_unichain.dvf.json --chainid 130 --initblock 16567310

dv init --project ./projects/usds --address 0x7E10036Acc4B56d4dFCa3b77810356CE52313F9C --contractname ERC1967Proxy --implementation Usds l2Usds_unichain.dvf.json --chainid 130 --initblock 16567310

dv init --project ./projects/usds --address 0x8fb6EF2dA06a6957fC84C2C55bb195837fB7DBa9 --contractname Usds l2Usds_unichain.impl.dvf.json --chainid 130 --initblock 16567310

dv init --project ./projects/op-token-bridge --address 0x3d25B7d486caE1810374d37A48BCf0963c9B8057 --contractname ERC1967Proxy --implementation L1TokenBridge l1Bridge_op.dvf.json --chainid 1 --initblock 22488821

dv init --project ./projects/op-token-bridge --address 0xA50adBad34c1e9786979bD44220F8fd46e43A6B0 --contractname L1TokenBridge l1Bridge_op.impl.dvf.json --chainid 1 --initblock 22488821

dv init --project ./projects/op-token-bridge --address 0x8F41DBF6b8498561Ce1d73AF16CD9C0d8eE20ba6 --contractname ERC1967Proxy --implementation L2TokenBridge l2Bridge_op.dvf.json --chainid 10 --initblock 135858527

dv init --project ./projects/op-token-bridge --address 0xc2702C859016db756149716cc4d2B7D7A436CF04 --contractname L2TokenBridge l2Bridge_op.impl.dvf.json --chainid 10 --initblock 135858527

dv init --project ./projects/op-token-bridge --address 0x99892216eD34e8FD924A1dBC758ceE61a9109409 --contractname L2TokenBridgeSpell l2BridgeSpell_op.dvf.json --chainid 10 --initblock 135858527

dv init --project ./projects/usds --address 0x4F13a96EC5C4Cf34e442b46Bbd98a0791F20edC3 --contractname ERC1967Proxy --implementation Usds l2Usds_op.dvf.json --chainid 10 --initblock 135858527

dv init --project ./projects/usds --address 0x2A3541003B34f34833a82F194e4dC69a7a39B057 --contractname Usds l2Usds_op.impl.dvf.json --chainid 10 --initblock 135858527

dv init --project ./projects/susds --address 0xA06b10Db9F390990364A3984C04FaDf1c13691b5 --contractname ERC1967Proxy --implementation SUsds sUsds_unichain.dvf.json --chainid 130 --initblock 16567310

dv init --project ./projects/susds --address 0x15c2A564b987470FAFCaB0B036029532bd168E10 --contractname SUsds sUsds_unichain.impl.dvf.json --chainid 130 --initblock 16567310

dv init --project ./projects/susds --address 0xb5B2dc7fd34C249F4be7fB1fCea07950784229e0 --contractname ERC1967Proxy --implementation SUsds sUsds_op.dvf.json --chainid 10 --initblock 135858527

dv init --project ./projects/susds --address 0x6f0888DDA6a5E35451D5bE0fABb20171715788B3 --contractname SUsds sUsds_op.impl.dvf.json --chainid 10 --initblock 135858527
```

> Note: You need to run `dv id <dvf>` after altering the dvf files. 
  
</details>
