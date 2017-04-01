---
---
Canonical verification

$$
\text{Vrfy}_k(m,t) =
\begin{cases}
    1, & \text{if}\ \text{Mac}_k(m) = t \\
    0, & \text{otherwise}
\end{cases}
$$

Watch out for timing attacks in <code>strcmp</code>
