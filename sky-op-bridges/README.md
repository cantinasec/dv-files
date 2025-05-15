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

#### DV-file creation


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


#### Validating against DV-files

Validated against the `dvf.json` files on blocks:

- Ethereum: [22488821](https://etherscan.io/block/22488821): May-15-2025 01:29:47 PM +UTC
- Optimism: [135858527](https://optimistic.etherscan.io/block/135858527): May-15-2025 01:30:31 PM +UTC
- Unichain: [16567310](https://uniscan.xyz/block/16567310) May-15-2025 01:27:49 PM +UTC

> TODO: use `dv validate` instead of `dv init`

```bash
dv validate dvf/escrow_unichain.dvf.json --allowuntrusted --validationblock 22488821
```
