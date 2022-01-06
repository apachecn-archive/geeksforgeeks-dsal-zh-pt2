# 使用不同成本的反转操作对字符串进行排序的最小成本

> 原文:[https://www . geesforgeks . org/最低成本-排序-字符串-使用-反转-操作-不同-成本/](https://www.geeksforgeeks.org/minimum-cost-sort-strings-using-reversal-operations-different-costs/)

给定一个字符串数组和反转所有字符串的成本，我们需要对数组进行排序。我们不能移动数组中的字符串，只允许字符串反转。我们需要反转一些字符串，使所有字符串按照字典顺序排列，并且成本也最小化。如果无法以任何方式对字符串进行排序，则无法输出。
**例:**

```
Input  : arr[] = {“aa”, “ba”, “ac”}, 
        reverseCost[] = {1, 3, 1}
Output : Minimum cost of sorting = 1
Explanation : We can make above string array sorted 
by reversing one of 2nd or 3rd string, but reversing
2nd string cost 3, so we will reverse 3rd string to 
make string array sorted with a cost 1 which is 
minimum.
```

我们可以用动态规划来解决这个问题。我们制作了一个 2D 数组来存储最小的排序成本。

```
dp[i][j] represents the minimum cost to make first i
strings sorted.
 j = 1 means i'th string is reversed.
 j = 0 means i'th string is not reversed.

Value of dp[i][j] is computed using dp[i-1][1] and 
dp[i-1][0].

Computation of dp[i][0]
If arr[i] is greater than str[i-1], we update dp[i][0] 
by dp[i-1][0] 
If arr[i] is greater than reversal of previous string 
we update dp[i][0] by dp[i-1][1] 

Same procedure is applied to compute dp[i][1], we 
reverse str[i] before applying the procedure.

At the end we will choose minimum of dp[N-1][0] and 
dp[N-1][1] as our final answer if both of them not 
updated yet even once, we will flag that sorting is
not possible.
```

以下是上述想法的实现。

## C++

```
// C++ program to get minimum cost to sort
// strings by reversal operation
#include <bits/stdc++.h>
using namespace std;

// Returns minimum cost for sorting arr[]
// using reverse operation. This function
// returns -1 if it is not possible to sort.
int minCost(string arr[], int cost[], int N)
{
    // dp[i][j] represents the minimum cost to
    // make first i strings sorted.
    // j = 1 means i'th string is reversed.
    // j = 0 means i'th string is not reversed.
    int dp[N][2];

    // initializing dp array for first string
    dp[0][0] = 0;
    dp[0][1] = cost[0];

    // getting array of reversed strings
    string revStr[N];
    for (int i = 0; i < N; i++)
    {
        revStr[i] = arr[i];
        reverse(revStr[i].begin(), revStr[i].end());
    }

    string curStr;
    int curCost;

    // looping for all strings
    for (int i = 1; i < N; i++)
    {
        // Looping twice, once for string and once
        // for reversed string
        for (int j = 0; j < 2; j++)
        {
            dp[i][j] = INT_MAX;

            // getting current string and current
            // cost according to j
            curStr = (j == 0) ? arr[i] : revStr[i];
            curCost = (j == 0) ? 0 : cost[i];

            // Update dp value only if current string
            // is lexicographically larger
            if (curStr >= arr[i - 1])
                dp[i][j] = min(dp[i][j], dp[i-1][0] + curCost);
            if (curStr >= revStr[i - 1])
                dp[i][j] = min(dp[i][j], dp[i-1][1] + curCost);
        }
    }

    // getting minimum from both entries of last index
    int res = min(dp[N-1][0], dp[N-1][1]);

    return (res == INT_MAX)? -1 : res;
}

// Driver code to test above methods
int main()
{
    string arr[] = {"aa", "ba", "ac"};
    int cost[] = {1, 3, 1};
    int N = sizeof(arr) / sizeof(arr[0]);

    int res = minCost(arr, cost, N);
    if (res == -1)
        cout << "Sorting not possible\n";
    else
        cout << "Minimum cost to sort strings is "
            << res;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get minimum cost to sort
// strings by reversal operation
import java.util.*;

class GFG
{

// Returns minimum cost for sorting arr[]
// using reverse operation. This function
// returns -1 if it is not possible to sort.
static int minCost(String arr[], int cost[], int N)
{
    // dp[i][j] represents the minimum cost to
    // make first i strings sorted.
    // j = 1 means i'th string is reversed.
    // j = 0 means i'th string is not reversed.
    int [][]dp = new int[N][2];

    // initializing dp array for first string
    dp[0][0] = 0;
    dp[0][1] = cost[0];

    // getting array of reversed strings
    String []revStr = new String[N];
    for (int i = 0; i < N; i++)
    {
        revStr[i] = arr[i];
        revStr[i] = reverse(revStr[i], 0,
                            revStr[i].length() - 1);
    }

    String curStr = "";
    int curCost;

    // looping for all strings
    for (int i = 1; i < N; i++)
    {
        // Looping twice, once for string and once
        // for reversed string
        for (int j = 0; j < 2; j++)
        {
            dp[i][j] = Integer.MAX_VALUE;

            // getting current string and current
            // cost according to j
            curStr = (j == 0) ? arr[i] : revStr[i];
            curCost = (j == 0) ? 0 : cost[i];

            // Update dp value only if current string
            // is lexicographically larger
            if (curStr.compareTo(arr[i - 1]) >= 0)
                dp[i][j] = Math.min(dp[i][j],
                                    dp[i - 1][0] + curCost);
            if (curStr.compareTo(revStr[i - 1]) >= 0)
                dp[i][j] = Math.min(dp[i][j],
                                    dp[i - 1][1] + curCost);
        }
    }

    // getting minimum from both entries of last index
    int res = Math.min(dp[N - 1][0], dp[N - 1][1]);

    return (res == Integer.MAX_VALUE)? -1 : res;
}

static String reverse(String s, int start, int end)
{

    // Temporary variable to store character
    char temp;
    char []str = s.toCharArray();
    while (start <= end)
    {

        // Swapping the first and last character
        temp = str[start];
        str[start] = str[end];
        str[end] = temp;
        start++;
        end--;
    }
    return String.valueOf(str);
}

// Driver Code
public static void main(String[] args)
{
    String arr[] = {"aa", "ba", "ac"};
    int cost[] = {1, 3, 1};
    int N = arr.length;

    int res = minCost(arr, cost, N);
    if (res == -1)
        System.out.println("Sorting not possible\n");
    else
        System.out.println("Minimum cost to " +
                           "sort strings is " + res);
    }
}

// This code is contributed by Rajput-Ji
```

## 计算机编程语言

```
# Python program to get minimum cost to sort
# strings by reversal operation

# Returns minimum cost for sorting arr[]
# using reverse operation. This function
# returns -1 if it is not possible to sort.
def ReverseStringMin(arr, reverseCost, n):

    # dp[i][j] represents the minimum cost to
    # make first i strings sorted.
    # j = 1 means i'th string is reversed.
    # j = 0 means i'th string is not reversed.

    dp = [[float("Inf")] * 2 for i in range(n)]

    # initializing dp array for first string
    dp[0][0] = 0

    dp[0][1] = reverseCost[0]

    # getting array of reversed strings
    rev_arr = [i[::-1] for i in arr]

    # looping for all strings
    for i in range(1, n):

        # Looping twice, once for string and once
        # for reversed string
        for j in range(2):

            # getting current string and current
            # cost according to j
            curStr = arr[i] if j==0 else rev_arr[i]

            curCost = 0 if j==0 else reverseCost[i]

            # Update dp value only if current string
            # is lexicographically larger
            if (curStr >= arr[i - 1]):

                dp[i][j] = min(dp[i][j], dp[i-1][0] + curCost)

            if (curStr >= rev_arr[i - 1]):

                dp[i][j] = min(dp[i][j], dp[i-1][1] + curCost)

    # getting minimum from both entries of last index
    res = min(dp[n-1][0], dp[n-1][1])

    return res if res != float("Inf") else -1

# Driver code
def main():

    arr = ["aa", "ba", "ac"]

    reverseCost = [1, 3, 1]

    n = len(arr)

    dp = [float("Inf")] * n

    res = ReverseStringMin(arr, reverseCost,n)

    if res != -1 :

        print "Minimum cost to sort sorting is" , res

    else :
        print "Sorting not possible"

if __name__ == '__main__':
    main()

#This code is contributed by Neelam Yadav
```

## C#

```
// C# program to get minimum cost to sort
// strings by reversal operation
using System;

class GFG
{

// Returns minimum cost for sorting arr[]
// using reverse operation. This function
// returns -1 if it is not possible to sort.
static int minCost(String []arr,
                   int []cost, int N)
{
    // dp[i,j] represents the minimum cost to
    // make first i strings sorted.
    // j = 1 means i'th string is reversed.
    // j = 0 means i'th string is not reversed.
    int [,]dp = new int[N, 2];

    // initializing dp array for first string
    dp[0, 0] = 0;
    dp[0, 1] = cost[0];

    // getting array of reversed strings
    String []revStr = new String[N];
    for (int i = 0; i < N; i++)
    {
        revStr[i] = arr[i];
        revStr[i] = reverse(revStr[i], 0,
                            revStr[i].Length - 1);
    }

    String curStr = "";
    int curCost;

    // looping for all strings
    for (int i = 1; i < N; i++)
    {
        // Looping twice, once for string and once
        // for reversed string
        for (int j = 0; j < 2; j++)
        {
            dp[i, j] = int.MaxValue;

            // getting current string and current
            // cost according to j
            curStr = (j == 0) ? arr[i] : revStr[i];
            curCost = (j == 0) ? 0 : cost[i];

            // Update dp value only if current string
            // is lexicographically larger
            if (curStr.CompareTo(arr[i - 1]) >= 0)
                dp[i, j] = Math.Min(dp[i, j],
                                    dp[i - 1, 0] + curCost);
            if (curStr.CompareTo(revStr[i - 1]) >= 0)
                dp[i, j] = Math.Min(dp[i, j],
                                    dp[i - 1, 1] + curCost);
        }
    }

    // getting minimum from both entries of last index
    int res = Math.Min(dp[N - 1, 0],
                       dp[N - 1, 1]);

    return (res == int.MaxValue) ? -1 : res;
}

static String reverse(String s, int start, int end)
{

    // Temporary variable to store character
    char temp;
    char []str = s.ToCharArray();
    while (start <= end)
    {

        // Swapping the first and last character
        temp = str[start];
        str[start] = str[end];
        str[end] = temp;
        start++;
        end--;
    }
    return String.Join("", str);
}

// Driver Code
public static void Main(String[] args)
{
    String []arr = {"aa", "ba", "ac"};
    int []cost = {1, 3, 1};
    int N = arr.Length;

    int res = minCost(arr, cost, N);
    if (res == -1)
        Console.WriteLine("Sorting not possible\n");
    else
        Console.WriteLine("Minimum cost to " +
                          "sort strings is " + res);
    }
}

// This code is contributed by Princi Singh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to get minimum cost to sort
// strings by reversal operation

// Returns minimum cost for sorting arr[]
// using reverse operation. This function
// returns -1 if it is not possible to sort.
function minCost(&$arr, &$cost, $N)
{
    // dp[i][j] represents the minimum cost
    // to make first i strings sorted.
    // j = 1 means i'th string is reversed.
    // j = 0 means i'th string is not reversed.
    $dp = array_fill(0, $N,
          array_fill(0, 2, NULL));

    // initializing dp array for
    // first string
    $dp[0][0] = 0;
    $dp[0][1] = $cost[0];

    // getting array of reversed strings
    $revStr = array_fill(false, $N, NULL);
    for ($i = 0; $i < $N; $i++)
    {
        $revStr[$i] = $arr[$i];
        $revStr[$i] = strrev($revStr[$i]);
    }

    $curStr = "";

    // looping for all strings
    for ($i = 1; $i < $N; $i++)
    {
        // Looping twice, once for string
        // and once for reversed string
        for ($j = 0; $j < 2; $j++)
        {
            $dp[$i][$j] = PHP_INT_MAX;

            // getting current string and
            // current cost according to j
            if($j == 0)
                $curStr = $arr[$i];
            else
                $curStr = $revStr[$i];

            if($j == 0)
                $curCost = 0 ;
            else
                $curCost = $cost[$i];

            // Update dp value only if current string
            // is lexicographically larger
            if ($curStr >= $arr[$i - 1])
                $dp[$i][$j] = min($dp[$i][$j],
                                  $dp[$i - 1][0] +
                                  $curCost);
            if ($curStr >= $revStr[$i - 1])
                $dp[$i][$j] = min($dp[$i][$j],
                                  $dp[$i - 1][1] +
                                  $curCost);
        }
    }

    // getting minimum from both entries
    // of last index
    $res = min($dp[$N - 1][0], $dp[$N - 1][1]);

    if($res == PHP_INT_MAX)
        return -1 ;
    else
        return $res;
}

// Driver Code
$arr = array("aa", "ba", "ac");
$cost = array(1, 3, 1);
$N = sizeof($arr);
$res = minCost($arr, $cost, $N);
if ($res == -1)
    echo "Sorting not possible\n";
else
    echo "Minimum cost to sort strings is " . $res;

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program to get minimum cost to sort
// strings by reversal operation

    // Returns minimum cost for sorting arr[]
    // using reverse operation. This function
    // returns -1 if it is not possible to sort.
    function minCost(arr,cost,N)
    {
        // dp[i][j] represents the minimum cost to
        // make first i strings sorted.
        // j = 1 means i'th string is reversed.
        // j = 0 means i'th string is not reversed.

        let dp=new Array(N);
        for(let i=0;i<N;i++)
        {
            dp[i]=new Array(2);
            for(let j=0;j<2;j++)
            {
                dp[i][j]=0;
            }
        }

        // initializing dp array for first string
        dp[0][0] = 0;
        dp[0][1] = cost[0];

        // getting array of reversed strings
        let revStr = new Array(N);
        for(let i=0;i<N;i++)
        {
            revStr[i]="";
        }

        for (let i = 0; i < N; i++)
        {
            revStr[i] = arr[i];
            revStr[i] = reverse(revStr[i], 0,
                                revStr[i].length - 1);
        }

        let curStr = "";
        let curCost;

        // looping for all strings
        for (let i = 1; i < N; i++)
        {
            // Looping twice, once for string and once
            // for reversed string
            for (let j = 0; j < 2; j++)
            {
                dp[i][j] = Number.MAX_VALUE;

                // getting current string and current
                // cost according to j
                curStr = (j == 0) ? arr[i] : revStr[i];
                curCost = (j == 0) ? 0 : cost[i];

                // Update dp value only if current string
                // is lexicographically larger
                if (curStr>=arr[i - 1])
                    dp[i][j] = Math.min(dp[i][j],
                                        dp[i - 1][0] + curCost);
                if (curStr>=revStr[i - 1])
                    dp[i][j] = Math.min(dp[i][j],
                                        dp[i - 1][1] + curCost);
            }
        }

        // getting minimum from both entries of last index
        let res = Math.min(dp[N - 1][0], dp[N - 1][1]);

        return (res == Number.MAX_VALUE)? -1 : res;
    }

    function reverse(s,start,end)
    {
        // Temporary variable to store character
        let temp;
        let str=s.split("");
        while (start <= end)
        {

            // Swapping the first and last character
            temp = str[start];
            str[start] = str[end];
            str[end] = temp;
            start++;
            end--;
        }
        return str.toString();

    }

    // Driver Code
    let arr=["aa", "ba", "ac"];
    let cost=[1, 3, 1];
    let N = arr.length;
    let res = minCost(arr, cost, N);
    if (res == -1)
        document.write("Sorting not possible\n");
    else
        document.write("Minimum cost to " +
                           "sort strings is " + res);

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
Minimum cost to sort strings is 1
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。