![Seltkirk of Gulet](/images/seltkirk.png)

To get max
value out of Seltkirk, you want to kill your target in EXACTLY two hits while
also using up all of your armor. If you kill it in one or don't use up all your
armor, then you're missing potential value. If you can't kill your target by the
second hit, you will be taking unnecessary damage (!) and your subsequent
attacks get weaker. The max potential value with Seltkirk is calculated by the
following formula: **2P + A** where **P** - power, **A** - armor

Max value
target: **1.5P + 0.5A**.

*Explanation*: we need to kill an enemy in two turns.
Let **Y** be the power of your target.

After first hit enemy power will be:
**(Y - P)**.

Enemy does **(Y - P - A)** damage to Seltkirk, where **A** - armor
of Seltkirk.

Seltkirk's second hit does **(P- (Y - P - A))** which needs to
kill enemy, who is sitting at **(Y-P)** power. So, if you set those two
expressions *equal* to each other, that's when Seltkirk's 2nd hit is just enough
to kill the target, so you will get the biggest target that can still be killed
in two hits.

So P - (Y - P - A) = Y- P

  2*P - Y + A = Y - P

  3P + A = 2Y
Y = 1.5P + 0.5A
 
A max value target is one that has a power of at least **P +
A**, and at most **1.5P + 0.5A**. This is assuming your **target has no armor**!
So for a 8 PWR Seltkirk, you get max value for hitting a target between 11 and
13 PWR. For a 10 PWR Seltkirk, it's a target between 13 and 16 PWR.

If your
target has power lower than P + A, your value is decreased by 1 for each power
lower. If your target has power higher than 1.5P + 0.5A, your value falls off
pretty quickly, and rapidly reaches a lower bound of P, which occurs when your
target is at least 2*P + A (meaning it kills Seltkirk on its first retaliation).
**TL;DR**: Seltkirk's value increases by 2 for each point he's buffed. His max
potential value is **2*P + A**, which is achieved by choosing a target that he
kills in exactly two hits and destroys all of Seltkirk's armor on their
retaliation hit.
