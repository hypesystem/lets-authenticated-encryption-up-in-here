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

We use the proving strategy of analyzing the scheme using truly random
functions, and then proving that the security loss incurred by using
pseudo-random functions insead is negligible.

</section>
<section markdown="1" style="text-align:left;">

Let $$\widetilde{\Pi}$$ and $$\Pi$$ denote the scheme from construction 4.5,
except that $$\widetilde\Pi$$ uses a truly random function $$f$$ instead of
$$\text{F}_k$$

It follows that

$$\text{Pr}[\text{Mac-forge}_{\mathcal{A},\widetilde\Pi}(n) = 1] \le 2^{-n} \quad \text{(4.1)}$$

Because $$\widetilde\Pi$$ directly applies $$f$$, and because for any message
$$m \not\in \mathcal{Q}$$, the value $$t = f(m)$$ is uniformly distributed in
$${0, 1}^n$$ from the point of view of the adversary $$\mathcal{A}$$.

</section>
<section markdown="1" style="text-align: left;">

From

$$\text{Pr}[\text{Mac-forge}_{\mathcal{A},\widetilde\Pi}(n) = 1] \le 2^{-n}
\quad \text{(4.1)}$$

It follows that if 

> $$|\text{Pr}[\text{Mac-forge}_{\mathcal{A},\Pi}(n) = 1]$$
> $$-$$
> $$\text{Pr}[\text{Mac-forge}_{\mathcal{A},\widetilde{\Pi}}(n) = 1]| \le negl(n)$$ (4.2)

then

$$\text{Pr}[\text{Mac-forge}_{\mathcal{A},\Pi}(n) = 1] \le 2^{-n} + negl(n)$$

</section>
<section markdown="1" style="text-align: left;">

## Proof by Distinguisher
  1. Run $$\mathcal{A}(1^n)$$. Whenever $$\mathcal{A}$$ queries its MAC oracle
     on a message m (i.e., whenever $$\mathcal{A}$$ requests a tag on a message $$m$$), answer
     this query in the following way: Query $$\mathcal{O}$$ with m and obtain response t;
     return $$t$$ to $$\mathcal{A}$$.
  2. When $$\mathcal{A}$$ outputs $$(m, t)$$ at the end of its execution, do:
     1.  Query $$\mathcal{O}$$ with $$m$$ and obtain response $$\tilde t$$.
     2. If (1) $$\tilde t = t$$ and (2) $$\mathcal{A}$$ never queried its MAC oracle on $$m$$, then
     output 1; otherwise, output 0.
</section>
<section markdown="1" style="text-align: left;">

## Proof by Distinguisher

Since the view of $$\mathcal{A}$$ inside $$D$$ is  distributed identically to
that of $$\mathcal{A}$$ in $$\text{Mac-forge}_{\mathcal{A},\Pi}(n)$$, and since
$$D = 1$$ exactly when $$\text{Mac-forge}_{\mathcal{A},\Pi}(n) = 1$$:

$$\text{Pr}[D^{F_k(\cdot)} = 1] = \text{Pr}[\text{Mac-forge}_{\mathcal{A},\Pi}(n) = 1]$$

and

$$\text{Pr}[D^{f_k(\cdot)} = 1] = \text{Pr}[\text{Mac-forge}_{\mathcal{A},\widetilde\Pi}(n) = 1]$$

</section>
<section markdown="1" style="text-align: left;">

$$\text{Pr}[D^{F_k(\cdot)} = 1] = \text{Pr}[\text{Mac-forge}_{\mathcal{A},\Pi}(n) = 1]$$

and

$$\text{Pr}[D^{f_k(\cdot)} = 1] = \text{Pr}[\text{Mac-forge}_{\mathcal{A},\widetilde\Pi}(n) = 1]$$

Gives

$$\text{Pr}[D^{F_k(\cdot)} = 1] - \text{Pr}[D^{f_k(\cdot)} = 1] \le negl(n)$$

Since $$D$$ runs in polynomial time.

Hence equaion (4.2) is proven!

</section>
