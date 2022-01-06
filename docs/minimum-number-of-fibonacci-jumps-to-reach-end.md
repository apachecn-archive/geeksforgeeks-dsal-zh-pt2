# 到达终点的最小斐波那契跳跃次数

> 原文:[https://www . geeksforgeeks . org/Fibonacci 最小跳数到达终点/](https://www.geeksforgeeks.org/minimum-number-of-fibonacci-jumps-to-reach-end/)

给定一组 **0s** 和 **1s** ，如果任何特定指数 **i** 具有值 **1** ，则它是一个**安全指数**，如果该值是 **0** ，则它是一个**不安全指数**。站在指数 **-1** (来源)的人只能落在安全的指数上，他必须到达第 N 个指数(最后位置)。每次跳跃，该男子只能行进等于任意 [**斐波那契数**](https://en.wikipedia.org/wiki/Fibonacci_number) 的距离。只要人只能向前跳，你就必须尽量减少步数。
**注:**前几个斐波那契数是–0、1、1、2、3、5、8、13、21……。
**举例:**

> **输入:** arr[]= {0，0，0，1，1，0，1，0，0，0，0，0}
> **输出:** 3
> 此人将从:
> 1)索引-1 跳转到索引 4(跳转距离= 5)
> 2)索引 4 到索引 6(跳转距离= 2)
> 3)索引 6 到目的地(跳转距离= 5)
> **输入:**arr[=]

**进场:**

