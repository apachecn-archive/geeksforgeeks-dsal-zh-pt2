# 二进制表示中两个直接 1 之间的最大 0

> 原文:[https://www . geesforgeks . org/maximum-0s-two-immediate-1s-二进制表示/](https://www.geeksforgeeks.org/maximum-0s-two-immediate-1s-binary-representation/)

给定一个数字 n，任务是在给定 n 的二进制表示中找到两个直接 1 之间的最大 0。如果二进制表示包含少于两个 1，则返回-1

**示例:**

```
Input : n = 47
Output: 1
// binary of n = 47 is 101111

Input : n = 549
Output: 3
// binary of n = 549 is 1000100101

Input : n = 1030
Output: 7
// binary of n = 1030 is 10000000110

Input : n = 8
Output: -1
// There is only one 1 in binary representation
// of 8.
```

解决这个问题的思路是使用**换挡操作符**。我们只需要找到 n 的二进制表示中两个直接 1 的位置，并最大化这些位置的差。

*   如果数字是 0 或 2 的幂，则返回-1。在这些情况下，二进制表示中的 1 少于两个。
*   用第一个最右边 1 的位置初始化变量 **prev** ，它基本上存储了之前看到的 1 的位置。
*   现在取另一个变量 **cur** ，它在 **prev** 之后存储立即 1 的位置。
*   现在取**cur–prev–1**之差，它将是 0 到立即 1 之间的数，并将其与以前的最大值 0 进行比较，更新 **prev** 即；prev =下一次迭代的 cur。
*   使用辅助变量**设置位**，扫描 n 的所有位，帮助检测当前位是 0 还是 1。
*   首先检查 N 是 0 还是 2 的[次方。](https://www.geeksforgeeks.org/write-one-line-c-function-to-find-whether-a-no-is-power-of-two/)

下面是上述想法的实现:

## C++

```
// C++ program to find maximum number of 0's
// in binary representation of a number
#include <bits/stdc++.h>
using namespace std;

// Returns maximum 0's between two immediate
// 1's in binary representation of number
int maxZeros(int n)
{
    // If there are no 1's or there is only
    // 1, then return -1
    if (n == 0 || (n & (n - 1)) == 0)
        return -1;

    // loop to find position of right most 1
    // here sizeof int is 4 that means total 32 bits
    int setBit = 1, prev = 0, i;
    for (i = 1; i <= sizeof(int) * 8; i++) {
        prev++;

        // we have found right most 1
        if ((n & setBit) == setBit) {
            setBit = setBit << 1;
            break;
        }

        // left shift setBit by 1 to check next bit
        setBit = setBit << 1;
    }

    // now loop through for remaining bits and find
    // position of immediate 1 after prev
    int max0 = INT_MIN, cur = prev;
    for (int j = i + 1; j <= sizeof(int) * 8; j++) {
        cur++;

        // if current bit is set, then compare
        // difference of cur - prev -1 with
        // previous maximum number of zeros
        if ((n & setBit) == setBit) {
            if (max0 < (cur - prev - 1))
                max0 = cur - prev - 1;

            // update prev
            prev = cur;
        }
        setBit = setBit << 1;
    }
    return max0;
}

// Driver program to run the case
int main()
{
    int n = 549;

    // Initially check that number must not
    // be 0 and power of 2
    cout << maxZeros(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum number of 0's
// in binary representation of a number
class GFG {

    // Returns maximum 0's between two immediate
    // 1's in binary representation of number
    static int maxZeros(int n) {
        // If there are no 1's or there is only
        // 1, then return -1
        if (n == 0 || (n & (n - 1)) == 0) {
            return -1;
        }
        //int size in java is 4 byte
        byte b = 4;
        // loop to find position of right most 1
        // here sizeof int is 4 that means total 32 bits
        int setBit = 1, prev = 0, i;
        for (i = 1; i <= b* 8; i++) {
            prev++;

            // we have found right most 1
            if ((n & setBit) == setBit) {
                setBit = setBit << 1;
                break;
            }

            // left shift setBit by 1 to check next bit
            setBit = setBit << 1;
        }

        // now loop through for remaining bits and find
        // position of immediate 1 after prev
        int max0 = Integer.MIN_VALUE, cur = prev;
        for (int j = i + 1; j <= b * 8; j++) {
            cur++;

            // if current bit is set, then compare
            // difference of cur - prev -1 with
            // previous maximum number of zeros
            if ((n & setBit) == setBit) {
                if (max0 < (cur - prev - 1)) {
                    max0 = cur - prev - 1;
                }

                // update prev
                prev = cur;
            }
            setBit = setBit << 1;
        }
        return max0;
    }

    // Driver program to run the case
    static public void main(String[] args) {
        int n = 549;

        // Initially check that number must not
        // be 0 and power of 2
        System.out.println(maxZeros(n));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find maximum number of
# 0's in binary representation of a number

# Returns maximum 0's between two immediate
# 1's in binary representation of number
def maxZeros(n):
    # If there are no 1's or there is
    # only 1, then return -1
    if (n == 0 or (n & (n - 1)) == 0):
        return -1

    # loop to find position of right most 1
    # here sizeof is 4 that means total 32 bits
    setBit = 1
    prev = 0
    i = 1
    while(i < 33):
        prev += 1

        # we have found right most 1
        if ((n & setBit) == setBit):
            setBit = setBit << 1
            break

        # left shift setBit by 1 to check next bit
        setBit = setBit << 1

    # now loop through for remaining bits and find
    # position of immediate 1 after prev
    max0 = -10**9
    cur = prev
    for j in range(i + 1, 33):
        cur += 1

        # if current bit is set, then compare
        # difference of cur - prev -1 with
        # previous maximum number of zeros
        if ((n & setBit) == setBit):
            if (max0 < (cur - prev - 1)):
                max0 = cur - prev - 1

            # update prev
            prev = cur
        setBit = setBit << 1

    return max0

# Driver Code
n = 549

# Initially check that number must not
# be 0 and power of 2
print(maxZeros(n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find maximum number of 0's
// in binary representation of a number
using System;

class GFG {

    // Returns maximum 0's between two immediate
    // 1's in binary representation of number
    static int maxZeros(int n)
    {
        // If there are no 1's or there is only
        // 1, then return -1
        if (n == 0 || (n & (n - 1)) == 0)
            return -1;

        // loop to find position of right most 1
        // here sizeof int is 4 that means total 32 bits
        int setBit = 1, prev = 0, i;
        for (i = 1; i <= sizeof(int) * 8; i++) {
            prev++;

            // we have found right most 1
            if ((n & setBit) == setBit) {
                setBit = setBit << 1;
                break;
            }

            // left shift setBit by 1 to check next bit
            setBit = setBit << 1;
        }

        // now loop through for remaining bits and find
        // position of immediate 1 after prev
        int max0 = int.MinValue, cur = prev;
        for (int j = i + 1; j <= sizeof(int) * 8; j++) {
            cur++;

            // if current bit is set, then compare
            // difference of cur - prev -1 with
            // previous maximum number of zeros
            if ((n & setBit) == setBit) {
                if (max0 < (cur - prev - 1))
                    max0 = cur - prev - 1;

                // update prev
                prev = cur;
            }
            setBit = setBit << 1;
        }
        return max0;
    }

    // Driver program to run the case
    static public void Main()
    {
        int n = 549;

        // Initially check that number must not
        // be 0 and power of 2
        Console.WriteLine(maxZeros(n));
    }
}

// This code is contributed by vt_m.
```

## java 描述语言

```
<script>

// JavaScript program to find maximum number of 0's
// in binary representation of a number

// Returns maximum 0's between two immediate
// 1's in binary representation of number
function maxZeros(n)
{

    // If there are no 1's or there is only
    // 1, then return -1
    if (n == 0 || (n & (n - 1)) == 0)
    {
        return -1;
    }

    // int size in java is 4 byte
    let b = 4;

    // Loop to find position of right most 1
    // here sizeof int is 4 that means total 32 bits
    let setBit = 1, prev = 0, i;

    for(i = 1; i <= b* 8; i++)
    {
        prev++;

        // We have found right most 1
        if ((n & setBit) == setBit)
        {
            setBit = setBit << 1;
            break;
        }

        // Left shift setBit by 1
        // to check next bit
        setBit = setBit << 1;
    }

    // Now loop through for remaining bits
    // and find position of immediate 1 after prev
    let max0 = Number.MIN_VALUE, cur = prev;
    for(let j = i + 1; j <= b * 8; j++)
    {
        cur++;

        // If current bit is set, then compare
        // difference of cur - prev -1 with
        // previous maximum number of zeros
        if ((n & setBit) == setBit)
        {
            if (max0 < (cur - prev - 1))
            {
                max0 = cur - prev - 1;
            }

            // Update prev
            prev = cur;
        }
        setBit = setBit << 1;
    }
    return max0;
}

// Driver Code
let n = 549;

// Initially check that number must not
// be 0 and power of 2
document.write(maxZeros(n));

// This code is contributed by code_hunt

</script>
```

**输出:**

```
3
```

本文由 [**沙莎克·米什拉(古卢)**](https://www.facebook.com/shashank.mishra.92167) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。