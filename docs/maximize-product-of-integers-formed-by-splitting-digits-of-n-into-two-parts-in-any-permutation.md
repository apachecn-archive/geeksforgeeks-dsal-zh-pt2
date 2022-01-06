# 在任意排列中将 N 的数字分成两部分形成的整数乘积最大化

> 原文:[https://www . geeksforgeeks . org/通过将 n 位数字分成任意排列的两部分形成整数乘积最大化/](https://www.geeksforgeeks.org/maximize-product-of-integers-formed-by-splitting-digits-of-n-into-two-parts-in-any-permutation/)

给定一个在**【0，10】<sup>9</sup>**范围内的整数 **N** ，任务是找出两个整数的最大乘积，这两个整数是通过将整数 **N** 的数字的任意[排列](https://www.geeksforgeeks.org/permutation-coefficient/)分成两部分而形成的。

**示例:**

> **输入:** N = 123
> **输出:** 63
> **说明:**将 N = 123 分为 2 个整数的方式数为{12，3}、{21，3}、{13，2}、{31，2}、{23，1}和{32，1}。{21，3}的乘积是 63，这是所有可能性中的最大值。
> 
> **输入:**N = 101
> T3】输出: 10

**方法:**给定的问题可以通过使用基本的[排列和组合](https://www.geeksforgeeks.org/permutation-and-combination-gq/)借助于以下观察来解决:

*   将给定整数分成两部分的方法总数可以计算为*(可能排列的数量)*(划分排列的方法)* = > ***9！* 8***=>***2903040***。因此，所有可能的分离都可以迭代。
*   任何排列中的前导零也不会影响答案。

因此，可以使用[下一个置换函数](https://www.geeksforgeeks.org/stdnext_permutation-prev_permutation-c/)对当前整数的数字的所有置换进行迭代，并且对于每个置换，保持将置换划分到变量中的所有可能方式的最大乘积，这是所需的答案。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum product
// of integers formed by dividing any
// permutation of N into two parts.
int maxProduct(string N)
{
    // Stores the maximum product
    int ans = 0;

    // Sort the digits in the string
    sort(N.begin(), N.end());

    // Iterating over all permutaions
    do {

        // Loop to iterate over all
        // possible partitions
        for (int i = 1; i < N.size(); i++) {
            int l = 0, r = 0;

            // Calculate the left partition
            for (int j = 0; j < i; j++)
                l = l * 10 + N[j] - '0';

            // Calculate the right partition
            for (int j = i; j < N.size(); j++)
                r = r * 10 + N[j] - '0';

            // Update answer
            ans = max(ans, l * r);
        }
    } while (next_permutation(N.begin(), N.end()));

    // Return answer
    return ans;
}

// Driver code
int main()
{
    int N = 101;
    cout << maxProduct(to_string(N));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{
  static boolean next_permutation(char[] p) {
    for (int a = p.length - 2; a >= 0; --a)
      if (p[a] < p[a + 1])
        for (int b = p.length - 1;; --b)
          if (p[b] > p[a]) {
            char t = p[a];
            p[a] = p[b];
            p[b] = t;
            for (++a, b = p.length - 1; a < b; ++a, --b) {
              t = p[a];
              p[a] = p[b];
              p[b] = t;
            }
            return true;
          }
    return false;
  }

  // Function to find maximum product
  // of integers formed by dividing any
  // permutation of N into two parts.
  static int maxProduct(String a)
  {
    // Stores the maximum product
    int ans = 0;

    // Sort the digits in the String
    char []N = a.toCharArray();
    Arrays.sort(N);

    // Iterating over all permutaions
    do {

      // Loop to iterate over all
      // possible partitions
      for (int i = 1; i < N.length; i++) {
        int l = 0, r = 0;

        // Calculate the left partition
        for (int j = 0; j < i; j++)
          l = l * 10 + N[j] - '0';

        // Calculate the right partition
        for (int j = i; j < N.length; j++)
          r = r * 10 + N[j] - '0';

        // Update answer
        ans = Math.max(ans, l * r);
      }
    } while (next_permutation(N));

    // Return answer
    return ans;
  }

  // Driver code
  public static void main(String[] args)
  {
    int N = 101;
    System.out.print(maxProduct(String.valueOf(N)));
  }
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function for next permutation
def next_permutation(arr):

    # Find the length of the array
    n = len(arr)

    # Start from the right most digit and
    # find the first digit that is smaller
    # than the digit next to it.
    k = n - 2
    while k >= 0:
        if arr[k] < arr[k + 1]:
            break

        k -= 1

    # Reverse the list if the digit that
    # is smaller than the digit next to
    # it is not found.
    if k < 0:
        arr = arr[::-1]
    else:

        # Find the first greatest element
        # than arr[k] from the end of the list
        for l in range(n - 1, k, -1):
            if arr[l] > arr[k]:
                break

        # Swap the elements at arr[k] and arr[l
        arr[l], arr[k] = arr[k], arr[l]

        # Reverse the list from k + 1 to the end
        # to find the most nearest greater number
        # to the given input number
        arr[k + 1:] = reversed(arr[k + 1:])

    return arr

# Function to find maximum product
# of integers formed by dividing any
# permutation of N into two parts.
def maxProduct(N):

    # Stores the maximum product
    ans = 0

    # Sort the digits in the string
    Nstr = sorted(N)
    Instr = sorted(N)

    # Iterating over all permutaions
    while next_permutation(Nstr) != Instr:

        # Loop to iterate over all
        # possible partitions
        for i in range(len(Nstr)):
            l = 0
            r = 0

            # Calculate the left partition
            for j in range(0, i):
                l = l * 10 + ord(N[j]) - ord('0')

            # Calculate the right partition
            for j in range(i, len(Nstr)):
                r = r * 10 + ord(N[j]) - ord('0')

            # Update answer
            ans = max(ans, l * r)

    # Return answe
    return ans

# Driver code
N = 101

print(maxProduct(str(N)))

# This code is contributed by Potta Lokesh
```

## C#

```
// C# implementation of the above approach
using System;

class GFG {
  static bool next_permutation(char[] p)
  {
    for (int a = p.Length - 2; a >= 0; --a)
      if (p[a] < p[a + 1])
        for (int b = p.Length - 1;; --b)
          if (p[b] > p[a]) {
            char t = p[a];
            p[a] = p[b];
            p[b] = t;
            for (++a, b = p.Length - 1; a < b;
                 ++a, --b) {
              t = p[a];
              p[a] = p[b];
              p[b] = t;
            }
            return true;
          }
    return false;
  }

  // Function to find maximum product
  // of integers formed by dividing any
  // permutation of N into two parts.
  static int maxProduct(string a)
  {
    // Stores the maximum product
    int ans = 0;

    // Sort the digits in the String
    char[] N = a.ToCharArray();
    Array.Sort(N);

    // Iterating over all permutaions
    do {

      // Loop to iterate over all
      // possible partitions
      for (int i = 1; i < N.Length; i++) {
        int l = 0, r = 0;

        // Calculate the left partition
        for (int j = 0; j < i; j++)
          l = l * 10 + N[j] - '0';

        // Calculate the right partition
        for (int j = i; j < N.Length; j++)
          r = r * 10 + N[j] - '0';

        // Update answer
        ans = Math.Max(ans, l * r);
      }
    } while (next_permutation(N));

    // Return answer
    return ans;
  }

  // Driver code
  public static void Main(string[] args)
  {
    int N = 101;
    Console.Write(maxProduct(N.ToString()));
  }
}

// This code is contributed by ukasp.
```

**Output**

```
10
```

***时间复杂度:** O((log N)！* log N)*
***辅助空间:** O(1)*