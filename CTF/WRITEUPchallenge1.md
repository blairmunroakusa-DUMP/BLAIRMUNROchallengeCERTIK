#### CANDIDATE: Blair Munro

#### EMAIL: blairmunroakusa@wp.computer

##### CHALLENGE 1 WRITEUP:

(?) denotes a statement I am not sure of

The first reason this wallet was vulnerable was that the constructed wallet address was made as a public state variable in the setup account. This made it possible to determine the location of the owner's wallet using a getter. Once found, we could then easily check to verify that indeed, the wallet has 10 ETH stored inside it.

The ultimate reason this wallet was vulnerable was due to a combination of the public setOwner function, and the onlyOwner modifier that checks to see if the sender of a withdraw transaction is the same as the owner variable in the wallet. The public setOwner function makes it possible to first set the wallet owner variable to the from address of the attacker's transaction. After doing so, the attacker can then circumvent the onlyOwner modifier check and withdraw funds to their account address specified in the transaction.

It seems like the first point of improvement would be the public wallet variable. If that variable were private, it would have been much more challenging to find the mark in the first place. In theory however, this could still be done by correlating activity on the specific block that the setup contract was deployed on. (?) 

The second point of improvement would be the setOwner function. This could either be made private (?), or simply taken out. I cannot think of why the setOwner function would be necessary, if not perhaps to give the wallet to somebody else. If the setOwner function does need to be public, then something needs to be done about the onlyOwner modifier check on the withdrawl function. I am not sure how the onlyOwner check could get around the sender having the owner address. Perhaps requiring a signed transaction would do.
