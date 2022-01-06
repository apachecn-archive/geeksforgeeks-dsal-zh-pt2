# 最大和，精确地选择一半的元素，并且没有两个相邻的

> 原文:[https://www . geeksforgeeks . org/maximum-sum-这样-恰好一半的元素被选中-并且没有两个相邻的/](https://www.geeksforgeeks.org/maximum-sum-such-that-exactly-half-of-the-elements-are-selected-and-no-two-adjacent/)

给定一个包含 N 个整数的数组 A。找到可能的最大和，以便选择精确的楼层(N/2)元素，并且没有两个选择的元素彼此相邻。(如果 N = 5，则应选择恰好 2 个元素作为楼层(5/2) = 2)
对于此问题的更简单版本，请查看[此](https://www.geeksforgeeks.org/maximum-sum-such-that-no-two-elements-are-adjacent/)。

**示例:**

> **输入:** A = [1，2，3，4，5，6]
> **输出:** 12
> **说明:**
> 选择 2，4，6 做和 12。
> 
> **输入:** A = [-1000，-100，-10，0，10]
> **输出:** 0
> **说明:**
> 选择-10 和 10，使和为 0。

**进场:**

*   我们将使用动态编程的概念。以下是 dp 状态的定义方式:

> **dp[i][j]** =直到索引 I 的最大和，使得 j 个元素被选择

*   由于不能选择两个相邻的元素:

> **dp[i][j]** =最大值(a[i] + dp[i-2][j-1]，dp[i-1][j])

下面是上述方法的实现。

## C++

```
// C++ program to find maximum sum possible
// such that exactly floor(N/2) elements
// are selected and no two selected
// elements are adjacent to each other
#include <bits/stdc++.h>
using namespace std;

// Function return the maximum sum
// possible under given condition
int MaximumSum(int a[], int n)
{
    int dp[n + 1][n + 1];

    // Intitialising the dp table
    for (int i = 0; i < n + 1; i++)
    {
        for (int j = 0; j < n + 1; j++)
            dp[i][j] = INT_MIN;
    }

    // Base case
    for (int i = 0; i < n + 1; i++)
        dp[i][0] = 0;

    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= i; j++)
        {
            int val = INT_MIN;

            // Condition to select the current
            // element
            if ((i - 2 >= 0
                 && dp[i - 2][j - 1] != INT_MIN)
                                   || i - 2 < 0)
            {
                val = a[i - 1] +
                    (i - 2 >= 0 ?
                     dp[i - 2][j - 1] : 0);
            }

            // Condition to not select the
            // current element if possible
            if (i - 1 >= j)
            {
                val = max(val, dp[i - 1][j]);
            }
            dp[i][j] = val;
        }
    }

    return dp[n][n / 2];
}

//Driver code
int main()
{

    int A[] = {1, 2, 3, 4, 5, 6};

    int N = sizeof(A) / sizeof(A[0]);

    cout << MaximumSum(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum sum possible
// such that exactly Math.floor(N/2) elements
// are selected and no two selected
// elements are adjacent to each other
class GFG{

// Function return the maximum sum
// possible under given condition
static int MaximumSum(int a[], int n)
{
    int [][]dp = new int[n + 1][n + 1];

    // Intitialising the dp table
    for(int i = 0; i < n + 1; i++)
    {
       for(int j = 0; j < n + 1; j++)
          dp[i][j] = Integer.MIN_VALUE;
    }

    // Base case
    for(int i = 0; i < n + 1; i++)
       dp[i][0] = 0;

    for(int i = 1; i <= n; i++)
    {
       for(int j = 1; j <= i; j++)
       {
          int val = Integer.MIN_VALUE;

          // Condition to select the current
          // element
          if ((i - 2 >= 0 &&
            dp[i - 2][j - 1] != Integer.MIN_VALUE) ||
               i - 2 < 0)
          {
              val = a[i - 1] + (i - 2 >= 0 ?
                             dp[i - 2][j - 1] : 0);
          }

          // Condition to not select the
          // current element if possible
          if (i - 1 >= j)
          {
              val = Math.max(val, dp[i - 1][j]);
          }
          dp[i][j] = val;
        }
    }
    return dp[n][n / 2];
}

// Driver code
public static void main(String[] args)
{
    int A[] = { 1, 2, 3, 4, 5, 6 };
    int N = A.length;

    System.out.print(MaximumSum(A, N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find maximum sum possible
# such that exactly floor(N/2) elements
# are selected and no two selected
# elements are adjacent to each other

import sys
# Function return the maximum sum
# possible under given condition
def MaximumSum(a,n):
    dp = [[0 for i in range(n+1)] for j in range(n+1)]

    # Intitialising the dp table
    for i in range(n + 1):
        for j in range(n + 1):
            dp[i][j] = -sys.maxsize-1

    # Base case
    for i in range(n+1):
        dp[i][0] = 0

    for i in range(1,n+1,1):
        for j in range(1,i+1,1):
            val = -sys.maxsize-1

            # Condition to select the current
            # element
            if ((i - 2 >= 0 and dp[i - 2][j - 1] != -sys.maxsize-1) or i - 2 < 0):
                if (i - 2 >= 0):
                    val = a[i - 1] + dp[i - 2][j - 1]
                else:
                    val = a[i - 1]

            # Condition to not select the
            # current element if possible
            if (i - 1 >= j):
                val = max(val, dp[i - 1][j])

            dp[i][j] = val

    return dp[n][n // 2]

#Driver code
if __name__ == '__main__':
    A = [1, 2, 3, 4, 5, 6]

    N = len(A)

    print(MaximumSum(A,N))

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# program to find maximum sum possible
// such that exactly Math.floor(N/2) elements
// are selected and no two selected
// elements are adjacent to each other
using System;

class GFG{

// Function return the maximum sum
// possible under given condition
static int MaximumSum(int []a, int n)
{
    int [,]dp = new int[n + 1, n + 1];

    // Intitialising the dp table
    for(int i = 0; i < n + 1; i++)
    {
       for(int j = 0; j < n + 1; j++)
          dp[i, j] = Int32.MinValue;
    }

    // Base case
    for(int i = 0; i < n + 1; i++)
       dp[i, 0] = 0;

    for(int i = 1; i <= n; i++)
    {
       for(int j = 1; j <= i; j++)
       {
          int val = Int32.MinValue;

          // Condition to select the current
          // element
          if ((i - 2 >= 0 &&
            dp[i - 2, j - 1] != Int32.MinValue) ||
               i - 2 < 0)
          {
              val = a[i - 1] + (i - 2 >= 0 ?
                             dp[i - 2, j - 1] : 0);
          }

          // Condition to not select the
          // current element if possible
          if (i - 1 >= j)
          {
              val = Math.Max(val, dp[i - 1, j]);
          }
          dp[i, j] = val;
       }
    }
    return dp[n, n / 2];
}

// Driver code
public static void Main()
{
    int []A = { 1, 2, 3, 4, 5, 6 };
    int N = A.Length;

    Console.Write(MaximumSum(A, N));
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>

// JavaScript program to find maximum sum possible
// such that exactly Math.floor(N/2) elements
// are selected and no two selected
// elements are adjacent to each other

// Function return the maximum sum
// possible under given condition
function MaximumSum(a,n)
{
    let dp = [];

    for(let i=0;i<n+1;i++) dp.push(Array(n+1));

    // Intitialising the dp table
    for(let i = 0; i < n + 1; i++)
    {
       for(let j = 0; j < n + 1; j++)
          dp[i][j] = -10000;
    }

    // Base case
    for(let i = 0; i < n + 1; i++)
       dp[i][0] = 0;

    for(let i = 1; i <= n; i++)
    {
       for(let j = 1; j <= i; j++)
       {
          let val = -10000;

          // Condition to select the current
          // element
          if ((i - 2 >= 0 &&
            dp[i - 2, j - 1] != -10000) ||
               i - 2 < 0)
          {
              val = a[i - 1] + (i - 2 >= 0 ?
                             dp[i - 2][j - 1] : 0);
          }

          // Condition to not select the
          // current element if possible
          if (i - 1 >= j)
          {
              val = Math.max(val, dp[i - 1][j]);
          }
          dp[i][j] = val;
       }
    }
    return dp[n][n / 2]
}

// Driver code

let A = [1, 2, 3, 4, 5, 6];
let N = A.length;

document.write(MaximumSum(A, N));

// This code is contributed by Nidhi_biet

</script>
```

**Output:** 

```
12
```

**时间复杂度:** O(N <sup>2</sup> )

**高效方法**

*   我们将使用动态编程，但状态略有修改。存储索引和到目前为止获取的元素数量都是徒劳的，因为我们总是需要获取精确的 floor(i/2)元素，所以在 dp 存储的第 I 个位置，我们将假设到目前为止子集中的 floor(i/2)元素。
*   以下是 dp 表状态:

> **dp[i][1]** =直到第 I 个索引的最大和，选择元素 a[i]，带有楼层(i/2)元素，彼此不相邻。
> **dp[i][0]** =直到第 I 个索引的最大和，不挑选元素 a[i]，带有楼层(i/2)元素，彼此不相邻。

*   我们有两个案例:
    *   **当 I 为奇数时**:如果我们必须选择一个[i]，那么我们就不能选择一个[i-1]，所以剩下的唯一选项就是(I–2)th 和(I–3)rd 状态(因为 floor((I–2)/2)= floor((I–3)/2)= floor(i/2)–1，而且因为我们选择了一个[i]，所以总的选择元素将是 floor(I/2))。如果我们不选择一个[i]，那么取一个[i-1]并使用状态 I–1、I–2 和 I–3 或使用状态 I–3 的一个[I–2]将形成一个和，因为这些只会给出总的下限(i/2)。

> **dp[i][1]** = scar[i] + max（{dp[i – 3][1]， dp[i – 3][0]， dp[i – 2][1]， dp[i –2][0]}）
> **dp[i][0]** = max（{arr[i – 1] + dp[i – 2][0]， scar[i – 1] + dp[i –3][1]， scar[i – 1] + dp[i –3][0]，
> 疤痕[i – 2] + dp[i – 3][0]}）

*   **当 I 为偶数时**:如果我们选择一个[i]，那么使用状态 I–1 和 I–2，否则选择一个[I–1]并使用状态 I–2。

> **DP[I][1]**= arr[I]+max({ DP[I-2][1]、DP[I-2][0]、DP[I-1][0]})
> **【DP[I][0]**= arr[I-1]+DP[I-2][0])

下面是上述方法的实现。

## C++

```
// C++ program to find maximum sum possible
// such that exactly floor(N/2) elements
// are selected and no two selected
// elements are adjacent to each other
#include <bits/stdc++.h>
using namespace std;

// Function return the maximum sum
// possible under given condition
int MaximumSum(int a[], int n)
{

    int dp[n + 1][2];

    // Intitialising the dp table
    memset(dp, 0, sizeof(dp));

    // Base case
    dp[2][1] = a[1];
    dp[2][0] = a[0];

    for (int i = 3; i < n + 1; i++) {
        // When i is odd
        if (i & 1) {
            int temp = max({ dp[i - 3][1],
                             dp[i - 3][0],
                             dp[i - 2][1],
                             dp[i - 2][0] });

            dp[i][1] = a[i - 1] + temp;
            dp[i][0] = max({ a[i - 2] + dp[i - 2][0],
                             a[i - 2] + dp[i - 3][1],
                             a[i - 2] + dp[i - 3][0],
                             a[i - 3] + dp[i - 3][0] });
        }

        // When i is even
        else {
            dp[i][1] = a[i - 1] + max({ dp[i - 2][1],
                                        dp[i - 2][0],
                                        dp[i - 1][0] });

            dp[i][0] = a[i - 2] + dp[i - 2][0];
        }
    }
    // Maximum of if we pick last element or not
    return max(dp[n][1], dp[n][0]);
}

// Driver code
int main()
{
    int A[] = {1, 2, 3, 4, 5, 6};

    int N = sizeof(A) / sizeof(A[0]);

    cout << MaximumSum(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum sum possible
// such that exactly Math.floor(N/2) elements
// are selected and no two selected
// elements are adjacent to each other
import java.util.*;

class GFG{

// Function return the maximum sum
// possible under given condition
static int MaximumSum(int a[], int n)
{

    int [][]dp = new int[n + 1][2];

    // Base case
    dp[2][1] = a[1];
    dp[2][0] = a[0];

    for(int i = 3; i < n + 1; i++)
    {

       // When i is odd
       if (i % 2 == 1)
       {
           int temp = Math.max((Math.max(dp[i - 3][1],
                                         dp[i - 3][0])),
                                Math.max(dp[i - 2][1],
                                         dp[i - 2][0]));
           dp[i][1] = a[i - 1] + temp;
           dp[i][0] = Math.max((Math.max(a[i - 2] +
                                        dp[i - 2][0],
                                         a[i - 2] +
                                        dp[i - 3][1])),
                                Math.max(a[i - 2] +
                                        dp[i - 3][0],
                                         a[i - 3] +
                                        dp[i - 3][0]));
       }

       // When i is even
       else
       {
           dp[i][1] = a[i - 1] + (Math.max((
                                  Math.max(dp[i - 2][1],
                                           dp[i - 2][0])),
                                           dp[i - 1][0]));
           dp[i][0] = a[i - 2] + dp[i - 2][0];
       }
    }

    // Maximum of if we pick last element or not
    return Math.max(dp[n][1], dp[n][0]);
}

static int max(int []arr)
{
    return 1;
}

// Driver code
public static void main(String[] args)
{
    int A[] = {1, 2, 3, 4, 5, 6};
    int N = A.length;

    System.out.print(MaximumSum(A, N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find maximum sum possible
# such that exactly floor(N/2) elements
# are selected and no two selected
# elements are adjacent to each other

# Function return the maximum sum
# possible under given condition
def MaximumSum(a, n):

    dp = [[0 for x in range (2)]
             for y in range(n + 1)]

    # Base case
    dp[2][1] = a[1]
    dp[2][0] = a[0]

    for i in range (3, n + 1):

        # When i is odd
        if (i & 1):
            temp = max([dp[i - 3][1],
                        dp[i - 3][0],
                        dp[i - 2][1],
                        dp[i - 2][0]])

            dp[i][1] = a[i - 1] + temp
            dp[i][0] = max([a[i - 2] + dp[i - 2][0],
                            a[i - 2] + dp[i - 3][1],
                            a[i - 2] + dp[i - 3][0],
                            a[i - 3] + dp[i - 3][0]])

        # When i is even
        else:
            dp[i][1] = (a[i - 1] + max([dp[i - 2][1],
                                        dp[i - 2][0],
                                        dp[i - 1][0]]))

            dp[i][0] = a[i - 2] + dp[i - 2][0]

    # Maximum of if we pick last
    # element or not
    return max(dp[n][1], dp[n][0])

# Driver code
if __name__ == "__main__": 

    A = [1, 2, 3, 4, 5, 6]   
    N = len(A)
    print(MaximumSum(A, N))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find maximum sum possible
// such that exactly Math.Floor(N/2) elements
// are selected and no two selected
// elements are adjacent to each other
using System;

class GFG{

// Function return the maximum sum
// possible under given condition
static int MaximumSum(int []a, int n)
{
    int [,]dp = new int[n + 1, 2];

    // Base case
    dp[2, 1] = a[1];
    dp[2, 0] = a[0];

    for(int i = 3; i < n + 1; i++)
    {

       // When i is odd
       if (i % 2 == 1)
       {
           int temp = Math.Max((Math.Max(dp[i - 3, 1],
                                         dp[i - 3, 0])),
                                Math.Max(dp[i - 2, 1],
                                         dp[i - 2, 0]));
           dp[i, 1] = a[i - 1] + temp;
           dp[i, 0] = Math.Max((Math.Max(a[i - 2] +
                                        dp[i - 2, 0],
                                         a[i - 2] +
                                        dp[i - 3, 1])),
                                Math.Max(a[i - 2] +
                                        dp[i - 3, 0],
                                         a[i - 3] +
                                        dp[i - 3, 0]));
       }

       // When i is even
       else
       {
           dp[i, 1] = a[i - 1] + (Math.Max((
                                  Math.Max(dp[i - 2, 1],
                                           dp[i - 2, 0])),
                                           dp[i - 1, 0]));
           dp[i, 0] = a[i - 2] + dp[i - 2, 0];
       }
    }

    // Maximum of if we pick last element or not
    return Math.Max(dp[n, 1], dp[n, 0]);
}

static int max(int []arr)
{
    return 1;
}

// Driver code
public static void Main(String[] args)
{
    int []A = { 1, 2, 3, 4, 5, 6 };
    int N = A.Length;

    Console.Write(MaximumSum(A, N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find maximum sum possible
// such that exactly floor(N/2) elements
// are selected and no two selected
// elements are adjacent to each other

// Function return the maximum sum
// possible under given condition
function MaximumSum(a, n)
{

    var dp = Array.from(Array(n+1), ()=>Array(2).fill(0));

    // Base case
    dp[2][1] = a[1];
    dp[2][0] = a[0];

    for (var i = 3; i < n + 1; i++) {
        // When i is odd
        if (i & 1) {
            var temp = ([dp[i - 3][1],
                             dp[i - 3][0],
                             dp[i - 2][1],
                             dp[i - 2][0] ].reduce((a,b)=>
                               Math.max(a,b)));

            dp[i][1] = a[i - 1] + temp;
            dp[i][0] = ([ a[i - 2] + dp[i - 2][0],
                             a[i - 2] + dp[i - 3][1],
                             a[i - 2] + dp[i - 3][0],
                             a[i - 3] + dp[i - 3][0] ].reduce((a,b)=>
                               Math.max(a,b)));
        }

        // When i is even
        else {
            dp[i][1] = a[i - 1] + ([ dp[i - 2][1],
                                        dp[i - 2][0],
                                        dp[i - 1][0] ].reduce((a,b)=>
                                          Math.max(a,b)));

            dp[i][0] = a[i - 2] + dp[i - 2][0];
        }
    }
    // Maximum of if we pick last element or not
    return Math.max(dp[n][1], dp[n][0]);
}

// Driver code
var A = [1, 2, 3, 4, 5, 6];

var N = A.length;
document.write( MaximumSum(A, N));

</script>
```

**Output:** 

```
12
```

**时间复杂度:** O(N)