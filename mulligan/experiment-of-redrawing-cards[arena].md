# Mulligan bug

**Definition**: mulligan bug is a bug (or a feature depends how you look at it) which makes it more likely to draw certain cards in **r2** and **r3** if you mulliganed them in **r1**.

Devs told us that there is no bug (in Gwent xD). So, "If everything is working properly and there are no bugs atm, what are the chances of redrawing these cards that I tossed away?". This is the question that people should be asking themselves. If they do the math and the times they redraw the cards they tossed away are found to reasonably or vastly exceed the expected statistic, then we can call it out and try to get attention of the devs.

# Experiment of redrawing cards

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