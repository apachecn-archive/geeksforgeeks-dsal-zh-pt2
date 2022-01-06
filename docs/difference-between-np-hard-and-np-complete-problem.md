# NP 难和 NP 完全问题的区别

> 原文:[https://www . geesforgeks . org/NP-hard-和-np-complete-problem/](https://www.geeksforgeeks.org/difference-between-np-hard-and-np-complete-problem/)

**先决条件:**[NP-完全性](https://www.geeksforgeeks.org/np-completeness-set-1/)

**NP 问题:**
NP 问题是一组问题，其解很难找到，但很容易验证，由[非确定性机器](https://www.geeksforgeeks.org/difference-between-deterministic-and-non-deterministic-algorithms/)在多项式时间内求解。

[**【NP-Hard 问题】**](https://www.geeksforgeeks.org/tag/nphard/) **:**
A 问题 X 是 NP-Hard 如果存在 NP-Complete 问题 Y，那么 Y 在多项式时间内可约化为 X。NP 难问题和 NP 完全问题一样难。NP 难问题不需要在 NP 类中。

[**NP-完成问题**](https://www.geeksforgeeks.org/algorithms-gq/np-complete-gq/) **:**

一个问题 X 是 NP 完全的如果有一个 NP 问题 Y，使得 Y 在多项式时间内可约化为 X。NP-完全问题和 NP 问题一样难。如果一个问题是 NP 完全问题和 NP 难问题的一部分，那么它就是 NP 完全问题。非确定性图灵机可以在多项式时间内求解 NP 完全问题。

**<u>NP-Hard 和 NP-Complete 的区别</u>** :

<figure class="table">

| NP 硬 | NP-完成 |
| --- | --- |
| NP-Hard 问题(比如 X)可以解当且仅当有一个 NP-Complete 问题(比如 Y)可以在多项式时间内约化为 X。 | NP-完全问题可以在多项式时间内通过非确定性算法/图灵机来解决。 |
| 要解决这个问题，它不一定要在 NP 中。 | 要解决这个问题，必须同时是 NP 和 NP 难问题。 |
| 不一定是决策问题。 | 这完全是一个决策问题。 |
| 例如:停顿问题、顶点覆盖问题等。 | 例如:判定图是否有哈密顿圈、判定布尔公式是否可满足、电路可满足性问题等。 |

</figure>