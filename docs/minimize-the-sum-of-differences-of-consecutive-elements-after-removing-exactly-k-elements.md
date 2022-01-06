# 精确去除 K 个元素后，最小化连续元素的差值之和

> 原文:[https://www . geeksforgeeks . org/最小化移除精确 k 元素后连续元素的差异总和/](https://www.geeksforgeeks.org/minimize-the-sum-of-differences-of-consecutive-elements-after-removing-exactly-k-elements/)

给定长度为“N”的排序数组和整数“K”(K<n the="" task="" is="" to="" remove="" exactly="" elements="" from="" array="" such="" that="" sum="" of="" difference="" consecutive="" minimized.="">**)示例:**</n> 

```
Input :  arr[]  = {1, 2, 3, 4}, k = 1
Output : 2

Let's consider all possible cases.
a) Remove 0th index: arr[] = {2, 3, 4}, ans = 2
b) Remove 1th index: arr[] = {1, 3, 4}, ans = 3
c) Remove 2th index: arr[] = {1, 2, 4}, ans = 3
d) Remove 3th index: arr[] = {1, 2, 3}, ans = 2

Minimum of them all is 2, thus answer = 2

Input : arr[] = {1, 2, 10}, k = 1
Output : 1
```

**方法:**
从末端去除元素是降低总和值的唯一可能方法。
例如，让数组= {1，2，3，4}。如果数组中的第二个元素被移除，则总和保持与前一个相同，即等于 3。但是，如果删除第一个或最后一个元素，总和将减少到 2。
**贪婪方法:**在每一步中，移除使总和减少更多的元素。例如，让数组= {1，3，9，33}，33 被移除，因为它将总和从 32 减少到 8。
但是，这种贪婪的方法对某些测试用例不起作用。例子。arr[] = {1，2，100，120，140}和 k = 2。这里，贪婪方法的最终数组是{1，2，100}，其中最佳数组是{100，120，140}。
**动态编程:**DP 的状态如下:
DP[l][r]是指通过移除子阵列 arr[l 至 r]中所需的元素数量可以获得的最小总和。
因此，递归关系为

```
DP[l][r] = min(DP[l][r-1], DP[l+1][r])
```

下面是上述思想的 C++实现。

## C++

```
// C++ implementation of the above approach.
#include <bits/stdc++.h>
using namespace std;
#define N 100
#define INF 1000000

// states of DP
int dp[N][N];
bool vis[N][N];

// function to find minimum sum
int findSum(int* arr, int n, int k, int l, int r)
{
    // base-case
    if ((l) + (n - 1 - r) == k)
        return arr[r] - arr[l];
    // if state is solved before, return
    if (vis[l][r])
        return dp[l][r];
    // marking the state as solved
    vis[l][r] = 1;
    // recurrence relation
    return dp[l][r] = min(findSum(arr, n, k, l, r - 1),
                          findSum(arr, n, k, l + 1, r));
}

// driver function
int32_t main()
{
    // input values
    int arr[] = { 1, 2, 100, 120, 140 };
    int k = 2;
    int n = sizeof(arr) / sizeof(int);

    // callin the required function;
    cout << findSum(arr, n, k, 0, n - 1);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach.
class GFG
{
    final static int N = 100 ;
    final static int INF = 1000000 ;

    // states of DP
    static int dp[][] = new int[N][N];
    static int vis[][] = new int[N][N];

    // function to find minimum sum
    static int findSum(int []arr, int n,
                       int k, int l, int r)
    {
        // base-case
        if ((l) + (n - 1 - r) == k)
            return arr[r] - arr[l];

        // if state is solved before, return
        if (vis[l][r] == 1)
            return dp[l][r];

        // marking the state as solved
        vis[l][r] = 1;

        // recurrence relation
        dp[l][r] = Math.min(findSum(arr, n, k, l, r - 1),
                            findSum(arr, n, k, l + 1, r));

        return dp[l][r] ;
    }

    // Driver function
    public static void main (String[] args)
    {
        // input values
        int arr[] = { 1, 2, 100, 120, 140 };
        int k = 2;
        int n = arr.length;

        // calling the required function;
        System.out.println(findSum(arr, n, k, 0, n - 1));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach.
import numpy as np

N = 100
INF = 1000000

# states of DP
dp = np.zeros((N, N));
vis = np.zeros((N, N));

# function to find minimum sum
def findSum(arr, n, k, l, r) :

    # base-case
    if ((l) + (n - 1 - r) == k) :
        return arr[r] - arr[l];

    # if state is solved before, return
    if (vis[l][r]) :
        return dp[l][r];

    # marking the state as solved
    vis[l][r] = 1;

    # recurrence relation
    dp[l][r] = min(findSum(arr, n, k, l, r - 1),
                    findSum(arr, n, k, l + 1, r));

    return dp[l][r]

# driver function
if __name__ == "__main__" :

    # input values
    arr = [ 1, 2, 100, 120, 140 ];
    k = 2;
    n = len(arr);

    # calling the required function;
    print(findSum(arr, n, k, 0, n - 1));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach.
using System;

class GFG
{
    static int N = 100 ;

    // states of DP
    static int [,]dp = new int[N, N];
    static int [,]vis = new int[N, N];

    // function to find minimum sum
    static int findSum(int []arr, int n,
                    int k, int l, int r)
    {
        // base-case
        if ((l) + (n - 1 - r) == k)
            return arr[r] - arr[l];

        // if state is solved before, return
        if (vis[l, r] == 1)
            return dp[l, r];

        // marking the state as solved
        vis[l, r] = 1;

        // recurrence relation
        dp[l, r] = Math.Min(findSum(arr, n, k, l, r - 1),
                            findSum(arr, n, k, l + 1, r));

        return dp[l, r] ;
    }

    // Driver function
    public static void Main ()
    {
        // input values
        int []arr = { 1, 2, 100, 120, 140 };
        int k = 2;
        int n = arr.Length;

        // calling the required function;
        Console.WriteLine(findSum(arr, n, k, 0, n - 1));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach.
var N = 100;
var INF = 1000000;

// states of DP
var dp = Array.from(Array(N), ()=> Array(N));
var vis = Array.from(Array(N), ()=> Array(N));

// function to find minimum sum
function findSum(arr, n, k, l, r)
{
    // base-case
    if ((l) + (n - 1 - r) == k)
        return arr[r] - arr[l];

    // if state is solved before, return
    if (vis[l][r])
        return dp[l][r];

    // marking the state as solved
    vis[l][r] = 1;

    // recurrence relation
    dp[l][r] = Math.min(findSum(arr, n, k, l, r - 1),
                        findSum(arr, n, k, l + 1, r));

    return dp[l][r];
}

// driver function
// input values
var arr = [1, 2, 100, 120, 140];
var k= 2;
var n = arr.length;

// calling the required function;
document.write( findSum(arr, n, k, 0, n - 1));

</script>
```

**Output:** 

```
40
```

**时间复杂度:**O(n^2)
T3】注:对于这个问题也存在一个 o(n)的方法。但只要稍加修改，上述方法也可以用来解决未排序数组的问题。
**替代方法:**
仅从左右角移除元素。因此，如果 **x** 元素从左边移除，那么 **K-x** 元素在**中每 x(0，K)从右边移除一个。**
如果执行上述操作，差值之和将等于**arr[N-(K-X)-1]–arr[X]**。
在从(0，K)迭代 x 时，从获得的值中选择最小值。
**例:**

```
Input: arr[] = {1, 3, 7, 8, 13} ; k = 3
Output:  1
Explanation: 
Looping from X = 0 to X = K;
1) X = 0 and K-X = 3
 So 0 elements removed from left and 3 from right.
 array will be {1, 3} and answer will be 3 - 1 = 2\. 
 min = 2
2) X = 1 and K-X = 2
 So 1 elements removed from left and 2 from right.
 array will be {3, 7} and answer will be 7 - 3  = 4.
  min = 2
3) X = 2 and K-X = 1
 So 2 elements removed from left and 1 from right.
 array will be {7, 8} and answer will be 8 - 7 = 1.
 min = 1
4) X = 3 and K-X = 0
 So 3 elements removed from left and 0 from right.
 array will be {8, 13} and answer will be 13 - 8 = 5.
 min =  1
```

下面是上述方法的实现。

## C++

```
//C++ implementation of the above approach.
#include <bits/stdc++.h>
using namespace std;

// function to find minimum sum
int findSum(int* arr, int n, int k)
{

    // variable to store final answer
    // and initialising it with the values
    // when 0 elements is removed from the left and
    // K from the right.
    int ans = arr[n - k - 1] - arr[0];

    // loop to simulate removal of elements
    for (int i = 1; i <= k; i++) {
        //removing i elements from the left and and K-i elements
        //from the right and updating the answer correspondingly
        ans = min(arr[n - 1 - (k - i)] - arr[i], ans);
    }

    // returning final answer
    return ans;
}

// driver function
int32_t main()
{
    // input values
    int arr[] = { 1, 2, 100, 120, 140 };
    int k = 2;
    int n = sizeof(arr) / sizeof(int);

    // callin the required function;
    cout << findSum(arr, n, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach.
class GFG
{

    // function to find minimum sum
    static int findSum(int []arr, int n, int k)
    {

        // variable to store final answer
        // and initialising it with the values
        // when 0 elements is removed from the left and
        // K from the right.
        int ans = arr[n - k - 1] - arr[0];

        // loop to simulate removal of elements
        for (int i = 1; i <= k; i++)
        {
            // removing i elements from the left and and K-i elements
            // from the right and updating the answer correspondingly
            ans = Math.min(arr[n - 1 - (k - i)] - arr[i], ans);
        }

        // returning final answer
        return ans;
    }

    // Driver function
    public static void main (String[] args)
    {
        // input values
        int arr[] = { 1, 2, 100, 120, 140 };
        int k = 2;
        int n = arr.length;

        // callin the required function;
        System.out.println(findSum(arr, n, k));
    }

}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach.

# function to find minimum sum
def findSum(arr, n, k) :

    # variable to store final answer
    # and initialising it with the values
    # when 0 elements is removed from the left and
    # K from the right.
    ans = arr[n - k - 1] - arr[0];

    # loop to simulate removal of elements
    for i in range(1, k + 1) :

        # removing i elements from the left and and K-i elements
        # from the right and updating the answer correspondingly
        ans = min(arr[n - 1 - (k - i)] - arr[i], ans);

    # returning final answer
    return ans;

# Driver code
if __name__ == "__main__" :

    # input values
    arr = [ 1, 2, 100, 120, 140 ];
    k = 2;
    n = len(arr);

    # calling the required function;
    print(findSum(arr, n, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach.
using System;

class GFG
{

    // function to find minimum sum
    static int findSum(int []arr, int n, int k)
    {

        // variable to store final answer
        // and initialising it with the values
        // when 0 elements is removed from the left and
        // K from the right.
        int ans = arr[n - k - 1] - arr[0];

        // loop to simulate removal of elements
        for (int i = 1; i <= k; i++)
        {
            // removing i elements from the left and and K-i elements
            // from the right and updating the answer correspondingly
            ans = Math.Min(arr[n - 1 - (k - i)] - arr[i], ans);
        }

        // returning final answer
        return ans;
    }

    // Driver function
    public static void Main ()
    {
        // input values
        int []arr = { 1, 2, 100, 120, 140 };
        int k = 2;
        int n = arr.Length;

        // calling the required function;
        Console.WriteLine(findSum(arr, n, k));
    }

}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach.

// function to find minimum sum
function findSum(arr, n, k)
{

    // variable to store final answer
    // and initialising it with the values
    // when 0 elements is removed from the left and
    // K from the right.
    var ans = arr[n - k - 1] - arr[0];

    // loop to simulate removal of elements
    for (var i = 1; i <= k; i++) {
        // removing i elements from the left and and K-i elements
        // from the right and updating the answer correspondingly
        ans = Math.min(arr[n - 1 - (k - i)] - arr[i], ans);
    }

    // returning final answer
    return ans;
}

// driver function

// input values
var arr = [1, 2, 100, 120, 140];
var k = 2;
var n = arr.length;

// callin the required function;
document.write( findSum(arr, n, k));

// This code is contributed by noob2000.

</script>
```

**Output:** 

```
40
```