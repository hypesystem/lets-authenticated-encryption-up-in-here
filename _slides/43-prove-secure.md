---
---

<section markdown="1" style="text-align: left;">
## Construction 4.18

Let $$\Pi_E = (\text{Enc}, \text{Dec})$$ be a private-key encryption scheme and let $$\Pi_M=
(\text{Mac}, \text{Vrfy})$$ be a message authentication code, where in each case key
generation is done by simply choosing a uniform $$n$$-bit key. Define a private-key
encryption scheme $$(\text{Gen}', \text{Enc}', \text{Dec}')$$ as follows:

</section>
<section markdown="1" style="text-align: left;">
## Construction 4.18

  * $$\text{Gen}'$$: on input $$1^n$$, choose independent, uniform $$k_E, k_M
  \in {0, 1}^n$$ and output the key $$(k_E, k_M)$$.

  * $$\text{Enc}'$$: on input a key $$(k_E, k_M)$$ and a plaintext message
    $$m$$, compute $$c \leftarrow \text{Enc}_{k_E}(m)$$ and $$t \leftarrow \text{Mac}_{k_M}(c)$$.
    Output the ciphertext $$\langle c, t\rangle$$.

  * $$\text{Dec}'$$: on input a key $$(k_E, k_M)$$ and a ciphertext $$\langle c,
    t\rangle$$, first
    check whether $$\text{Vrfy}_{k_M}(c, t) = 1$$. If yes, then output $$\text{Dec}_{k_E}(c)$$; if
    no, then output $$\bot$$.
</section>

<section markdown="1">
## Intution:

  1. Since $$\text{Mac}$$'ing is the final step, unforgeability is implied!
  2. Since an adversary cannot hope to forge a valid ciphertext, CPA
     implies CCA!
</section>

<section markdown="1" style="text-align: left;">
## Theorem 4.19

Let $$\Pi_E$$ be a CPA-secure private-key encryption scheme, and let $$\Pi_M$$ be a
strongly secure message authentication code. Then Construction 4.18 is an
authenticated encryption scheme.

</section>
