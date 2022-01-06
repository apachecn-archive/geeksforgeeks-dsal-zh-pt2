# 在元素上交替加减号后最大化子序列和

> 原文:[https://www . geesforgeks . org/maximize-subsequer-sum-after-put-加号-减号-alternative-on-elements/](https://www.geeksforgeeks.org/maximize-subsequence-sum-after-putting-plus-minus-sign-alternatively-on-elements/)

给定一个大小为 **N** 的数组 **arr[]** 。任务是找到数组中任何**子序列**元素的**替代减–加**可以达到的**最大**分数。

**示例:**

> **输入:** arr[] = {2，3，6，5，4，7，8}，N = 7
> **输出:** 10
> **解释:**选取顺序为{2，3， **6** ，5， **4** ，7， **8** } = {6，4，8}。所以，备选减–加=(6**–**4**+**8)= 10。
> 
> **输入:** {9，2，4，5，3}，N =5
> **输出:** 12

**方法:**我们可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的方法来解决问题。

*   让 **dp1 <sub>i</sub>** ⇢是来自第一个 **i** 元素的前缀上的子序列的最大可能和，假设子序列的长度是**奇数**。类似地，输入 **dp2 <sub>i</sub>** ⇢仅用于**甚至**长度的子序列。
*   那么**dp1<sub>I</sub>T3**dp2<sub>I</sub>T7】就很容易重新计算为:****
    *   <sub>DP 1<sub><sub>=**最大值(DP 1<sub>【I】</sub>、DP 2<sub>【I】</sub>+arr<sub>【I】</sub>**)</sub></sub></sub>
    *   DP 2<sub>I+1</sub>=**最大值(dp2 <sub>i</sub> ，DP 1<sub>I</sub>—arr<sub>【I【T10 })</sub>**
*   初始值为**dp1<sub>0</sub>**=**∨**、 **dp2 <sub>0</sub>** = **0** ，答案将存储在**max**(**dp1<sub>n</sub>**、 **dp2 <sub>n</sub>** )。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define INF 1e9

// Function to find the maximum score
// achieved by alternative minus-plus
// of elements of a subsequence in
// the given array
int maxScore(int arr[], int N)
{
    vector<int> dp1(N + 1);
    vector<int> dp2(N + 1);

    dp1[0] = -INF;
    dp2[0] = 0;

    for (int i = 0; i < N; ++i) {
        dp1[i + 1] = max(dp1[i], dp2[i] + arr[i]);
        dp2[i + 1] = max(dp2[i], dp1[i] - arr[i]);
    }
    // Return the maximum
    return max(dp1.back(), dp2.back());
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 6, 5, 4, 7, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maxScore(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    static double INF = 1E9;

    // Function to find the maximum score
    // achieved by alternative minus-plus
    // of elements of a subsequence in
    // the given array
    public static int maxScore(int arr[], int N) {
        int[] dp1 = new int[N + 1];
        int[] dp2 = new int[N + 1];

        dp1[0] = (int) -INF;
        dp2[0] = 0;

        for (int i = 0; i < N; ++i) {
            dp1[i + 1] = Math.max(dp1[i], dp2[i] + arr[i]);
            dp2[i + 1] = Math.max(dp2[i], dp1[i] - arr[i]);
        }

        // Return the maximum
        return Math.max(dp1[dp1.length - 1], dp2[dp2.length - 1]);
    }

    // Driver Code
    public static void main(String args[]) {
        int arr[] = { 2, 3, 6, 5, 4, 7, 8 };
        int N = arr.length;

        System.out.println(maxScore(arr, N));
    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach
INF = 1e9

# Function to find the maximum score
# achieved by alternative minus-plus
# of elements of a subsequence in
# the given array
def maxScore(arr, N):
    dp1 = [0] * (N + 1)
    dp2 = [0] * (N + 1)

    dp1[0] = -INF
    dp2[0] = 0

    for i in range(N):
        dp1[i + 1] = max(dp1[i], dp2[i] + arr[i])
        dp2[i + 1] = max(dp2[i], dp1[i] - arr[i])

    # Return the maximum
    return max(dp1[len(dp1) - 1], dp2[len(dp2) - 1])

# Driver Code
arr = [2, 3, 6, 5, 4, 7, 8]
N = len(arr)

print(maxScore(arr, N))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# code to implement the above approach
using System;
class GFG
{

    static double INF = 1E9;

    // Function to find the maximum score
    // achieved by alternative minus-plus
    // of elements of a subsequence in
    // the given array
    public static int maxScore(int []arr, int N) {
        int []dp1 = new int[N + 1];
        int []dp2 = new int[N + 1];

        dp1[0] = (int) -INF;
        dp2[0] = 0;

        for (int i = 0; i < N; ++i) {
            dp1[i + 1] = Math.Max(dp1[i], dp2[i] + arr[i]);
            dp2[i + 1] = Math.Max(dp2[i], dp1[i] - arr[i]);
        }

        // Return the maximum
        return Math.Max(dp1[dp1.Length - 1], dp2[dp2.Length - 1]);
    }

    // Driver Code
    public static void Main() {
        int []arr = { 2, 3, 6, 5, 4, 7, 8 };
        int N = arr.Length;

        Console.Write(maxScore(arr, N));
    }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

        // JavaScript Program to implement
        // the above approach
        let INF = 1e9

        // Function to find the maximum score
        // achieved by alternative minus-plus
        // of elements of a subsequence in
        // the given array
        function maxScore(arr, N) {
            let dp1 = new Array(N + 1);
            let dp2 = new Array(N + 1);

            dp1[0] = -INF;
            dp2[0] = 0;

            for (let i = 0; i < N; ++i) {
                dp1[i + 1] = Math.max(dp1[i], dp2[i] + arr[i]);
                dp2[i + 1] = Math.max(dp2[i], dp1[i] - arr[i]);
            }

            // Return the maximum
            return Math.max(dp1[dp1.length - 1], dp2[dp2.length - 1]);
        }

        // Driver Code
        let arr = [2, 3, 6, 5, 4, 7, 8]
        let N = arr.length;

        document.write(maxScore(arr, N));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
10
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)