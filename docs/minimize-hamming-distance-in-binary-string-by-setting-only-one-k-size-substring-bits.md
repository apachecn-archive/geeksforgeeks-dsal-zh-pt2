# 通过仅设置一个 K 大小的子串位来最小化二进制字符串中的汉明距离

> 原文:[https://www . geeksforgeeks . org/minimum-hamming-distance-in-binary-string-by-set-only-one-k-size-substring-bits/](https://www.geeksforgeeks.org/minimize-hamming-distance-in-binary-string-by-setting-only-one-k-size-substring-bits/)

给定两个长度为 **N** 的二进制[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和 **T** 以及一个正整数 **K** 。最初 **T** 的所有字符都是**‘0’**。任务是在选择一个大小为 **K** 的[子串](https://www.geeksforgeeks.org/substring-in-cpp/)并将[串](https://www.geeksforgeeks.org/string-data-structure/) **T** 的所有元素只做一次**【1】后，找到最小[汉明距离](https://www.geeksforgeeks.org/hamming-distance-two-strings/)。**

****示例:****

> ****输入:**S =“101”，K = 2
> **输出:** 1
> **说明:**最初字符串 T =“000”，一种可能的方法是将范围[0，1]内的所有 0 都改为 1。因此，字符串 T 变成“110”，S 和 T 之间的汉明距离是 2，这是最小可能的。**
> 
> ****输入:**S =“1100”，K = 3
> T3】输出: 1**

****天真法:**最简单的方法是考虑大小为 **K** 的每个[子串](https://www.geeksforgeeks.org/substring-in-cpp/)，将所有元素设为 1，然后用字符串 **S** 检查汉明距离。检查完所有子字符串后，打印最小汉明距离。**

*****时间复杂度:** O(N×K)*
***辅助空间:** O(1)***

****方法:**这个问题可以通过[创建前缀数组和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)来解决，该前缀数组和将 1 的计数的前缀和存储在[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 中。按照以下步骤解决问题:**

*   **通过将 **pref[0]** 初始化为 **0** 将 **pref[i]** 更新为**pref[I-1]+(S[I]–‘0’)**为每个索引 **i** ，创建[字符串](https://www.geeksforgeeks.org/string-data-structure/)T6】S 的[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) **pref[]** 。**
*   **将字符串中 1 的总数 **S** 存储在变量 **cnt** 中。**
*   **将变量**和**初始化为 **cnt** 来存储所需的结果。**
*   **[使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-K】**中迭代

    *   将变量**值**初始化为**pref[I+K-1]–pref[I-1]**，以存储子串 **S[i，i+K-1]** 中的 1 的计数。
    *   创建两个变量 **A** 和 **B** 来存储当前子串外部的汉明距离和当前子串内部的汉明距离，并用**CNT–K**初始化 **A** ，用**K–val**初始化 **B** 。
    *   用 **ans** 和 **(A + B)** 的最小值更新 **ans** 的值。** 
*   **打印**和**的值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum Hamming
// Distance after atmost one operation
int minimumHammingDistance(string S, int K)
{
    // Store the size of the string
    int n = S.size();

    // Store the prefix sum of 1s
    int pref[n];

    // Create Prefix Sum array
    pref[0] = S[0] - '0';
    for (int i = 1; i < n; i++)
        pref[i] = pref[i - 1] + (S[i] - '0');

    // Initialize cnt as number of ones
    // in string S
    int cnt = pref[n - 1];

    // Store the required result
    int ans = cnt;

    // Traverse the string, S
    for (int i = 0; i < n - K; i++) {

        // Store the number of 1s in the
        // substring S[i, i+K-1]
        int value = pref[i + K - 1]
                    - (i - 1 >= 0 ? pref[i - 1] : 0);

        // Update the answer
        ans = min(ans, cnt - value + (K - value));
    }

    // Return the result
    return ans;
}

// Driver Code
int main()
{

    // Given Input
    string s = "101";
    int K = 2;

    // Function Call
    cout << minimumHammingDistance(s, K);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
public class GFG
{

// Function to find minimum Hamming
// Distance after atmost one operation
static int minimumHammingDistance(String S, int K)
{

    // Store the size of the string
    int n = S.length();

    // Store the prefix sum of 1s
    int []pref =  new int [n];

    // Create Prefix Sum array
    pref[0] = S.charAt(0) - '0';
    for (int i = 1; i < n; i++)
        pref[i] = pref[i - 1] + (S.charAt(i) - '0');

    // Initialize cnt as number of ones
    // in string S
    int cnt = pref[n - 1];

    // Store the required result
    int ans = cnt;

    // Traverse the string, S
    for (int i = 0; i < n - K; i++) {

        // Store the number of 1s in the
        // substring S[i, i+K-1]
        int value = pref[i + K - 1] - (i - 1 >= 0 ? pref[i - 1] : 0);

        // Update the answer
        ans = Math.min(ans, cnt - value + (K - value));
    }

    // Return the result
    return ans;
}

// Driver Code
public static void main(String args[])
{
    // Given Input
    String s = "101";
    int K = 2;

    // Function Call
    System.out.println(minimumHammingDistance(s, K));
    }
}

// This code is contributed by SoumikMondal
```

## **蟒蛇 3**

```
# Py program for the above approach

# Function to find minimum Hamming
# Distance after atmost one operation
def minimumHammingDistance(S, K):
    # Store the size of the string
    n = len(S)

    # Store the prefix sum of 1s
    pref = [0] * n

    # Create Prefix Sum array
    pref[0] = ord(S[0]) - ord('0')
    for i in range(1,n):
        pref[i] = pref[i - 1] + (ord(S[i]) - ord('0'))

    # Initialize cnt as number of ones
    # in string S
    cnt = pref[n - 1]

    # Store the required result
    ans = cnt

    # Traverse the string, S
    for i in range(n - K):

        # Store the number of 1s in the
        # substring S[i, i+K-1]
        value = pref[i + K - 1] - (pref[i-1] if (i - 1) >= 0 else 0)

        # Update the answer
        ans = min(ans, cnt - value + (K - value))

    # Return the result
    return ans

# Driver Code
if __name__ == '__main__':

    # Given Input
    s = "101"
    K = 2

    # Function Call
    print (minimumHammingDistance(s, K))

# This code is contributed by mohit kumar 29.
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find minimum Hamming
// Distance after atmost one operation
static int minimumHammingDistance(string S, int K)
{

    // Store the size of the string
    int n = S.Length;

    // Store the prefix sum of 1s
    int []pref =  new int [n];

    // Create Prefix Sum array
    pref[0] = (int)S[0] - 48;
    for (int i = 1; i < n; i++)
        pref[i] = pref[i - 1] + ((int)S[i] - 48);

    // Initialize cnt as number of ones
    // in string S
    int cnt = pref[n - 1];

    // Store the required result
    int ans = cnt;

    // Traverse the string, S
    for (int i = 0; i < n - K; i++) {

        // Store the number of 1s in the
        // substring S[i, i+K-1]
        int value = pref[i + K - 1] - (i - 1 >= 0 ? pref[i - 1] : 0);

        // Update the answer
        ans = Math.Min(ans, cnt - value + (K - value));
    }

    // Return the result
    return ans;
}

// Driver Code
public static void Main()
{
    // Given Input
    string s = "101";
    int K = 2;

    // Function Call
     Console.Write(minimumHammingDistance(s, K));
    }
}

// This code is contributed by SURENDRA_GANGWAR.
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

// Function to find minimum Hamming
// Distance after atmost one operation
function minimumHammingDistance(S, K)
{

    // Store the size of the string
    let n = S.length;

    // Store the prefix sum of 1s
    let pref =  new Array(n);

    // Create Prefix Sum array
    pref[0] = S[0] - '0';
    for (let i = 1; i < n; i++)
        pref[i] = pref[i - 1] + (S[i] - '0');

    // Initialize cnt as number of ones
    // in string S
    let cnt = pref[n - 1];

    // Store the required result
    let ans = cnt;

    // Traverse the string, S
    for (let i = 0; i < n - K; i++) {

        // Store the number of 1s in the
        // substring S[i, i+K-1]
        let value = pref[i + K - 1] - (i - 1 >= 0 ? pref[i - 1] : 0);

        // Update the answer
        ans = Math.min(ans, cnt - value + (K - value));
    }

    // Return the result
    return ans;
}

// Driver Code

    // Given Input
    let s = "101";
    let K = 2;

    // Function Call
    document.write(minimumHammingDistance(s, K));

</script>
```

****Output**

```
2
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**