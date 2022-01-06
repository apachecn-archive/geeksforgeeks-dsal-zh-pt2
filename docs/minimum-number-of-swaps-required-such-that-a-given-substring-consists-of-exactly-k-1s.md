# 给定子串恰好由 K 个 1 组成所需的最小交换次数

> 原文:[https://www . geesforgeks . org/最小交换次数-要求-这样-给定子串-由-k-1s 组成/](https://www.geeksforgeeks.org/minimum-number-of-swaps-required-such-that-a-given-substring-consists-of-exactly-k-1s/)

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** 和三个正整数 **L** 、 **R** 和 **K** ，任务是找到所需的最小交换次数，..S[R]} 正好由 **K** **1** s 组成，如果做不到，那么打印 **"-1"** 。

**示例:**

> **输入:** S = "110011111000101 "，L = 5，R = 8，K = 2
> **输出:**2
> T6】解释:
> 最初，子串{S[5]，..s[8]} =“1111”由 4 个 1 组成。
> 互换(S[5]，S[3])和(S[6]，S[4])。
> 修改字符串 S =“111100111000101”和{S[5]，..s[8]} =“0011”。
> 因此，需要 2 次互换。
> 
> **输入:**S =“01010101010101”，L = 3，R = 7，K = 8
> **输出:** -1

**方法:**思路是统计子串内和子串外存在的 **1s** 和 **0s** 的个数， **{S[L]，…，S[R]}** 。然后，检查是否有足够的 **1** s 或 **0** s 出现在可交换的范围之外，以使子串恰好包含 **K** **1** s。

按照以下步骤解决问题:

*   [将字符串](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)中的 1 和 0 的频率分别存储到**中的 **S** 中的**和**中的**中。
*   另外，[将子串](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/) **中 **1** s 和 **0** s 的频率分别存储在**1**和**0**中。**
*   使用公式:**(rem _ one = cntone****–one)**和**rem _ zero =(CNT zero****–zero)**求出子串**S【L，R】**外 **1s** 和 **0s** 的频率。
*   如果**k≥1**，则执行以下操作:
    *   初始化**rem =(K-one)**，表示使和等于 **K** 所需的 **1s** 的个数。
    *   如果**零≥ rem** 和**rem _ one≥rem**，则打印 **rem** 的值作为结果。
*   否则，如果 **K <为**，则执行以下操作:
    *   初始化**rem =(one–K)**，表示使和等于 **K** 所需的 0 的个数。
    *   如果**1≥rem****rem _ 0≥rem**，则打印 **rem** 的值作为结果。
*   在所有其他情况下，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include<bits/stdc++.h>
using namespace std;

    // Function to find the minimum number
    // of swaps required such that the
    // substring {s[l], .., s[r]} consists
    // of exactly k 1s
   int minimumSwaps(string s, int l, int r, int k)
    {

        // Store the size of the string
        int n = s.length();

        // Store the total number of 1s
        // and 0s in the entire string
        int tot_ones = 0, tot_zeros = 0;

        // Traverse the string S to find
        // the frequency of 1 and 0
        for (int i = 0; i < s.length(); i++)
        {
            if (s[i] == '1')
                tot_ones++;
            else
                tot_zeros++;
        }

        // Store the number of 1s and
        // 0s in the substring s[l, r]
        int ones = 0, zeros = 0, sum = 0;

        // Traverse the substring S[l, r]
        // to find the frequency of 1s
        // and 0s in it
        for (int i = l - 1; i < r; i++)
        {
            if (s[i] == '1')
            {
                ones++;
                sum++;
            }
            else
                zeros++;
        }

        // Store the count of 1s and
        // 0s outside substring s[l, r]
        int rem_ones = tot_ones - ones;
        int rem_zeros = tot_zeros - zeros;

        // Check if the sum of the
        // substring is at most K
        if (k >= sum)
        {

            // Store number of 1s required
            int rem = k - sum;

            // Check if there are enough 1s
            // remaining to be swapped
            if (zeros >= rem && rem_ones >= rem)
                return rem;
        }

        // If the count of 1s in the substring exceeds k
        else if (k < sum)
        {

            // Store the number of 0s required
            int rem = sum - k;

            // Check if there are enough 0s
            // remaining to be swapped
            if (ones >= rem && rem_zeros >= rem)
                return rem;
        }

        // In all other cases, print -1
        return -1;
    }

    // Driver Code
    int main()
    {
        string S = "110011111000101";
        int L = 5, R = 8, K = 2;
        cout<<minimumSwaps(S, L, R, K);
    }

