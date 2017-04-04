---
---
<section markdown="1" style="text-align: left;">
## Definitions
$$\text{Enc-forge}_{\mathcal{A},\Pi}(n)$$:

  1. Run $$\text{Gen(1^n)}$$ to obtain a key $$k$$

  2. The adversary $$\mathcal{A}$$ is given input $$1^n$$ and access to an
     encryption oracle $$\text{Enc}_k(\cdot)$$. The adversary outputs a ciphertext $$c$$.

  3. Let $$m := \text{Deck}(c)$$, and let $$\mathcal{Q}$$ denote the set of all queries that
    $$\mathcal{A}$$ asked its encryption oracle. The output of the experiment
    is 1 if and only if _(1)_ $$m \ne \bot$$ and _(2)_ $$m \not\in \mathcal{Q}$$.


</section>

<section markdown="1" style="text-align: left;">
## Definition 4.16
A private-key encryption scheme $$\Pi$$ is unforgeable if for all probabilistic
polynomial-time adversaries $$\mathcal{A}$$, there is a negligible function
$$negl$$ such that:

$$Pr[\text{Enc-forge}_{\mathcal{A},\Pi}(n)=1] \le negl(n)$$

</section>
<section markdown="1" style="text-align: left;">
## Definition 4.17
A private-key encryption scheme is an authenticated encryption scheme if it is
___CCA-secure___ and ___unforgeable___.

This is the strongest security definition yet!
</section>
