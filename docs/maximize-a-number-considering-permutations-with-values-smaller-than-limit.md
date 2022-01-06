# 考虑数值小于极限的排列，最大化一个数

> 原文:[https://www . geesforgeks . org/maximum-a-number-concept-置换-带值-小于限制/](https://www.geeksforgeeks.org/maximize-a-number-considering-permutations-with-values-smaller-than-limit/)

给定两个数字 N 和 m，通过置换(改变顺序)N 的数字构造最大数，不超过 m
**注:**允许保留 N 不变。

**示例:**

> 输入:N = 123，M = 222
> 输出:213
> 共有 3 个！对于 N = 123，排列是可能的，但是满足给定条件的唯一排列是 213。同样，在示例 2 中，总共有 4 个！对于 N = 3921，排列是可能的，但是满足给定条件的唯一排列是 9321。
> 
> 输入:N = 3921，M = 10000
> 输出:9321

**方法:**让我们从最左边开始一个数字一个数字地构造答案。我们被要求建立 ***字典式的*** 最大答案。所以按照这个顺序，我们应该在每一步选择最大的数字。方法是从最大的开始迭代所有可能的数字。对于每个数字，检查是否可以将其放在这个位置，并将结果数字与数字 M 进行比较。如果它小于或等于 M 的值，则继续下一个数字。

下面是 CPP 的实现:

```
// CPP program to Maximize the given number.
#include <bits/stdc++.h>
using namespace std;

// Function to maximize the number N with
// limit as M.
string maximizeNumber(string N, int M)
{
    // Sorting the digits of the
    // number in increasing order.
    sort(N.begin(), N.end());

    for (int i = 0; i < N.size(); i++)
        for (int j = i + 1; j < N.size(); j++) {

            // Copying the string into another
            // temp string.
            string t = N;

            // Swaping the j-th char(digit)
            // with i-th char(digit)
            swap(t[j], t[i]);

            // Sorting the temp string 
            // from i-th pos to end.
            sort(t.begin() + i + 1, t.end());

            // Checking if the string t is 
            // greater than string N and less
            // than or equal to the number M.
            if (stoll(t) > stoll(N) && stoll(t) <= M)

                // If yes then, we will permanently
                // swap the i-th char(or digit)
                // with j-th char(digit).
                swap(N[i], N[j]);
        }

    // Returns the maximized number.
    return N;
}

// Driver function
int main()
{
    string N = "123";
    int M = 222;
    cout << maximizeNumber(N, M) << endl;
    return 0;
}
```

输出:

```
213

```