# 给定范围[L，R]内的数字计数，该范围为正正方形，数字为波形

> 原文:[https://www . geeksforgeeks . org/给定范围内的数字计数-l-r-即完美的方波和数字波形/](https://www.geeksforgeeks.org/count-of-numbers-in-given-range-l-r-that-is-perfect-square-and-digits-are-in-wave-form/)

给定两个整数 **L** 和 **R** ，任务是计算**【L，R】**范围内的整数，使它们满足以下两个性质:

*   [数必须是任意整数](https://www.geeksforgeeks.org/square-root-of-an-integer/)的完美平方。
*   整数的位数必须为[波形](https://www.geeksforgeeks.org/sort-array-wave-form-2/)即让 **d1** 、 **d2** 、 **d3** 、 **d4** 、 **d5** 为当前整数的位数，则**D1<D2>D3<D4……**必须为真。

**示例:**

> **输入:** L = 1，R = 64
> **输出:** 7
> **说明:**
> 范围内的特殊数字为 1、4、9、16、25、36、49。
> 
> **输入:** L = 80，R = 82
> T3】输出: 0

**天真法:**解决问题最简单的方法是[在【L，R】](https://www.geeksforgeeks.org/range-based-loop-c/)范围内遍历，对于范围内的每个数字，检查上述两个条件。
***时间复杂度:** O(N)*
***辅助空间:** O(1)*

**有效方法:**要优化上述方法，只需迭代**完美正方形**并检查第二个条件。按照以下步骤进行操作:

*   初始化一个变量，比如说**计数= 0** ，来计数范围**【L，R】**内的所有特殊数字。
*   迭代所有小于 **R** 的[完美正方形](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)。
*   定义一个[函数](https://www.geeksforgeeks.org/functions-in-c/)，比如说**检查(N)** ，通过对偶数和奇数进行迭代来检查数字 **N** 是否满足第二个条件。
*   增加**计数**，如果数字大于 **L** 并且功能**检查**对于给定的数字返回真。
*   最后，返回**计数**。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to check if
// the digits of the current
// integer forms a wave pattern
bool check(int N)
{
    // Convert the number to a string
    string S = to_string(N);

    // Loop to iterate over digits
    for (int i = 0; i < S.size(); i++) {
        if (i == 0) {

            // Next character of
            // the number
            int next = i + 1;

            // Current character is
            // not a local minimum
            if (next < S.size()) {
                if (S[i] >= S[next]) {

                    return false;
                }
            }
        }

        else if (i == S.size() - 1) {

            // Previous character of
            // the number
            int prev = i - 1;
            if (prev >= 0) {

                // Character is a
                // local maximum
                if (i & 1) {

                    // Character is not
                    // a local maximum
                    if (S[i] <= S[prev]) {
                        return false;
                    }
                }
                else {
                    // Character is a
                    // local minimum
                    if (S[i] >= S[prev]) {
                        return false;
                    }
                }
            }
        }
        else {
            int prev = i - 1;
            int next = i + 1;
            if (i & 1) {

                // Character is a
                // local maximum
                if ((S[i] > S[prev])
                    && (S[i] > S[next])) {
                }
                else {
                    return false;
                }
            }
            else {
                // Character is a
                // local minimum
                if ((S[i] < S[prev])
                    && (S[i] < S[next])) {
                }
                else {
                    return false;
                }
            }
        }
    }
    return true;
}

// Function to calculate total
// integer in the given range
int totalUniqueNumber(int L, int R)
{
    // Base case
    if (R <= 0) {
        return 0;
    }

    // Current number
    int cur = 1;

    // Variable to store
    // total unique numbers
    int count = 0;

    // Iterating over perfect
    // squares
    while ((cur * cur) <= R) {
        int num = cur * cur;

        // If number is greater
        // than L and satisfies
        // required conditions
        if (num >= L && check(num)) {
            count++;
        }

        // Moving to the
        // next number
        cur++;
    }

    // Return Answer
    return count;
}

// Driver Code
int main()
{
    int L = 1, R = 64;
    cout << totalUniqueNumber(L, R);
}
```

**Output**

```
7
```

***时间复杂度:** O(sqrt(N))*
***辅助空间:** O(1)*