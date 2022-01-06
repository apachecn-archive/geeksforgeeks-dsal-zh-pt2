# 最大化总和可被 3 整除的数组中的拆分数

> 原文:[https://www . geeksforgeeks . org/最大化数组中可被 3 整除的拆分数/](https://www.geeksforgeeks.org/maximize-the-numbers-of-splits-in-an-array-having-sum-divisible-by-3/)

给定大小为 **N** 的整数数组 **arr** 。任务是找到分裂的最大数目，使得每个分裂的和能被 **3** 整除。并非所有拆分都可以被 **3** 整除，任务只是最大化可以被 **3** 整除的拆分数量。
**举例:**

> **输入:**arr[]=【2，36，1，9，2，0，1，8，1】
> **输出:** 4
> **解释**
> 数组可以拆分为 4 个部分:
> 【2，36，1】Sum = 39
> 【9】Sum = 9
> 【2，0，1】Sum = 3
> 【8，1】Sum = 9
> 所有拆分都可以被 3 整除
> **输入:**arr[]=【40，40，40，5】
> **输出:** 1
> **解释:**
> 数组只能拆分为两部分
> 【40，40】Sum = 80。
> 【40，5】总和= 45。
> 第二次分割的总和可被 3 整除，因此只有一次分割可被 3 整除，因此输出为 1。

**逼近**
一个很容易观察到的现象是，如果我们对每个元素取 3 的模，就更容易处理数组。因为这对分裂没有任何影响。现在问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决了。

1.  让***DP【I】***表示位置 **i** 处的最大分裂次数。

2.  然后计算 ***前缀和*** 的模 3。
3.  所以如果一个线段的和能被 3 整除，那么它的左右前缀和也是一样的。
4.  需要注意的另一件事是前缀和模 3 可以是 0、1 或 2。所以如果当前前缀和模 3 是 1。选择左指针作为前缀和为 1 的最右边的索引。或者忽略这个片段，继续前进。

> ***DP[I]= max(DP[从 0 到 I 的最右边索引，前缀和与 I 相同] + 1，DP[I-1])***
> **DP[I-1]**表示我们没有考虑将 **i** 作为某段的右指针。
> **dp【从 0 到 I 的最右侧索引，前缀和与 I 相同】+1** 表示 **i** 是该段的右指针，拆分总数将是该段左指针处的拆分总数+1(对于该段)。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

int calculate_maximum_splits(int arr[], int N)
{

    // Prefix array storing right most
    // index with prefix sums 0, 1, 2
    int pre[] = { 0, -1, -1 };    

    // dp array
    int dp[N];
    memset(dp, 0, sizeof(dp));

    // Current prefix sum
    int C = 0;

    for(int i = 0; i < N; i++)
    {
       C = C + arr[i];

       // Calculating the prefix sum modulo 3
       C = C % 3;

       // We dont have a left pointer
       // with prefix sum C
       if (pre[C] == -1)
       {
           dp[i] = dp[i - 1];

           // We cannot consider i as
           // a right pointer of any segment
       }
       else
       {

           // We have a left pointer
           // pre[C] with prefix sum C
           dp[i] = max(dp[i - 1], dp[pre[C]] + 1);
       }

       // i is the rightmost index of
       // prefix sum C
       pre[C] = i;
    }
    return dp[N - 1];
}

// Driver code
int main()
{
    int arr[] = { 2, 36, 1, 9, 2, 0, 1, 8, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << (calculate_maximum_splits(arr, N));
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG{

static int calculate_maximum_splits(int arr[],
                                    int N)
{

    // Prefix array storing right most
    // index with prefix sums 0, 1, 2
    int pre[] = { 0, -1, -1 };    

    // dp array
    int[] dp = new int[N];
    Arrays.fill(dp, 0);

    // Current prefix sum
    int C = 0;

    for(int i = 0; i < N; i++)
    {
        C = C + arr[i];

        // Calculating the prefix sum modulo 3
        C = C % 3;

        // We dont have a left pointer
        // with prefix sum C
        if (pre[C] == -1)
        {
            if(1 <= i)
            dp[i] = dp[i - 1];

            // We cannot consider i as
            // a right pointer of any segment
        }
        else
        {

            // We have a left pointer
            // pre[C] with prefix sum C
            dp[i] = Math.max(dp[i - 1],
                             dp[pre[C]] + 1);
        }

        // i is the rightmost index of
        // prefix sum C
        pre[C] = i;
    }
    return dp[N - 1];
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 36, 1, 9, 2, 0, 1, 8, 1 };
    int N = arr.length;

    System.out.println(calculate_maximum_splits(arr, N));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for above approach
def calculate_maximum_splits(arr, N):

    # prefix array storing right most
    # index with prefix sums 0, 1, 2
    pre =[0, -1, -1]        

    # dp array
    dp =[0 for i in range(N)]
    # current prefix sum
    C = 0

    for i in range(N):

        C = C + arr[i]

        # Calculating the prefix sum modulo 3
        C = C % 3

        # We dont have a left pointer
        # with prefix sum C
        if pre[C]==-1:

            dp[i]= dp[i-1]
            # We cannot consider i as
            # a right pointer of any segment
        else:
            # We have a left pointer
            # pre[C] with prefix sum C
            dp[i]= max(dp[i-1], dp[pre[C]]+1)

        # i is the rightmost index of
        # prefix sum C
        pre[C]= i

    return dp[N-1]
# Driver code
arr = [2, 36, 1, 9, 2, 0, 1, 8, 1]
N = len(arr)
print(calculate_maximum_splits(arr, N))    
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

static int calculate_maximum_splits(int []arr,
                                    int N)
{

    // Prefix array storing right most
    // index with prefix sums 0, 1, 2
    int []pre = { 0, -1, -1 };    

    // dp array
    int[] dp = new int[N];
    for(int i = 0; i < N; i++)
    {
        dp[i] = 0;
    }

    // Current prefix sum
    int C = 0;

    for(int i = 0; i < N; i++)
    {
        C = C + arr[i];

        // Calculating the prefix sum modulo 3
        C = C % 3;

        // We dont have a left pointer
        // with prefix sum C
        if (pre[C] == -1)
        {
            if(1 <= i)
            dp[i] = dp[i - 1];

            // We cannot consider i as
            // a right pointer of any segment
        }
        else
        {

            // We have a left pointer
            // pre[C] with prefix sum C
            dp[i] = Math.Max(dp[i - 1],
                             dp[pre[C]] + 1);
        }

        // i is the rightmost index of
        // prefix sum C
        pre[C] = i;
    }
    return dp[N - 1];
}

// Driver code
public static void Main(string[] args)
{
    int []arr = { 2, 36, 1, 9, 2, 0, 1, 8, 1 };
    int N = arr.Length;

    Console.Write(calculate_maximum_splits(arr, N));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program for the above approach

function calculate_maximum_splits(arr, N)
{

    // Prefix array storing right most
    // index with prefix sums 0, 1, 2
    var pre = [0, -1, -1];   
    var i;
    // dp array
    var dp = new Array(N);
    for(i=0;i<N;i++)
      dp[i] = 0;

    // Current prefix sum
    var C = 0;

    for(i = 1; i < N; i++)
    {
       C = C + arr[i];

       // Calculating the prefix sum modulo 3
       C = C % 3;

       // We dont have a left pointer
       // with prefix sum C
       if (pre[C] == -1)
       {
           dp[i] = dp[i - 1];

           // We cannot consider i as
           // a right pointer of any segment
       }
       else
       {

           // We have a left pointer
           // pre[C] with prefix sum C
           dp[i] = Math.max(dp[i - 1], dp[pre[C]] + 1);
       }

       // i is the rightmost index of
       // prefix sum C
       pre[C] = i;
    }
    document.write(dp[N - 1]);
}

// Driver code

    var arr = [2, 36, 1, 9, 2, 0, 1, 8, 1];
    var N = arr.length;

    calculate_maximum_splits(arr, N);

</script>
```

**Output:** 

```
4
```

***时间复杂度:** O (N)*
***辅助空间:** O (N)*