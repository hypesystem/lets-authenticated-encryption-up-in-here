---
---
<section markdown="1">

## Problem:
Construction 4.5 only works for small messages; same length as the key!

</section>
<section markdown="1">

We can fix that. For a message $$m_1,\ldots,m_d$$ of $$d$$ $$n$$-length blocks,
let

> $$t_{1\ldots i \ldots d} = \text{Mac}_k(m_i)$$

Then use $$t$$ as the tag of $$m$$.

</section>
<section markdown="1">

## More Problems:

  1. Re-ordering attack\\
     Solved by adding $$i$$ to $$m_i$$

  2. Truncation attack\\
     Solved by adding message length $$l$$ to $$m_i$$

  3. Mix 'n' match
     Solved by adding a random message id $$r$$ to $$m_i$$

</section>
<section markdown="1">
We get:
> $$t_{1\ldots i \ldots d} = \text{Mac}_k(r||l||i||m_i)$$

This is impractical. The message length is still fixed, and the message-space got a
lot smaller.
</section>
