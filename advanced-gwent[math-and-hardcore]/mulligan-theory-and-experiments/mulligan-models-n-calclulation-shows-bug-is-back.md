# Mulligan bug

**Definition**: mulligan bug is a bug (or a feature depends how you look at it) which makes it more likely to draw certain cards in **r2** and **r3** if you mulliganed them in **r1**.

# Mulligan bug is back

## TL;DR

Analysis of a data set of 500 R1 mulligans - 1500 mulliganed cards - provided by three independent sources, reveal that the infamous mulligan "bug" is back in full force, even in singleton decks. The data are an astronomically better match with the original mulligan implementation[M1], than with what was thought to be the updated version[M2], indicating that Gwent has reverted to it's roots of heightened odds of drawing your mulligans.

## Method

A 26-card singleton deck with Calveit as leader was used in practice mode. After mulliganing three cards, Calveit was played and the number of mulliganed cards present in the deck's top three spots recorded. The results are then compared to the expected amount of repeats.

## Mulligans (mulligan models)

There are three main ways mulliganing and blacklisting can be implemented in Gwent, let's call them M1, M2 and M3:

---

### M1

<details>
	<summary><b>mulligan bias (a high chance that mulliganed cards will be on top) + blacklist bias (a high chance that blacklist cards will be on top) </b></summary>

Whenever a card is mulliganed, it is **instantly** placed back in the deck at a random position. It, and it's duplicates, are blacklisted. Blacklisted cards are skipped and left at the top of deck if they were supposed to be drawn during the mulligan phase. This is the original implementation in Gwent. It has the drawbacks of both mulligan bias and blacklist bias. The former[первый из них] being an increased chance of mulliganed cards landing in the top of the deck, and the latter[последний] being an increased chance of blacklisted duplicates being present in the top.

</details>

### M2

<details>
	<summary><b>blacklist bias (a high chance that blacklist cards will be on top) + mulliganed cards get set aside and then after the mul phase set aside re-enters the deck at random positions</b></summary>

Whenever a card is mulliganed, it is set aside for the remainder[остаток] of the mulligan phase. Duplicates are blacklisted, and thus skipped and left at the top of the deck if they were supposed to be drawn during mulligan. After the mulligan phase is over, the cards set aside re-enters the deck at random positions. This is the implementation we've been under the impression CDPR changed Gwent into having. It has no mulligan bias, but does have blacklist bias.

</details>

### M3

<details>
	<summary><b>ALL cards get set aside and then after the mulligan phase set aside re-enters the deck at random positions</b></summary>