*   首先，我们将创建一个数组 fib[]来存储斐波那契数。
*   然后，我们将创建一个 DP 数组，并使用 **INT_MAX** 和第 0 个索引 **DP[0] = 0** 对其进行初始化，并将按照与 [**硬币数量最少的硬币兑换问题**](https://www.geeksforgeeks.org/find-minimum-number-of-coins-that-make-a-change/) 相同的方式移动。
*   The DP definition and recurrence is as followed:

    ```

     DP[i] = min( DP[i], 1 + DP[i-fib[j]] )

    where i is the current index and j denotes
    the jth fibonacci number of which the
    jump is possible
    ```

    *   这里 DP[i]表示考虑所有斐波那契数达到指数 **i** 所需的最小步数。

    以下是实施办法:

    ## C++

    ```
    // A Dynamic Programming based
    // C++ program to find minimum
    // number of jumps to reach
    // Destination
    #include <bits/stdc++.h>
    using namespace std;
    #define MAX 1e9

    // Function that returns the min
    // number of jump to reach the
    // destination
    int minJumps(int arr[], int N)
    {
        // We consider only those Fibonacci
        // numbers which are less than n,
        // where we can consider fib[30]
        // to be the upper bound as this
        // will cross 10^5
        int fib[30];
        fib[0] = 0;
        fib[1] = 1;
        for (int i = 2; i < 30; i++)
            fib[i] = fib[i - 1] + fib[i - 2];

        // DP[i] will be storing the minimum
        // number of jumps required for
        // the position i. So DP[N+1] will
        // have the result we consider 0
        // as source and N+1 as the destination
        int DP[N + 2];

        // Base case (Steps to reach source is)
        DP[0] = 0;

        // Initialize all table values as Infinite
        for (int i = 1; i <= N + 1; i++)
            DP[i] = MAX;

        // Compute minimum jumps required
        // considering each Fibonacci
        // numbers one by one.

        // Go through each positions
        // till destination.
        for (int i = 1; i <= N + 1; i++) {

            // Calculate the minimum of that
            // position if all the Fibonacci
            // numbers are considered
            for (int j = 1; j < 30; j++) {

                // If the position is safe
                // or the position is the
                // destination then only we
                // calculate the minimum
                // otherwise the cost is
                // MAX as default
                if ((arr[i - 1] == 1
                     || i == N + 1)
                    && i - fib[j] >= 0)
                    DP[i] = min(DP[i],
                                1 + DP[i - fib[j]]);
            }
        }

        // -1 denotes if there is
        // no path possible
        if (DP[N + 1] != MAX)
            return DP[N + 1];
        else
            return -1;
    }

    // Driver program to test above function
    int main()
    {
        int arr[] = { 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0 };
        int n = sizeof(arr) / sizeof(arr[0]);

        cout << minJumps(arr, n);
        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // A Dynamic Programming based 
    // Java program to find minimum 
    // number of jumps to reach 
    // Destination
    import java.util.*; 
    import java.lang.*; 

    class GFG 
    {

    // Function that returns the min 
    // number of jump to reach the 
    // destination
    public static int minJumps(int arr[], int N) 
    {
        int MAX = 1000000;

        // We consider only those Fibonacci 
        // numbers which are less than n, 
        // where we can consider fib[30] 
        // to be the upper bound as this 
        // will cross 10^5 
        int[] fib = new int[30]; 
        fib[0] = 0; 
        fib[1] = 1;

        for (int i = 2; i < 30; i++) 
        fib[i] = fib[i - 1] + fib[i - 2]; 

        // DP[i] will be storing the minimum 
        // number of jumps required for 
        // the position i. So DP[N+1] will 
        // have the result we consider 0 
        // as source and N+1 as the destination 
        int[] DP = new int[N + 2]; 

        // Base case (Steps to reach source is) 
        DP[0] = 0; 

        // Initialize all table values as Infinite 
        for (int i = 1; i <= N + 1; i++) 
            DP[i] = MAX; 

        // Compute minimum jumps required 
        // considering each Fibonacci 
        // numbers one by one. 

        // Go through each positions 
        // till destination. 
        for (int i = 1; i <= N + 1; i++)
        { 

            // Calculate the minimum of that 
            // position if all the Fibonacci 
            // numbers are considered 
            for (int j = 1; j < 30; j++) 
            { 

                // If the position is safe 
                // or the position is the 
                // destination then only we 
                // calculate the minimum 
                // otherwise the cost is 
                // MAX as default 
                if ((i == N + 1 || 
                     arr[i - 1] == 1) &&
                     i - fib[j] >= 0) 
                    DP[i] = Math.min(DP[i], 1 +
                                     DP[i - fib[j]]); 
            } 
        } 

        // -1 denotes if there is 
        // no path possible 
        if (DP[N + 1] != MAX) 
            return DP[N + 1]; 
        else
            return -1; 
    } 

    // Driver Code 
    public static void main (String[] args) 
    { 
        int[] arr = new int[]{ 0, 0, 0, 1, 1, 0,
                                  1, 0, 0, 0, 0 }; 
        int n = 11; 
        int ans = minJumps(arr, n); 
        System.out.println(ans); 
    }
    }

    // This code is contributed by Mehul
    ```

    ## 蟒蛇 3

    ```
    # A Dynamic Programming based Python3 program 
    # to find minimum number of jumps to reach
    # Destination
    MAX = 1e9

    # Function that returns the min number 
    # of jump to reach the destination
    def minJumps(arr, N):

        # We consider only those Fibonacci
        # numbers which are less than n,
        # where we can consider fib[30]
        # to be the upper bound as this
        # will cross 10^5
        fib = [0 for i in range(30)]
        fib[0] = 0
        fib[1] = 1
        for i in range(2, 30):
            fib[i] = fib[i - 1] + fib[i - 2]

        # DP[i] will be storing the minimum
        # number of jumps required for
        # the position i. So DP[N+1] will
        # have the result we consider 0
        # as source and N+1 as the destination
        DP = [0 for i in range(N + 2)]

        # Base case (Steps to reach source is)
        DP[0] = 0

        # Initialize all table values as Infinite
        for i in range(1, N + 2):
            DP[i] = MAX

        # Compute minimum jumps required
        # considering each Fibonacci
        # numbers one by one.

        # Go through each positions
        # till destination.
        for i in range(1, N + 2):

            # Calculate the minimum of that
            # position if all the Fibonacci
            # numbers are considered
            for j in range(1, 30):

                # If the position is safe or the 
                # position is the destination then 
                # only we calculate the minimum
                # otherwise the cost is MAX as default
                if ((arr[i - 1] == 1 or i == N + 1) and 
                                        i - fib[j] >= 0):
                    DP[i] = min(DP[i], 1 + DP[i - fib[j]])

        # -1 denotes if there is
        # no path possible
        if (DP[N + 1] != MAX):
            return DP[N + 1]
        else:
            return -1

    # Driver Code
    arr = [0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0, 0]
    n = len(arr)

    print(minJumps(arr, n - 1))

    # This code is contributed by Mohit Kumar
    ```

    ## C#

    ```
    // A Dynamic Programming based 
    // C# program to find minimum 
    // number of jumps to reach 
    // Destination
    using System;
    using System.Collections.Generic;

    class GFG 
    {

    // Function that returns the min 
    // number of jump to reach the 
    // destination
    public static int minJumps(int []arr, int N) 
    {
        int MAX = 1000000;

        // We consider only those Fibonacci 
        // numbers which are less than n, 
        // where we can consider fib[30] 
        // to be the upper bound as this 
        // will cross 10^5 
        int[] fib = new int[30]; 
        fib[0] = 0; 
        fib[1] = 1;

        for (int i = 2; i < 30; i++) 
        fib[i] = fib[i - 1] + fib[i - 2]; 

        // DP[i] will be storing the minimum 
        // number of jumps required for 
        // the position i. So DP[N+1] will 
        // have the result we consider 0 
        // as source and N+1 as the destination 
        int[] DP = new int[N + 2]; 

        // Base case (Steps to reach source is) 
        DP[0] = 0; 

        // Initialize all table values as Infinite 
        for (int i = 1; i <= N + 1; i++) 
            DP[i] = MAX; 

        // Compute minimum jumps required 
        // considering each Fibonacci 
        // numbers one by one. 

        // Go through each positions 
        // till destination. 
        for (int i = 1; i <= N + 1; i++)
        { 

            // Calculate the minimum of that 
            // position if all the Fibonacci 
            // numbers are considered 
            for (int j = 1; j < 30; j++) 
            { 

                // If the position is safe 
                // or the position is the 
                // destination then only we 
                // calculate the minimum 
                // otherwise the cost is 
                // MAX as default 
                if ((i == N + 1 || 
                    arr[i - 1] == 1) &&
                    i - fib[j] >= 0) 
                    DP[i] = Math.Min(DP[i], 1 +
                                     DP[i - fib[j]]); 
            } 
        } 

        // -1 denotes if there is 
        // no path possible 
        if (DP[N + 1] != MAX) 
            return DP[N + 1]; 
        else
            return -1; 
    } 

    // Driver Code 
    public static void Main (String[] args) 
    { 
        int[] arr = new int[]{ 0, 0, 0, 1, 1, 0,
                                  1, 0, 0, 0, 0 }; 
        int n = 11; 
        int ans = minJumps(arr, n); 
        Console.WriteLine(ans); 
    }
    }

    // This code is contributed by Princi Singh
    ```

    ## java 描述语言

    ```
    <script>

    // A Dynamic Programming based
    // Javascript program to find minimum
    // number of jumps to reach
    // Destination

    const MAX = 1000000000;

    // Function that returns the min
    // number of jump to reach the
    // destination
    function minJumps(arr, N)
    {
        // We consider only those Fibonacci
        // numbers which are less than n,
        // where we can consider fib[30]
        // to be the upper bound as this
        // will cross 10^5
        let fib = new Array(30);
        fib[0] = 0;
        fib[1] = 1;
        for (let i = 2; i < 30; i++)
            fib[i] = fib[i - 1] + fib[i - 2];

        // DP[i] will be storing the minimum
        // number of jumps required for
        // the position i. So DP[N+1] will
        // have the result we consider 0
        // as source and N+1 as the destination
        let DP = new Array(N + 2);

        // Base case (Steps to reach source is)
        DP[0] = 0;

        // Initialize all table values as Infinite
        for (let i = 1; i <= N + 1; i++)
            DP[i] = MAX;

        // Compute minimum jumps required
        // considering each Fibonacci
        // numbers one by one.

        // Go through each positions
        // till destination.
        for (let i = 1; i <= N + 1; i++) {

            // Calculate the minimum of that
            // position if all the Fibonacci
            // numbers are considered
            for (let j = 1; j < 30; j++) {

                // If the position is safe
                // or the position is the
                // destination then only we
                // calculate the minimum
                // otherwise the cost is
                // MAX as default
                if ((arr[i - 1] == 1
                     || i == N + 1)
                    && i - fib[j] >= 0)
                    DP[i] = Math.min(DP[i],
                                1 + DP[i - fib[j]]);
            }
        }

        // -1 denotes if there is
        // no path possible
        if (DP[N + 1] != MAX)
            return DP[N + 1];
        else
            return -1;
    }

    // Driver program to test above function
        let arr = [ 0, 0, 0, 1, 1, 0, 1, 0, 0, 0, 0 ];
        let n = arr.length;

        document.write(minJumps(arr, n));

    </script>
    ```

    **Output:** 

    ```
    3
    ```

    **时间复杂度:** ![O(Nlog(N))  ](img/11800cd73564bc1f3de848efdee4308e.png "Rendered by QuickLaTeX.com")