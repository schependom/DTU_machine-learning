## Sum rule

$$\boxed{P(A|C) + P(\bar{A}|C) = 1}$$

## Product rule

$$
\boxed{P(AB|C) = P(A|BC) P(B|C)} = P(B|AC) P(A|C)
$$

## Probability of union

$$
P(A + B) = P(A) + P(B) - P(AB)
$$

## Total probability rule

$$
P(B) = P(B | A) P(A) + P(B | \bar{A}) P(\bar{A}) \quad \Longrightarrow \quad \boxed{P(B|C) = P(B|AC) P(A|C) + P(B|\bar{A}C) P(\bar{A}|C)}
$$

## Bayes' rule

$$
P(A|B) = \frac{P(AB)}{P(B)} = \frac{P(B|A) P(A)}{P(B)} \quad \Longrightarrow \quad \boxed{P(A|BC) = \frac{P(B|AC) P(A|C)}{P(B|C)}}
$$

## Mutually exclusive events

Two events $A_i$ and $A_j$ are **mutually exclusive** if they **cannot happen at the same time**:
$$A_i A_j = 0 \text{ for } i \neq j$$

For $n$ mutually exclusive events $A_1, \ldots, A_n$:
$$\boxed{P(A_1 + A_2 + \ldots + A_n) = \sum_{i=1}^n P(A_i)} = P(A_1) + P(A_2) + \ldots + P(A_n)$$

## Exhaustive events

A set of events $A_1, \ldots, A_n$ is **exhaustive** if **at least one of them must happen**:
$$A_1 + A_2 + \ldots + A_n = 1$$

If the events are **mutually exclusive and exhaustive**, then:
$$\boxed{\sum_{i=1}^n P(A_i) = P(A_1 + A_2 + \ldots + A_n) = 1}$$

## Marginalization

If $B$ can take on a finite number of **mutually exclusive and exhaustive** values $B_1, \ldots, B_n$, then the total probability rule can be generalized to:

$$P(A|C) = \sum_{i=1}^n P(A|B_iC)P(B_i|C)$$

## Stochastic variables

![[images/5-stochastic-variables.png]]

## Independence

Two events $A$ and $B$ are **independent** if:
$$\boxed{P(AB) = P(A)P(B)} \quad \Longleftrightarrow \quad P(A|B) = P(A) \quad \Longleftrightarrow \quad P(B|A) = P(B)$$

Two events $A$ and $B$ are **conditionally independent given $C$** if:
$$\boxed{P(AB|C) = P(A|C)P(B|C)} \quad \Longleftrightarrow \quad P(A|BC) = P(A|C) \quad \Longleftrightarrow \quad P(B|AC) = P(B|C)$$

## Expectations

$$
\boxed{\E[f] = \sum_{i=1}^N f(x_i) p(x_i)}
$$

## Mean

$$
\boxed{\E[x] = \sum_{i=1}^N x_i p(x_i)}
$$

## Variance

$$
\boxed{\text{Var}[x] = \sum_{i=1}^N (x_i - \E[x])^2 p(x_i) }= \E[(x - \E[x])^2] = \E[x^2] - (\E[x])^2
$$

## Bernouilli distribution

-   Random variable $b \in \{0, 1\}$
-   $p(b = 1) = \theta \in [0, 1]$
-   $p(b = 0) = 1 - \theta$

$$\boxed{p(b|\theta) = \theta^b (1 - \theta)^{1-b}}$$

---

## Repeated Bernouilli trials

Suppose we observe a sequence $b_1,\ldots,b_N$ of Bernoulli (binary) events. The **likelihood function** of this sequence given the parameter $\theta$ - assuming the events are **independent** - is:

$$
\begin{aligned}
p(b_1, \ldots, b_N | \theta) &= \prod_{i=1}^N p(b_i | \theta) && \text{by independence} p(x,y|z) = p(x|z)p(y|z) \\
&= \prod_{i=1}^N \theta^{b_i} (1 - \theta)^{1 - b_i} \\
&= \theta^{\sum_{i=1}^N b_i} (1 - \theta)^{N - \sum_{i=1}^N b_i} \\
&= \boxed{\theta^m (1 - \theta)^{N - m}} && m = b_1 + \ldots + b_N
\end{aligned}
$$

The likelihood is the joint possibility of the observations to be true given the parameter $\theta$.

Now, we want to find the value of $\theta$ that maximizes this likelihood. This is called **Maximum Likelihood Estimation (MLE)**:
$$\theta^* = \arg\max_\theta p(b_1, \ldots, b_N | \theta) = \arg\max_\theta \theta^m (1 - \theta)^{N - m}$$
