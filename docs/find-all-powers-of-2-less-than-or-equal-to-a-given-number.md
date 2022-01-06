# 求小于等于给定数的 2 的所有幂

> 原文:[https://www . geesforgeks . org/find-2 的所有幂小于或等于给定数/](https://www.geeksforgeeks.org/find-all-powers-of-2-less-than-or-equal-to-a-given-number/)

给定一个正数 **N** ，任务是找出所有小于或等于给定数 **N** 的二的完美幂。

**示例:**

> **输入:** N = 63
> **输出:** 32 16 8 4 2 1
> **说明:**
> 总共有 2 的 6 次方，小于等于给定数 N
> 
> **输入:** N = 193
> **输出:** 128 64 32 16 8 4 2 1
> **说明:**
> 总共有 8 的 2 次方，小于等于给定的数 N

**天真方法:**想法是从 N 到 1 遍历每个数字，检查它是否是 2 的完美幂。如果是，则打印该号码。

**另一种方法:**思路是找出 2 的所有幂，简单打印小于或等于 n 的幂。

**另一种方法:**这个想法基于这样一个概念，即 2 的所有幂都以二进制形式设置了所有位。[比特集功能](https://www.geeksforgeeks.org/c-bitset-and-its-application/)就是用这种方法解决上述问题的。以下是步骤:

1.  求 2 的最大幂(比如 **temp** )，用来求小于等于 **N** 的数。
2.  初始化一个最大大小为 **64** 的位组数组 **arr[]** ，以存储给定数字 **N** 的二进制表示。
3.  使用[重置()](https://www.geeksforgeeks.org/bitset-reset-function-in-c-stl/)功能重置位组数组中的所有位。
4.  从**总计到 0** 迭代一个循环，依次使每个位 **1** ，找到那个二进制表达式的值，然后复位该位。

下面是上述方法的实现:

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
const int MAX = 64;

// Function to return max exponent of
// 2 which evaluates a number less
// than or equal to N
int max_exponent(int n)
{
    return (int)(log2(n));
}

// Function to print all the powers
// of 2 less than or equal to N
void all_powers(int N)
{
    bitset<64> arr(N);

    // Reset all the bits
    arr.reset();

    int total = max_exponent(N);

    // Iterate from total to 0
    for (int i = total; i >= 0; i--) {

        // Reset the next bit
        arr.reset(i + 1);

        // Set the current bit
        arr.set(i);

        // Value of the binary expression
        cout << arr.to_ulong() << " ";
    }
}

// Driver Code
int main()
{
    // Given Number
    int N = 63;

    // Function Call
    all_powers(N);
    return 0;
}
```

**Output:**

```
32 16 8 4 2 1

```

**时间复杂度:***O(log N)*
T5】辅助空间: *O(1)*