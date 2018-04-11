# In depth: Sequencing theory and blacklist bias

## Mulligan algorithm

1. Choose a card in your hand.
2. This card is blacklisted, meaning a card with the same name cannot be drawn for the remainder of this particular mulligan phase
3. The chosen card is placed in a random position in your deck. As far as we know, any position, including the top or bottom of your deck, is equally likely[в равной степени вероятна]. The order of the other cards remains the same.
4. Draw the top non-blacklisted card of your deck
5. Repeat the process until all of your available mulligans are completed or you decide to end the mulligan.

Steps 3 and 4 of the mulligan algorithm dictate that a blacklisted card is more likely to end up close to the top of your deck than a non-blacklisted one. This occurs because blacklisted cards are not taken out of your deck during the mulligan process. Instead, they remain in the deck, but are unable to be drawn. This causes them to rise up as cards are drawn from above them, or remain on top (without being drawn) if they started off there, making them more likely to be higher up in your deck. But, it's easier to understand this by looking at a simple example

## Example Horsing Around

Suppose you have 9 cards left in your deck, and mulligan a single Roach. The Roach has 10 equally likely positions in your deck where it could end up.

- If Roach lands on top of your deck, you will draw the second card in your deck to replace it (as Roach is blacklisted)
- If Roach lands second from the top, then you will draw the top card to replace it, and Roach will once again be on top of your deck
- If Roach lands anywhere else, it can not end up at the top of your deck after just one mulligan.

 110 + 110 = 15 where (Roach on before 1 card) + (Roach between 1 and 2 card) = union because Roach will be on top even after drawing the first card

Thus, there is a 20% chance that Roach will be on top of your deck (compared with 10% chance for any of the remaining 8 cards to be on top).

## Example A Base Case

Suppose you are playing a deck of 25 unique cards, and you mulligan 3 cards (say Geralt, Roach and Triss Merigold, in that order) at the start of the game. What is the probability that each of those cards will be on top of your deck after the mulligan

- Geralt 20.6%
- Roach 15.4%
- Triss Merigold 10.7%
- Total 46.7%

---

**Explanation** 


**20.6%**

Geralt is the top card if he is mulliganed into position 1,2,3 or 4 in your deck (before the replacement card is drawn), AND after that neither Roach nor Triss are placed above Geralt in the deck. If this occurs, all cards above Geralt will be drawn during the mulligan process and he will end up being the top card.

The probability that Geralt is mulliganed into position 1234 is 116=0.0625 for every position.

For each of the above positions, calculate the probability that neither Roach nor Triss are ever mulliganed above geralt. This is 0.880.880.820.71. Or rather

### Geralt ends up on top of the deck 

We assume that Geralt is mulliganed before card 1.

1 - 1/16 - 1 * 15/16^2 = 0.88

Same for Geralt which was mulliganed between cards 1 and 2. 

1 - 1/16 - 1 * 15/16^2 = 0.88

### Geralt ends up on 
1 - 2/16 - 1 * 14/16^2 =0.82

1 - 3/16 - 2 * 13/16^2 = 0.71

Multiply the first probability by the second, and sum over all possible positions

 (1/16 * 0.88) + (1/16 * 0.88) + (1/16 * 0.82) + (1/16 + 0.71) = 20.6

**15.4%**

Roach is the top card of your deck if he is mulliganed into position 1,2 or 3 (before replacement) AND Geralt was not already in a position above it AND Triss is not placed in a position above it.

(1/16 * 1 * 15/16) + (1/16 * 14/16 * 15/16) + (1/16 * 13/16 * 14/16) = 0.154

**10.7%**

Triss is the top card of your deck if she is mulliganed into position 1 or 2 (before replacement) AND Neither Geralt nor Roach were already in a position above her

 (1/16 * 1) + (1/16 * [1 - 3/16 - 13/16 * 2/16]) = 0.107

---

To compare, the probability of drawing Geralt, Roach or Triss Merigold from the top of a shuffled deck is a combined 20%. Furthermore, suppose, like in the ‘Horsing Around’ example above, only Geralt was mulliganed. Then the probability of him being at the top of your deck would be 216=12.5%. So mulliganing more cards after him actually increased the chance of Geralt rising to the top.

Importantly, this is a lower bound. If we relax the assumption that mulliganed cards are unique, then the probability of drawing a copy of a mulliganed card would be even higher. Thus, if you are playing a 25 card deck and mulligan 3 cards at the start of the game the probability of one of them being on top of is always at least 46.7%

## To Summarise

Blacklist Bias Mulliganed cards are more likely to end up higher in your deck. This also applies to copies of mulliganed cards that started off in your deck (e.g. foglets).

Generally, the more mulligans are performed in a given sitting, the more likely it is that one of the blacklisted cards ends up on top of your deck.