// This code is contributed bgangwar59.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find the minimum number
    // of swaps required such that the
    // substring {s[l], .., s[r]} consists
    // of exactly k 1s
    static int minimumSwaps(
        String s, int l, int r, int k)
    {
        // Store the size of the string
        int n = s.length();

        // Store the total number of 1s
        // and 0s in the entire string
        int tot_ones = 0, tot_zeros = 0;

        // Traverse the string S to find
        // the frequency of 1 and 0
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '1')
                tot_ones++;
            else
                tot_zeros++;
        }

        // Store the number of 1s and
        // 0s in the substring s[l, r]
        int ones = 0, zeros = 0, sum = 0;

        // Traverse the substring S[l, r]
        // to find the frequency of 1s
        // and 0s in it
        for (int i = l - 1; i < r; i++) {
            if (s.charAt(i) == '1') {
                ones++;
                sum++;
            }
            else
                zeros++;
        }

        // Store the count of 1s and
        // 0s outside substring s[l, r]
        int rem_ones = tot_ones - ones;
        int rem_zeros = tot_zeros - zeros;

        // Check if the sum of the
        // substring is at most K
        if (k >= sum) {

            // Store number of 1s required
            int rem = k - sum;

            // Check if there are enough 1s
            // remaining to be swapped
            if (zeros >= rem && rem_ones >= rem)
                return rem;
        }

        // If the count of 1s in the substring exceeds k
        else if (k < sum) {

            // Store the number of 0s required
            int rem = sum - k;

            // Check if there are enough 0s
            // remaining to be swapped
            if (ones >= rem && rem_zeros >= rem)
                return rem;
        }

        // In all other cases, print -1
        return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "110011111000101";
        int L = 5, R = 8, K = 2;
        System.out.println(
            minimumSwaps(S, L, R, K));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# of swaps required such that the
# substring {s[l], .., s[r]} consists
# of exactly k 1s
def minimumSwaps(s, l, r, k) :

    # Store the size of the string
    n = len(s)

    # Store the total number of 1s
    # and 0s in the entire string
    tot_ones, tot_zeros = 0, 0

    # Traverse the string S to find
    # the frequency of 1 and 0
    for i in range(0, len(s)) :

        if (s[i] == '1') :
            tot_ones += 1
        else :
            tot_zeros += 1

    # Store the number of 1s and
    # 0s in the substring s[l, r]
    ones, zeros, Sum = 0, 0, 0

    # Traverse the substring S[l, r]
    # to find the frequency of 1s
    # and 0s in it
    for i in range(l - 1, r) :

        if (s[i] == '1') :

            ones += 1
            Sum += 1

        else :
            zeros += 1

    # Store the count of 1s and
    # 0s outside substring s[l, r]
    rem_ones = tot_ones - ones
    rem_zeros = tot_zeros - zeros

    # Check if the sum of the
    # substring is at most K
    if (k >= Sum) :

        # Store number of 1s required
        rem = k - Sum

        # Check if there are enough 1s
        # remaining to be swapped
        if (zeros >= rem and rem_ones >= rem) :
            return rem

    # If the count of 1s in the substring exceeds k
    elif (k < Sum) :

        # Store the number of 0s required
        rem = Sum - k

        # Check if there are enough 0s
        # remaining to be swapped
        if (ones >= rem and rem_zeros >= rem) :
            return rem

    # In all other cases, print -1
    return -1

