# 最大小费计算器

> 原文:[https://www.geeksforgeeks.org/maximum-tip-calculator/](https://www.geeksforgeeks.org/maximum-tip-calculator/)

Rahul 和 Ankit 是皇家餐厅仅有的两个服务员。今天餐厅收到 **N** 订单。当由不同的服务员处理并以[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**的形式给出时，小费的金额可能会有所不同，因此如果**拉胡尔**接受**I<sup>th</sup>T13】订单，他将会得到小费**A【I】**卢比，如果**安基特**接受该订单，小费将会是**B【I】**卢比。**

为了最大化总小费价值，他们决定在他们之间分配订单。一个订单将由一个人处理。此外，由于时间**的限制**，拉胡尔不能接受超过 **X** 的订单，安基特不能接受超过 **Y** 的订单。保证 **X + Y** 大于等于 **N** ，意味着所有订单都可以由 Rahul 或者 Ankit 处理。任务是在处理完所有订单后，找出最大可能的小费总额。

**示例:**

> **输入:** N = 5，X = 3，Y = 3，A[] = {1，2，3，4，5}，B[] = {5，4，3，2， 1}
> **输出:** 21
> **说明:**
> **第一步:** 5 包含在安基特的数组中
> **第二步:** 4 包含在安基特的数组中
> **第三步:**由于两者具有相同的值 3，则选择其中任意一个
> **第四步:** 4 包含在拉胡尔的数组
> **中**
> 
> **输入:** N = 7，X = 3，Y = 4，A[] = {8，7，15，19，16，16，18}，B[] = {1，7，15，11，12，31，9}
> **输出:** 110

**天真方法:**最简单的方法是遍历给定的数组，同时开始遍历两个数组，并在其中选择最大的元素，如果元素取自 **X** ，则减少 **X** 的数量，否则减少 **Y** 的数量。如果 **X** 或 **Y** 中的一个变为 **0** ，遍历其他非零数组，将其值加到最大利润上。每一步都有一个选择，这类似于 [0-1 背包问题](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)，在这个问题中决定是包含还是排除一个元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds the maximum tips
// from the given arrays as per the
// given conditions
int maximumTip(vector<int> &arr1,vector<int> & arr2,
               int n, int x, int y)
{

    // Base Condition
    if (n == 0)
        return 0;

    // If both have non-zero count then
    // return max element from both array
    if (x != 0 and y != 0)
        return max(
            arr1[n - 1] + maximumTip(arr1, arr2, n - 1,
                                                 x - 1, y),
            arr2[n - 1] + maximumTip(arr1, arr2, n - 1, x,
                                                 y - 1));

    // Traverse first array, as y
    // count has become 0
    if (y == 0)
        return arr1[n - 1] + maximumTip(arr1, arr2, n - 1,
                                                    x - 1, y);

    // Traverse 2nd array, as x
    // count has become 0
    else
        return arr2[n - 1] + maximumTip(arr1, arr2, n - 1,
                                                 x, y - 1);
}

// Drive Code
int main()
{
    int N = 5;
    int X = 3;
    int Y = 3;

    vector<int> A = { 1, 2, 3, 4, 5 };
    vector<int> B = { 5, 4, 3, 2, 1 };

    // Function Call
    cout << (maximumTip(A, B, N, X, Y));
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;

class GFG
{

  // Function that finds the maximum tips
// from the given arrays as per the
// given conditions
static int maximumTip(int []arr1,int []arr2,
               int n, int x, int y)
{

    // Base Condition
    if (n == 0)
        return 0;

    // If both have non-zero count then
    // return max element from both array
    if (x != 0 && y != 0)
        return Math.max(
            arr1[n - 1] + maximumTip(arr1, arr2, n - 1,
                                                 x - 1, y),
            arr2[n - 1] + maximumTip(arr1, arr2, n - 1, x,
                                                 y - 1));

    // Traverse first array, as y
    // count has become 0
    if (y == 0)
        return arr1[n - 1] + maximumTip(arr1, arr2, n - 1,
                                                    x - 1, y);

    // Traverse 2nd array, as x
    // count has become 0
    else
        return arr2[n - 1] + maximumTip(arr1, arr2, n - 1,
                                                 x, y - 1);
}

// Drive Code
    public static void main (String[] args) {
       int N = 5;
    int X = 3;
    int Y = 3;

    int A[] = { 1, 2, 3, 4, 5 };
    int B[] = { 5, 4, 3, 2, 1 };

    // Function Call

        System.out.println(maximumTip(A, B, N, X, Y));
    }
}

    // This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach

# Function that finds the maximum tips
# from the given arrays as per the
# given conditions
def maximumTip(arr1, arr2, n, x, y):

    # Base Condition
    if n == 0:
        return 0

    # If both have non-zero count then
    # return max element from both array
    if x != 0 and y != 0:
        return max(
            arr1[n-1] + maximumTip(arr1, arr2, n - 1, x-1, y),
            arr2[n-1] + maximumTip(arr1, arr2, n-1, x, y-1)
            )

    # Traverse first array, as y
    # count has become 0
    if y == 0:
        return arr1[n-1] + maximumTip(arr1, arr2, n-1, x-1, y)

    # Traverse 2nd array, as x
    # count has become 0
    else:
        return arr2[n - 1] + maximumTip(arr1, arr2, n-1, x, y-1)

# Drive Code
N = 5
X = 3
Y = 3
A = [1, 2, 3, 4, 5]
B = [5, 4, 3, 2, 1]

# Function Call
print(maximumTip(A, B, N, X, Y))
```

## java 描述语言

```
<script>
        // JavaScript Program for the above approach

        // Function that finds the maximum tips
        // from the given arrays as per the
        // given conditions
        function maximumTip(arr1, arr2, n, x, y) {

            // Base Condition
            if (n == 0)
                return 0;

            // If both have non-zero count then
            // return max element from both array
            if (x != 0 && y != 0)
                return Math.max(
                    arr1[n - 1] + maximumTip(arr1, arr2, n - 1,
                        x - 1, y),
                    arr2[n - 1] + maximumTip(arr1, arr2, n - 1, x,
                        y - 1));

            // Traverse first array, as y
            // count has become 0
            if (y == 0)
                return arr1[n - 1] + maximumTip(arr1, arr2, n - 1,
                    x - 1, y);

            // Traverse 2nd array, as x
            // count has become 0
            else
                return arr2[n - 1] + maximumTip(arr1, arr2, n - 1,
                    x, y - 1);
        }

        // Drive Code

        let N = 5;
        let X = 3;
        let Y = 3;

        let A = [1, 2, 3, 4, 5];
        let B = [5, 4, 3, 2, 1];

        // Function Call
        document.write(maximumTip(A, B, N, X, Y));

    // This code is contributed by Potta Lokesh

    </script>
```

**Output**

```
21
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)和[记忆](https://www.geeksforgeeks.org/tabulation-vs-memoization/)进行优化。如果对 **N** 、 **X** 、 **Y** 的值进行执行追踪，可以看出存在[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)。当[递归](https://www.geeksforgeeks.org/recursion/)调用中调用相同的子问题时，这些重叠的子问题可以计算一次并存储和使用。以下是步骤:

*   初始化一个[图/字典](https://www.geeksforgeeks.org/python-mapping-key-values-to-dictionary/)来存储重叠子问题的结果。地图的关键点将是 **N** 、 **X** 和 **Y** 的组合值。
*   每次递归调用时，检查给定的键是否出现在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，然后从映射本身返回值。
*   否则，递归调用该函数并将值存储在映射中并返回存储的值。
*   如果 **X** 和 **Y** 非零，递归调用函数，取使用 **X** 和使用 **Y** 时返回值的最大值。
*   如果 **X** 或 **Y** 为零，递归调用非零数组。
*   上述递归调用结束后，再打印计算出的最大可能小费金额。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;
int dp[1001][101][101];
int rec(int level, int x, int y, int arr1[], int arr2[],
        int n)
{
    if (level == n)
        return 0;
    if (x == 0 && y == 0)
        return 0;
    if (x == 0)
        return arr2[level]
               + rec(level + 1, x, y - 1, arr1, arr2, n);
    if (y == 0)
        return arr1[level]
               + rec(level + 1, x - 1, y, arr1, arr2, n);
    if (dp[level][x][y] != -1)
        return dp[level][x][y];
    int ans = max(rec(level + 1, x - 1, y, arr1, arr2, n)
                      + arr1[level],
                  rec(level + 1, x, y - 1, arr1, arr2, n)
                      + arr2[level]);
    return dp[level][x][y] = ans;
}

void solve()
{
    int n = 7, x = 3, y = 4;
    int arr1[] = { 8, 7, 15, 19, 16, 16, 18 },
        arr2[] = { 1, 7, 15, 11, 12, 31, 9 };
    memset(dp, -1, sizeof(dp));
    cout << rec(0, x, y, arr1, arr2, n);
}
int main()
{
    solve();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.HashMap;

class GFG {

    // Function that finds the maximum tips
    // from the given arrays as per the
    // given conditions
    static int maximumTip(int[] arr1, int[] arr2, int n,
                          int x, int y,
                          HashMap<String, Integer> dd)
    {
        // Create key of N, X, Y
        String key = Integer.toString(n) + "_"
                     + Integer.toString(x) + "_"
                     + Integer.toString(y);

        // Return if the current state is
        // already calculated
        if (dd.get(key) != null)
            return dd.get(key);
        // Base Condition
        if (n == 0)
            return 0;

        // If both have non-zero count then store and
        // return max element from both array
        if (x != 0 && y != 0) {
            int temp = Math.max(
                arr1[n - 1]
                    + maximumTip(arr1, arr2, n - 1, x - 1,
                                 y, dd),
                arr2[n - 1]
                    + maximumTip(arr1, arr2, n - 1, x,
                                 y - 1, dd));
            dd.put(key, temp);
            // Return the current state result
            return dd.get(key);
        }

        // if y is zero, only x value
        // can be used
        if (y == 0) {
            int temp = arr1[n - 1]
                       + maximumTip(arr1, arr2, n - 1,
                                    x - 1, y, dd);
            dd.put(key, temp);
            // Return the current state result
            return dd.get(key);
        }

        // if x is zero, only y value
        // can be used
        else {
            int temp = arr2[n - 1]
                       + maximumTip(arr1, arr2, n - 1, x,
                                    y - 1, dd);
            dd.put(key, temp);
            // Return the current state result
            return dd.get(key);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 5;
        int X = 3;
        int Y = 3;

        int A[] = { 1, 2, 3, 4, 5 };
        int B[] = { 5, 4, 3, 2, 1 };

        // Stores the results of the
        // overlapping state
        HashMap<String, Integer> dd
            = new HashMap<String, Integer>();

        // Function Call
        System.out.println(maximumTip(A, B, N, X, Y, dd));
    }
}

// This code is contributed by MuskanKalra1
```

## 蟒蛇 3

```
# Python program for the above approach

# Function that finds the maximum tips
# from the given arrays as per the
# given conditions
def maximumTip(arr1, arr2, n, x, y, dd):

    # Create key of N, X, Y
    key = str(n) + '_' + str(x) + '_' + str(y)

    # Return if the current state is
    # already calculated
    if key in dd:
        return dd[key]

    # Base Condition
    if n == 0:
        return 0

    # Store and return
    if x != 0 and y != 0:
        dd[key] = max(
            arr1[n-1] + maximumTip(arr1, arr2, n-1, x-1, y, dd),
            arr2[n-1] + maximumTip(arr1, arr2, n-1, x, y-1, dd)
        )

        # Return the current state result
        return dd[key]

    # If y is zero, only x value
    # can be used
    if y == 0:
        dd[key] = arr1[n-1] + maximumTip(arr1, arr2, n-1, x-1, y, dd)

        # Return the current state result
        return dd[key]

    # If x is zero, only y value
    # can be used
    else:

        dd[key] = arr2[n-1] + maximumTip(arr1, arr2, n-1, x, y-1, dd)

        # Return the current state result
        return dd[key]

# Drive Code
N = 5
X = 3
Y = 3
A = [1, 2, 3, 4, 5]
B = [5, 4, 3, 2, 1]

# Stores the results of the
# overlapping state
dd = {}

# Function Call
print(maximumTip(A, B, N, X, Y, dd))
```

## java 描述语言

```
<script>

// JavaScript program for the above approach
// Function that finds the maximum tips
// from the given arrays as per the
// given conditions

function maximumTip(arr1, arr2, n, x, y, dd) {
  // Create key of N, X, Y
  key = `${n}_${x}_${y}`;

  // Return if the current state is
  // already calculated
  for (var key in dd) {
    return dd[key];
  }

  // Base Condition
  if (n == 0) {
    return 0;
  }

  // Store and return
  if (x != 0 && y != 0) {
    dd[key] = Math.max(
      arr1[n - 1] + maximumTip(arr1, arr2, n - 1, x - 1, y, dd),
      arr2[n - 1] + maximumTip(arr1, arr2, n - 1, x, y - 1, dd)
    );

    // Return the current state result
    return dd[key];
  }

  // If y is zero, only x value
  // can be used
  if (y == 0)
  {
    dd[key] = arr1[n - 1] + maximumTip(arr1, arr2, n - 1, x - 1, y, dd);

    // Return the current state result
    return dd[key];
  }
  // If x is zero, only y value
  // can be used
  else {
    dd[key] = arr2[n - 1] + maximumTip(arr1, arr2, n - 1, x, y - 1, dd);
    // Return the current state result
    return dd[key];
  }
}

// Drive Code
let N = 5;
let X = 3;
let Y = 3;
let A = [1, 2, 3, 4, 5];
let B = [5, 4, 3, 2, 1];

// Stores the results of the
// overlapping state
dd = {};

// Function Call
document.write(maximumTip(A, B, N, X, Y, dd));

// This code is contributed by rdtank.
</script>
```

**Output**

```
21
```

***时间复杂度:**O(N * X * Y)*
T5**辅助空间:** O(N*X*Y)