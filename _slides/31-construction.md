---
---
<section markdown="1" style="text-align: left;">
## Construction 4.11

Let $$F$$ be a pseudorandom function, and fix a length function $$l > 0$$.
The basic CBC-MAC construction is as follows:
</section>
<section markdown="1">
- $$\text{Mac}$$: on input of key $$k \in \{0,1\}^n$$ and a message $$m$$ of length $$l(n)*n$$, do the following (we set $$l = l(n)$$ in what follows):
  1. Parse $$m$$ as $$m = m_1, ..., m_l$$ where each $$m_i$$ is of length $$n$$.
  2. Set $$t_1 := F_k(m_1)$$. Then for $$1 < i \leq l$$:  
     $$\quad$$ Set $$t_i := F_k(m_i \oplus t_{i-1})$$

  Output $$t_l$$ as the tag.
</section>
<section markdown="1">
- $$\text{Vrfy}$$: on input a key $$k \in \{0,1\}^n$$, a message $$m$$, and a tag $$d$$, do:
  If $$m$$ is not length $$l(n)*n$$ then output $$0$$.
  Otherwise, output $$1$$ if and only if $$t =^? \text{Mac}_k(m)$$

(Length check + canonical verification.)
</section>
<section>
    <figure>
        <img src="img/cbc-mac.png">
        <figcaption><small>(Illustration: Katz & Lindell 2015)</small></figcaption>
    </figure>
</section>
<section markdown="1">

### Is it ordering attack safe?

<div class="fragment" markdown="1">
$$\text{Mac}_k( \langle m_1, m_2 \rangle ) \neq \text{Mac}_k( \langle m_2, m_1 \rangle )$$

$$\Leftrightarrow$$

$$F_k(m_2 \oplus F_k(m_1)) \neq F_k(m_1 \oplus F_k(m_2))$$
</div>

</section>
<section markdown="1">

### Is it truncation attack safe?

<div class="fragment" markdown="1">
$$\text{Mac}_k( \langle m_1, m_2 \rangle ) \neq \text{Mac}_k( \langle m_1 \rangle )$$

$$\Leftrightarrow$$

$$F_k(m_2 \oplus F_k(m_1)) \neq F_k(m_1)$$
</div>

</section>
<section markdown="1">

### Is it mix 'n' match attack safe?

<div class="fragment" markdown="1">
$$\text{Mac}_k( \langle m_{1,1}, m_{1,2} \rangle ) \neq \text{Mac}_k( \langle m_{2,1}, m_{2,2} \rangle )$$  
$$\neq \text{Mac}_k( \langle m_{1,1}, m_{2,2} \rangle )$$

$$\Leftrightarrow$$

$$F_k(m_{1,2} \oplus F_k(m_{1,1})) \neq F_k(m_{2,2} \oplus F_k(m_{2,1}))$$      
$$\neq F_k(m_{2,2} \oplus F_k(m_{1,1}))$$
</div>

</section>
<section markdown="1">

### New problem: prefix attack

$$\text{Mac}_k( \langle m_1, m_2 \rangle ) = \text{Mac}_k( m_2 \oplus \text{Mac}_k(m1) )$$

$$\Leftrightarrow$$

$$F_k(m_2 \oplus F_k(m_1)) = F_k(m_2 \oplus F_k(m_1))$$

(This scales to arbitrary length messages.)

</section>
<section markdown="1">

### Prefix attack solution

Prefix the length:

$$\text{Mac'}_k( \langle m_1, ..., m_n \rangle ) = \text{Mac}_k( \langle n, m_1, ..., m_n)$$

<figure>
    <figcaption><small>(Illustration: Katz & Lindell 2015)</small></figcaption>
    <img src="img/cbc-mac-length-prefix.png">
</figure>

</section>
<section markdown="1">

$$\text{Mac'}_k( \langle m_1, m_2 \rangle )$$
$$\neq \text{Mac'}_k( m_2 \oplus \text{Mac'}_k(m1) )$$

$$\Leftrightarrow$$

$$F_k(m_2 \oplus F_k(m_1 \oplus F_k(2)))$$
$$\neq F_k(m_2 \oplus F_k(m_1 \oplus F_k(1)) \oplus F_k(1))$$

<small>(hold on to your horses)</small>

</section>
