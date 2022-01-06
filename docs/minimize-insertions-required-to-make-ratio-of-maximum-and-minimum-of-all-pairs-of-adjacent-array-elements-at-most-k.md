# 最大限度地减少插入，使所有相邻阵列元素对的最大值和最小值之比最多为 K

> 原文:[https://www . geesforgeks . org/minimum-insertions-要求最多 k 个相邻数组元素对的最大和最小构成比/](https://www.geeksforgeeks.org/minimize-insertions-required-to-make-ratio-of-maximum-and-minimum-of-all-pairs-of-adjacent-array-elements-at-most-k/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr** []和一个整数 **K** ( *> 1* )，任务是找到所需的最小插入次数，使得数组中所有相邻元素对的最大值和最小值之比减少到最多 **K** 。

**示例:**

> **输入:** arr[] = { 2，10，25，21}，K = 2
> **输出:** 3
> **解释:**
> 跟随插入使数组满足所需条件{ 2， **4** ， **7** ，10， **17** ，25，21 }。
> 
> **输入:** arr[] = {2，4，1}，K = 2
> T3】输出: 1

**进场:**思路是贪婪地使用。按照以下步骤解决问题:

*   [穿越阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)T2【arr】。
*   初始化一个变量，比如**和**，来存储需要插入的数量。
*   迭代范围**【0，N–2】**，并执行以下步骤:
    *   计算 **min(arr[i]、arr[i + 1])** 和 **max(arr[i]、arr[i + 1])** 并将其存储在变量中，比如说 **a** 和 **b** 。
    *   **If (b > K * a):** 更新 **a = K * a** 并将 **ans** 增加 **1** 。
*   打印**和**的值作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum
// number of insertions required
int mininsert(int arr[], int K, int N)
{
    // Stores the number of
    // insertions required
    int ans = 0;

    // Traverse the array
    for (int i = 0; i < N - 1; i++) {

        // Store the minimum array element
        int a = min(arr[i], arr[i + 1]);

        // Store the maximum array element
        int b = max(arr[i], arr[i + 1]);

        // Checking condition
        while (K * a < b) {

            a *= K;

            // Increase current count
            ans++;
        }
    }

    // Return the count of insertions
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 2, 10, 25, 21 };
    int K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << mininsert(arr, K, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Function to count the minimum
// number of insertions required
static int mininsert(int arr[], int K, int N)
{

    // Stores the number of
    // insertions required
    int ans = 0;

    // Traverse the array
    for (int i = 0; i < N - 1; i++) {

        // Store the minimum array element
        int a = Math.min(arr[i], arr[i + 1]);

        // Store the maximum array element
        int b = Math.max(arr[i], arr[i + 1]);

        // Checking condition
        while (K * a < b) {

            a *= K;

            // Increase current count
            ans++;
        }
    }

    // Return the count of insertions
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 10, 25, 21 };
    int K = 2;
    int N = arr.length;

    System.out.print(mininsert(arr, K, N));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the minimum
# number of insertions required
def mininsert(arr, K, N) :

    # Stores the number of
    # insertions required
    ans = 0

    # Traverse the array
    for i in range(N - 1):

        # Store the minimum array element
        a = min(arr[i], arr[i + 1])

        # Store the maximum array element
        b = max(arr[i], arr[i + 1])

        # Checking condition
        while (K * a < b) :
            a *= K

            # Increase current count
            ans += 1

    # Return the count of insertions
    return ans

# Driver Code
arr = [ 2, 10, 25, 21 ]
K = 2
N = len(arr)

print(mininsert(arr, K, N))

# This code is contributed by susmitakundugoaldanga.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

  // Function to count the minimum
  // number of insertions required
  static int mininsert(int[] arr, int K, int N)
  {

    // Stores the number of
    // insertions required
    int ans = 0;

    // Traverse the array
    for (int i = 0; i < N - 1; i++) {

      // Store the minimum array element
      int a = Math.Min(arr[i], arr[i + 1]);

      // Store the maximum array element
      int b = Math.Max(arr[i], arr[i + 1]);

      // Checking condition
      while (K * a < b) {

        a *= K;

        // Increase current count
        ans++;
      }
    }

    // Return the count of insertions
    return ans;
  }

  // Driver Code
  public static void Main(string[] args)
  {
    int[] arr = { 2, 10, 25, 21 };
    int K = 2;
    int N = arr.Length;

    Console.Write(mininsert(arr, K, N));
  }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

    // Function to count the minimum
    // number of insertions required
    function mininsert(arr , K , N) {

        // Stores the number of
        // insertions required
        var ans = 0;

        // Traverse the array
        for (i = 0; i < N - 1; i++) {

            // Store the minimum array element
            var a = Math.min(arr[i], arr[i + 1]);

            // Store the maximum array element
            var b = Math.max(arr[i], arr[i + 1]);

            // Checking condition
            while (K * a < b) {

                a *= K;

                // Increase current count
                ans++;
            }
        }

        // Return the count of insertions
        return ans;
    }

    // Driver Code

        var arr = [ 2, 10, 25, 21 ];
        var K = 2;
        var N = arr.length;

        document.write(mininsert(arr, K, N));

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N * log(M))，其中 **M** 是数组中最大的* [元素。
***辅助空间:** O(1)*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)