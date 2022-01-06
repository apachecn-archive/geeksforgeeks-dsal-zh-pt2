# 平均值小于 K 的最长子序列

> 原文:[https://www . geesforgeks . org/最长子序列-其平均值小于-k/](https://www.geeksforgeeks.org/longest-subsequence-whose-average-is-less-than-k/)

给定 N 个正整数的数组和由整数 K 组成的 Q 个查询，任务是打印平均值小于 K 的最长子序列的长度。
**示例:**

> **输入:** a[] = {1，3，2，5，4}
> 查询 1: K = 3
> 查询 2:K = 5
> T5】输出:
> 4
> 5
> 查询 1:子序列为:{1，3，2，4}或{1，3，2，5}
> 查询 2:子序列为:{1，3，2，5，4}

一种**天真的方法**是使用[幂集](https://www.geeksforgeeks.org/power-set/)生成所有子序列，并检查平均值小于 k 的最长子序列。
T5】时间复杂度: O(2 <sup>N</sup> * N )
一种**高效的方法**是对数组元素进行排序，并从左边开始寻找元素的平均值。将从左侧计算的元素平均值插入容器中([向量或数组](https://www.geeksforgeeks.org/vector-in-cpp-stl/))。对容器的元素进行排序，然后使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)在容器中搜索数字 K。因此，最长子序列的长度将是[上限()](https://www.geeksforgeeks.org/upper_bound-in-cpp/)为每个查询返回的索引号。
以下是上述办法的实施情况。

## C++

```
// C++ program to perform Q queries
// to find longest subsequence whose
// average is less than K
#include <bits/stdc++.h>
using namespace std;

// Function to print the length for evey query
int longestSubsequence(int a[], int n, int q[], int m)
{

    // sort array of N elements
    sort(a, a + n);
    int sum = 0;

    // Array to store average from left
    int b[n];

    for (int i = 0; i < n; i++) {
        sum += a[i];
        double av = (double)(sum) / (double)(i + 1);
        b[i] = ((int)(av + 1));
    }

    // Sort array of average
    sort(b, b + n);

    // number of queries

    for (int i = 0; i < m; i++) {
        int k = q[i];

        // print answer to every query
        // using binary search
        int longest = upper_bound(b, b + n, k) - b;

        cout << "Answer to Query" << i + 1 << ": "
             << longest << endl;
    }
}

// Driver Code
int main()
{
    int a[] = { 1, 3, 2, 5, 4 };
    int n = sizeof(a) / sizeof(a[0]);

    // 4 queries
    int q[] = { 4, 2, 1, 5 };
    int m = sizeof(q) / sizeof(q[0]);

    longestSubsequence(a, n, q, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to perform Q queries
// to find longest subsequence whose
// average is less than K
import java.util.Arrays;

class GFG
{

    // Function to print the length for evey query
    static void longestSubsequence(int a[], int n,
                                    int q[], int m)
    {

        // sort array of N elements
        Arrays.sort(a);
        int sum = 0;

        // Array to store average from left
        int []b = new int[n];

        for (int i = 0; i < n; i++)
        {
            sum += a[i];
            double av = (double)(sum) / (double)(i + 1);
            b[i] = ((int)(av + 1));
        }

        // Sort array of average
        Arrays.sort(b);

        // number of queries

        for (int i = 0; i < m; i++)
        {
            int k = q[i];

            // print answer to every query
            // using binary search
            int longest = upperBound(b,0, n, k);

            System.out.println("Answer to Query" + (i + 1) +": "
                + longest);
        }
    }
    private static int upperBound(int[] a, int low, int high, int element)
    {
        while(low < high)
        {
            int middle = low + (high - low)/2;
            if(a[middle] > element)
                high = middle;
            else
                low = middle + 1;
        }
        return low;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int a[] = { 1, 3, 2, 5, 4 };
        int n = a.length;

        // 4 queries
        int q[] = { 4, 2, 1, 5 };
        int m = q.length;

        longestSubsequence(a, n, q, m);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to perform Q queries to find
# longest subsequence whose average is less than K
import bisect

# Function to print the length for evey query
def longestSubsequence(a, n, q, m):

    # sort array of N elements
    a.sort()
    Sum = 0

    # Array to store average from left
    b = [None] * n

    for i in range(0, n): 
        Sum += a[i]
        av = Sum // (i + 1)
        b[i] = av + 1

    # Sort array of average
    b.sort()

    # number of queries

    for i in range(0, m): 
        k = q[i]

        # print answer to every query
        # using binary search
        longest = bisect.bisect_right(b, k)

        print("Answer to Query", i + 1, ":", longest)

# Driver Code
if __name__ == "__main__":

    a = [1, 3, 2, 5, 4] 
    n = len(a)

    # 4 queries
    q = [4, 2, 1, 5] 
    m = len(q)

    longestSubsequence(a, n, q, m)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to perform Q queries
// to find longest subsequence whose
// average is less than K
using System;

class GFG
{

    // Function to print the length for evey query
    static void longestSubsequence(int []a, int n,
                                    int []q, int m)
    {

        // sort array of N elements
        Array.Sort(a);
        int sum = 0;

        // Array to store average from left
        int []b = new int[n];

        for (int i = 0; i < n; i++)
        {
            sum += a[i];
            double av = (double)(sum) / (double)(i + 1);
            b[i] = ((int)(av + 1));
        }

        // Sort array of average
        Array.Sort(b);

        // number of queries

        for (int i = 0; i < m; i++)
        {
            int k = q[i];

            // print answer to every query
            // using binary search
            int longest = upperBound(b,0, n, k);

            Console.WriteLine("Answer to Query" + (i + 1) +": "
                + longest);
        }
    }

    private static int upperBound(int[] a, int low,
                                    int high, int element)
    {
        while(low < high)
        {
            int middle = low + (high - low)/2;
            if(a[middle] > element)
                high = middle;
            else
                low = middle + 1;
        }
        return low;
    }

    // Driver Code
    static public void Main ()
    {
        int []a = { 1, 3, 2, 5, 4 };
        int n = a.Length;

        // 4 queries
        int []q = { 4, 2, 1, 5 };
        int m = q.Length;

        longestSubsequence(a, n, q, m);
    }
}

/* This code contributed by ajit */
```

## java 描述语言

```
<script>

    // Javascript program to perform Q queries
    // to find longest subsequence whose
    // average is less than K

    // Function to print the length for evey query
    function longestSubsequence(a, n, q, m)
    {

        // sort array of N elements
        a.sort(function(a, b){return a - b});
        let sum = 0;

        // Array to store average from left
        let b = new Array(n);

        for (let i = 0; i < n; i++)
        {
            sum += a[i];
            let av = parseInt((sum) / (i + 1), 10);
            b[i] = (av + 1);
        }

        // Sort array of average
        b.sort(function(a, b){return a - b});

        // number of queries

        for (let i = 0; i < m; i++)
        {
            let k = q[i];

            // print answer to every query
            // using binary search
            let longest = upperBound(b,0, n, k);

            document.write("Answer to Query" +
            (i + 1) +": "
                + longest + "</br>");
        }
    }

    function upperBound(a, low, high, element)
    {
        while(low < high)
        {
            let middle = low +
            parseInt((high - low)/2, 10);
            if(a[middle] > element)
                high = middle;
            else
                low = middle + 1;
        }
        return low;
    }

    let a = [ 1, 3, 2, 5, 4 ];
    let n = a.length;

    // 4 queries
    let q = [ 4, 2, 1, 5 ];
    let m = q.length;

    longestSubsequence(a, n, q, m);

</script>
```

**输出:**

```
Answer to Query1: 5
Answer to Query2: 2
Answer to Query3: 0
Answer to Query4: 5
```

**时间复杂度:**O(N * log N+M * log N)
T3】辅助空间: O(N)