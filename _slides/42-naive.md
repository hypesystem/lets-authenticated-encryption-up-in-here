---
---
<section markdown="1">
## Generic constructions
Goal: Come up with a construction that combines _any CPA-secure encryption scheme_
with _any unforgeable_ $$\text{Mac}$$ to achieve authenticated
encryption.

</section>
<section markdown="1">
Given $$Enc_{k_E}(x)$$, $$Mac_{k_M}(y)$$, come up with ciphertext and tag $$\langle c,t\rangle$$.
</section>
<section markdown="1">

Three obvious constructions:
  1. Encrypt _and_ authenticate\\
    $$c\leftarrow Enc_{k_E}(m)$$, $$t\leftarrow Mac_{k_M}(m)$$

  2. Authenticate _then_ encrypt\\
    $$t\leftarrow Mac_{k_M}(m)$$, $$c\leftarrow Enc_{k_E}(m||t)$$

  3. Encrypt _then_ authenticate\\
    $$c\leftarrow Enc_{k_E}(m)$$, $$t\leftarrow Mac_{k_M}(c)$$
</section>
<section markdown="1">
#### 1. Encrypt _and_ authenticate

$$c\leftarrow Enc_{k_E}(m)$$, $$t\leftarrow Mac_{k_M}(m)$$

Nope.\\
_Unforgabilty_ does not guarantee secrecy; $$t$$ may leak information about
$$m$$
</section>
<section markdown="1">
#### 2. Authenticate _then_ encrypt

$$t\leftarrow Mac_{k_M}(m)$$, $$c\leftarrow Enc_{k_E}(m||t)$$\\
\\
Nope.\\
_Mumble mumble,_ padding oracle attack, _mumble mumble_
</section>
<section markdown="1">
#### 3. Encrypt _then_ authenticate

$$c\leftarrow Enc_{k_E}(m)$$, $$t\leftarrow Mac_{k_M}(c)$$

Yes!
</section>
