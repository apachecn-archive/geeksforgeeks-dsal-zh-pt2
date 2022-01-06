# 最大限度地减少 K 值以下的替换，使两个给定数组的和相等

> 原文:[https://www . geesforgeks . org/minimum-replacements-with-values-up-k-to-make-sum-of-two-给定数组-equal/](https://www.geeksforgeeks.org/minimize-replacements-with-values-up-to-k-to-make-sum-of-two-given-arrays-equal/)

给定一个正整数 **K** 和两个分别由范围**【1，K】**中的正整数 **M** 和 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **A[]** 和 **B[]** ，任务是将数组元素被范围**【1，K】**中的值替换的次数减到最少，使得两个数组的元素之和[变为如果无法使总和相等，则打印 **-1** 。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** K = 6，A[] = {3，4，1}，B[] = {6，6，6}
> **输出:** 2
> **解释:**
> 一种可能的方法是在两次移动中用 1 替换索引 0 和 1 处数组 B[]的元素。因此，数组 B[]修改为{1，1，6}。
> 现在两个数组的和是 8，相等。
> 
> **输入:** A[] = {4，3，2}，B[] = {2，3，3，1}，K = 6，N = 4，M = 3
> **输出:** 0

**方法:**给定的问题可以使用[两点技巧](https://www.geeksforgeeks.org/two-pointers-technique/)来解决。按照以下步骤解决问题:

*   初始化 4 个变量，比如 **l1 = 0，R1 = M–1，l2 = 0，R2 = N–1**，用来[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
*   初始化一个变量，比如 **res** ，以存储所需的最小替换次数。
*   [按升序排列两个给定的数组](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)。
*   找出两个数组之和[的差值，并将其存储在一个变量中，比如**差值**。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   重复至 **l1 ≤ r1** 或 **l2 ≤ r2** 并执行以下步骤:
    *   **如果 diff = 0:** [跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
    *   **如果 diff 超过 0:** 取**(A[R1]–1)**和**(K–B[L2])**之间的最大值，从差值 **diff** 中减去，如果**(K–B[L2])**的值更大，则增加 **l2** 。否则，将 **r1** 减 1。
    *   否则，取**(B[R2]–1)****(K–A[L1])**之间的最大值，加到差 **diff** 上，如果**(K–A[L1])**更大，则增加 **l1** 。否则，将 **r2** 的值递减 **1** 。
    *   将 **res** 的值增加 **1** 。
*   完成上述步骤后，打印 **res** 的值，作为所需数组元素的最小替换次数。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum number
// of replacements required to make
// the sum of two arrays equal
int makeSumEqual(vector<int> a, vector<int> b,
                 int K, int M, int N)
{

  // Stores the sum of a[]
  int sum1 = 0;

  // Stores the sum of b[]
  int sum2 = 0;

  // Calculate sum of the array a[]
  for (int el : a)
    sum1 += el;

  // Calculate sum of the array b[]
  for (int el : b)
    sum2 += el;

  // Stores the difference
  // between a[] and b[]
  int diff = sum1 - sum2;

  // Left and Right pointer
  // to traverse the array a[]
  int l1 = 0, r1 = M - 1;

  // Left and Right pointer
  // to traverse the array b[]
  int l2 = 0, r2 = N - 1;

  // Stores the count of moves
  int res = 0;

  // Sort the arrays in
  // ascending order
  sort(a.begin(),a.end());
  sort(b.begin(),b.end());

  // Iterate while diff != 0 and
  // l1 <= r1 or l2 <= r2
  while (l1 <= r1 || l2 <= r2)
  {
    if (diff == 0)
    {
      break;
    }

    // If diff is greater than 0
    if (diff > 0)
    {

      // If all pointers are valid
      if (l2 <= r2 && l1 <= r1)
      {

        if (K - b[l2] < a[r1] - 1) {

          int sub = min(
            a[r1] - 1, diff);
          diff -= sub;
          a[r1] -= sub;
          r1--;
        }
        else {

          int sub = min(
            K - b[l2], diff);
          diff -= sub;
          b[l2] += sub;
          l2++;
        }
      }

      // Otherwise, if only pointers
      // of array a[] is valid
      else if (l1 <= r1) {

        int sub = min(
          a[r1] - 1, diff);
        diff -= sub;
        a[r1] -= sub;
        r1--;
      }

      // Otherwise
      else {

        int sub = min(
          K - b[l2], diff);
        diff -= sub;
        b[l2] += sub;
        l2++;
      }
    }

    // If diff is less than 0
    else {

      // If all pointers are valid
      if (l1 <= r1 && l2 <= r2) {
        if (K - a[l1]
            < b[r2] - 1) {

          int sub = min(
            b[r2] - 1,
            -1 * diff);
          diff += sub;
          b[r2] -= sub;
          r2--;
        }

        else {

          int sub = min(
            K - a[l1],
            -1 * diff);
          diff += sub;
          a[l1] -= sub;
          l1++;
        }
      }

      // Otherwise, if only pointers
      // of array a[] is valid
      else if (l2 <= r2) {

        int sub
          = min(
          b[r2] - 1,
          -1 * diff);
        diff += sub;
        b[r2] -= sub;
        r2--;
      }

      // Otherwise
      else {

        int sub = min(
          K - a[l1], diff);
        diff += sub;
        a[l1] += sub;
        l1++;
      }
    }

    // Increment count
    // of res by one
    res++;
  }

  // If diff is 0, then return res
  if (diff == 0)
    return res;

  // Otherwise, return -1
  else
    return -1;
}

// Driver Code
int main()
{
  vector<int> A = { 1, 4, 3 };
  vector<int> B = { 6, 6, 6 };
  int M = A.size();
  int N = B.size();
  int K = 6;

  cout << makeSumEqual(A, B, K,M, N);

  return 0;
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find minimum number
    // of replacements required to make
    // the sum of two arrays equal
    public static int makeSumEqual(
        int[] a, int[] b, int K,
        int M, int N)
    {
        // Stores the sum of a[]
        int sum1 = 0;

        // Stores the sum of b[]
        int sum2 = 0;

        // Calculate sum of the array a[]
        for (int el : a)
            sum1 += el;

        // Calculate sum of the array b[]
        for (int el : b)
            sum2 += el;

        // Stores the difference
        // between a[] and b[]
        int diff = sum1 - sum2;

        // Left and Right pointer
        // to traverse the array a[]
        int l1 = 0, r1 = M - 1;

        // Left and Right pointer
        // to traverse the array b[]
        int l2 = 0, r2 = N - 1;

        // Stores the count of moves
        int res = 0;

        // Sort the arrays in
        // ascending order
        Arrays.sort(a);
        Arrays.sort(b);

        // Iterate while diff != 0 and
        // l1 <= r1 or l2 <= r2
        while (l1 <= r1 || l2 <= r2) {
            if (diff == 0) {

                break;
            }

            // If diff is greater than 0
            if (diff > 0) {

                // If all pointers are valid
                if (l2 <= r2 && l1 <= r1) {

                    if (K - b[l2] < a[r1] - 1) {

                        int sub = Math.min(
                            a[r1] - 1, diff);
                        diff -= sub;
                        a[r1] -= sub;
                        r1--;
                    }
                    else {

                        int sub = Math.min(
                            K - b[l2], diff);
                        diff -= sub;
                        b[l2] += sub;
                        l2++;
                    }
                }

                // Otherwise, if only pointers
                // of array a[] is valid
                else if (l1 <= r1) {

                    int sub = Math.min(
                        a[r1] - 1, diff);
                    diff -= sub;
                    a[r1] -= sub;
                    r1--;
                }

                // Otherwise
                else {

                    int sub = Math.min(
                        K - b[l2], diff);
                    diff -= sub;
                    b[l2] += sub;
                    l2++;
                }
            }

            // If diff is less than 0
            else {

                // If all pointers are valid
                if (l1 <= r1 && l2 <= r2) {
                    if (K - a[l1]
                        < b[r2] - 1) {

                        int sub = Math.min(
                            b[r2] - 1,
                            -1 * diff);
                        diff += sub;
                        b[r2] -= sub;
                        r2--;
                    }

                    else {

                        int sub = Math.min(
                            K - a[l1],
                            -1 * diff);
                        diff += sub;
                        a[l1] -= sub;
                        l1++;
                    }
                }

                // Otherwise, if only pointers
                // of array a[] is valid
                else if (l2 <= r2) {

                    int sub
                        = Math.min(
                            b[r2] - 1,
                            -1 * diff);
                    diff += sub;
                    b[r2] -= sub;
                    r2--;
                }

                // Otherwise
                else {

                    int sub = Math.min(
                        K - a[l1], diff);
                    diff += sub;
                    a[l1] += sub;
                    l1++;
                }
            }

            // Increment count
            // of res by one
            res++;
        }

        // If diff is 0, then return res
        if (diff == 0)
            return res;

        // Otherwise, return -1
        else
            return -1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] A = { 1, 4, 3 };
        int[] B = { 6, 6, 6 };
        int M = A.length;
        int N = B.length;
        int K = 6;

        System.out.println(
            makeSumEqual(A, B, K,
                         M, N));
    }
}
```

## C#

```
// C# program to implement
// the above approach
using System;

public class GFG
{

    // Function to find minimum number
    // of replacements required to make
    // the sum of two arrays equal
    public static int makeSumEqual(
        int[] a, int[] b, int K,
        int M, int N)
    {

        // Stores the sum of a[]
        int sum1 = 0;

        // Stores the sum of b[]
        int sum2 = 0;

        // Calculate sum of the array a[]
        foreach (int el in a)
            sum1 += el;

        // Calculate sum of the array b[]
        foreach (int el in b)
            sum2 += el;

        // Stores the difference
        // between a[] and b[]
        int diff = sum1 - sum2;

        // Left and Right pointer
        // to traverse the array a[]
        int l1 = 0, r1 = M - 1;

        // Left and Right pointer
        // to traverse the array b[]
        int l2 = 0, r2 = N - 1;

        // Stores the count of moves
        int res = 0;

        // Sort the arrays in
        // ascending order
        Array.Sort(a);
        Array.Sort(b);

        // Iterate while diff != 0 and
        // l1 <= r1 or l2 <= r2
        while (l1 <= r1 || l2 <= r2) {
            if (diff == 0) {

                break;
            }

            // If diff is greater than 0
            if (diff > 0) {

                // If all pointers are valid
                if (l2 <= r2 && l1 <= r1) {

                    if (K - b[l2] < a[r1] - 1) {

                        int sub = Math.Min(
                            a[r1] - 1, diff);
                        diff -= sub;
                        a[r1] -= sub;
                        r1--;
                    }
                    else {

                        int sub = Math.Min(
                            K - b[l2], diff);
                        diff -= sub;
                        b[l2] += sub;
                        l2++;
                    }
                }

                // Otherwise, if only pointers
                // of array a[] is valid
                else if (l1 <= r1) {

                    int sub = Math.Min(
                        a[r1] - 1, diff);
                    diff -= sub;
                    a[r1] -= sub;
                    r1--;
                }

                // Otherwise
                else {

                    int sub = Math.Min(
                        K - b[l2], diff);
                    diff -= sub;
                    b[l2] += sub;
                    l2++;
                }
            }

            // If diff is less than 0
            else {

                // If all pointers are valid
                if (l1 <= r1 && l2 <= r2) {
                    if (K - a[l1]
                        < b[r2] - 1) {

                        int sub = Math.Min(
                            b[r2] - 1,
                            -1 * diff);
                        diff += sub;
                        b[r2] -= sub;
                        r2--;
                    }

                    else {

                        int sub = Math.Min(
                            K - a[l1],
                            -1 * diff);
                        diff += sub;
                        a[l1] -= sub;
                        l1++;
                    }
                }

                // Otherwise, if only pointers
                // of array a[] is valid
                else if (l2 <= r2) {

                    int sub
                        = Math.Min(
                            b[r2] - 1,
                            -1 * diff);
                    diff += sub;
                    b[r2] -= sub;
                    r2--;
                }

                // Otherwise
                else {

                    int sub = Math.Min(
                        K - a[l1], diff);
                    diff += sub;
                    a[l1] += sub;
                    l1++;
                }
            }

            // Increment count
            // of res by one
            res++;
        }

        // If diff is 0, then return res
        if (diff == 0)
            return res;

        // Otherwise, return -1
        else
            return -1;
    }

// Driver Code
public static void Main(String[] args)
{
    int[] A = { 1, 4, 3 };
        int[] B = { 6, 6, 6 };
        int M = A.Length;
        int N = B.Length;
        int K = 6;

        Console.WriteLine(
            makeSumEqual(A, B, K,
                         M, N));
}
}
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find minimum number
// of replacements required to make
// the sum of two arrays equal
function makeSumEqual(a,b,K,M,N)
{
        // Stores the sum of a[]
        let sum1 = 0;

        // Stores the sum of b[]
        let sum2 = 0;

        // Calculate sum of the array a[]
        for (let el=0;el< a.length;el++)
            sum1 += a[el];

        // Calculate sum of the array b[]
        for (let el=0;el< b.length;el++)
            sum2 += b[el];

        // Stores the difference
        // between a[] and b[]
        let diff = sum1 - sum2;

        // Left and Right pointer
        // to traverse the array a[]
        let l1 = 0, r1 = M - 1;

        // Left and Right pointer
        // to traverse the array b[]
        let l2 = 0, r2 = N - 1;

        // Stores the count of moves
        let res = 0;

        // Sort the arrays in
        // ascending order
        a.sort(function(c,d){return c-d;});
        b.sort(function(c,d){return c-d;});

        // Iterate while diff != 0 and
        // l1 <= r1 or l2 <= r2
        while (l1 <= r1 || l2 <= r2) {
            if (diff == 0) {

                break;
            }

            // If diff is greater than 0
            if (diff > 0) {

                // If all pointers are valid
                if (l2 <= r2 && l1 <= r1) {

                    if (K - b[l2] < a[r1] - 1) {

                        let sub = Math.min(
                            a[r1] - 1, diff);
                        diff -= sub;
                        a[r1] -= sub;
                        r1--;
                    }
                    else {

                        let sub = Math.min(
                            K - b[l2], diff);
                        diff -= sub;
                        b[l2] += sub;
                        l2++;
                    }
                }

                // Otherwise, if only pointers
                // of array a[] is valid
                else if (l1 <= r1) {

                    let sub = Math.min(
                        a[r1] - 1, diff);
                    diff -= sub;
                    a[r1] -= sub;
                    r1--;
                }

                // Otherwise
                else {

                    let sub = Math.min(
                        K - b[l2], diff);
                    diff -= sub;
                    b[l2] += sub;
                    l2++;
                }
            }

            // If diff is less than 0
            else {

                // If all pointers are valid
                if (l1 <= r1 && l2 <= r2) {
                    if (K - a[l1]
                        < b[r2] - 1) {

                        let sub = Math.min(
                            b[r2] - 1,
                            -1 * diff);
                        diff += sub;
                        b[r2] -= sub;
                        r2--;
                    }

                    else {

                        let sub = Math.min(
                            K - a[l1],
                            -1 * diff);
                        diff += sub;
                        a[l1] -= sub;
                        l1++;
                    }
                }

                // Otherwise, if only pointers
                // of array a[] is valid
                else if (l2 <= r2) {

                    let sub
                        = Math.min(
                            b[r2] - 1,
                            -1 * diff);
                    diff += sub;
                    b[r2] -= sub;
                    r2--;
                }

                // Otherwise
                else {

                    let sub = Math.min(
                        K - a[l1], diff);
                    diff += sub;
                    a[l1] += sub;
                    l1++;
                }
            }

            // Increment count
            // of res by one
            res++;
        }

        // If diff is 0, then return res
        if (diff == 0)
            return res;

        // Otherwise, return -1
        else
            return -1;
}

// Driver Code
let A=[1, 4, 3 ];
let B=[6, 6, 6 ];
let M = A.length;
let N = B.length;
let K = 6;
document.write(makeSumEqual(A, B, K,
                         M, N));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)