> [!term] Binning
> Counting how many observations fall within each bin.
> Each **bin** is an interval (of equal width or not).

## Boxplot

Denote

-   $v_1 \leq v_2 \leq ... \leq v_N$: sorted values of the variable

    -   $\Rightarrow v_1$ = value of smallest observation
    -   $\Rightarrow v_N$ = value of largest observation

-   $l_{25}$: $p=0.25$ percentile
-   $l_{50}$: $p=0.50$ percentile = median
-   $l_{75}$: $p=0.75$ percentile

Then:

-   Upper whisker: $$\min\{l_{75} + \frac{3}{2}(l_{75} - l_{25}), v_N\}$$
-   Lower whisker: $$\max\{l_{25} - \frac{3}{2}(l_{75} - l_{25}), v_1\}$$

## Baseline performance

> [!term] Baseline performance
> Performance of a naieve method.

-   Should be
    -   Quick to compute
    -   Easy to implement
    -   Foolproof

| Task               | Baseline performance                         |
| ------------------ | -------------------------------------------- |
| Classification     | Predict class with most elements (mode)      |
| Regression         | Predict mean or median (constant prediction) |
| Density estimation | Uniform density                              |
| Outlier detection  | Everything / nothing is an outlier           |

## Target / ceiling performance

> [!term] Target / ceiling performance
> Provides an upper bound on performance.

-   How well **humans** perform
-   How well we **have** to perform
-   Comparable methods in **literature**
