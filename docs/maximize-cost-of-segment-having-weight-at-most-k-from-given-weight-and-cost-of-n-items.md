# 从给定的重量和 N 个项目的成本中最大化重量最多为 K 的段的成本

> 原文:[https://www . geeksforgeeks . org/从给定的重量和 n 件物品成本中获得最大的细分市场成本](https://www.geeksforgeeks.org/maximize-cost-of-segment-having-weight-at-most-k-from-given-weight-and-cost-of-n-items/)

给定两个数组 W[]和 C[]，分别包含 N (1 到 N)个项目的重量和成本，以及一个整数 K，求一个从 1 到 N 的段，使得该段的总重量最多为 K，总成本最大。打印该段的成本。

**示例:**

> **输入:** N = 6，K = 20，W[] = {9，7，6，5，8，4}，C[] = {7，1，3，6，8，3}
> **输出:** 17
> **说明:**选取段{6，5，8}的索引(2，3，4)权重为 19 的段。段成本= 3 + 6 + 8 = 17，这是最大可能。
> 
> **输入:** N = 3，K = 55，W[] = {10，20，30}，C[] = {60，100，120 }
> T3】输出: 220

**天真法:**该方法是找出权重最多为 k 的所有段，并跟踪最大成本。为每个元素找到一个从这个元素开始的线段。

下面是上述方法的实现。

## C++

```
// C++ code to find maximum cost of
// a segment whose weight is at most K.
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum cost of
// a segment whose weight is at most k.
int findMaxCost(int W[], int C[],
                int N, int K)
{
    // Variable to keep track of
    // current weight.
    int weight = 0;

    // Variable to keep track
    // of current cost.
    int cost = 0;

    // variable to keep track of
    // maximum cost of a segment
    // whose weight is at most K.
    int maxCost = 0;

    // Loop to get segment
    // having weight at most K
    for (int l = 0; l < N; l++) {
        weight = 0;
        cost = 0;
        for (int r = l; r < N; r++) {
            weight += W[r];
            cost += C[r];
            if (weight <= K)
                maxCost = max(maxCost, cost);
        }
    }
    return maxCost;
}

// Driver code
int main()
{
    int W[] = { 9, 7, 6, 5, 8, 4 };
    int C[] = { 7, 1, 3, 6, 8, 3 };
    int N = sizeof(W) / sizeof(W[0]);
    int K = 20;

    cout << findMaxCost(W, C, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find maximum cost of
// a segment whose weight is at most K.
class GFG{

// Function to find the maximum cost of
// a segment whose weight is at most k.
static int findMaxCost(int W[], int C[],
                int N, int K)
{

    // Variable to keep track of
    // current weight.
    int weight = 0;

    // Variable to keep track
    // of current cost.
    int cost = 0;

    // variable to keep track of
    // maximum cost of a segment
    // whose weight is at most K.
    int maxCost = 0;

    // Loop to get segment
    // having weight at most K
    for (int l = 0; l < N; l++) {
        weight = 0;
        cost = 0;
        for (int r = l; r < N; r++) {
            weight += W[r];
            cost += C[r];
            if (weight <= K)
                maxCost = Math.max(maxCost, cost);
        }
    }
    return maxCost;
}

// Driver code
public static void main(String[] args)
{
    int W[] = { 9, 7, 6, 5, 8, 4 };
    int C[] = { 7, 1, 3, 6, 8, 3 };
    int N = W.length;
    int K = 20;

    System.out.print(findMaxCost(W, C, N, K));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python code to find maximum cost of
# a segment whose weight is at most K.

# Function to find the maximum cost of
# a segment whose weight is at most k.
def findMaxCost(W, C, N, K) :

    # Variable to keep track of
    # current weight.
    weight = 0;

    # Variable to keep track
    # of current cost.
    cost = 0;

    # variable to keep track of
    # maximum cost of a segment
    # whose weight is at most K.
    maxCost = 0;

    # Loop to get segment
    # having weight at most K
    for l in range(N):
        weight = 0;
        cost = 0;

        for r in range(l, N):
            weight += W[r];
            cost += C[r];
            if (weight <= K):
                maxCost = max(maxCost, cost);
    return maxCost;

# Driver code
W = [ 9, 7, 6, 5, 8, 4 ];
C = [ 7, 1, 3, 6, 8, 3 ];
N = len(W);
K = 20;

print(findMaxCost(W, C, N, K));

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# code to find maximum cost of
// a segment whose weight is at most K.
using System;

class GFG
{

    // Function to find the maximum cost of
    // a segment whose weight is at most k.
    static int findMaxCost(int[] W, int[] C, int N, int K)
    {

        // Variable to keep track of
        // current weight.
        int weight = 0;

        // Variable to keep track
        // of current cost.
        int cost = 0;

        // variable to keep track of
        // maximum cost of a segment
        // whose weight is at most K.
        int maxCost = 0;

        // Loop to get segment
        // having weight at most K
        for (int l = 0; l < N; l++) {
            weight = 0;
            cost = 0;
            for (int r = l; r < N; r++) {
                weight += W[r];
                cost += C[r];
                if (weight <= K)
                    maxCost = Math.Max(maxCost, cost);
            }
        }
        return maxCost;
    }

    // Driver code
    public static void Main()
    {
        int[] W = { 9, 7, 6, 5, 8, 4 };
        int[] C = { 7, 1, 3, 6, 8, 3 };
        int N = W.Length;
        int K = 20;

        Console.WriteLine(findMaxCost(W, C, N, K));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// JavaScript code to find maximum cost of
// a segment whose weight is at most K.

// Function to find the maximum cost of
// a segment whose weight is at most k.
function findMaxCost(W, C, N, K)
{

    // Variable to keep track of
    // current weight.
    let weight = 0;

    // Variable to keep track
    // of current cost.
    let cost = 0;

    // variable to keep track of
    // maximum cost of a segment
    // whose weight is at most K.
    let maxCost = 0;

    // Loop to get segment
    // having weight at most K
    for(let l = 0; l < N; l++)
    {
        weight = 0;
        cost = 0;

        for(let r = l; r < N; r++)
        {
            weight += W[r];
            cost += C[r];

            if (weight <= K)
                maxCost = Math.max(maxCost, cost);
        }
    }
    return maxCost;
}

// Driver code
let W = [ 9, 7, 6, 5, 8, 4 ];
let C = [ 7, 1, 3, 6, 8, 3 ];
let N = W.length;
let K = 20;

document.write(findMaxCost(W, C, N, K));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
17
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(1)

**有效方法:**一种有效方法是使用[滑动窗口技术。](https://www.geeksforgeeks.org/window-sliding-technique/)

*   让 l 和 r 分别表示当前窗口中第一个和最后一个元素的索引。
*   开始遍历数组，跟踪当前窗口中元素的总重量和总成本，以及到目前为止找到的最大总成本。
*   当窗口的权重大于 k 时，继续从窗口开始移除元素。
*   现在更新最大成本。
*   旅行完所有物品后，返回最大费用。

下面是上述方法的实现。

## C++

```
// C++ code to find maximum cost of
// a segment whose weight is at most K.
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum cost of
// a segment whose weight is at most K.
int findMaxCost(int W[], int C[],
                int N, int K)
{   
    // Variable to keep track
    // of current weight.
    int weight = 0;

    // Variable to keep track
    // of current cost.
    int cost = 0;

    // Variable to keep track of
    // maximum cost of a segment
    // whose weight is at most K.
    int maxCost = 0;

    // Loop to implement
    // sliding window technique
    int l = 0;
    for (int r = 0; r < N; r++) {

        // Add current element to the window.
        weight += W[r];
          cost += C[r];

        // Keep removing elements
        // from the start of current window
        // while weight is greater than K
        while(weight > K)
        {
            weight -= W[l];
            cost -= C[l];
              l++;
        }

          // Update maxCost
          maxCost = max(maxCost, cost);
    }
    return maxCost;
}

// Driver code
int main()
{
    int W[] = {9, 7, 6, 5, 8, 4};
    int C[] = {7, 1, 3, 6, 8, 3};
    int N = sizeof(W) / sizeof(W[0]);
    int K = 20;

    cout << findMaxCost(W, C, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find maximum cost of
// a segment whose weight is at most K.
class GFG{

// Function to find the maximum cost of
// a segment whose weight is at most K.
static int findMaxCost(int W[], int C[],
                int N, int K)
{   

    // Variable to keep track
    // of current weight.
    int weight = 0;

    // Variable to keep track
    // of current cost.
    int cost = 0;

    // Variable to keep track of
    // maximum cost of a segment
    // whose weight is at most K.
    int maxCost = 0;

    // Loop to implement
    // sliding window technique
    int l = 0;
    for (int r = 0; r < N; r++) {

        // Add current element to the window.
        weight += W[r];
          cost += C[r];

        // Keep removing elements
        // from the start of current window
        // while weight is greater than K
        while(weight > K)
        {
            weight -= W[l];
            cost -= C[l];
              l++;
        }

          // Update maxCost
          maxCost = Math.max(maxCost, cost);
    }
    return maxCost;
}

// Driver code
public static void main(String[] args)
{
    int W[] = {9, 7, 6, 5, 8, 4};
    int C[] = {7, 1, 3, 6, 8, 3};
    int N = W.length;
    int K = 20;

    System.out.print(findMaxCost(W, C, N, K));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 code to find maximum cost of
# a segment whose weight is at most K.

# Function to find the maximum cost of
# a segment whose weight is at most K.
def findMaxCost(W, C, N, K):

    # Variable to keep track
    # of current weight.
    weight = 0

    # Variable to keep track
    # of current cost.
    cost = 0

    # Variable to keep track of
    # maximum cost of a segment
    # whose weight is at most K.
    maxCost = 0

    # Loop to implement
    # sliding window technique
    l = 0
    for r in range(N):

        # Add current element to the window.
        weight += W[r]
        cost += C[r]

        # Keep removing elements
        # from the start of current window
        # while weight is greater than K
        while(weight > K):

            weight -= W[l]
            cost -= C[l]
            l += 1

        # Update maxCost
        maxCost = max(maxCost, cost)
    return maxCost

# Driver code
if __name__ == "__main__":

    W = [9, 7, 6, 5, 8, 4]
    C = [7, 1, 3, 6, 8, 3]
    N = len(W)
    K = 20

    print(findMaxCost(W, C, N, K))

    # This code is contributed by gaurav01.
```

## C#

```
// C# code to find maximum cost of
// a segment whose weight is at most K.
using System;
using System.Collections.Generic;
public class GFG{

  // Function to find the maximum cost of
  // a segment whose weight is at most K.
  static int findMaxCost(int []W, int []C,
                         int N, int K)
  {   

    // Variable to keep track
    // of current weight.
    int weight = 0;

    // Variable to keep track
    // of current cost.
    int cost = 0;

    // Variable to keep track of
    // maximum cost of a segment
    // whose weight is at most K.
    int maxCost = 0;

    // Loop to implement
    // sliding window technique
    int l = 0;
    for (int r = 0; r < N; r++) {

      // Add current element to the window.
      weight += W[r];
      cost += C[r];

      // Keep removing elements
      // from the start of current window
      // while weight is greater than K
      while(weight > K)
      {
        weight -= W[l];
        cost -= C[l];
        l++;
      }

      // Update maxCost
      maxCost = Math.Max(maxCost, cost);
    }
    return maxCost;
  }

  // Driver code
  public static void Main(String[] args)
  {
    int []W = {9, 7, 6, 5, 8, 4};
    int []C = {7, 1, 3, 6, 8, 3};
    int N = W.Length;
    int K = 20;

    Console.Write(findMaxCost(W, C, N, K));
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
    // JavaScript code to find maximum cost of
    // a segment whose weight is at most K.

    // Function to find the maximum cost of
    // a segment whose weight is at most K.
    const findMaxCost = (W, C, N, K) => {

        // Variable to keep track
        // of current weight.
        let weight = 0;

        // Variable to keep track
        // of current cost.
        let cost = 0;

        // Variable to keep track of
        // maximum cost of a segment
        // whose weight is at most K.
        let maxCost = 0;

        // Loop to implement
        // sliding window technique
        let l = 0;
        for (let r = 0; r < N; r++) {

            // Add current element to the window.
            weight += W[r];
            cost += C[r];

            // Keep removing elements
            // from the start of current window
            // while weight is greater than K
            while (weight > K) {
                weight -= W[l];
                cost -= C[l];
                l++;
            }

            // Update maxCost
            maxCost = Math.max(maxCost, cost);
        }
        return maxCost;
    }

    // Driver code

    let W = [9, 7, 6, 5, 8, 4];
    let C = [7, 1, 3, 6, 8, 3];
    let N = W.length;
    let K = 20;

    document.write(findMaxCost(W, C, N, K));

// This code is contributed by rakesh sahani.
</script>
```

**Output**

```
17
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)