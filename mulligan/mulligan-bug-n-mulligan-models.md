# Mulligan bug

**Definition**: mulligan bug is a bug (or a feature depends how you look at it) which makes it more likely to draw certain cards in **r2** and **r3** if you mulliganed them in **r1**.

# Mulligan bug is back

## TL;DR

Analysis of a data set of 500 R1 mulligans - 1500 mulliganed cards - provided by three independent sources, reveal that the infamous mulligan "bug" is back in full force, even in singleton decks. The data are an astronomically better match with the original mulligan implementation, than with what was thought to be the updated version, indicating that Gwent has reverted to it's roots of heightened odds of drawing your mulligans.

## Method

A 26-card singleton deck with Calveit as leader was used in practice mode. After mulliganing three cards, Calveit was played and the number of mulliganed cards present in the deck's top three spots recorded. The results are then compared to the expected amount of repeats.

## Mulligans 

There are three main ways mulliganing and blacklisting can be implemented in Gwent, let's call them M1, M2 and M3:

---

### M1

<details>
	<summary>**mulligan bias (a high chance that mulliganed cards will be on top) + blacklist bias (a high chance that blacklist cards will be on top)**</summary>

Whenever a card is mulliganed, it is instantly placed back in the deck at a random position. It, and it's duplicates, are blacklisted. Blacklisted cards are skipped and left at the top of deck if they were supposed to be drawn during the mulligan phase. This is the original implementation in Gwent. It has the drawbacks of both mulligan bias and blacklist bias. The former[первый из них] being an increased chance of mulliganed cards landing in the top of the deck, and the latter[последний] being an increased chance of blacklisted duplicates being present in the top.

</details>

### M2

<details>
	<summary>**blacklist bias (a high chance that blacklist cards will be on top) + mulliganed cards get set aside and then after the mul phase set aside re-enters the deck at random positions**</summary>

Whenever a card is mulliganed, it is set aside for the remainder[остаток] of the mulligan phase. Duplicates are blacklisted, and thus skipped and left at the top of the deck if they were supposed to be drawn during mulligan. After the mulligan phase is over, the cards set aside re-enters the deck at random positions. This is the implementation we've been under the impression CDPR changed Gwent into having. It has no mulligan bias, but does have blacklist bias.

</details>

### M3

<details>
	<summary>**ALL cards get set aside and then after the mulligan phase set aside re-enters the deck at random positions**</summary>

Whenever a card is mulliganed, it is set aside for the remainder of the mulligan phase. Blacklisted duplicates get set aside as well (either instantly, or when they were supposed to be drawn - it doesn't matter). After the mulligan phase is over, the cards set aside re-enters the deck at random positions. This implementation has **neither mulligan bias, nor blacklist bias**. We have no reason to believe this is an implementation CDPR wants for Gwent, 

author: *I'm simply including it because many in this community seem to want it. Personally, I favor M2 as the optimal implementation (because I believe blacklisting should have a downside), but that's a different discussion.*

</details>

---

Why not simply shuffle the deck after the mulligan phase? First of all, because this would limit design that interact with cards' position in the deck (e.g. Xarthisius). Secondly, M3 is *mathematically equivalent* to shuffling the deck, so there's no reason to even consider shuffling.

## Details

In conventional decks containing duplicates, both blacklisting bias and mulligan bias has an impact. Singleton decks (e.g. Shupe/arena decks), are only affected by mulligan bias. M1 is the only implementation with mulligan bias. In this study we use singleton decks hoping to prove or disprove the existence of mulligan bias in Gwent. If mulligan bias is proven to exist, this means Gwent definitely does not employ M2 or M3. If the data is a good fit with M1, it makes M1 likely to be the case. Bayesian inference - the comparison of the probability of the data given M1 to M2/3 - gives us an indication of the likelihood of each mulligan implementation.

## Math

The expected/average number of mulliganed cards ending up in the top three spots of a deck can be estimated by running a simulation millions of times, or calculated directly. 

## Results

In the following table we compare the number of mulliganed cards expected to be found in the top three of the deck after the R1 mulligan to the actual number found in the data set:

| Number of repeats | Expected w/M1 ("old") | Expected w/M2 ("new") | Observed results |
| :--- | :--- | :--- | :--- |
|None |	175.7 |	255.2  | 197 |
|One |	238.0 |	209.0 |	217 |
|Two |	80.8 |	34.9 |	73 |
|Three | 6.5 | 0.9 | 13 |

