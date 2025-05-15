# Sky OP Bridges Deployment Validation


Validated commits:

- op-token-bridge: `82918f4853d50c6520dac53fdb70a42fd4ce671b`
- susds: `dfc7f41cb7599afcb0f0eb1ddaadbf9dd4015dce`
- usds: `d65551dbc11cfe1afcc4718ab790663b99d766af`


## Validation commands

Check out the git repositories at the mentioned commits:

```bash
git submodule init .
git submodule update .
# print checked out commits, should match above
git submodule status
```

## Install Deployment Verification Tool

Pull the [Deployment Verification tool](https://github.com/mario-eth/deployment_validation) and install it via docker or from sources, more information [here](https://github.com/mario-eth/deployment_validation?tab=readme-ov-file#installation)

## Create Validation File

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
## DV-file creation THIS WILL NEED TO BE DELETED IN THE FINAL COMMIT, this is just for bootstraping the dv files



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

The DV files where generated based on the following deployed contracts

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
