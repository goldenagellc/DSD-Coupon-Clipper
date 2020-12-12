# Coupon-Clipper
A cheaper version of Austin Williams' Coupon Clipper. Easy-access UI is
available [here](https://emptyset.coupons/).

> Disclaimer: This code is not unaudited. Interact with it at your own risk,
and *do not* send tokens to it. DeFi can be dangerous; exercise discretion.

## Summary

The **Empty Set Dollar** protocol incentivizes users to burn their tokens
by offering coupons when ESD is worth less than $1. If the price rises
above $1, coupons can be redeemed for extra ESD. Unfortunately, coupons
expire after ~30 days, and bots have an advantage in the
first-come-first-serve system. **This contract lets you put the bots to
work!**

A [previous version](https://github.com/Austin-Williams/coupon-clipper)
of this contract, by [Austin Williams](https://github.com/Austin-Williams/)
takes a 1% house fee and transfers funds to the house after redeeming *any*
amount of coupons. To save on gas, we've updated it so that a separate
function transfers accumulated fees to the house.

We've also reduced the initial house fee to 0.5%. Every time a bot generates
10000ESD for the house, the house's cut will be halved for that bot's
transactions. This results in a more fair playing field for the bots, and
rewards long-time players for their commitment.

> An example: If Bot A has earned 15000ESD for the house, the house cut drops
to `0.5/2 = 0.25%` for them. If Bot B has earned 30001ESD for the house, the
house cut drops to `0.5/2**3 = 0.06%` for them. Due to rounding, the house
cut eventually goes to zero.

> Pro tip: You can use both versions (this and Austin William's)
simultaneously to increase the odds that a bot will redeem your coupons.
You'll only pay the tip to the one that succeeds.

## Deployed Contract

`CouponClipper` is deployed to [0x5fb89D51c236C4dfF35bf62b7821B6bF92611630](https://etherscan.io/address/0x5fb89D51c236C4dfF35bf62b7821B6bF92611630)
and the code is verified on Etherscan.

## How does it work?

Users can interact with the contract directly or go to [emptyset.coupons](https://emptyset.coupons/) (currently under construction) to configure
their tip and approve the contract.

This will emit a `CouponApproval` event for which bots can listen. When
coupons become available, bots can call a variety of functions to redeem
the coupons of one or more users. The users' new ESD will magically appear
in their account, and the bot receives (at minimum) a 1.5% cut for their
effort. Users can increase this tip size via the `setOffer` function.

For more information, we recommend checking out the original repository. If
you like this code, Austin is the one to thank.
