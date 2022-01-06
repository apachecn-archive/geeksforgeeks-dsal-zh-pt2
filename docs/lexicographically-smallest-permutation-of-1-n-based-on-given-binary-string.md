# 基于给定二进制字符串的[1，N]的字典最小排列

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的基于给定二进制字符串的最小 1-n 排列/](https://www.geeksforgeeks.org/lexicographically-smallest-permutation-of-1-n-based-on-given-binary-string/)

给定一个大小为**(N–1)**的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找到第一个 **N** [自然数](https://www.geeksforgeeks.org/natural-numbers/)的[字典上最小的排列](https://www.geeksforgeeks.org/find-smallest-permutation-given-number/) **P** ，这样对于每个索引 **i** ，如果**S【I】**等于“ **0** ，那么**P【I+1】**

**示例:**

> **输入:** N = 7， *S = 1* 00101
> **输出:** 2 1 3 5 4 7 6
> **解释:**
> 将满足给定标准的排列视为{2，1，3，5，4，7，6}，如:
> 对于索引 0，S[0] = 1，P[1] < P[0]，即 1 < S[2] = 0，P[3] < P[2]，即 5 > 3
> 对于指数 3，S[3] = 1，P[4] < P[3]，即 4 < 5
> 对于指数 4，S[4] = 0，P[5] < P[4]，即 7 > 4
> 对于指数 5，S[5] = 1，P[6] <
> 
> **输入:** N = 4，S = 000
> T3】输出: 1 2 3 4

**方法:**给定的问题可以通过使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决，通过尽可能在较低的索引处使用较小的数字，将创建字典序上最小的排列。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，比如说**和**的大小 **N** ，存储结果[排列](https://www.geeksforgeeks.org/permutation-and-combination/)。
*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，并执行以下步骤:
    *   如果 **S[i]** 的值等于“ **0** ，则分配比最后分配的号码大的号码。
    *   否则，分配比当前使用的所有数字都大的最小数字。
*   完成上述步骤后，打印数组**和**中形成的结果排列。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to generate the lexicographically
// smallest permutation according to the
// given criteria
void constructPermutation(string S, int N)
{
    // Stores the resultant permutation
    int ans[N];

    // Initialize the first elements to 1
    ans[0] = 1;

    // Traverse the given string S
    for (int i = 1; i < N; ++i) {
        if (S[i - 1] == '0') {

            // Number greater than last
            // number
            ans[i] = i + 1;
        }
        else {
            // Number equal to the last
            // number
            ans[i] = ans[i - 1];
        }

        // Correct all numbers to the left
        // of the current index
        for (int j = 0; j < i; ++j) {
            if (ans[j] >= ans[i]) {
                ans[j]++;
            }
        }
    }

    // Printing the permutation
    for (int i = 0; i < N; i++) {
        cout << ans[i];
        if (i != N - 1) {
            cout << " ";
        }
    }
}

// Driver Code
int main()
{
    string S = "100101";
    constructPermutation(S, S.length() + 1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to generate the lexicographically
    // smallest permutation according to the
    // given criteria
    static void constructPermutation(String S, int N)
    {

        // Stores the resultant permutation
        int[] ans = new int[N];

        // Initialize the first elements to 1
        ans[0] = 1;

        // Traverse the given string S
        for (int i = 1; i < N; ++i) {
            if (S.charAt(i - 1) == '0') {

                // Number greater than last
                // number
                ans[i] = i + 1;
            }
            else {
                // Number equal to the last
                // number
                ans[i] = ans[i - 1];
            }

            // Correct all numbers to the left
            // of the current index
            for (int j = 0; j < i; ++j) {
                if (ans[j] >= ans[i]) {
                    ans[j]++;
                }
            }
        }

        // Printing the permutation
        for (int i = 0; i < N; i++) {
            System.out.print(ans[i]);
            if (i != N - 1) {
                System.out.print(" ");
            }
        }
    }

    // Driver Code
    public static void main(String[] args) {

        String S = "100101";
        constructPermutation(S, S.length() + 1);
    }
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to generate the lexicographically
# smallest permutation according to the
# given criteria
def constructPermutation(S, N):

    # Stores the resultant permutation
    ans = [0] * N

    # Initialize the first elements to 1
    ans[0] = 1

    # Traverse the given string S
    for i in range(1, N):
        if (S[i - 1] == '0'):

            # Number greater than last
            # number
            ans[i] = i + 1
        else :
            # Number equal to the last
            # number
            ans[i] = ans[i - 1]

        # Correct all numbers to the left
        # of the current index
        for j in range(i):
            if (ans[j] >= ans[i]):
                ans[j] += 1

    # Printing the permutation
    for i in range(N):
        print(ans[i], end="")
        if (i != N - 1):
            print(" ", end="")

# Driver Code
S = "100101"
constructPermutation(S, len(S) + 1)

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to generate the lexicographically
    // smallest permutation according to the
    // given criteria
    static void constructPermutation(string S, int N)
    {

        // Stores the resultant permutation
        int[] ans = new int[N];

        // Initialize the first elements to 1
        ans[0] = 1;

        // Traverse the given string S
        for (int i = 1; i < N; ++i) {
            if (S[i - 1] == '0') {

                // Number greater than last
                // number
                ans[i] = i + 1;
            }
            else {
                // Number equal to the last
                // number
                ans[i] = ans[i - 1];
            }

            // Correct all numbers to the left
            // of the current index
            for (int j = 0; j < i; ++j) {
                if (ans[j] >= ans[i]) {
                    ans[j]++;
                }
            }
        }

        // Printing the permutation
        for (int i = 0; i < N; i++) {
            Console.Write(ans[i]);
            if (i != N - 1) {
                Console.Write(" ");
            }
        }
    }

    // Driver Code
    public static void Main()
    {
        string S = "100101";
        constructPermutation(S, S.Length + 1);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to generate the lexicographically
        // smallest permutation according to the
        // given criteria
        function constructPermutation(S, N) {
            // Stores the resultant permutation
            let ans = new Array(N);

            // Initialize the first elements to 1
            ans[0] = 1;

            // Traverse the given string S
            for (let i = 1; i < N; ++i) {
                if (S[i - 1] == '0') {

                    // Number greater than last
                    // number
                    ans[i] = i + 1;
                }
                else {
                    // Number equal to the last
                    // number
                    ans[i] = ans[i - 1];
                }

                // Correct all numbers to the left
                // of the current index
                for (let j = 0; j < i; ++j) {
                    if (ans[j] >= ans[i]) {
                        ans[j]++;
                    }
                }
            }

            // Printing the permutation
            for (let i = 0; i < N; i++) {
                document.write(ans[i]);
                if (i != N - 1) {
                    document.write(" ");
                }
            }
        }

        // Driver Code

        let S = "100101";
        constructPermutation(S, S.length + 1);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
2 1 3 5 4 7 6
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*