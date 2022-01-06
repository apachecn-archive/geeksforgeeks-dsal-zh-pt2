# 最小化指数差(j–I)，使得范围[arr[i]，arr[j]]包含至少 K 个奇数

> 原文:[https://www . geesforgeks . org/minimum-index-difference-j-I-so-range-arri-arrj-contains-至少-k-奇数整数/](https://www.geeksforgeeks.org/minimise-index-difference-j-i-such-that-range-arri-arrj-contains-at-least-k-odd-integers/)

给定一个具有非递减顺序的 **N** 个整数和一个整数 K 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是为一对 **(i，j)** 找到**(j–I)**的最小值，使得范围**【arr[I]，arr[j]】**至少包含 **K** 个奇数。

**示例**:

> **输入** : arr[] = {1，3，6，8，15，21}，K = 3
> **输出** : 1
> **解释**:对于(I，j) = (3，4)，它表示具有 4 个奇数{9，11，13，15}(即大于 K)的范围[8，15]。因此 j–I = 1，这是最小可能值。
> 
> **输入** : arr[] = {5，6，7，8，9}，K = 5
> **输出** : -1

**逼近**:给定的问题可以用[两点逼近](https://www.geeksforgeeks.org/two-pointers-technique/)和一些基础数学来解决。想法是使用[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)检查范围内奇数的[计数，找到至少包含 **K** 个奇数的最小窗口的大小。可以通过维护两个指针 **i** 和 **j** 并计算范围**【arr[I]、arr[j]**内奇数的计数来完成。对于奇数大于 **K** 的窗口，保持变量**(j–I)**的最小值，这是必需的答案。](https://www.geeksforgeeks.org/count-odd-and-even-numbers-in-a-range-from-l-to-r/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum value of j - i
// such that the count of odd integers in the
// range [arr[i], arr[j]] is more than K
int findEven(int arr[], int N, int K)
{
    // Base Case
    int L = arr[0];
    int R = arr[N - 1];

    // Maximum count of odd integers
    int Count = (L & 1)
                    ? ceil((float)(R - L + 1) / 2)
                    : (R - L + 1) / 2;

    // If no valid (i, j) exists
    if (K > Count) {
        return -1;
    }

    // Initialize the variables
    int i = 0, j = 0, ans = INT_MAX;

    // Loop for the two pointer approach
    while (j < N) {

        L = arr[i];
        R = arr[j];

        // Calculate count of odd numbrs in the
        // range [L, R]
        Count = (L & 1)
                    ? ceil((float)(R - L + 1) / 2)
                    : (R - L + 1) / 2;

        if (K > Count) {
            j++;
        }

        else {

            // If the current value of j - i
            // is smaller, update answer
            if (j - i < ans) {
                ans = j - i;
            }

            i++;
        }
    }

    // Return Answer
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 6, 8, 15, 21 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 3;

    cout << findEven(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

public class GFG
{

// Function to find the minimum value of j - i
// such that the count of odd integers in the
// range [arr[i], arr[j]] is more than K
static int findEven(int []arr, int N, int K)
{

    // Base Case
    int L = arr[0];
    int R = arr[N - 1];

    int Count = 0;

    // Maximum count of odd integers
    if ((L & 1) > 0) {
        Count = (int)Math.ceil((float)(R - L + 1) / 2.0);
    }
    else {
        Count = (R - L + 1) / 2;
    }
    // If no valid (i, j) exists
    if (K > Count) {
        return -1;
    }

    // Initialize the variables
    int i = 0, j = 0, ans = Integer.MAX_VALUE;

    // Loop for the two pointer approach
    while (j < N) {

        L = arr[i];
        R = arr[j];

        // Calculate count of odd numbrs in the
        // range [L, R]
        if ((L & 1) > 0) {
            Count = (int)Math.ceil((float)(R - L + 1) / 2);
        }
        else {
            Count = (R - L + 1) / 2;
        }

        if (K > Count) {
            j++;
        }

        else {

            // If the current value of j - i
            // is smaller, update answer
            if (j - i < ans) {
                ans = j - i;
            }

            i++;
        }
    }

    // Return Answer
    return ans;
}

// Driver Code
public static void main(String args[])
{
    int []arr = { 1, 3, 6, 8, 15, 21 };
    int N = arr.length;
    int K = 3;

    System.out.println(findEven(arr, N, K));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach
import math as Math

# Function to find the minimum value of j - i
# such that the count of odd integers in the
# range [arr[i], arr[j]] is more than K
def findEven(arr, N, K):

    # Base Case
    L = arr[0]
    R = arr[N - 1]

    # Maximum count of odd integers
    Count = Math.ceil((R - L + 1) / 2) if (L & 1) else (R - L + 1) / 2

    # If no valid (i, j) exists
    if (K > Count):
        return -1

    # Initialize the variables
    i = 0
    j = 0
    ans = 10**9

    # Loop for the two pointer approach
    while (j < N):

        L = arr[i]
        R = arr[j]

        # Calculate count of odd numbrs in the
        # range [L, R]
        Count = Math.ceil((R - L + 1) / 2) if (L & 1) else (R - L + 1) / 2

        if (K > Count):
          j += 1

        else:
            # If the current value of j - i
            # is smaller, update answer
            if (j - i < ans):
                ans = j - i
            i += 1

    # Return Answer
    return ans

# Driver Code
arr = [1, 3, 6, 8, 15, 21]
N = len(arr)
K = 3

print(findEven(arr, N, K))

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

// Function to find the minimum value of j - i
// such that the count of odd integers in the
// range [arr[i], arr[j]] is more than K
static int findEven(int []arr, int N, int K)
{
    // Base Case
    int L = arr[0];
    int R = arr[N - 1];

    int Count = 0;

    // Maximum count of odd integers
    if ((L & 1) > 0) {
        Count = (int)Math.Ceiling((float)(R - L + 1) / 2.0);
    }
    else {
        Count = (R - L + 1) / 2;
    }
    // If no valid (i, j) exists
    if (K > Count) {
        return -1;
    }

    // Initialize the variables
    int i = 0, j = 0, ans = Int32.MaxValue;

    // Loop for the two pointer approach
    while (j < N) {

        L = arr[i];
        R = arr[j];

        // Calculate count of odd numbrs in the
        // range [L, R]
        if ((L & 1) > 0) {
            Count = (int)Math.Ceiling((float)(R - L + 1) / 2);
        }
        else {
            Count = (R - L + 1) / 2;
        }

        if (K > Count) {
            j++;
        }

        else {

            // If the current value of j - i
            // is smaller, update answer
            if (j - i < ans) {
                ans = j - i;
            }

            i++;
        }
    }

    // Return Answer
    return ans;
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 3, 6, 8, 15, 21 };
    int N = arr.Length;
    int K = 3;

    Console.Write(findEven(arr, N, K));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

        // JavaScript Program to implement
        // the above approach

        // Function to find the minimum value of j - i
        // such that the count of odd integers in the
        // range [arr[i], arr[j]] is more than K
        function findEven(arr, N, K) {
            // Base Case
            let L = arr[0];
            let R = arr[N - 1];

            // Maximum count of odd integers
            let Count = (L & 1)
                ? Math.ceil((R - L + 1) / 2)
                : (R - L + 1) / 2;

            // If no valid (i, j) exists
            if (K > Count) {
                return -1;
            }

            // Initialize the variables
            let i = 0, j = 0, ans = Number.MAX_VALUE;

            // Loop for the two pointer approach
            while (j < N) {

                L = arr[i];
                R = arr[j];

                // Calculate count of odd numbrs in the
                // range [L, R]
                Count = (L & 1)
                    ? Math.ceil((R - L + 1) / 2)
                    : (R - L + 1) / 2;

                if (K > Count) {
                    j++;
                }

                else {

                    // If the current value of j - i
                    // is smaller, update answer
                    if (j - i < ans) {
                        ans = j - i;
                    }

                    i++;
                }
            }

            // Return Answer
            return ans;
        }

        // Driver Code
        let arr = [1, 3, 6, 8, 15, 21];
        let N = arr.length;
        let K = 3;

        document.write(findEven(arr, N, K));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
1
```

***时间** **复杂度** : O(N)*
***辅助** **空间** : O(1)*