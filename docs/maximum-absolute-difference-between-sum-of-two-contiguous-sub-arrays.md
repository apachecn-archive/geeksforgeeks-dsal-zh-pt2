# 两个相邻子阵列之和的最大绝对差

> 原文:[https://www . geeksforgeeks . org/两个连续子数组之和的最大绝对差值/](https://www.geeksforgeeks.org/maximum-absolute-difference-between-sum-of-two-contiguous-sub-arrays/)

给定一个整数数组，找到两个不重叠的连续子数组，使得两个子数组之和的绝对差最大。

**示例:**

```
Input: [-2, -3, 4, -1, -2, 1, 5, -3]
Output: 12
Two subarrays are [-2, -3] and [4, -1, -2, 1, 5]

Input: [2, -1, -2, 1, -4, 2, 8]
Output: 16
Two subarrays are [-1, -2, 1, -4] and [2, 8] 
```

预期时间复杂度为 0(n)。

其思想是对于给定数组 arr[0…n-1]中的每个索引 I，计算位于子数组 arr[0…i]和 arr[i+1 …n-1]中的子数组的最大和最小和。我们维护四个数组，对于数组中的每个索引 I，这些数组存储子数组 arr[0…i]和 arr[i+1 … n-1]中的最大和最小和。

```
leftMax[] : An element leftMax[i] of this 
            array stores the maximum value 
            in subarray arr[0..i]

leftMin[] : An element leftMin[i] of this 
            array stores the minimum value
            in subarray arr[0..i]

rightMax[] : An element rightMax[i] of this 
             array stores the maximum value 
             in subarray arr[i+1..n-1]

rightMin[] : An element rightMin[i] of this
             array stores the minimum value
             in subarray arr[i+1..n-1] 
```

我们可以使用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)在 O(n)时间内构建以上四个数组。

为了计算位于 arr[0…i]的最大和子阵，我们从 0 到 n-1 运行卡丹算法，为了寻找位于 arr[i+1 … n-1]的最大和子阵，我们从 n-1 到 0 运行卡丹算法。

