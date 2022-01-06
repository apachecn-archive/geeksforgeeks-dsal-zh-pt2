# 计算将一个字符串拆分成两个彼此相反的子集的方法

> 原文:[https://www . geeksforgeeks . org/count-way-to-split-a-string-to-two-subset-相互反向/](https://www.geeksforgeeks.org/count-ways-to-split-a-string-into-two-subsets-that-are-reverse-of-each-other/)

给定一个由 **N** 个字符组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找出将该字符串拆分为两个子集的方法，使得第一个子集与第二个子集相反。

**示例:**

> **输入:** S =【卡巴克巴】
> **输出:** 4
> **说明:**
> 下面是满足给定条件的字符串的划分方式:
> 
> 1.  将索引{0，4，6，7}处的字符作为第一个子集，其余字符作为第二个子集。然后形成的字符串是“caba”和“abac”，第二个字符串是第一个字符串的反义词。
> 2.  将索引{0，3，6，7}处的字符作为第一个子集，剩余的字符作为第二个子集。然后形成的字符串是“caba”和“abac”，第二个字符串是第一个字符串的反义词。
> 3.  将索引{1，2，3，5}处的字符作为第一个子集，剩余的字符作为第二个子集。然后形成的字符串是“abac”和“caba”，第二个字符串是第一个字符串的反义词。
> 4.  将索引{1，2，4，5}处的字符作为第一个子集，剩余的字符作为第二个子集。然后形成的字符串是“abac”和“caba”，第二个字符串是第一个字符串的反义词。
> 
> 因此，拆分的方式数为 4。
> 
> **输入:** N = 11，S =
> 输出: 504

**方法:**给定的问题可以通过使用[位屏蔽](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)的概念来解决，以生成所有可能的分裂字符串的方式，并检查是否存在任何这种彼此相反的字符串分裂。按照以下步骤解决问题:

*   初始化一个变量，说 **ans** 为 **0** 来存储字符串的分区方式总数。
*   [使用变量**掩码**迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，2<sup>N</sup>**，并执行以下步骤:
    *   初始化两个字符串说 **X** 和 **Y** 存储第一子集和第二子集的字符。
    *   迭代范围**【0，N】**，如果整数**掩码**中的 **i <sup>第</sup>位**为[设置](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)，则将字符**S【I】**追加到 **X** 中。否则将字符 **S[i]** 附加到 **Y** 上。
    *   [反转弦](https://www.geeksforgeeks.org/reverse-a-string-in-c-cpp-different-methods/) **Y** 然后检查第一弦 **X** 是否等于第二弦 **Y** 然后将 **ans** 增加 **1** 。
*   完成上述步骤后，打印**和**的值作为总路数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the total number
// of ways to partitiaon the string into
// two subset satisfying the conditions
int countWays(string S, int N)
{
    // Stores the resultant number of
    // ways of splitting
    int ans = 0;

    // Iterate over the range [0, 2^N]
    for (int mask = 0;
         mask < (1 << N); mask++) {

        string X, Y;

        // Traverse the string S
        for (int i = 0; i < N; i++) {

            // If ith bit is set, then
            // append the character
            // S[i] to X
            if (mask >> i & 1) {
                X += S[i];
            }

            // Otherwise, append the
            // character S[i] to Y
            else {
                Y += S[i];
            }
        }

        // Reverse the second string
        reverse(Y.begin(), Y.end());

        // If X is equal to Y
        if (X == Y) {
            ans++;
        }
    }

    // Return the total number of ways
    return ans;
}

// Driver Code
int main()
{
    string S = "mippiisssisssiipsspiim";
    int N = S.length();
    cout << countWays(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.io.*;
import java.util.*;

class GFG {

    // Function to find the total number
    // of ways to partitiaon the String into
    // two subset satisfying the conditions
    static int countWays(String S, int N)
    {
        // Stores the resultant number of
        // ways of splitting
        int ans = 0;

        // Iterate over the range [0, 2^N]
        for (int mask = 0;
             mask < (1 << N); mask++) {

            String X="" , Y="";

            // Traverse the String S
            for (int i = 0; i < N; i++) {

                // If ith bit is set, then
                // append the character
                // S[i] to X
                if ((mask >> i & 1) == 1) {
                    X += S.charAt(i);
                }

                // Otherwise, append the
                // character S[i] to Y
                else {
                    Y += S.charAt(i);
                }
            }

            // Reverse the second String
            Y = new StringBuilder(Y).reverse().toString();
            // If X is equal to Y
            if (X.equals(Y)) {
                ans++;
            }
        }

        // Return the total number of ways
        return ans;
    }

    // Driver Code
    public static void main (String[] args)
    {
        String S = "mippiisssisssiipsspiim";
        int N = S.length();
        System.out.println(countWays(S, N));
    }
}

// This code is contributed by shubhamsingh10
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the total number
# of ways to partitiaon the string into
# two subset satisfying the conditions
def countWays(S, N):

    # Stores the resultant number of
    # ways of splitting
    ans = 0

    # Iterate over the range [0, 2^N]
    for mask in range((1 << N)):
        X, Y = "",""

        # Traverse the string S
        for i in range(N):

            # If ith bit is set, then
            # append the character
            # S[i] to X
            if (mask >> i & 1):
                X += S[i]

            # Otherwise, append the
            # character S[i] to Y
            else:
                Y += S[i]

        # Reverse the second string
        Y = Y[::-1]

        # If X is equal to Y
        if (X == Y):
            ans += 1

    # Return the total number of ways
    return ans

# Driver Code
if __name__ == '__main__':

    S = "mippiisssisssiipsspiim"
    N = len(S)

    print(countWays(S, N))

# This code is contributed by mohit kumar 29
```

**Output:** 

```
504
```

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(N)*