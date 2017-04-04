---
---

<section markdown="1" style="text-align: left;">

## Theorem 4.6

If $$\text{F}$$ is a pseudorandom function, then Construction 4.5
is a secure fixed-length MAC for messages of length $$n$$.

or:

$$\text{Pr}[\text{Mac-forge}_{\mathcal{A},\Pi}(n) = 1] \le 2^{-n} + negl(n)$$

</section>
<section markdown="1" style="text-align: left;">

## Proof

We use the prooving strategy of analyzing the scheme using truly random
functions, and then proving that the security loss incurred by using
pseudo-random functions insead is negligible.

</section>
<section markdown="1" style="text-align: left;">

Let $$\widetilde{\Pi}$$ and $$\Pi$$ denote the scheme from construction 4.5,
except that $$\widetilde\Pi$$ uses a truly random function $$f$$ instead of
$$\text{F}_k$$

$$\text{Pr}[\text{Mac-forge}_{\mathcal{A},\widetilde\Pi}(n) = 1] \le 2^{-n}$$

</section>
<section markdown="1" style="text-align: left;">

## Proof

$$|\text{Pr}[\text{Mac-forge}_{\mathcal{A},\Pi}(n) = 1]$$

$$-$$

$$\text{Pr}[\text{Mac-forge}_{\mathcal{A},\widetilde{\Pi}}(n) = 1]| \le 2^{-n}$$

</section>
