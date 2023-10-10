# ETH-Solo-Validator-Addresses

**unique ETH addresses belonging to solo stakers**

**This is intended to identify addresses under control of solo stakers, for projects that wish to target solo stakers for incentives or onboard actors capable of supporting decentralised node operations**

**Methodology**
ETH2 Deposit Contract: `0x00000000219ab540356cbb839cbe05303d7705fa`

This attempts to identify solo staker owned addresses, by combining all unique validator deposit addresses including RocketPool node operator (withdrawal) addresses, and removing identified centralised entities such as CEXs (ex: Coinbase, Kraken), and Staking as a Service/ Liquid staking providers (ex: Lido and Stakewise)

More details and information on some findings from this repository are expanded on here [Ethereum - How Many Solo Stakers?](https://mirror.xyz/0xf3bF9DDbA413825E5DdF92D15b09C2AbD8d190dd/CzCNFznCveDlKnlVaSU5-MzUtbn9gW0KlgPe5FVrQME)

**Solo Stakers** are the [backbone of Ethereum](https://blog.rated.network/blog/solo-stakers) and its credible neutrality, Rated Network have researched this looking at a wide array of metrics related to validator performance
estimating that around 6.5% of the network are solo stakers, where this is taking a different approach focusing on deposit addresses and aims to make details public.

## Solo-Stakers

**Solo_Stakers_A**

**17,065** Addresses that have made a valid Beacon Chain deposit, with identified entities removed.

known large and easily identified entities are filtered out, however small pools/institutions not easily identified and /can’t be differentiated from potential solo-stakers

does not attempt to ‘join’ addresses, there are stakers that will use a single use deposit address for privacy concerns meaning multiple addresses can be under control of one

_NOTE: this also includes RocketPool NO withdrawal addresses._


**Solo_Stakers_B**

Addresses that have made a valid Beacon Chain deposit and have also interacted with smart contracts, with identified entities removed.

_from Rated: “**Solo stakers fund all (or some if in Rocketpool) of the stake through their own means**. This is usually via a generic wallet that is used for multiple purposes.”_

**9,420** addresses with history of contract interaction/token transfers indicative of Ethereum users experienced in defi and general on chain activity, and not institutional/exchange owned addresses.

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

**Solo_Stakers_merge**

This list contains solo-staker addresses up to the **_merge activation on Sep 15 06:42:42 2022 UTC,_ Block: 15,537,393**

when Ethereum fully transitioned to proof of stake, all stakers before this upgrade had committed to bootstrap the proof of stake chain before proof of stake was proven on Ethereum and taken on early execution risk.

**Solo_Stakers_Shapella**

This list contains solo-staker addresses up to the **Shapella hardfork Apr-12-2023 23:27:35 UTC+1, slot: 6,209,536**

before withdrawals were enabled, all stakers before this upgrade had committed to lock ETH and secure the network before withdrawals were possible and for an unknown period, sacrificing liquidity to provide security to Ethereum.

## Entity-List

Known Staking as a Service/ Liquid Staking provider addresses (such as Lido and Stakewise) and Exchange CEX addresses (such as Kraken and Binance).

Entity tags from https://github.com/hildobby/spellbook/tree/main

**Coinbase A**

94,008 addresses

confirmed Coinbase addresses, these follow a pattern of change returning fees to Coinbase owned accounts. Confirming these deposit addresses are Coinbase owned and controlled.

**Coinbase B**

10,862 addresses

likely Coinbase addresses, addresses that have the same pattern.

there are potentially solo-stakers within this set using Coinbase to obfuscate their deposit, but cannot be distinguished from Coinbase themselves or other entities using this pattern.

Data can be queried from dune with the following:
```
WITH CoinbaseReceived AS (
    SELECT "to" AS recipient_address
    FROM ethereum."transactions"
    WHERE "from" IN (
        0x71660c4005BA85c37ccec55d0C4493E66Fe775d3,
        0x503828976D22510aad0201ac7EC88293211D23Da,
        0xddfAbCdc4D8FfC6d5beaf154f18B778f892A0740,
        0x3cD751E6b0078Be393132286c442345e5DC49699,
        0xb5d85CBf7cB3EE0D56b3bB207D5Fc4B82f43F511,
        0xeB2629a2734e272Bcc07BDA959863f316F4bD4Cf,
        0xD688AEA8f7d450909AdE10C47FaA95707b0682d9,
        0x02466E547BFDAb679fC49e96bBfc62B9747D997C,
        0x6b76F8B1e9E59913BfE758821887311bA1805cAB,
        0xA9D1e08C7793af67e9d92fe308d5697FB81d3E43,
        0x77696bb39917C91A0c3908D577d5e322095425cA,
        0x7c195D981AbFdC3DDecd2ca0Fed0958430488e34,
        0x95A9bd206aE52C4BA8EecFc93d18EACDd41C88CC,
        0xb739D0895772DBB71A89A3754A160269068f0D45
    )
),
BeaconDeposits AS (
    SELECT "from"
    FROM ethereum."traces"
    WHERE "to" = 0x00000000219ab540356cBB839Cbe05303d7705Fa
    AND "from" IN (SELECT recipient_address FROM CoinbaseReceived)
),
AllTransactions AS (
    SELECT "from", COUNT(*) as tx_count
    FROM ethereum."transactions"
    WHERE "from" IN (SELECT "from" FROM BeaconDeposits)
    GROUP BY "from"
)
SELECT "from"
FROM AllTransactions
WHERE tx_count = 1;
```

## RocketPool-Node-Operators

All unique ‘withdrawal addresses’ associated with RocketPool node accounts; data can be queried from [Rocketscan](https://rocketscan.io/) API

Example:

```
curl --compressed "https://rocketscan.io/api/mainnet/nodes" | jq -r '.[].withdrawalAddress' | sort | uniq
```

RocketPool validator deposits to the beacon chain are done via smart contract, this manages the matching with ETH from the pool, there are approx. 28,983 Mini-pools - using withdrawal addresses is a better indication of solo-staker owned accounts.

## Beacon-Chain-Depositors

**All unique addresses** that deposited a **valid** **(32ETH)** transaction to the ‘ETH2 deposit contract’. this will include addresses belonging to exchanges and liquid/pooled staking providers.

All Contract addresses are excluded from this, (Including RocketPool Mini-pool contract addresses)

**This is up to 17/09/2023.**
