# Design Proposal

## Problem statement
Determine out the lowest price of an open offer of an NFT collection (in real-time?).

#### Challenges
* Many marketplaces with different proprietary smart contracts.
* HUGE NFT collections (~10k), unfeasible to process in a single ix.
* Oracle has to parse on-chain data to be trusted, cannot be aggregated offline and just stored on chain.

#### Design

The idea behind the oracle is to keep the floor price in lamports for a given collection.
The program works by either:
* Lowering the floor: Simply set the floor to the asking price of an active offer.
* Raising the floor: First prove that the offer for the last floor doesn't exist anymore (sold or unlisted), and then set a new floor.

#### Challenges
* Incentives - This contract should be called by anyone? Why should I do it? How can we stimulate long-term participation? Users should receive some sort of reward for participating.
* Floor Jitter - The floor always resembles the "lowest we've seen so far". Meaning that in the worst case, the floor could go down by one offer each time it is updated. We need to incentivize users to always send the cheapest offer they can find. Maybe the reward for setting the floor is given based on how long the floor remains set, this way users are incentivized to always give the lowest floor as it has the highest expected lifetime (the highest reward). The reward for setting the floor should be low enough for users to not be incentivized to list items just to set the floor, and high enough where tx fees are more expensive.


