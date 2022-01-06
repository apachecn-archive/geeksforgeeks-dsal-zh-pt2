# 计数乘积小于 K 的所有子序列

> 原文:[https://www . geesforgeks . org/count-subseries-product-less-k/](https://www.geeksforgeeks.org/count-subsequences-product-less-k/)

给定一个正数组，求乘积小于 k 的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的个数
**例:**

```
Input : [1, 2, 3, 4] 
        k = 10
Output :11 
The subsequences are {1}, {2}, {3}, {4}, 
{1, 2}, {1, 3}, {1, 4}, {2, 3}, {2, 4}, 
{1, 2, 3}, {1, 2, 4}

Input  : [4, 8, 7, 2] 
         k = 50
Output : 9
```

这个问题可以用动态规划来解决，其中 dp[i][j] =使用数组的前 j 项，乘积小于 I 的子序列数。其可以通过以下方式获得:使用第 j-1 项的子序列数+可以使用第 j 项形成的子序列数。

## C++

```
// CPP program to find number of subarrays having
// product less than k.
#include <bits/stdc++.h>
using namespace std;

// Function to count numbers of such subsequences
// having product less than k.
int productSubSeqCount(vector<int> &arr, int k)
{
    int n = arr.size();
    int dp[k + 1][n + 1];
    memset(dp, 0, sizeof(dp));

    for (int i = 1; i <= k; i++) {
        for (int j = 1; j <= n; j++) {

            // number of subsequence using j-1 terms
            dp[i][j] = dp[i][j - 1];

            // if arr[j-1] > i it will surely make product greater
            // thus it won't contribute then
            if (arr[j - 1] <= i)

                // number of subsequence using 1 to j-1 terms
                // and j-th term
                dp[i][j] += dp[i/arr[j-1]][j-1] + 1;
        }
    }
    return dp[k][n];
}

// Driver code
int main()
{
    vector<int> A;
    A.push_back(1);
    A.push_back(2);
    A.push_back(3);
    A.push_back(4);
    int k = 10;
    cout << productSubSeqCount(A, k) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number of subarrays
// having product less than k.
import java.util.*;
class CountSubsequences
{
    // Function to count numbers of such
    // subsequences having product less than k.
    public static int productSubSeqCount(ArrayList<Integer> arr,
                                                 int k)
    {
        int n = arr.size();
        int dp[][]=new int[k + 1][n + 1];

        for (int i = 1; i <= k; i++) {
            for (int j = 1; j <= n; j++) {

                // number of subsequence using j-1 terms
                dp[i][j] = dp[i][j - 1];

                // if arr[j-1] > i it will surely make
                // product greater thus it won't contribute
                // then
                if (arr.get(j-1) <= i && arr.get(j-1) > 0)

                    // number of subsequence using 1 to j-1
                    // terms and j-th term
                    dp[i][j] += dp[i/arr.get(j - 1)][j - 1] + 1;
            }
        }
        return dp[k][n];
    }

    // Driver code
    public static void main(String args[])
    {
        ArrayList<Integer> A = new ArrayList<Integer>();
        A.add(1);
        A.add(2);
        A.add(3);
        A.add(4);
        int k = 10;
        System.out.println(productSubSeqCount(A, k));
    }
}

// This Code is contributed by Danish Kaleem
```

## 蟒蛇 3

```
# Python3 program to find
# number of subarrays having
# product less than k.
def productSubSeqCount(arr, k):
    n = len(arr)
    dp = [[0 for i in range(n + 1)]
             for j in range(k + 1)]
    for i in range(1, k + 1):
        for j in range(1, n + 1):

            # number of subsequence
            # using j-1 terms
            dp[i][j] = dp[i][j - 1]

            # if arr[j-1] > i it will
            # surely make product greater
            # thus it won't contribute then
            if arr[j - 1] <= i and arr[j - 1] > 0:

                # number of subsequence
                # using 1 to j-1 terms
                # and j-th term
                dp[i][j] += dp[i // arr[j - 1]][j - 1] + 1
    return dp[k][n]

# Driver code
A = [1,2,3,4]
k = 10
print(productSubSeqCount(A, k))

# This code is contributed
# by pk_tautolo
```

## C#

```
// C# program to find number of subarrays
// having product less than k.
using System ;
using System.Collections ;

class CountSubsequences
{
    // Function to count numbers of such
    // subsequences having product less than k.
    public static int productSubSeqCount(ArrayList arr, int k)
    {
        int n = arr.Count ;
        int [,]dp = new int[k + 1,n + 1];

        for (int i = 1; i <= k; i++) {
            for (int j = 1; j <= n; j++) {

                // number of subsequence using j-1 terms
                dp[i,j] = dp[i,j - 1];

                // if arr[j-1] > i it will surely make
                // product greater thus it won't contribute
                // then
                if (Convert.ToInt32(arr[j-1]) <= i && Convert.ToInt32(arr[j-1]) > 0)

                    // number of subsequence using 1 to j-1
                    // terms and j-th term
                    dp[i,j] += dp[ i/Convert.ToInt32(arr[j - 1]),j - 1] + 1;
            }
        }
        return dp[k,n];
    }

    // Driver code
    public static void Main()
    {
        ArrayList A = new ArrayList();
        A.Add(1);
        A.Add(2);
        A.Add(3);
        A.Add(4);
        int k = 10;
        Console.WriteLine(productSubSeqCount(A, k));
    }
}

// This Code is contributed Ryuga
```

## java 描述语言

```
<script>
    // Javascript program to find number of subarrays
    // having product less than k.

    // Function to count numbers of such
    // subsequences having product less than k.
    function productSubSeqCount(arr, k)
    {
        let n = arr.length;
        let dp = new Array(k + 1);
        for (let i = 0; i < k + 1; i++)
        {
            dp[i] = new Array(n + 1);
            for (let j = 0; j < n + 1; j++)
            {
                dp[i][j] = 0;
            }
        }

        for (let i = 1; i <= k; i++) {
            for (let j = 1; j <= n; j++) {

                // number of subsequence using j-1 terms
                dp[i][j] = dp[i][j - 1];

                // if arr[j-1] > i it will surely make
                // product greater thus it won't contribute
                // then
                if (arr[j-1] <= i && arr[j-1] > 0)

                    // number of subsequence using 1 to j-1
                    // terms and j-th term
                    dp[i][j] += dp[parseInt(i/arr[j - 1], 10)][j - 1] + 1;
            }
        }
        return dp[k][n];
    }

    let A = [1, 2, 3, 4];
    let k = 10;
    document.write(productSubSeqCount(A, k));

    // This code is contributed by suresh07.
</script>
```

**输出:**

```
11
```

本文由 **Raghav Sharma** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。