# 至少有-k 个远元素的最大和子序列

> 原文:[https://www . geesforgeks . org/maximum-sum-subsequence-minist-k-distance-elements/](https://www.geeksforgeeks.org/maximum-sum-subsequence-least-k-distant-elements/)

给定一个数组和一个数 k，找到一个子序列

1.  子序列中元素的总和最大
2.  子序列元素的索引至少相差 k

    例子

    ```
    Input : arr[] = {4, 5, 8, 7, 5, 4, 3, 4, 6, 5}
               k = 2
    Output: 19
    Explanation: The highest value is obtained 
    if you pick indices 1, 4, 7, 10 giving 
    4 + 7 + 3 + 5 = 19

    Input: arr[] = {50, 70, 40, 50, 90, 70, 60, 
                                  40, 70, 50}
               k = 2
    Output: 230
    Explanation: There are 10 elements and k = 2\. 
    If you select 2, 5, and 9 you get a total 
    value of 230, which is the maximum possible.

    ```

    一个**简单的解决方法**就是逐个考虑[所有的子序列](https://www.geeksforgeeks.org/print-subsequences-string/)。在每个子序列中，检查距离条件并返回最大和子序列。

    一个**有效的解决方案**是使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)。

    有两种情况:

    1.  如果我们选择索引 I 处的元素，使得 i + k + 1 >= N，那么我们不能选择任何其他元素作为子序列的一部分。因此，我们需要决定是选择这个元素还是它后面的一个元素。
    2.  如果我们在索引 I 处选择元素，使得 i + k + 1 < N，那么我们可以选择的下一个元素是在 i + k + 1 索引处。因此，我们需要决定是选择这两个元素，还是继续下一个相邻的元素。

    这两种情况可以写成:

    ```
    Let MS[i] denotes the maximum sum of subsequence 
    from i = N-2 to 0\. 

    Base Case: 
       MS[N-1] = arr[N-1]

    If  i + 1 + k >= N
       MS[i] = max(arr[i], MS[i+1]),  
    Else
       MS[i] = max(arr[i] + MS[i+k+1], MS[i+1])

    Evidently, the solution to the problem
    is to find MS[0].
    ```

    下面是实现:

    ## C++

    ```
    // CPP program to find maximum sum subsequence
    // such that elements are at least k distance
    // away.
    #include <bits/stdc++.h>
    using namespace std;

    int maxSum(int arr[], int N, int k)
    {
        // MS[i] is going to store maximum sum
        // subsequence in subarray from arr[i]
        // to arr[n-1]
        int MS[N];

        // We fill MS from right to left.
        MS[N - 1] = arr[N - 1];
        for (int i = N - 2; i >= 0; i--) {
            if (i + k + 1 >= N)
                MS[i] = max(arr[i], MS[i + 1]);
            else
                MS[i] = max(arr[i] + MS[i + k + 1], MS[i + 1]);
        }

        return MS[0];
    }

    // Driver code
    int main()
    {
        int N = 10, k = 2;
        int arr[] = { 50, 70, 40, 50, 90, 70, 60, 40, 70, 50 };
        cout << maxSum(arr, N, k);
        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program to find maximum sum subsequence
    // such that elements are at least k distance
    // away.
    import java.io.*;

    class GFG {

        static int maxSum(int arr[], int N, int k)
        {
            // MS[i] is going to store maximum sum
            // subsequence in subarray from arr[i]
            // to arr[n-1]
            int MS[] = new int[N];

            // We fill MS from right to left.
            MS[N - 1] = arr[N - 1];
            for (int i = N - 2; i >= 0; i--) {
                if (i + k + 1 >= N)
                    MS[i] = Math.max(arr[i], MS[i + 1]);
                else
                    MS[i] = Math.max(arr[i] + MS[i + k + 1],
                                    MS[i + 1]);
            }

            return MS[0];
        }

        // Driver code
        public static void main(String[] args)
        {
            int N = 10, k = 2;
            int arr[] = { 50, 70, 40, 50, 90, 70, 60,
                          40, 70, 50 };
            System.out.println(maxSum(arr, N, k));
        }
    }
    // This code is contributed by Prerna Saini
    ```

    ## 蟒蛇 3

    ```

    # Python3 program to find maximum
    # sum subsequence such that elements
    # are at least k distance away.

    def maxSum(arr, N, k):

        # MS[i] is going to store maximum sum
        # subsequence in subarray from arr[i]
        # to arr[n-1]
        MS = [0 for i in range(N)]

        # We fill MS from right to left.
        MS[N - 1] = arr[N - 1]
        for i in range(N - 2, -1, -1):
            if (i + k + 1 >= N):
                MS[i] = max(arr[i], MS[i + 1])
            else:
                MS[i] = max(arr[i] + MS[i + k + 1],
                                     MS[i + 1])

        return MS[0]

    # Driver code
    N = 10; k = 2
    arr = [ 50, 70, 40, 50, 90, 70, 60, 40, 70, 50 ]
    print(maxSum(arr, N, k))

    # This code is contributed by Anant Agarwal.
    ```

    ## C#

    ```
    // C# program to find maximum sum
    // subsequence such that elements
    // are at least k distance away.
    using System;

    class GFG {

        static int maxSum(int []arr, int N, int k)
        {
            // MS[i] is going to store maximum sum
            // subsequence in subarray from arr[i]
            // to arr[n-1]
            int []MS = new int[N];

            // We fill MS from right to left.
            MS[N - 1] = arr[N - 1];
            for (int i = N - 2; i >= 0; i--) {

                if (i + k + 1 >= N)
                    MS[i] = Math.Max(arr[i], MS[i + 1]);
                else
                    MS[i] = Math.Max(arr[i] + MS[i + k + 1],
                                    MS[i + 1]);
            }

            return MS[0];
        }

        // Driver code
        public static void Main()
        {
            int N = 10, k = 2;
            int []arr = { 50, 70, 40, 50, 90, 70, 60,
                                        40, 70, 50 };
            Console.WriteLine(maxSum(arr, N, k));
        }
    }

    // This code is contributed by Anant Agarwal.
    ```

    ## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

    ```
    <?php
    // PHP program to find 
    // maximum sum subsequence
    // such that elements are 
    // at least k distance
    // away.

    function maxSum($arr, $N, $k)
    {

        // MS[i] is going to
        // store maximum sum
        // subsequence in 
        // subarray from arr[i]
        // to arr[n-1]

        // We fill MS from 
        // right to left.
        $MS[$N - 1] = $arr[$N - 1];
        for ($i = $N - 2; $i >= 0; $i--) 
        {
            if ($i + $k + 1 >= $N)
                $MS[$i] = max($arr[$i], 
                          $MS[$i + 1]);
            else
                $MS[$i] = max($arr[$i] + 
                          $MS[$i + $k + 1], 
                          $MS[$i + 1]);
        }

        return $MS[0];
    }

    // Driver code
    $N = 10; $k = 2;
    $arr = array(50, 70, 40, 50, 90, 
                 70, 60, 40, 70, 50);
    echo(maxSum($arr, $N, $k));

    // This code is contributed by Ajit.
    ?>
    ```

    ```
    230

    ```

    时间复杂度:O(n)
    辅助空间:O(n)

    本文由 [**萨彦·马哈帕特拉**](https://auth.geeksforgeeks.org/profile.php?user=Sayan Mahapatra) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

    如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。