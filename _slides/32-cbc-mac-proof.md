---
---
<section markdown="1">
## CBC-MAC

# Proof of Security

"intended for advanced readers."
</section>
<section markdown="1">
$$F$$ is a keyed function that, for security parameter $$n$$, maps $$n$$-bit keys and $$n$$-bit inputs to $$n$$-bit outputs.

$$\text{CBC}$$ is a keyed function that, for security parameter $$n$$, maps $$n$$-bit keys and inputs in $$(\{0,1\}^n)^*$$ to $$n$$-bit outputs.

$$\text{CBC}_k(x_1,...,x_l) \stackrel{\text{def}}{=}$$
$$F_k(F_k(\cdots F_k(x_1) \oplus \cdots ) \oplus x_l)$$

Exactly like CBC-MAC, but without a fixed length-function ($$l$$ may vary).
</section>
<section markdown="1">
A set of strings $$P \subset (\{0,1\}^n)^*$$ is prefix-free if it does not contain the empty string, and no string $$X \in P$$ is a prefix for any other string $$X' \in P$$.
</section>
<section markdown="1" style="text-align: left;">
## Theorem 4.13

If $$F$$ is a pseudorandom function, then $$\text{CBC}$$ is a pseudorandom function on prefix-free inputs:
for all probabilistic polynomial-time distinguishers $$D$$ that query their oracle on a prefix-free set of inputs, there is a negligible function $$\text{negl}$$ such that:
</section>
<section markdown="1">
$$| { \text{Pr}[D^{\text{CBC}_k(\cdot)}(1^n) = 1] - \text{Pr}[D^{f(\cdot)}(1^n) = 1] } |$$
$$\leq \text{negl}(n)$$,

<div markdown="1" style="text-align: left;">
where $$k$$ is chosen uniformly from $$\{0,1\}^n$$ and $$f$$ is chosen uniformly from the set of functions mapping $$(\{0,1\}^n)^*$$ to $$\{0,1\}^n$$.
</div>
</section>
<section markdown="1" style="text-align: left;">
We can make $$\text{CBC}_k$$ work as a pseudorandom function for arbitrary-length inputs by converting these inputs to belong to the proper input space.

$$\text{encode}(m) \in (\{0,1\}^n)^*$$

To get a tag from arbitrary length message $$m$$:

$$t \leftarrow \text{CBC}_k(\text{encode}(m))$$

This is based on theorem 4.6, for secure fixed-length MACs.
It works because $$\text{encode}(m)$$ ensures that the messages are unique.
</section>
<section markdown="1">
How do we implement $$\text{encode}$$?

(a) Fix the length $$l$$, and then simply:  
$$\text{encode}(m) = m$$

(b) Prepend the length:  
$$ \text{encode} ( \langle m_1, ... m_{| m |} \rangle ) = $$ 
$$ \langle n, m_1, ... m_{|m|-1}, \text{pad}(m_{|m|}) \rangle $$

where $$\text{pad}$$ pads a message with 0s until it has the valid block length.
</section>
<section markdown="1" style="text-align: left;">
We want to prove that the security of $$\text{CBC}$$ depends solely on the security of $$F_k$$.

First, we replace $$F_k$$ in $$\text{CBC}$$ with a random function $$g$$ that maps $$n$$-bit inputs to $$n$$-bit outputs for security parameter $$n$$.

We need to show: if $$g$$ is chosen uniformly in $$\text{Func}_n$$, then $$\text{CBC}_g$$ is indistinguishable from a random function mapping $$(\{0,1\}^n)^*$$ to $$n$$-bit strings, as long as the set of inputs queried is prefix-free.
</section>
<section markdown="1" style="text-align: left;">
## Claim 4.14

Fix any $$n \geq 1$$. For all distinguishers $$D$$ that query their oracle on a prefix-free set of $$q$$ inputs, where the longest input contains $$l$$ blocks, it holds that:

$$ | \text{Pr}[D^{\text{CBC}_g( \cdot )}(1^n) = 1] - \text{Pr}[D^{f(\cdot)}(1^n) = 1] | $$
$$ \leq \frac{q^2 l^2}{2^n} $$

where $$g$$ is chosen uniformly from $$\text{Func}_n$$, and $$f$$ is chosen uniformly from the set of functions mapping $$(\{0,1\}^n)^*$$ to $$\{0,1\}^n$$.
</section>
<section markdown="1">
Notice that for any $$t_1,...,t_q \in \{0,1\}^n$$ it holds:

$$\text{Pr}[ \forall i : f(X_i) = t_i ] = \frac{1}{2^{nq}}$$
</section>
<section markdown="1" style="text-align: left;">
## Proof of claims 4.14-15

First we show that $$\text{CBC}$$ is <em>smooth</em>. Then we show that smoothness implies claim 4.14.

Fix some $$n \geq 1$$.

Let $$P \subset \{X_1,...X_q\}$$ be a prefix-free set of inputs $$X_i \in (\{0,1\}^n)^*$$.

Let $$l$$ be the length (in blocks) of the longest input $$X_i$$.
</section>
<section markdown="1" style="text-align: left;">
We define smoothness:

$$\text{CBC}$$ is $$(q,l,\delta)$$-smooth if for every $$P$$ and every $$t_1,...t_q \in \{0,1\}^n$$, it holds that:

$$\text{Pr}[ \forall i : \text{CBC}_g(X_i) = t_i] \geq \frac{1 - \delta}{2^{nq}}$$

