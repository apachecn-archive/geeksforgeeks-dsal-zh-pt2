# 最小化修改数组的成本，使得偶数索引具有偶数元素，反之亦然

> 原文:[https://www . geeksforgeeks . org/最小化修改数组的成本这样偶数索引就有偶数元素，反之亦然/](https://www.geeksforgeeks.org/minimize-cost-to-modify-the-array-such-that-even-indices-have-even-elements-and-vice-versa/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和两个整数 **X** 和 **Y** ，任务是找到修改数组所需的**最小**成本，使得**偶数**索引具有[**偶数**元素](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)和**奇数**索引具有**奇数**元素 或者通过[以 **X** 的代价交换数组的两个元素](https://www.geeksforgeeks.org/c-program-swap-two-numbers/)，或者通过以 **Y** 的代价递增或递减该元素的 **1** 。

**示例:**

> **输入:** arr[] = {5，3，7，2，1}，X = 1，Y = 2
> **输出:** 5
> **解释:**
> 以下是执行的操作:
> **操作 1:** 交换索引 0 和 3 处的数组元素，将数组修改为{2，3，7，5，1}。这些操作的成本是 X(= 1)。
> **操作 2:** 递增索引 2 处的数组元素，将数组修改为{2，3，8，5，1}。这次手术的费用是 2 英镑。
> **操作 3:** 递增索引 4 处的数组元素，将数组修改为{2，3，8，5，2}。这次手术的费用是 2 英镑。
> 因此总成本为 1 + 2 + 2 = 5，最小。
> 
> **输入:** arr[] = {1，2，3，4}，X = 1，Y = 2
> **输出:** 2

**方法:**通过首先找出错误地放置在奇数和偶数索引处的元素的计数分别为**奇数计数**和**偶数计数**，可以使用以下观察来解决给定的问题:

*   **情况 1:** 可以通过以 **X** 的成本对最少的**奇数**和**偶数**执行交换操作，并以 **Y** 的成本对剩余元素执行递减操作来计算成本。
*   **情况 2:** 可以通过对剩余元素执行递减操作来计算成本，成本为 **Y** 。

在上述两种情况下获得的最小成本就是所需的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost to
// modify the array according to the
// given criteria
int minimumCost(int arr[], int N,
                int X, int Y)
{
    // Count of wrong positioned odd
    // and even elements
    int even_count = 0, odd_count = 0;
    for (int i = 0; i < N; i++) {

        // Odd Count
        if ((arr[i] & 1)
            && (i % 2 == 0)) {
            odd_count++;
        }

        // Even Count
        if ((arr[i] % 2) == 0
            && (i & 1)) {
            even_count++;
        }
    }

    // Cost for Case 1

    // Swapping Cost
    int cost1 = X * min(odd_count, even_count);

    // Decrementing cost after swapping
    int cost2 = Y
                * (max(odd_count, even_count)
                   - min(odd_count, even_count));

    // Cost for Case 2

    // Only decrementing cost
    int cost3 = (odd_count + even_count) * Y;

    // Return the minimum cost of the
    // two cases
    return min(cost1 + cost2, cost3);
}

// Driver Code
int main()
{
    int arr[] = { 5, 3, 7, 2, 1 }, X = 10, Y = 2;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << minimumCost(arr, N, X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to find the minimum cost to
    // modify the array according to the
    // given criteria
    public static int minimumCost(int arr[], int N, int X, int Y)
    {

        // Count of wrong positioned odd
        // and even elements
        int even_count = 0, odd_count = 0;
        for (int i = 0; i < N; i++) {

            // Odd Count
            if ((arr[i] & 1) > 0 && (i % 2 == 0)) {
                odd_count++;
            }

            // Even Count
            if ((arr[i] % 2) == 0 && (i & 1) > 0) {
                even_count++;
            }
        }

        // Cost for Case 1

        // Swapping Cost
        int cost1 = X * Math.min(odd_count, even_count);

        // Decrementing cost after swapping
        int cost2 = Y * (Math.max(odd_count, even_count) - Math.min(odd_count, even_count));

        // Cost for Case 2

        // Only decrementing cost
        int cost3 = (odd_count + even_count) * Y;

        // Return the minimum cost of the
        // two cases
        return Math.min(cost1 + cost2, cost3);
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = { 5, 3, 7, 2, 1 }, X = 10, Y = 2;
        int N = arr.length;
        System.out.println(minimumCost(arr, N, X, Y));
    }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the minimum cost to
# modify the array according to the
# given criteria
def minimumCost(arr, N, X, Y):

        # Count of wrong positioned odd
        # and even elements
    even_count = 0
    odd_count = 0
    for i in range(0, N):

                # Odd Count
        if ((arr[i] & 1) and (i % 2 == 0)):
            odd_count += 1

            # Even Count
        if ((arr[i] % 2) == 0 and (i & 1)):
            even_count += 1

        # Cost for Case 1

        # Swapping Cost
    cost1 = X * min(odd_count, even_count)

    # Decrementing cost after swapping
    cost2 = Y * (max(odd_count, even_count) - min(odd_count, even_count))

    # Cost for Case 2

    # Only decrementing cost
    cost3 = (odd_count + even_count) * Y

    # Return the minimum cost of the
    # two cases
    return min(cost1 + cost2, cost3)

# Driver Code
if __name__ == "__main__":

    arr = [5, 3, 7, 2, 1]
    X = 10
    Y = 2
    N = len(arr)
    print(minimumCost(arr, N, X, Y))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    // Function to find the minimum cost to
    // modify the array according to the
    // given criteria
    public static int minimumCost(int []arr, int N, int X, int Y)
    {

        // Count of wrong positioned odd
        // and even elements
        int even_count = 0, odd_count = 0;
        for (int i = 0; i < N; i++) {

            // Odd Count
            if ((arr[i] & 1) > 0 && (i % 2 == 0)) {
                odd_count++;
            }

            // Even Count
            if ((arr[i] % 2) == 0 && (i & 1) > 0) {
                even_count++;
            }
        }

        // Cost for Case 1

        // Swapping Cost
        int cost1 = X * Math.Min(odd_count, even_count);

        // Decrementing cost after swapping
        int cost2 = Y * (Math.Max(odd_count, even_count) - Math.Min(odd_count, even_count));

        // Cost for Case 2

        // Only decrementing cost
        int cost3 = (odd_count + even_count) * Y;

        // Return the minimum cost of the
        // two cases
        return Math.Min(cost1 + cost2, cost3);
    }

    // Driver Code
    public static void Main(string []args)
    {
        int []arr= { 5, 3, 7, 2, 1 };
        int X = 10, Y = 2;
        int N = arr.Length;
        Console.WriteLine(minimumCost(arr, N, X, Y));
    }
}

// This code is contributed by rutvik_56.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the minimum cost to
        // modify the array according to the
        // given criteria
        function minimumCost(arr, N,
            X, Y)
        {

            // Count of wrong positioned odd
            // and even elements
            let even_count = 0, odd_count = 0;
            for (let i = 0; i < N; i++) {

                // Odd Count
                if ((arr[i] & 1)
                    && (i % 2 == 0)) {
                    odd_count++;
                }

                // Even Count
                if ((arr[i] % 2) == 0
                    && (i & 1)) {
                    even_count++;
                }
            }

            // Cost for Case 1

            // Swapping Cost
            let cost1 = X * Math.min(odd_count, even_count);

            // Decrementing cost after swapping
            let cost2 = Y
                * (Math.max(odd_count, even_count)
                    - Math.min(odd_count, even_count));

            // Cost for Case 2

            // Only decrementing cost
            let cost3 = (odd_count + even_count) * Y;

            // Return the minimum cost of the
            // two cases
            return Math.min(cost1 + cost2, cost3);
        }

        // Driver Code
        let arr = [5, 3, 7, 2, 1], X = 10, Y = 2;
        let N = arr.length;
        document.write(minimumCost(arr, N, X, Y));

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)