2.  Kadane’s algorithm can be modified to find minimum absolute sum of a subarray as well. The idea is to change the sign of each element in the array and run Kadane Algorithm to find maximum sum subarray that lies in arr[0…i] and arr[i+1 … n-1]. Now invert the sign of maximum subarray sum found. That will be our minimum subarray sum. This idea is taken from [here](https://www.geeksforgeeks.org/maximum-contiguous-circular-sum/).

    现在从上面四个数组中，我们可以很容易地找到两个相邻子数组之和的最大绝对差。对于每个索引 I，取最大值

    1.  abs(位于 arr[0…i]的最大和子阵列–位于 arr[i+1…n-1]的最小和子阵列)
    2.  abs(位于 arr[0…i]的最小和子阵列–位于 arr[i+1…n-1]的最大和子阵列)

    以下是上述想法的实现。

    ## C++

    ```
    // C++ program to find two non-overlapping contiguous
    // sub-arrays such that the absolute difference
    // between the sum of two sub-array is maximum.
    #include <bits/stdc++.h>
    using namespace std;

    // Find maximum subarray sum for subarray [0..i]
    // using standard Kadane's algorithm. This version of
    // Kadane's Algorithm will work if all numbers are
    // negative.
    int maxLeftSubArraySum(int a[], int size, int sum[])
    {
        int max_so_far = a[0];
        int curr_max = a[0];
        sum[0] = max_so_far;

        for (int i = 1; i < size; i++)
        {
            curr_max = max(a[i], curr_max + a[i]);
            max_so_far = max(max_so_far, curr_max);
            sum[i] = max_so_far;
        }

        return max_so_far;
    }

    // Find maximum subarray sum for subarray [i..n]
    // using Kadane's algorithm. This version of Kadane's
    // Algorithm will work if all numbers are negative
    int maxRightSubArraySum(int a[], int n, int sum[])
    {
        int max_so_far = a[n];
        int curr_max = a[n];
        sum[n] = max_so_far;

        for (int i = n-1; i >= 0; i--)
        {
            curr_max = max(a[i], curr_max + a[i]);
            max_so_far = max(max_so_far, curr_max);
            sum[i] = max_so_far;
        }

        return max_so_far;
    }

    // The function finds two non-overlapping contiguous
    // sub-arrays such that the absolute difference
    // between the sum of two sub-array is maximum.
    int findMaxAbsDiff(int arr[], int n)
    {
        // create and build an array that stores
        // maximum sums of subarrays that lie in
        // arr[0...i]
        int leftMax[n];
        maxLeftSubArraySum(arr, n, leftMax);

        // create and build an array that stores
        // maximum sums of subarrays that lie in
        // arr[i+1...n-1]
        int rightMax[n];
        maxRightSubArraySum(arr, n-1, rightMax);

        // Invert array (change sign) to find minumum
        // sum subarrays.
        int invertArr[n];
        for (int i = 0; i < n; i++)
            invertArr[i] = -arr[i];

        // create and build an array that stores
        // minimum sums of subarrays that lie in
        // arr[0...i]
        int leftMin[n];
        maxLeftSubArraySum(invertArr, n, leftMin);
        for (int i = 0; i < n; i++)
            leftMin[i] = -leftMin[i];

        // create and build an array that stores
        // minimum sums of subarrays that lie in
        // arr[i+1...n-1]
        int rightMin[n];
        maxRightSubArraySum(invertArr, n - 1, rightMin);
        for (int i = 0; i < n; i++)
            rightMin[i] = -rightMin[i];

        int result = INT_MIN;
        for (int i = 0; i < n - 1; i++)
        {
            /* For each index i, take maximum of
            1\. abs(max sum subarray that lies in arr[0...i] -
                min sum subarray that lies in arr[i+1...n-1])
            2\. abs(min sum subarray that lies in arr[0...i] -
                max sum subarray that lies in arr[i+1...n-1]) */
            int absValue = max(abs(leftMax[i] - rightMin[i + 1]),
                            abs(leftMin[i] - rightMax[i + 1]));
            if (absValue > result)
                result = absValue;
        }

        return result;
    }

    // Driver program
    int main()
    {
        int a[] = {-2, -3, 4, -1, -2, 1, 5, -3};

        int n = sizeof(a) / sizeof(a[0]);

        cout << findMaxAbsDiff(a, n);

        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program to find two non-overlapping
    // contiguous sub-arrays such that the 
    // absolute difference
    import java.util.*;

    class GFG {

        // Find maximum subarray sum for subarray
        // [0..i] using standard Kadane's algorithm.
        // This version of Kadane's Algorithm will 
        // work if all numbers are negative.
        static int maxLeftSubArraySum(int a[], int size, 
                                              int sum[])
        {
            int max_so_far = a[0];
            int curr_max = a[0];
            sum[0] = max_so_far;

            for (int i = 1; i < size; i++) {
                curr_max = Math.max(a[i], curr_max + a[i]);
                max_so_far = Math.max(max_so_far, curr_max);
                sum[i] = max_so_far;
            }

            return max_so_far;
        }

        // Find maximum subarray sum for subarray [i..n]
        // using Kadane's algorithm. This version of Kadane's
        // Algorithm will work if all numbers are negative
        static int maxRightSubArraySum(int a[], int n, int sum[])
        {
            int max_so_far = a[n];
            int curr_max = a[n];
            sum[n] = max_so_far;

            for (int i = n - 1; i >= 0; i--) {
                curr_max = Math.max(a[i], curr_max + a[i]);
                max_so_far = Math.max(max_so_far, curr_max);
                sum[i] = max_so_far;
            }

            return max_so_far;
        }

        // The function finds two non-overlapping contiguous
        // sub-arrays such that the absolute difference
        // between the sum of two sub-array is maximum.
        static int findMaxAbsDiff(int arr[], int n)
        {
            // create and build an array that stores
            // maximum sums of subarrays that lie in
            // arr[0...i]
            int leftMax[] = new int[n];
            maxLeftSubArraySum(arr, n, leftMax);

            // create and build an array that stores
            // maximum sums of subarrays that lie in
            // arr[i+1...n-1]
            int rightMax[] = new int[n];
            maxRightSubArraySum(arr, n - 1, rightMax);

            // Invert array (change sign) to find minumum
            // sum subarrays.
            int invertArr[] = new int[n];
            for (int i = 0; i < n; i++)
                invertArr[i] = -arr[i];

            // create and build an array that stores
            // minimum sums of subarrays that lie in
            // arr[0...i]
            int leftMin[] = new int[n];
            maxLeftSubArraySum(invertArr, n, leftMin);
            for (int i = 0; i < n; i++)
                leftMin[i] = -leftMin[i];

            // create and build an array that stores
            // minimum sums of subarrays that lie in
            // arr[i+1...n-1]
            int rightMin[] = new int[n];
            maxRightSubArraySum(invertArr, n - 1, rightMin);
            for (int i = 0; i < n; i++)
                rightMin[i] = -rightMin[i];

            int result = -2147483648;
            for (int i = 0; i < n - 1; i++) {

            /* For each index i, take maximum of
            1\. abs(max sum subarray that lies in arr[0...i] -
                min sum subarray that lies in arr[i+1...n-1])
            2\. abs(min sum subarray that lies in arr[0...i] -
                max sum subarray that lies in arr[i+1...n-1]) */
                int absValue = Math.max(Math.abs(leftMax[i] - rightMin[i + 1]),
                                        Math.abs(leftMin[i] - rightMax[i + 1]));
                if (absValue > result)
                    result = absValue;
            }

            return result;
        }

        // driver code
        public static void main(String[] args)
        {
            int a[] = { -2, -3, 4, -1, -2, 1, 5, -3 };
            int n = a.length;
            System.out.print(findMaxAbsDiff(a, n));
        }
    }

    // This code is contributed by Anant Agarwal.
    ```

    ## 蟒蛇 3

    ```

    # Python3 program to find two non-
    # overlapping contiguous sub-arrays
    # such that the absolute difference
    # between the sum of two sub-array is maximum.

    # Find maximum subarray sum for
    # subarray [0..i] using standard
    # Kadane's algorithm. This version 
    # of Kadane's Algorithm will work if 
    # all numbers are negative.
    def maxLeftSubArraySum(a, size, sum):

        max_so_far = a[0]
        curr_max = a[0]
        sum[0] = max_so_far

        for i in range(1, size):

            curr_max = max(a[i], curr_max + a[i])
            max_so_far = max(max_so_far, curr_max)
            sum[i] = max_so_far

        return max_so_far

    # Find maximum subarray sum for
    # subarray [i..n] using Kadane's
    # algorithm. This version of Kadane's
    # Algorithm will work if all numbers are negative
    def maxRightSubArraySum(a, n, sum):

        max_so_far = a[n]
        curr_max = a[n]
        sum[n] = max_so_far

        for i in range(n - 1, -1, -1):

            curr_max = max(a[i], curr_max + a[i])
            max_so_far = max(max_so_far, curr_max)
            sum[i] = max_so_far

        return max_so_far

    # The function finds two non-overlapping
    # contiguous sub-arrays such that the
    # absolute difference between the sum
    # of two sub-array is maximum.
    def findMaxAbsDiff(arr, n):

        # create and build an array that 
        # stores maximum sums of subarrays 
        # that lie in arr[0...i]
        leftMax = [0 for i in range(n)]
        maxLeftSubArraySum(arr, n, leftMax)

        # create and build an array that stores
        # maximum sums of subarrays that lie in
        # arr[i+1...n-1]
        rightMax = [0 for i in range(n)]
        maxRightSubArraySum(arr, n-1, rightMax)

        # Invert array (change sign) to 
        # find minumum sum subarrays.
        invertArr = [0 for i in range(n)]
        for i in range(n):
            invertArr[i] = -arr[i]

        # create and build an array that stores
        # minimum sums of subarrays that lie in
        # arr[0...i]
        leftMin = [0 for i in range(n)]
        maxLeftSubArraySum(invertArr, n, leftMin)
        for i in range(n):
            leftMin[i] = -leftMin[i]

        # create and build an array that stores
        # minimum sums of subarrays that lie in
        # arr[i+1...n-1]
        rightMin = [0 for i in range(n)]
        maxRightSubArraySum(invertArr, n - 1, rightMin)
        for i in range(n):
            rightMin[i] = -rightMin[i]

        result = -2147483648
        for i in range(n - 1):

            ''' For each index i, take maximum of
            1\. abs(max sum subarray that lies in arr[0...i] -
                min sum subarray that lies in arr[i+1...n-1])
            2\. abs(min sum subarray that lies in arr[0...i] -
                max sum subarray that lies in arr[i+1...n-1]) '''
            absValue = max(abs(leftMax[i] - rightMin[i + 1]),
                           abs(leftMin[i] - rightMax[i + 1]))
            if (absValue > result):
                result = absValue

        return result

    # Driver Code
    a = [-2, -3, 4, -1, -2, 1, 5, -3]
    n = len(a)
    print(findMaxAbsDiff(a, n))

    # This code is contributed by Anant Agarwal.
    ```

    ## C#

    ```
    // C# program to find two non-overlapping 
    // contiguous sub-arrays such that the
    // absolute difference
    using System;
    class GFG {

    // Find maximum subarray sum for subarray
    // [0..i] using standard Kadane's algorithm.
    // This version of Kadane's Algorithm will
    // work if all numbers are negative.
    static int maxLeftSubArraySum(int []a, int size, 
                                          int []sum)
    {
        int max_so_far = a[0];
        int curr_max = a[0];
        sum[0] = max_so_far;

        for (int i = 1; i < size; i++)
        {
            curr_max = Math.Max(a[i], curr_max + a[i]);
            max_so_far = Math.Max(max_so_far, curr_max);
            sum[i] = max_so_far;
        }

        return max_so_far;
    }

    // Find maximum subarray sum for subarray
    // [i..n] using Kadane's algorithm. 
    // This version of Kadane's Algorithm will
    // work if all numbers are negative
    static int maxRightSubArraySum(int []a, int n,
                                        int []sum)
    {
        int max_so_far = a[n];
        int curr_max = a[n];
        sum[n] = max_so_far;

        for (int i = n-1; i >= 0; i--)
        {
            curr_max = Math.Max(a[i], curr_max + a[i]);
            max_so_far = Math.Max(max_so_far, curr_max);
            sum[i] = max_so_far;
        }

        return max_so_far;
    }

    // The function finds two non-overlapping
    // contiguous sub-arrays such that the 
    // absolute difference between the sum 
    // of two sub-array is maximum.
    static int findMaxAbsDiff(int []arr, int n)
    {
        // create and build an array that stores
        // maximum sums of subarrays that lie in
        // arr[0...i]
        int []leftMax=new int[n];
        maxLeftSubArraySum(arr, n, leftMax);

        // create and build an array that stores
        // maximum sums of subarrays that lie in
        // arr[i+1...n-1]
        int []rightMax=new int[n];
        maxRightSubArraySum(arr, n-1, rightMax);

        // Invert array (change sign) to find minumum
        // sum subarrays.
        int []invertArr=new int[n];
        for (int i = 0; i < n; i++)
            invertArr[i] = -arr[i];

        // create and build an array that stores
        // minimum sums of subarrays that lie in
        // arr[0...i]
        int []leftMin=new int[n];
        maxLeftSubArraySum(invertArr, n, leftMin);
        for (int i = 0; i < n; i++)
            leftMin[i] = -leftMin[i];

        // create and build an array that stores
        // minimum sums of subarrays that lie in
        // arr[i+1...n-1]
        int []rightMin=new int[n];
        maxRightSubArraySum(invertArr, n - 1, rightMin);
        for (int i = 0; i < n; i++)
            rightMin[i] = -rightMin[i];

        int result = -2147483648;
        for (int i = 0; i < n - 1; i++)
        {
            /* For each index i, take maximum of
            1\. abs(max sum subarray that lies in arr[0...i] -
                min sum subarray that lies in arr[i+1...n-1])
            2\. abs(min sum subarray that lies in arr[0...i] -
                max sum subarray that lies in arr[i+1...n-1]) */
            int absValue = Math.Max(Math.Abs(leftMax[i] - rightMin[i + 1]),
                                   Math.Abs(leftMin[i] - rightMax[i + 1]));
            if (absValue > result)
                result = absValue;
        }

        return result;
    }

    //driver code
    public static void Main()
    {
        int []a= {-2, -3, 4, -1, -2, 1, 5, -3};
        int n = a.Length;
        Console.Write(findMaxAbsDiff(a, n));
    }
    }

    //This code is contributed by Anant Agarwal.
    ```

    ## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

    ```
    <?php 
    // PHP program to find two non-overlapping 
    // contiguous sub-arrays such that the 
    // absolute difference between the sum of
    // two sub-array is maximum.

    // Find maximum subarray sum for subarray 
    // [0..i] using standard Kadane's algorithm. 
    // This version of Kadane's Algorithm will 
    // work if all numbers are negative
    function maxLeftSubArraySum(&$a, $size, &$sum)
    {
        $max_so_far = $a[0];
        $curr_max = $a[0];
        $sum[0] = $max_so_far;

        for ($i = 1; $i < $size; $i++)
        {
            $curr_max = max($a[$i], 
                            $curr_max + $a[$i]);
            $max_so_far = max($max_so_far, 
                              $curr_max);
            $sum[$i] = $max_so_far;
        }

        return $max_so_far;
    }

    // Find maximum subarray sum for subarray 
    // [i..n] using Kadane's algorithm. This 
    // version of Kadane's Algorithm will work
    // if all numbers are negative
    function maxRightSubArraySum(&$a, $n, &$sum)
    {
        $max_so_far = $a[$n];
        $curr_max = $a[$n];
        $sum[$n] = $max_so_far;

        for ($i = $n - 1; $i >= 0; $i--)
        {
            $curr_max = max($a[$i],
                            $curr_max + $a[$i]);
            $max_so_far = max($max_so_far,
                              $curr_max);
            $sum[$i] = $max_so_far;
        }

        return $max_so_far;
    }

    // The function finds two non-overlapping 
    // contiguous sub-arrays such that the 
    // absolute difference between the sum of
    // two sub-array is maximum.
    function findMaxAbsDiff(&$arr, $n)
    {
        // create and build an array that stores
        // maximum sums of subarrays that lie in
        // arr[0...i]
        $leftMax = array_fill(0, $n, NULL);
        maxLeftSubArraySum($arr, $n, $leftMax);

        // create and build an array that stores
        // maximum sums of subarrays that lie in
        // arr[i+1...n-1]
        $rightMax = array_fill(0, $n, NULL);
        maxRightSubArraySum($arr, $n - 1, $rightMax);

        // Invert array (change sign) to 
        // find minumum sum subarrays
        $invertArr = array_fill(0, $n, NULL);
        for ($i = 0; $i < $n; $i++)
            $invertArr[$i] = -$arr[$i];

        // create and build an array that stores
        // minimum sums of subarrays that lie in
        // arr[0...i]
        $leftMin = array_fill(0, $n, NULL);
        maxLeftSubArraySum($invertArr, $n,
                           $leftMin);
        for ($i = 0; $i < $n; $i++)
            $leftMin[$i] = -$leftMin[$i];

        // create and build an array that stores
        // minimum sums of subarrays that lie in
        // arr[i+1...n-1]
        $rightMin = array_fill(0, $n, NULL);
        maxRightSubArraySum($invertArr, 
                            $n - 1, $rightMin);
        for ($i = 0; $i < $n; $i++)
            $rightMin[$i] = -$rightMin[$i];

        $result = PHP_INT_MIN;
        for ($i = 0; $i <$n - 1; $i++)
        {
            /* For each index i, take maximum of
            1\. abs(max sum subarray that lies 
               in arr[0...i] - min sum subarray 
               that lies in arr[i+1...n-1])
            2\. abs(min sum subarray that lies 
               in arr[0...i] - max sum subarray
               that lies in arr[i+1...n-1]) */
            $absValue = max(abs($leftMax[$i] -  
                                $rightMin[$i + 1]),
                            abs($leftMin[$i] - 
                                $rightMax[$i + 1]));
            if ($absValue > $result)
                $result = $absValue;
        }

        return $result;
    }

    // Driver Code
    $a = array(-2, -3, 4, -1, -2, 1, 5, -3);

    $n = sizeof($a);

    echo findMaxAbsDiff($a, $n);

    // This code is contributed
    // by ChitraNayal
    ?>
    ```

    **Output :**

    ```
    12
    ```

    时间复杂度是 O(n)，其中 n 是输入数组中的元素个数。所需的辅助空间为 0(n)。

    本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

    如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论