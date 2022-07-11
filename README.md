# ETH-Solo-Validator-Addresses
unique ETH addresses belonging to solo stakers



**Contracts** 

Eth2 Deposit Contract

0x00000000219ab540356cbb839cbe05303d7705fa

RPL node Deposit contract Address

0xDCD51fc5Cd918e0461B9B7Fb75967fDfD10DAe2f

**#Validator List**

All unique validator deposit addresses including Rocketpool node operator (withdrawal addresses), this excludes exchanges such as Coinbase and kraken, and staking as a service/liquid staking such as Lido.

this list is every solo validator owned address that made at least 1 valid deposit to the beacon chain up until the end of June 2022. (will be keeping this updated until the merge)

**#Beacon Chain Depositors**

All unique addresses that deposited a valid (32ETH) transaction to the ‘ETH2 deposit contract’. this will include addresses belonging to exchanges and liquid/pooled staking providers. contract addresses are excluded from this, such as rocketpool minipool contract addresses

**#Rocketpool Depositors**

All unique ‘withdrawal addresses’ associated with rocketpool node accounts, due to security concerns withdrawal addresses which are better fit for receiving any token distributions. This excludes rETH minters.

**#Blacklist**

Data From ETHsta.com (https://github.com/Zachary-Lingle)
Known staking as a service/liquid staking addresses, Such as Lido, Stakewise. exchange addresses such as Kraken,
this includes Coinbase deposits which account for ~60,000 of the ‘Beacon Chain Depositors’ sheet. 
some addresses such as known QuadrigaCX wallets


**Methodology**

Data was pulled from associated contracts above, invalid deposits were removed and duplicate addresses filtered out. The blacklist was applied to remove those addresses belonging to LSD providers and Exchanges/Custodians.

Leaving all unique Ethereum addresses belonging to solo stakers that have deposited to the beacon chain contract to run a validator, pre- merge.