S = "110011111000101"
L, R, K = 5, 8, 2
print(minimumSwaps(S, L, R, K))

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

  // Function to find the minimum number
  // of swaps required such that the
  // substring {s[l], .., s[r]} consists
  // of exactly k 1s
  static int minimumSwaps(string s, int l, int r, int k)
  {

    // Store the size of the string
    int n = s.Length;

    // Store the total number of 1s
    // and 0s in the entire string
    int tot_ones = 0, tot_zeros = 0;

    // Traverse the string S to find
    // the frequency of 1 and 0
    for (int i = 0; i < s.Length; i++)
    {
      if (s[i] == '1')
        tot_ones++;
      else
        tot_zeros++;
    }

    // Store the number of 1s and
    // 0s in the substring s[l, r]
    int ones = 0, zeros = 0, sum = 0;

    // Traverse the substring S[l, r]
    // to find the frequency of 1s
    // and 0s in it
    for (int i = l - 1; i < r; i++)
    {
      if (s[i] == '1')
      {
        ones++;
        sum++;
      }
      else
        zeros++;
    }

    // Store the count of 1s and
    // 0s outside substring s[l, r]
    int rem_ones = tot_ones - ones;
    int rem_zeros = tot_zeros - zeros;

    // Check if the sum of the
    // substring is at most K
    if (k >= sum)
    {

      // Store number of 1s required
      int rem = k - sum;

      // Check if there are enough 1s
      // remaining to be swapped
      if (zeros >= rem && rem_ones >= rem)
        return rem;
    }

    // If the count of 1s in the substring exceeds k
    else if (k < sum)
    {

      // Store the number of 0s required
      int rem = sum - k;

      // Check if there are enough 0s
      // remaining to be swapped
      if (ones >= rem && rem_zeros >= rem)
        return rem;
    }

    // In all other cases, print -1
    return -1;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    string S = "110011111000101";
    int L = 5, R = 8, K = 2;
    Console.Write(minimumSwaps(S, L, R, K));
  }
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to find the minimum number
// of swaps required such that the
// substring {s[l], .., s[r]} consists
// of exactly k 1s
function minimumSwaps(s , l , r , k)
{
    // Store the size of the string
    var n = s.length;

    // Store the total number of 1s
    // and 0s in the entire string
    var tot_ones = 0, tot_zeros = 0;

    // Traverse the string S to find
    // the frequency of 1 and 0
    for (i = 0; i < s.length; i++) {
        if (s.charAt(i) == '1')
            tot_ones++;
        else
            tot_zeros++;
    }

    // Store the number of 1s and
    // 0s in the substring s[l, r]
    var ones = 0, zeros = 0, sum = 0;

    // Traverse the substring S[l, r]
    // to find the frequency of 1s
    // and 0s in it
    for (var i = l - 1; i < r; i++) {
        if (s.charAt(i) == '1') {
            ones++;
            sum++;
        }
        else
            zeros++;
    }

    // Store the count of 1s and
    // 0s outside substring s[l, r]
    var rem_ones = tot_ones - ones;
    var rem_zeros = tot_zeros - zeros;

    // Check if the sum of the
    // substring is at most K
    if (k >= sum) {

        // Store number of 1s required
        var rem = k - sum;

        // Check if there are enough 1s
        // remaining to be swapped
        if (zeros >= rem && rem_ones >= rem)
            return rem;
    }

    // If the count of 1s in the substring exceeds k
    else if (k < sum) {

        // Store the number of 0s required
        var rem = sum - k;

        // Check if there are enough 0s
        // remaining to be swapped
        if (ones >= rem && rem_zeros >= rem)
            return rem;
    }

    // In all other cases, print -1
    return -1;
}

// Driver Code
var S = "110011111000101";
var L = 5, R = 8, K = 2;
document.write(
    minimumSwaps(S, L, R, K));

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)