with the probability uniform over choice of $$g \in \text{Func}_n$$.
</section>
<section markdown="1" style="text-align: left;">
We will show that $$\text{CBC}_g$$ is $$(q,l,\delta)$$-smooth for $$\delta = \frac{q^2 l^2}{2^n}$$. (Claim 4.15)
</section>
<section markdown="1" style="text-align: left;">
$$C_g(X) = (I_1, \dots, I_m)$$ denotes the set of inputs on which $$g$$ is evaluated during the computation of $$\text{CBC}_g(X)$$ for any $$X \in (\{0,1\}^n)^*)$$ with $$X = x_1, ...$$ and $$x_i \in \{0,1\}^n$$.

Now let's look at two different messages with a different number of blocks:

$$X \in (\{0,1\}^n)^m \quad X' \in (\{0,1\}^n)^{m'}$$
</section>
<section markdown="1" style="text-align: left;">
There is a non-trivial collision if for $$i$$ and $$j$$ it holds that $$I_i = I_j$$, but $$i \neq j$$.

There is a non-trivial collision in $$X,X' \in P$$ if for $$i$$ and $$j$$ it holds that $$I_i = I'_j$$, but $$ \langle x_1, ..., x_i \rangle \neq \langle x'_1, ..., x'_j \rangle $$

Let $$\text{Coll}$$ be the event that such a collision occurs.
</section>
<section markdown="1" style="text-align: left;">
With no non-trivial collision:

We choose each output value for $$g$$ for a given input the first time it is requested.
Each time, we choose it randomly. (Not efficient, but very uniformly chosen.)

Fun fact:
We do not need to choose $$g(I_m)$$ and $$g(I'_{m'})$$ to determine if there is a collision:
If the last elements collide it can only be because $$X$$ is a prefix of $$X'$$, but $$P$$ is prefix-free.
</section>
<section markdown="1" style="text-align: left;">
No non-trivial collision occurs.

All values fixed by $$g$$, including $$\text{CBC}_g(X_1),...,\text{CBC}_g(X_q)$$ are uniform and independent of each other.

This means that or any $$t_1,...,t_q \in \{0,1\}^n$$:

$$\text{Pr}[ \forall i : \text{CBC}_g(X_i) = t_i | \overline{\text{Coll}} ] = \frac{1}{2^{nq}}$$
</section>
<section markdown="1" style="text-align: left;">
Let us find an upper bound for $$\text{Pr}[\text{Coll}]$$:

$$\text{Coll}_{i,j}$$ is a collision between or within any fixed $$X_i, X_j \in P$$.
So $$\text{Coll}$$ is the union of all $$\text{Coll}_{i,j}$$ for all $$i, j$$ within the length of $$P$$ (up to $$q$$).
(All unique collisions between or within inputs.)
</section>
<section markdown="1">
Using union-bound:

$$\text{Pr}[\text{Coll}] \leq \sum_{i,j: i < j} \text{Pr}[\text{Coll}_{i,j}]$$

$$= \begin{pmatrix}q\\2\end{pmatrix} * \text{Pr}[\text{Coll}_{i,j}] \leq \frac{q^2}{2} * \text{Pr}[\text{Coll}_{i,j}] $$
</section>
<section markdown="1" style="text-align: left;">
Let us find upper bound for $$\text{Pr}[\text{Coll}_{i,j}]$$:

Probability of any collision is larger with longer inputs, so we fix two inputs $$X, X'$$ with length $$l$$ (max length).

Fix $$t$$ as the largest integer such that $$(x_1,...,x_t) = (x'_1,...,x'_t)$$.
</section>
<section markdown="1">
1. For $$i = 1,...,t-1$$ fix $$g(I_i)$$ uniformly. (steps $$1$$ to $$t-1$$)
2. Fix $$g(I_t)$$ uniformly. (step $$t$$)
3. For $$i = t+1,...,l-1$$ choose $$g(I_i)$$ uniformly. (steps $$t+1$$ to $$l-1$$)
4. For $$i = t+1,...,l-1$$ choose $$g(I'_i)$$ uniformly. (steps $$l$$ to $$2l-2$$)

$$\text{Coll}(k)$$ is the event that a non-trivial collision occurs by step $$k$$.
</section>
<section markdown="1">

$$ \text{Pr}[\text{Coll}_{i,j}]$$
$$= \text{Pr}[\bigtriangleup_k \text{Coll}(k)}] $$
$$\leq \text{Pr}[Coll(1)] + \stackrel{2l-2}{\sum_{k=2}} \text{Pr}[\text{Coll}(k)|\overline{\text{Coll}(k-1)}]$$
</section>
<section markdown="1" style="text-align: left;">
Probability of collision first at step $$k < t$$ is $$k/2^n$$ (attempts over block space).

Probability of collision first at step $$t$$ is $$leq 2t/2^n$$ (2 values: 2 times attempts over block space).

Probability of collision first at step $$k > t$$ is $$(k + 1)/2^n$$. (attempts + 1 over block space) [why?]
</section>
<section markdown="1">

$$\text{Pr}[\text{Coll}_{i,j}] \leq \frac{1}{2^n} * (\sum\limits_{k=1}^{t-1} k + 2t + \sum\limits_{k=t+1}^{2l-2} (k + 1))$$

$$= \frac{1}{2^n} * \sum\limits_{k=2}^{2l-1} k$$

$$= \frac{1}{2^n} * (2l + 1) * (l - 1)$$

$$< \frac{2l^2}{2^n}$$
</section>
<section markdown="1">
Recall

$$\text{Pr}[\text{Coll}] \leq \frac{q^2}{2} * \text{Pr}[\text{Coll}_{i,j}] $$

$$\text{Pr}[\text{Coll}] < \frac{q^2l^2}{2^n} = d$$
</section>
<section>
<img src="img/proof-paste-1.png">
</section>
<section>
<img src="img/proof-paste-2.png">
</section>
