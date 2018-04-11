# Mulligan bug

**Definition**: mulligan bug is a bug (or a feature depends how you look at it) which makes it more likely to draw certain cards in **r2** and **r3** if you mulliganed them in **r1**.

Devs told us that there is no bug (in Gwent xD). So, "If everything is working properly and there are no bugs atm, what are the chances of redrawing these cards that I tossed away?". This is the question that people should be asking themselves. If they do the math and the times they redraw the cards they tossed away are found to reasonably or vastly exceed the expected statistic, then we can call it out and try to get attention of the devs.

# Redrawing cards tossed away in round 1 and 2

So let's see, what are the actual expected numbers here?

**Scenario**:

- it's arena, I have a 26 card deck, with 26 distinct *singleton cards*
- I mulligan 3 cards I don't want in the pregame mulligan
- I don't thin my deck at all (drypass meta lul)
- at the start of R2 I draw 2 cards like usual
- at the start of R2 I do or maybe don't mulligan a card

**R2**

On the first draw R2 the chances of drawing one of the "bad draws" is 3/16. So there is a **13/16** chance that I do **NOT** draw any of the "bad" cards.

First *draw*: 13/16.

On the second draw, if I have not drawn a "bad card" yet, the chance to draw one of the bad cards is now 3/15. On this draw I have a **12/15** chance of **NOT** drawing a bad card.

Second *draw*: 12/15.

Then I can choose to mulligan a card or not. If I choose to mulligan, and I have not drawn one of the three cards I tossed away in R1 yet, I will have a 3/14 chance to draw one of them here. Additionally, on this draw I have a **11/14** chance of **NOT** drawing one of the three bad cards.

*Draw* after mulligan (if we tossed a card): 11/14.

All round 2 without mulligan: 13/16 * 12/15 = 65%. 

The chances of not redrawing at least one of the "dead cards" is 65%. Which means that is is a 35% chance that we DO redraw at least one of them.

> 35% chance to redraw at least one of the three tossed cards come R2.

All round 2 with mulligan: 13/16 * 12/15 * 11/14 = 51%.

If we use our mulligan R2 this chance gets higher. The numbers come out to be (13/16)*(12/15)*(11/14) which is 51%. Or, 49% chance that if we use our mulligan that we now have at least one of the three cards tossed away R1 in our hand.

> 49% chance to redraw at least one of the three tossed cards come R2 if we use our R2 mulligan.

**R3**

*Draw* (if we did not mulligan R2): 11/14.

*Draw* (if we tossed a card in R2): 10/14. We don't want to see 4 cards: 3 cards mulliganed in the R1 & 1 card mulliganed in the R2.

*Draw* after mulligan: 9/13.

Both R2 & R3 without mulligan: 13/16 * 12/15 * 11/14 = 51%.

(R2 with mulligan & R3 without it) & (R2 without mulligan & R3 with it): 13/16 * 12/15 * 11/14 * 10/14 = 36.47%, which I'll rond to 36.5% -- so 36.5% you have not seen a tossed card show back up in your hand yet, or 63.5% that AT LEAST ONE of the tossed cards has made its way back into your hand by now.

> 63.5% to redraw at least one of the three tossed cards come R3 (after mulligan R2, or we din't mulligan R2 and we'll do this in R3)

R2 & R3 with mulliganed cards: 13/16 * 12/15 * 11/14 * 10/14 * 9/13 = 25.25% -- that's 74.75% that at least one tossed card will have shown up by now.

> 74.75% chance to redraw at least one of the three tossed cards come R3 (after mulligan R2) if we use our R3 mulligan.

# Sequencing theory

## mulligan algorithm:

1. Choose a card in your hand.
2. This card is blacklisted, meaning a card with the same name cannot be drawn for the remainder of this particular mulligan phase
3. The chosen card is placed in a random position in your deck. As far as we know, any position, including the top or bottom of your deck, is equally likely[в равной степени вероятна]. The order of the other cards remains the same.
4. Draw the top non-blacklisted card of your deck
5. Repeat the process until all of your available mulligans are completed or you decide to end the mulligan.

