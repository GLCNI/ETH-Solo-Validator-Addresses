
## metadata update 3 - 2024-05-22
### Fixes/Changes/updates
**RocketPool Allnodes**
Identified Allnodes accounts in Rocketpool 
• 1. Removed Rocketpool node accounts under control Allnodes entity from Rocketpool-node-operators.csv
• 2. Removed minipools keys under control of Allnodes entity from metadata
• 3. Rename to `Rocketpool-Solo-Stakers`.

**Duplicate (RPL) validator keys**
• 1. Removed duplicate public keys in `Solo-Staker-Metadata`(x674) showing up in both Rocketpool and Solo Staker metadata exports.
• 2. Rocketpool only stakers removed from Solo Stakers A + B:
```
0x3b68b1322691292415d51da7049200b796bc2060
0x08cfb15c7be7eb5e7363e6fcf1869fba2fa6a3d6
0xefb4bf17add87935b10941e6019848dd7fe5352b
0x0269292740fa092151e843603a3ab8a47e6287ed
```
**Identified Entity Addresses**
    • 1. Redacted Cartel: `0xa8d092b8b1a07ef7b8b409ced7cfb13c0e46e439`added to Entity List
    • 2. Removed from `Solo-Staker-(A+B)`

**Invalid Validators**
Identified `invalid` validators.
• 1. Removed invalid validators from metadata: 
```
0x86f473a006c566f1648a82c74cdfbd4a3cb2ea04eb2e0d49ef381ab2562576888554ef3d39e56996f24c804abb489600,0xac424d8a3e6ce38eb22109125357324a1c44ecad7a330a3d3deff91e68f4b567ba38c065d2cf852ef050d21705e5dfcb,0x918f080ca717afed4966901794ad8222ca618b523bbd3ce94be4a1240aa69d9be20f884950214a3cafa0404ce41213e1,0x8c69edd7a8e8da5330787952a1ad5075516e6fd4bda1586d62dd64701f7628d5229eb7f929017dea9ae6995f9c69ef5e
``` 
• 2. Addresses with only `invalid` validators removed `Solo-Staker-(A+B)`
`0x054e993e0ecc5bf2797515adfc81d58cb8de0478,0x7424e2d7a8c4ed89c19c8f4a3afae9fb277a1862 `  