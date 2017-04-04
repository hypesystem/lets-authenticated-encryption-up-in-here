---
---

<section markdown="1" style="text-align: left;">

## Construction 4.5

Let F be a pseudorandom function. Define a fixed-length MAC for messages of
length n as follows:
  * $$\text{Mac}$$: on input a key $$k \in \{0, 1\}^n$$ and a message $$m \in
    \{0, 1\}^n$$, output the tag $$t := \text{F}_k(m)$$. (If $$|m| = |k|$$ then
    output nothing.)

  * $$\text{Vrfy}$$: on input a key $$k \in \{0, 1\}^n$$, a message $$m \in \{0,
    1\}^n$$, and a tag $$t \in \{0, 1\}^n$$, output 1 if and only if $$t =
    \text{F}_k(m)$$. (If $$|m| = |k|$$, then output 0.)
</section>