Steps 3 and 4 of the mulligan algorithm dictate that a blacklisted card is more likely to end up close to the top of your deck than a non-blacklisted one. This occurs because blacklisted cards are not taken out of your deck during the mulligan process. Instead, they remain in the deck, but are unable to be drawn. This causes them to rise up as cards are drawn from above them, or remain on top (without being drawn) if they started off there, making them more likely to be higher up in your deck. But, it's easier to understand this by looking at a simple example:

## Example: Horsing Around

Suppose you have 9 cards left in your deck, and mulligan a single Roach. The Roach has 10 equally likely positions in your deck where it could end up.

- If Roach lands on top of your deck, you will draw the second card in your deck to replace it (as Roach is blacklisted)
- If Roach lands second from the top, then you will draw the top card to replace it, and Roach will once again be on top of your deck
- If Roach lands anywhere else, it can not end up at the top of your deck after just one mulligan.

> 1/10 + 1/10 = 1/5 where (Roach on top) + (Roach on second pos from top) = union because Roach will be on top even after drawing the first card

Thus, there is a 20% chance that Roach will be on top of your deck (compared with 10% chance for any of the remaining 8 cards to be on top).

## Example: A Base Case

Suppose you are playing a deck of 25 unique cards, and you mulligan 3 cards (say Geralt, Roach and Triss Merigold, in that order) at the start of the game. *What is the probability that each of those cards will be on top of your deck after the mulligan*?

- Geralt: 20.6%
- Roach: 15.4%
- Triss Merigold: 10.7%
- Total: 46.7%

**Explanation**

> 20.6%.
Geralt is the top card if he is mulliganed into position 1,2,3 or 4 in your deck (before the replacement card is drawn), AND after that **neither Roach nor Triss are placed above Geralt in the deck**. If this occurs, all cards above Geralt will be drawn during the mulligan process and he will end up being the top card.
The probability that Geralt is mulliganed into position 1/2/3/4 is **1/16**=0.0625 for every position.
For each of the above positions, calculate the probability that neither Roach nor Triss are ever mulliganed above geralt. This is 0.88/0.88/0.82/0.71. Or rather:
1-1/16-1*15/16^2=0.88
1-1/16-1*15/16^2=0.88
1-2/16-1*14/16^2=0.82
1-3/16-2*13/16^2=0.71
Multiply the first probability by the second, and sum over all possible positions:
(1/16 * 0.88) + (1/16 * 0.88) + (1/16 * 0.82) + (1/16 + 0.71) = 20.6

>15.4%
Roach is the top card of your deck if he is mulliganed into position 1,2 or 3 (before replacement) AND Geralt was not already in a position above it AND Triss is not placed in a position above it.
(1/16 * 1 * 15/16) + (1/16 * 14/16 * 15/16) + (1/16 * 13/16 * 14/16) = 0.154

>10.7%
Triss is the top card of your deck if she is mulliganed into position 1 or 2 (before replacement) AND Neither Geralt nor Roach were already in a position above her
(1/16 * 1) + (1/16 * [1-3/16-13/16 * 2/16]) = 0.107

To compare, the probability of drawing Geralt, Roach or Triss Merigold from the top of a shuffled deck is a combined 20%. Furthermore, suppose, like in the ‘Horsing Around’ example above, only Geralt was mulliganed. Then the probability of him being at the top of your deck would be 2/16=12.5%. So mulliganing more cards after him actually increased the chance of Geralt rising to the top.

Importantly, this is a lower bound. If we relax the assumption that mulliganed cards are unique, then the probability of drawing a copy of a mulliganed card would be even higher. Thus, if you are playing a 25 card deck and mulligan 3 cards at the start of the game the probability of one of them being on top of is always at least 46.7%