Whenever a card is mulliganed, it is set aside for the remainder of the mulligan phase. Blacklisted duplicates get set aside as well (either instantly, or when they were supposed to be drawn - it doesn't matter). After the mulligan phase is over, the cards set aside re-enters the deck at random positions. This implementation has **neither mulligan bias, nor blacklist bias**. We have no reason to believe this is an implementation CDPR wants for Gwent, 

author: *I'm simply including it because many in this community seem to want it. Personally, I favor M2 as the optimal implementation (because I believe blacklisting should have a downside), but that's a different discussion.*

</details>

---

Why not simply shuffle the deck after the mulligan phase? First of all, because this would limit design that interact with cards' position in the deck (e.g. Xarthisius). Secondly, M3 is *mathematically equivalent* to shuffling the deck, so there's no reason to even consider shuffling.

## Details

In conventional decks containing duplicates, both blacklisting bias and mulligan bias has an impact. Singleton decks (e.g. Shupe/arena decks), are only affected by mulligan bias. M1 is the only implementation with mulligan bias. In this study we use singleton decks hoping to prove or disprove the existence of mulligan bias in Gwent. If mulligan bias is proven to exist, this means Gwent definitely does not employ M2 or M3. If the data is a good fit with M1, it makes M1 likely to be the case. Bayesian inference - the comparison of the probability of the data given M1 to M2/3 - gives us an indication of the likelihood of each mulligan implementation.

## Math

The expected/average number of mulliganed cards ending up in the top three spots of a deck can be estimated by running a simulation millions of times, or calculated directly. There is a [thread on Reddit](https://www.reddit.com/r/gwent/comments/83eq8s/testing_of_mulligan_in_singleton_deck/) where other users find matching values using both approaches. The same thread also contains the sources of the data points, as well as some more in-depth math omitted here.

## Results

In the following table we compare the number of mulliganed cards expected to be found in the top three of the deck after the R1 mulligan to the actual number found in the data set:

| Number of repeats | Expected w/M1 ("old") | Expected w/M2 ("new") | Observed results |
| :--- | :--- | :--- | :--- |
|None |	175.7 |	255.2  | 197 |
|One |	238.0 |	209.0 |	217 |
|Two |	80.8 |	34.9 |	73 |
|Three | 6.5 | 0.9 | 13 |


<details>
	<summary>A chance that M2 gives 13 triples (three mulligan endings in the top of the deck) or more is **1.55 nano-percent**(%). Meanwhile, M1 gives **1.54%** which is still fairly unlikely.</summary>

At first glance it is apparent that the data is an incredibly bad match with M2, while fairly compatible with M1. Especially the number of triple repeats (all three mulligans ending up in the top of the deck) is an extreme outlier given M2. This is supposed to occur less than once in 500 mulligans, yet we observe a whooping 13. The odds of observing 13 or more triples given M2 is a ludicrous **1.55** nano-percent[link](https://www.wolframalpha.com/input/?i=sum+from+13+to+500+of+((500+choose+x)*0.0018%5Ex*0.9982%5E(500-x))). Meanwhile, the expected number of triples given M1 is 6.52 - half of the observed amount. 13 or more is still fairly unlikely - 1.54%[link](https://www.wolframalpha.com/input/?i=sum+from+13+to+500+of+((500+choose+x)*0.013%5Ex*0.987%5E(500-x))) - but not unreasonable and could be explained by bad luck.

</details>

Moving on to comparative hypothesis testing, we calculate the odds of these exact 500 data points given M1 and M2, and compare them to find an indication of the likelihood of the two:

P(Results|M1) = 500! / (197!217!73!13!) * 0.3494^197 * 0.4760^217 * 0.1615^73 * 0.0130^13 = 1.14 * 10^-6 
[link](https://www.wolframalpha.com/input/?i=500!%2F(197!217!73!13!)+*+0.3494%5E(197)+*+0.4760%5E(217)+*+0.1615%5E(73)+*+0.0130%5E(13))
P(Results|M2) = 500! / (197!217!73!13!) * 0.5107^197 * 0.4179^217 * 0.0696^73 * 0.0018^13 = 2.60 * 10^-24 
[link](https://www.wolframalpha.com/input/?i=500!%2F(197!217!73!13!)+*+0.5107%5E(197)+*+0.4179%5E(217)+*+0.0696%5E(73)+*+0.0018%5E(13))
P(Results|M1)/P(Results|M2) = 4.39 * 10^17 = **439 quadrillion**

## Conclusions: Based on these findings we can conclude that:

The observations are **439 quadrillion** times more likely to occur in a universe where **Gwent is employing M1** - the original mulligan implementation - than in a universe with M2.
It is incredibly unlikely for mulligan bias not to exist in Gwent at present time.
Gwent having reverted to it's original mulligan implementation seems to be the likely explanation, but more data points are required to say anything conclusive. It is entirely possible that none of the implementation methods mentioned here accurately describe what is going on under the hood.
Comments: The strength of a statistical study lies in it's sample size and diversity (number of independent sources). Our findings are undoubtedly statistically significant, but some might argue the data set still doesn't have enough data points or isn't diverse enough to truly prove anything. At the very least, however, the findings can be considered strong enough to warrant a response from CDPR. If anyone would like to help strengthen the data by providing their own observations that'd be great, but it is a massive chore - the gathering pace is close to 1 mulligan/minute.

<details>
	<summary>author's update:</summary>
Update: So I've been thinking, and there could be an alternative explanation to all this. There exists a variant of M1, let's call it M1b, that still has both mulligan bias and blacklisting bias, but with slightly lower impact. The difference is: M1 = A) Mulligan a card into deck, B) Draw a replacement. M1b = A) Choose a mulligan, B) Draw a replacement, C) Insert mulligan into deck.

> What if Gwent never moved to M2 in the first place? What if the only change made was from M1 to M1b and the community mistakenly thought mulligan bias was removed and Gwent had been updated to M2? It would mean that we've had the story all wrong in the first place. That no "revert" has been discovered; instead we've just realized that Gwent's had mulligan bias all along.

> The data is 171 times more likely to be observed given M1 than M1B, but this might not be enough to conclude anything with certainty. The data goes a long way to disprove M2, heavily indicates the existence of mulligan bias, but does not seem to accurately prove exactly which implementation is used. Proving something is wrong is a lot easier than proving something is correct!

</details>	