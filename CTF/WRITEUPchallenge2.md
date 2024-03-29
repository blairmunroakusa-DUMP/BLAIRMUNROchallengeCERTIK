#### CANDIDATE: Blair Munro

#### EMAIL: blairmunroakusa@wp.computer

##### CHALLENGE 2 WRITEUP:

I was going to try exploiting the Lender with fancy flashloans or something like that, but I noticed a simpler approach based off a flaw in the liquidation function. The liquidation function pays out the liquidated account's deposit amount in WETH, but it never zeros out the deposited balance, allowing anybody to just repeatedly borrow and liquidate until the poor lender is drained dry.

The fix is simple enough: either remove the liquidate function (and force the operation on the client side for safety-over-complexity), or build in the operations needed to ensure the deposited value for that account is always zeroed out after a liquidation.

Other than that, I approached this from a thief's perspective, not a security analyst. My only goal was to steal the money, so I focused on the simplest possible way to do so. For all I know there are loads of other securify flaws littered throughout those contracts, but my mission is complete.

I am assuming the Lender meant to keep 1/3 of the collateral, otherwise the liquidity function is missing a factor of 3/2 when determining the repay value.
