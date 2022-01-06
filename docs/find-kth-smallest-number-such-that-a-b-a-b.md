# 求第 K 个最小的数，使得 A + B = A | B

> 原文:[https://www . geesforgeks . org/find-kth-minist-number-so-a-b-a-b/](https://www.geeksforgeeks.org/find-kth-smallest-number-such-that-a-b-a-b/)

给定两个数字 **A** 和 **K** ，任务是找到**第 K 个最小正整数** B，使得 **A + B = A | B** ，其中|表示**按位 OR** 运算符。

**示例:**

```
Input: A = 10, K = 3
Output: 5
Explanation:
K = 1, 10 + 1 = 10 | 1 = 11
K = 2, 10 + 4 = 10 | 4 = 14
K = 3, 10 + 5 = 10 | 5 = 15

Input: A = 1, B = 1
Output: 2 
```

**进场:**

*   B 是给定方程的解，当且仅当 B 在 A 有 1 的所有位置都有 0(在二进制表示法中)。
*   所以，我们需要为 A 为 0 的位置确定 B 的位。设，如果 A = 10100001，那么 B 的最后八位必须是 0 _ 0 _ _ _ _ _ 0，其中 _ 表示 0 或 1。将 all _ 替换为 0 或 1 会给我们一个解决方案。
*   第 k 个最小的数字将通过用数字 k 的二进制表示的数字替换 all _ in y 来接收。

下面是上述方法的实现:

## C++

```
// C++ program for the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find k'th
// smallest number such that
// A + B = A | B
long long kthSmallest(long long a, long long k)
{

    // res will store
    // final answer
    long long res = 0;
    long long j = 0;

    for (long long i = 0; i < 32; i++) {

        // Skip when j'th position
        // has 1 in binary representation
        // as in res, j'th position will be 0.
        while (j < 32 && (a & (1 << j))) {
            // j'th bit is set
            j++;
        }

        // If i'th bit of k is 1
        // and i'th bit of j is 0
        // then set i'th bit in res.
        if (k & (1 << i)) {
            res |= (1LL << j);
        }

        // Proceed to next bit
        j++;
    }

    return res;
}

// Driver Code
int main()
{

    long long a = 5, k = 3;
    cout << kthSmallest(a, k) << "\n";

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find k'th
# smallest number such that
# A + B = A | B
def kthSmallest(a, k):

    # res will store
    # final answer
    res = 0
    j = 0

    for i in range(32):

        # Skip when j'th position
        # has 1 in binary representation
        # as in res, j'th position will be 0.
        while (j < 32 and (a & (1 << j))):

            # j'th bit is set
            j += 1

        # If i'th bit of k is 1
        # and i'th bit of j is 0
        # then set i'th bit in res.
        if (k & (1 << i)):
            res |= (1 << j)

        # Proceed to next bit
        j += 1

    return res

# Driver Code
a = 5
k = 3

print(kthSmallest(a, k))

# This code is contributed by himanshu77
```

## java 描述语言

```
<script>

// Javascript program for the
// above approach

// Function to find k'th
// smallest number such that
// A + B = A | B
function kthSmallest(a, k)
{

    // res will store
    // final answer
    let res = 0;
    let j = 0;

    for (let i = 0; i < 32; i++) {

        // Skip when j'th position
        // has 1 in binary representation
        // as in res, j'th position will be 0.
        while (j < 32 && (a & (1 << j))) {
            // j'th bit is set
            j++;
        }

        // If i'th bit of k is 1
        // and i'th bit of j is 0
        // then set i'th bit in res.
        if (k & (1 << i)) {
            res |= (1 << j);
        }

        // Proceed to next bit
        j++;
    }

    return res;
}

// Driver Code

    let a = 5, k = 3;
    document.write(kthSmallest(a, k));

</script>
```

**Output:** 

```
10
```

**时间复杂度:** O(log(n))

**辅助空间:** O(1)