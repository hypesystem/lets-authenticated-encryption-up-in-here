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
  2. Since an adversary cannot hope to forge a valid ciphertext, the CCA
     decryption oracle is useless; CPA
     implies CCA!

</section>
<section markdown="1" style="text-align: left;">
## Theorem 4.19

Let $$\Pi_E$$ be a CPA-secure private-key encryption scheme, and let $$\Pi_M$$ be a
strongly secure message authentication code. Then Construction 4.18 is an
authenticated encryption scheme.

</section>
<section markdown="1" style="text-align: left;">

### Strategy:
Show that strong security of $$\Pi_M$$ implies that any "new" ciphertexts
submitted by $$\mathcal{A}$$ will be invalid.

### Definitions:
  *  a ciphertext $$\langle c,t\rangle$$ is $$new$$, if $$\mathcal{A}$$ did not
     receive it from the encryption oracle
  * $$\text{ValidQuery}$$ is the event that $$\mathcal{A}$$ submits a $$new$$,
    valid, $$\langle c,t \rangle$$ to the decryption oracle.

</section>
<section markdown="1">

## Claim 4.20

$$\text{Pr}[\text{ValidQuery}]$$ _is negligible_

</section>
<section markdown="1" style="text-align:left;">

## Proof of 4.20

Intuitively (again): If $$\mathcal{A}$$ can forge a valid ciphertext, it has beaten
$$\text{Mac-sforge}$$

</section>
<section markdown="1" style="text-align:left;">

## Proof of 4.20

Formally: We construct an adversary $$\mathcal{A}_M$$ attacking $$\Pi_M$$
by running a a $$\text{Mac-sforge}$$ adversary $$\mathcal{A}$$.

Let $$q(\cdots)$$ be a polynomial upper-bound on the number of
decryption-oracle queries made by $$\mathcal{A}$$

</section>
<section markdown="1" style="text-align:left;">

  1. Choose uniform $$k_E \in \{0, 1\}^n$$ and $$i \in \{1, . . ., q(n)\}$$.
  2. Run $$\mathcal{A}$$ on input $$1^n$$. When $$\mathcal{A}$$ makes an
     encryption-oracle query for the message $$m$$, answer it as follows:
     1. Compute c ← EnckE(m).
     2. Query $$c$$ to the MAC oracle and receive $$t$$ in
     response. Return $$\langle c,t\rangle$$ to $$\mathcal{A}$$.

</section>
<section markdown="1" style="text-align:left;">

The challenge ciphertext is prepared in the exact same way (with a uniform
bit $$b \in \{0, 1\}$$ chosen to select the message mbthat gets encrypted).

When $$\mathcal{A}$$ makes a decryption-oracle query for the ciphertext
$$\langle c,t \rangle$$ answer it
as follows: If this is the ith decryption-oracle query, output (c, t).j0
Otherwise:
  1. If $$\langle c, t \rangle$$ was a response to a previous encryption-oracle query for a
     message m, return m.
  2. Otherwise, return ⊥.

</section>
