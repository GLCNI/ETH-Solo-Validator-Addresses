# ETH-Solo-Validator-Addresses

###  Ethereum addresses belonging to Solo Stakers

**This is intended to identify addresses under control of solo stakers, for projects that wish to target solo stakers for incentives or onboard actors capable of supporting decentralised node operations**

**Updated: Dencun network upgrade 2024/03/13**

**Methodology**
_This attempts to identify solo staker owned addresses, by combining all unique validator deposit addresses including RocketPool node operator (withdrawal) addresses, and removing identified centralised entities such as CEXs (ex: Coinbase, Kraken), and Staking as a Service/ Liquid staking providers (ex: Lido and Stakewise)_

ETH2 Deposit Contract: `0x00000000219ab540356cbb839cbe05303d7705fa`
All deposit transactions from normal Ethereum addresses to this contract, contract addresses excluded to get `Beacon-Chain-Depositors`, invalid deposits are filtered out.

Entities: compiling a comprehensive list of identified entities from etherscan/Hildoby dataset to get `Entity-List`

Solo Stakers: to get `solo-stakers-a` the known entity addresses are removed from the beacon chain depositors and `RocketPool-Node-Operators` addresses are added.

**Additional information and resources**
More details and information on some findings from this repository are expanded on here [Ethereum - How Many Solo Stakers?](https://mirror.xyz/0xf3bF9DDbA413825E5DdF92D15b09C2AbD8d190dd/CzCNFznCveDlKnlVaSU5-MzUtbn9gW0KlgPe5FVrQME) (2023-10-10)

[**Rated Network**](https://www.rated.network/) [Solo Stakers are the backbone of Ethereum](https://blog.rated.network/blog/solo-stakers) (2023-05-24) and its credible neutrality, researched a wide array of metrics related to validator performance estimating that around 6.5% of the network are solo stakers (at time of writing). Rated have since released this data publicly which can be [found here.](https://github.com/rated-network/solo-stakers/tree/main) 

Differences in Method:  Rated uses a wide range of metrics related to validator performance and ml techniques. This uses a simplistic approach focusing on deposit addresses to the contract and filters out known entities which are easily identifiable, it has been public since inception and is easily reproducible. 

## Solo-Stakers

**Solo_Stakers_A** Potential Solo Staker Owned Addresses

**18,835** Addresses that have made a valid Beacon Chain deposit, with identified entities removed.

known large and easily identified entities are filtered out, however small pools/institutions not easily identified and can’t be differentiated from potential solo-stakers.

does not attempt to ‘join’ addresses, there are stakers that will use a single use deposit address for privacy concerns meaning multiple addresses can be under control of one.

_NOTE: this also includes RocketPool NO withdrawal addresses._


**Solo_Stakers_B** High Confidence Solo Staker Owned Addresses

Addresses that have made a valid Beacon Chain deposit and have also interacted with smart contracts, with identified entities removed.

_from Rated: “**Solo stakers fund all (or some if in Rocketpool) of the stake through their own means**. This is usually via a generic wallet that is used for multiple purposes.”_

**10,849** addresses with history of contract interaction/token transfers indicative of Ethereum users experienced in defi and general on chain activity, and not institutional/exchange owned addresses.

Data can be queried from dune with the following:
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

_NOTE: this also includes RocketPool NO withdrawal addresses._

`/Solo-Stakers-Snapshots` various snapshots at earlier dates can be found here, such as Ethereum network upgrades eg: Merge 


## Entity-List

Known Staking as a Service/ Liquid Staking provider addresses (such as Lido and Stakewise) and Exchange CEX addresses (such as Kraken and Binance).

Entity tags from https://github.com/hildobby/spellbook/tree/main

**Coinbase**

135,084 addresses at 2024/04/10.

Data can be queried from dune with the following:
```
SELECT
  depositor_address
FROM staking_ethereum.entities
WHERE
  entity = 'Coinbase'
```

## RocketPool-Node-Operators

All unique ‘withdrawal addresses’ associated with RocketPool node accounts; data can be queried from [Rocketscan](https://rocketscan.io/) API

Example:

```
curl --compressed "https://rocketscan.io/api/mainnet/nodes" | jq -r '.[].withdrawalAddress' | sort | uniq
```

RocketPool validator deposits to the beacon chain are done via smart contract, this manages the matching with ETH from the pool, there are approx. 34,938 Mini-pools (2024/04/10) - using withdrawal addresses is a better indication of solo-staker owned accounts.

## Beacon-Chain-Depositors

**All unique addresses** that deposited a **valid** **(32ETH)** transaction to the ‘ETH2 deposit contract’. this will include addresses belonging to exchanges and liquid/pooled staking providers.

All Contract addresses are excluded from this, (Including RocketPool Mini-pool contract addresses)

**This is up to Dencun network upgrade 2024/03/13****


## Upcoming 

- Users of Abyss Finance see issue #10

- Adding associated withdrawal addresses as option to use instead.

- Adding validator count per address

- Adding DVT Stakers

- Update Gnosischain