# Coupon-Clipper
A Coupon Clipper for DSD. Easy-access UI will be available [here](https://dynamicdollar.coupons/)
within a week.

> Disclaimer: This code is not unaudited. Interact with it at your own risk,
and *do not* send tokens to it. DeFi can be dangerous; exercise discretion.

## Summary

The **Dynamic Set Dollar** protocol incentivizes users to burn their tokens
by offering coupons when DSD is worth less than $1. If the price rises
above $1, coupons can be redeemed for extra DSD. Unfortunately, coupons
expire, and bots have an advantage in the
first-come-first-serve system. **This contract lets you put the bots to
work!**

We've set the initial house fee to 1.0%. Every time a bot generates
100000DSD for the house, the house's cut will be halved for that bot's
transactions. This results in a more fair playing field for the bots, and
rewards long-time players for their commitment.

> An example: If Bot A has earned 150000DSD for the house, the house cut drops
to `1.0/2**1 = 0.5%` for them. If Bot B has earned 300001DSD for the house, the
house cut drops to `1.0/2**3 = 0.125%` for them. Due to rounding, the house
cut eventually goes to zero.

Because of DIP-2, some coupons also get burned if redeemed in the first hour of
an epoch. This contract allows users to specify the maximum percentage of coupons
they are willing to burn (default is 0%).

## Deployed Contract

`CouponClipper` is deployed to [0x01E7E854b76d59A8623DFf07dEaCBDa6ef60D981](https://etherscan.io/address/0x01E7E854b76d59A8623DFf07dEaCBDa6ef60D981)
and the code is verified on Etherscan.

## How does it work?

Users can interact with the contract directly or go to [dynamicdollar.coupons](https://dynamicdollar.coupons/) (currently under construction) to configure
their tip and approve the contract.

This will emit a `CouponApproval` event for which bots can listen. When
coupons become available, bots can call a variety of functions to redeem
the coupons of one or more users. The users' new DSD will magically appear
in their account, and the bot receives (at minimum) a 1.0% cut for their
effort. Users can increase this tip size via the `setOffer` function.
