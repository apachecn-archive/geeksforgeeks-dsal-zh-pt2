# 最大长度子序列，使得子序列中的相邻元素具有共同的因子

> 原文:[https://www . geeksforgeeks . org/最大长度子序列-这样子序列中的相邻元素具有共同的因子/](https://www.geeksforgeeks.org/maximum-length-subsequence-such-that-adjacent-elements-in-the-subsequence-have-a-common-factor/)

给定一个数组 **arr[]** ，任务是找到子序列的最大长度，使得子序列中的相邻元素具有一个公共因子。

**示例:**

> **输入:** arr[] = { 13，2，8，6，3，1，9 }
> **输出:** 5
> 满足条件的最大长度子序列:{ 2，8，6，3，9 }
> 
> **输入:** arr[] = { 12，2，8，6，3，1，9 }
> **输出:** 6
> 满足条件的最大长度子序列:{ 12，2，8，6，3，9 }
> 
> **输入:** arr[] = { 1，2，2，3，3，1 }
> T3】输出: 2

**方法:** A **幼稚**方法是考虑所有子序列，检查每个子序列是否满足条件。
一个高效的**解决方案是使用**动态编程**。设 dp[i]表示包含 arr[i]的子序列的最大长度。然后，以下关系适用于每个素数 p，使得 p 是 arr[i]的素数因子:**

```
dp[i] = max(dp[i], 1 + dp[pos[p]]) 
where pos[p] gives the index of p in the array 
where it last occurred.
```

**说明:**遍历数组。对于元素 arr[i]，有两种可能性。

1.  如果 arr[i]的质因数在数组中首次出现，那么 dp[i] = 1
2.  如果 arr[i]的质因数已经出现，那么这个元素可以添加到子序列中，因为有一个公共因数。因此 dp[i] = max(dp[i]，1 + dp[pos[p]])，其中 p 是公共质因数，pos[p]是数组中 p 的最新索引。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
#define N 100005
#define MAX 10000002

using namespace std;

int lpd[MAX];

// Function to compute least
// prime divisor of i
void preCompute()
{
    memset(lpd, 0, sizeof(lpd));
    lpd[0] = lpd[1] = 1;
    for (int i = 2; i * i < MAX; i++)
    {
        for (int j = i * 2; j < MAX; j += i)
        {
            if (lpd[j] == 0)
            {
                lpd[j] = i;
            }
        }
    }
    for (int i = 2; i < MAX; i++)
    {
        if (lpd[i] == 0)
        {
            lpd[i] = i;
        }
    }
}

// Function that returns the maximum
// length subsequence such that
// adjacent elements have a common factor.
int maxLengthSubsequence(int arr[], int n)
{
    int dp[N];
    unordered_map<int, int> pos;

    // Initialize dp array with 1.
    for (int i = 0; i <= n; i++)
        dp[i] = 1;

    for (int i = 0; i <= n; i++)
    {
        while (arr[i] > 1)
        {
            int p = lpd[arr[i]];
            if (pos[p])
            {
                // p has appeared at least once.
                dp[i] = max(dp[i], 1 + dp[pos[p]]);
            }

            // Update latest occurrence of prime p.
            pos[p] = i;
            while (arr[i] % p == 0)
                arr[i] /= p;
        }
    }

    // Take maximum value as the answer.
    int ans = 1;
    for (int i = 0; i <= n; i++)
    {
        ans = max(ans, dp[i]);
    }

    return ans;
}

// Driver code
int main()
{
    int arr[] = { 13, 2, 8, 6, 3, 1, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    preCompute();

    cout << maxLengthSubsequence(arr, n);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach
import math as mt

N = 100005
MAX = 1000002

lpd = [0 for i in range(MAX)]

# to compute least prime divisor of i

def preCompute():

    lpd[0], lpd[1] = 1, 1

    for i in range(2, mt.ceil(mt.sqrt(MAX))):
        for j in range(2 * i, MAX, i):
            if (lpd[j] == 0):
                lpd[j] = i

    for i in range(2, MAX):
        if (lpd[i] == 0):
            lpd[i] = i

# Function that returns the maximum
# length subsequence such that
# adjacent elements have a common factor.

def maxLengthSubsequence(arr, n):
    dp = [1 for i in range(N + 1)]

    pos = dict()

    # Initialize dp array with 1.
    for i in range(0, n):
        while (arr[i] > 1):
            p = lpd[arr[i]]
            if (p in pos.keys()):

                # p has appeared at least once.
                dp[i] = max(dp[i], 1 + dp[pos[p]])

            # Update latest occurrence of prime p.
            pos[p] = i
            while (arr[i] % p == 0):
                arr[i] //= p

    # Take maximum value as the answer.
    ans = 1
    for i in range(0, n + 1):
        ans = max(ans, dp[i])

    return ans

# Driver code
arr = [13, 2, 8, 6, 3, 1, 9]
n = len(arr)

preCompute()

print(maxLengthSubsequence(arr, n))

# This code is contributed by Mohit Kumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
class GfG {
    static int N, MAX;

    // Check if UpperBound is
    // given for all test Cases
    // N = 100005 ;
    // MAX = 10000002;
    static int lpd[];

    // Function to compute least prime divisor
    // of i upto MAX element of the  input array
    // it will be space efficient
    // if more test cases are there it's
    // better to find prime divisor
    // upto upperbound of input element
    // it will be cost efficient
    static void preCompute()
    {
        lpd = new int[MAX + 1];
        lpd[0] = lpd[1] = 1;
        for (int i = 2; i * i <= MAX; i++)
        {
            for (int j = i * 2; j <= MAX; j += i)
            {
                if (lpd[j] == 0)
                {
                    lpd[j] = i;
                }
            }
        }
        for (int i = 2; i <= MAX; i++)
        {
            if (lpd[i] == 0)
            {
                lpd[i] = i;
            }
        }
    }

    // Function that returns the maximum
    // length subsequence such that
    // adjacent elements have a common factor.
    static int maxLengthSubsequence(Integer arr[], int n)
    {
        Integer dp[] = new Integer[N];
        Map<Integer, Integer> pos
            = new HashMap<Integer, Integer>();

        // Initialize dp array with 1.
        for (int i = 0; i <= n; i++)
            dp[i] = 1;

        for (int i = 0; i <= n; i++)
        {
            while (arr[i] > 1) {
                int p = lpd[arr[i]];
                if (pos.containsKey(p))
                {
                    // p has appeared at least once.
                    dp[i] = Math.max(dp[i],
                                     1 + dp[pos.get(p)]);
                }

                // Update latest occurrence of prime p.
                pos.put(p, i);
                while (arr[i] % p == 0)
                    arr[i] /= p;
            }
        }

        // Take maximum value as the answer.
        int ans = Collections.max(Arrays.asList(dp));
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        Integer arr[] = { 12, 2, 8, 6, 3, 1, 9 };
        N = arr.length;
        MAX = Collections.max(Arrays.asList(arr));
        preCompute();
        System.out.println(
            maxLengthSubsequence(arr, N - 1));
    }
}

// This code is contributed by Prerna Saini.
```

## C#

```
// C# implementation of the
// above approach
using System;
using System.Collections;

class GFG {

    static int N = 100005;
    static int MAX = 10000002;

    static int[] lpd = new int[MAX];

    // to compute least prime divisor of i
    static void preCompute()
    {
        lpd[0] = lpd[1] = 1;
        for (int i = 2; i * i < MAX; i++)
        {
            for (int j = i * 2; j < MAX; j += i)
            {
                if (lpd[j] == 0)
                {
                    lpd[j] = i;
                }
            }
        }
        for (int i = 2; i < MAX; i++)
        {
            if (lpd[i] == 0)
            {
                lpd[i] = i;
            }
        }
    }

    // Function that returns the maximum
    // length subsequence such that
    // adjacent elements have a common factor.
    static int maxLengthSubsequence(int[] arr, int n)
    {
        int[] dp = new int[N];
        Hashtable pos = new Hashtable();

        // Initialize dp array with 1.
        for (int i = 0; i <= n; i++)
            dp[i] = 1;

        for (int i = 0; i <= n; i++)
        {
            while (arr[i] > 1) {
                int p = lpd[arr[i]];
                if (pos.ContainsKey(p))
                {
                    // p has appeared at least once.
                    dp[i] = Math.Max(
                        dp[i],
                        1 + dp[Convert.ToInt32(pos[p])]);
                }

                // Update latest occurrence of prime p.
                pos[p] = i;
                while (arr[i] % p == 0)
                    arr[i] /= p;
            }
        }

        // Take maximum value as the answer.
        int ans = 1;
        for (int i = 0; i <= n; i++)
        {
            ans = Math.Max(ans, dp[i]);
        }

        return ans;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 13, 2, 8, 6, 3, 1, 9 };
        int n = arr.Length - 1;

        preCompute();
        Console.WriteLine(maxLengthSubsequence(arr, n));
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach   

    let N, MAX;
    // Check if UpperBound is
    // given for all test Cases
    // N = 100005 ;
    // MAX = 10000002;
    let  lpd;

    // Function to compute least prime divisor
    // of i upto MAX element of the  input array
    // it will be space efficient
    // if more test cases are there it's
    // better to find prime divisor
    // upto upperbound of input element
    // it will be cost efficient
    function preCompute()
    {
        lpd = new Array(MAX + 1);
        for(let i=0;i<lpd.length;i++)
        {
            lpd[i]=0;
        }
        lpd[0] = lpd[1] = 1;
        for (let i = 2; i * i <= MAX; i++)
        {
            for (let j = i * 2; j <= MAX; j += i)
            {
                if (lpd[j] == 0)
                {
                    lpd[j] = i;
                }
            }
        }
        for (let i = 2; i <= MAX; i++)
        {
            if (lpd[i] == 0)
            {
                lpd[i] = i;
            }
        }
    }

    // Function that returns the maximum
    // length subsequence such that
    // adjacent elements have a common factor.
    function maxLengthSubsequence(arr,n)
    {
        let dp = new Array(N);
        let pos
            = new Map();

        // Initialize dp array with 1.
        for (let i = 0; i <= n; i++)
            dp[i] = 1;

        for (let i = 0; i <= n; i++)
        {
            while (arr[i] > 1) {
                let p = lpd[arr[i]];
                if (pos.has(p))
                {
                    // p has appeared at least once.
                    dp[i] = Math.max(dp[i],
                                     1 + dp[pos.get(p)]);
                }

                // Update latest occurrence of prime p.
                pos.set(p, i);
                while (arr[i] % p == 0)
                    arr[i] = Math.floor(arr[i]/p);
            }
        }

        // Take maximum value as the answer.
        let ans = Math.max(...dp);
        return ans;
    }

    // Driver code
    let arr=[13, 2, 8, 6, 3, 1, 9 ];
    N = arr.length;
    MAX = Math.max(...arr);
    preCompute();
    document.write(maxLengthSubsequence(arr, N - 1));

// This code is contributed by patel2127

</script>
```

**Output**

```
5
```

**时间复杂度:** O(N* log(N))
**辅助空间:** O(N)