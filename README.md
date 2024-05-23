# Ethereum addresses belonging to Solo Stakers

**This repository  is intended to identify addresses under the  control of Solo Stakers  and for projects that wish to target Solo Stakers for incentives or onboard actors capable of supporting decentralized node operations.**

**Latest Snapshot: Dencun network upgrade 2024/03/13**

----
## What is a Solo Staker

**Independent operators Staking for themselves who are not part of an entity staking on behalf of others.  Independent operators can run their own infrastructure (e.g. stake from home) or use cloud (VPS) for hosting but are in complete control of the setup, maintenance and keys.**

‘Liquid’, ‘managed’ or ‘custodial’ staking where entities stake on behalf of users are centralizing to the network as stake is concentrated to a few entities, also in other factors such as hardware/geographic distribution/client diversity.

For more detail see this [article from Nixo Ethstaker]([https://paragraph.xyz/@ethstaker/define-solo-staker](https://paragraph.xyz/@ethstaker/define-solo-staker))

## Intent

To identify Solo Stakers (independent node operators) and promote decentralization.

Incentivize decentralization with external incentives (such as airdrops to Solo Stakers) leading to more potential stakers opting to solo stake over using alternatives such as liquid staking. Increase the number of node operators independent of each other thus strengthening network integrity.

Provide value for projects that wish to onboard the type of actors capable of supporting node operations. 99% of normal users do not run nodes, solo stakers take on the responsibilities of node operations without delegating this work to third parties.

What is included as a Solo Staker:

-  Solo Stakers who run from home
-  Solo Stakers who run from the cloud
-  Rocket Pool home operators
-  EigenPod Solo Stakers

Other types of independent node operators:

-  Gnosischain home stakers
-  Other types of independent node operators: such as home DVT node operators to be included in time.

## List Exclusions

**All Contract address deposits:** deposits via contract address are indicative of entity behavior and excluded by default, see “Exceptions for Contracts”.

**Managed staking services:** such as ‘Allnodes’/’Bloxstaking’ are excluded, not only is the deposit via contract they act as an entity that manage/setup and run the validator on behalf of their users, who cannot be considered Solo Stakers or independent node operators.

**Temporary Coinbase Deposit Addresses:** Addresses with no other history but Coinbase withdrawal and beacon deposit, are identified as Coinbase. This set will likely contain some number of privacy focused Solo Stakers  but is significantly large that cannot reasonably be included as potential Solo Staker.

**Exceptions for Contracts:**  
Rocketpool  node operators:  deposits for  “minipools” are via smart contract, Rocketpool node operators make up a significant portion of the solo staking landscape and are included by looking at Rocketpool contracts.

Abyss Finance users: work is being done to identify Solo Stakers from the Entities that use the contract to make multiple deposits in one transaction. Issue #10

## How to Use Solo Stakers

**List A or List B**

Unlike identifying Entities with much more resources/disclosures and behavior to track (including openness from entities themselves to self-identify), identification of Solo stakers is much more difficult (like proving a negative).

### Solo-Staker-A:  Potential Solo Stakers

**Ethereum addresses that deposited a valid 32 ETH transaction to the beacon chain and have at least 1 active validator, with identified entity addresses  removed.**  _Solo-Staker-A will include all Solo-Staker-B addresses._

More inclusive is a 'ceiling' on the total Solo Staker profile; it is likely to contain unidentified entities, but all solo stakers should reside in. This simply takes all normal beacon chain depositors and removes positively identified entities.

**15,580** addresses in **Solo Staker A** at “Dencun” network upgrade **2024/03/13** epoch: 26958.

### Solo-Staker-B:  High confidence Solo Stakers

**Ethereum addresses that deposited a valid 32 ETH transaction to the beacon chain and have at least 1 active validator, with a history of smart contract/token interactions, identified entity addresses removed.** _All Solo-Staker-B addresses will be present in Solo-Staker-A._

More restrictive conditions for a more targeted curated set, by looking for additional contract/token interactions which is indicative of Ethereum network users with proven on-chain history.

_from Rated: “Solo stakers fund all (or some if in Rocketpool) of the stake through their own means. This is usually via a generic wallet that is used for multiple purposes.”_

**7,509** addresses in **Solo Staker B** at “Dencun” network upgrade **2024/03/13** epoch: 26958.

### Rocketpool node operators

**Rocketpool node operator owned Ethereum withdrawal addresses associated with a node account that operated at least one active validator.**

**Rocketpool accounts for a large portion of independent node operators on the network and should be included alongside Solo Stakers. [Rocketpool](https://rocketpool.net/) is a decentralized staking pool with permissionless node operators.**

Rocketpool node accounts are normal Ethereum addresses, which can be used for token interactions however act as a sudo cold wallet intended only for staking/unstaking interactions with the Rocketpool CLI, it is advised that withdrawal addresses be used.

**34,668 Minipools** (rocketpool validators) deployed with **2,642 node operator withdrawal addresses** belonging to Solo Stakers using Rocketpool, at “Dencun” network upgrade **2024/03/13** epoch: 26958.

### Eigenpod  Solo Stakers

Identified in `/Metadata`, Eigenpod  (Native Restakers) solo stakers will be included in Solo-Stakers-A + B via deposit address by default.

**Associated withdrawal addresses are eigenpod contracts and tokens sent to this contract are unrecoverable, therefore deposit addresses are  advised to be used.**

### Metadata

`/Solo-Stakers-Metadata/` takes deposit addresses and expands to include additional data which can be used to gather associated withdrawal addresses, validator count, time staked. Etc.

### Snapshots

`/Solo-Stakers-Snapshots/` various snapshots at earlier dates can be found here, such as Ethereum network upgrades eg: Merge

## Sybil identification:

The list makes no attempt to connect addresses, it is likely that some individual users are counted multiple times with access to multiple deposit addresses, thus an individual node operator might appear on the network as many. This is a much deeper topic but worth briefly going into.

Built in sybil: excluding temporary deposit addresses, projects may wish to use B list to filter potential sybil accounts.

Time: sybil behavior is not a significant problem as of now, this may become more relevant in future as Solo Staker inclusion catches on. Example: pre-merge, airdrops to solo stakers were non-existent meaning this behavior was not incentivized.

High Cost: Solo staking is anti-sybil due to high capital requirement, where DeFi users can create virtually x1000s of wallets at no cost and wash to generate large volume on each appearing as many separate users, this is not possible with validator deposits.

# Methodology

## Step 1: Beacon chain data

Data source: etherscan.io, Ethereum blockchain
Beacon Chain deposit contract: `0x00000000219ab540356cBB839Cbe05303d7705Fa`

Extract all ‘Normal Ethereum Transactions’ to the beacon chain contract address, from contract creation to the latest snapshot (Dencun network upgrade) to make the foundation data `Beacon-Chain-Data`.

Filter invalid or failed transactions: If the “Status” column displays any transaction that either ‘execution reverted’, ‘out of gas’, or ‘reverted’ with an 'Error(0)' code, it is an invalid transaction and the deposit failed, therefore entries with ‘Error(0)’ in the status column are removed.

Get unique deposit addresses: remove duplicate entries under the 'From' column, resulting in a dataset consisting of all unique deposit addresses that made a valid deposit to the beacon chain.

## Step 2: Entity list

Data source:
Hildoby: Entity tags from [https://github.com/hildobby/spellbook/tree/main](https://github.com/hildobby/spellbook/tree/main)
Etherscan/beaconcha.in entity tags

`Entity-List` compiles a comprehensive list of identified entities from various sources, such as etherscan.io/beaconcha.in & Hildoby dune dashboards.

Contains positively Identified addresses belonging to Staking as a Service/ Liquid Staking provider addresses (such as Lido and Stakewise) and Exchange CEX addresses (such as Kraken and Binance).

**Smart contract depositors:**
Deposits via smart contract address are indicative of entity behavior, entities with assets under management will typically use multi-sig with multiple signers to move funds, or smart contract to handle multiple deposits in one transaction.

_Example Lido: Batched transactions to deposit multiple validators via smart contract_
<LIDO BATCHED DEPOSITORS HERE>
So, by extracting only normal Ethereum transactions to the beacon contract many entities are already excluded, then exceptions can be made for select depositors such as Rocketpool users.

**Coinbase:**
135,084 addresses (2024/04/10)  represent  a significant portion of unique deposit addresses, using a fresh temporary address per deposit and can be identified with the following pattern, with change returned to `Coinbase: Miscellaneous`

<COINBASE IMAGE HERE>

Another pattern with change being left in the temporary deposit address, this set is over 10k addresses, does not positively identify as Coinbase owned with potential of belonging to Solo Stakers using a temporary address, but is simply too large a set with no way to differentiate Solo Stakers from Coinbase.

<COINBASE IMAGE HERE>

To get Coinbase from dune:
```
SELECT
  depositor_address
FROM staking_ethereum.entities
WHERE
  entity = 'Coinbase'
```

## Step 3: Filter Entities - Solo Staker A

All unique deposit addresses from `beacon-chain-data` with all identified entity addresses from `entity-list` removed. This leaves unidentified potential Solo Staker addresses.

## Step 4: Solo Staker B

Data source: Dune Analytics  (https://dune.com/)

**High Confidence Solo Staker Owned Addresses**

Find addresses that have made a valid Beacon Chain deposit and have also interacted with smart contracts/tokens, with identified entities from `Entity-List` removed.

Using Dune analytics, the following query looks for `(ethereum."transactions")` to the beacon contract `0x00000000219ab540356cBB839Cbe05303d7705Fa` and joins with `ContractInteractions` from senders who have interacted with contracts other than the beacon chain contract in past transactions.

Query for Dune analytics:
```  
WITH ContractInteractions AS (  
    SELECT DISTINCT "from" as address  
    FROM ethereum."transactions"  
    WHERE LENGTH(data) > 2 -- Excluding '0x' and empty inputs  
    AND "to" != 0x00000000219ab540356cBB839Cbe05303d7705Fa -- Excluding the beacon chain contract  
)  
  
SELECT  
  t."from" as address,  
  SUM(t.value / 1e18) as deposited_eth,  
  COUNT(t."from") as transaction_count  
FROM  
  ethereum."transactions" t  
JOIN ContractInteractions ci ON t."from" = ci.address  
WHERE  
  t."to" = 0x00000000219ab540356cBB839Cbe05303d7705Fa  
GROUP BY  
  t."from"  
HAVING  
  COUNT(t."from") >= 1  
ORDER BY  
  deposited_eth DESC;  
```

## Step 5: Rocketpool

Data source: Rocketscan  API  (https://rocketscan.io/)

All unique “withdrawal addresses” associated with RocketPool "node accounts"; data can be queried from [Rocketscan](https://rocketscan.io/) API

```
curl -Ss --compressed "https://rocketscan.io/api/mainnet/nodes/list" | jq -r '.[] | "\(.address) \(.withdrawalAddress)"' > output-add-with-wid-add.txt  
```

## Step 6: Metadata

Data source: beaconcha.in API or beacon node

Using Deposit addresses from `Solo-Staker-A` generate all associated validator `public-keys` with the following query <link to query reference>

Using `public-keys`metadata such as: `.block_number, .block_ts, .tx_hash, .withdrawal_credentials, .status, .exitepoch`  can be obtained with the following queries < link to query reference>

This data in then placed into the Metadata sheet, which is arranged in the following format:
(Deposit address, validator public key, deposit tx, date, status, exit date, withdrawal address.)

To see full list of api’s see beaconcha.in docs <LINK>

The same is done for Rocketpool but using Rocketpool Node Account addresses from <query link `rpl-accounts+minipool`>