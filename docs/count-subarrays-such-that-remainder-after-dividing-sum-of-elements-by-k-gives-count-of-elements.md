# 对子阵列进行计数，使得元素之和除以 K 后的余数给出元素的计数

> 原文:[https://www . geeksforgeeks . org/count-subarrays-这样元素的和除以 k 后的余数就给出了元素的计数/](https://www.geeksforgeeks.org/count-subarrays-such-that-remainder-after-dividing-sum-of-elements-by-k-gives-count-of-elements/)

给定一个大小为 **N** 的数组 **arr[]** 和一个元素 **K** 。任务是找到给定阵列的子阵列的数量，使得其元素之和除以 **K** 时的余数等于子阵列中的元素数量。

**示例:**

> **输入:** arr[] = {1，4，2，3，5}，K = 4
> **输出:** 4
> {1}、{1，4，2}、{4，2}和{5}
> 是唯一有效的子阵。
> **输入:** arr[] = {4，2，4，2，4，2，4，2}，K = 4
> **输出:** 7

**方法:**我们来定义一个顺序**S<sub>n</sub>T5**S<sub>I</sub>= A<sub>1</sub>+A<sub>2</sub>++A<sub>I</sub>**和 **S <sub>0</sub> = 0** 。那么，连续子序列 **A <sub>i+1</sub> ，…，A <sub>j</sub>** 有效的条件可以表示为**(S<sub>j</sub>–S<sub>I</sub>)% K = j–I**。
然后这个方程可以转化为以下等价条件:
**(S<sub>j</sub>–j)% K =(S<sub>I</sub>–I)% K**和**j–I<K**。
因此，对于每个 **j(1 ≤ j ≤ N)** ，计算**j–K<I<j**的数量，使得**(S<sub>j</sub>–j)% K =(S<sub>I</sub>–I)% K**。对于 **j** 需要搜索的段是**(j–K，j)** ，对于 **j + 1** 则是**(j–K+1，j + 1)** ，这两者在最左边和最右边只相差一个元素，所以在搜索 **j <sup>之后为了搜索 **(j + 1) <sup>第</sup>个**通过使用关联数组(如 C++中的 map 或 Python 中的 dict)管理**S<sub>I</sub>–I**的数量，可以快速执行丢弃或添加操作。</sup>****

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of subarrays
// of the given array such that the remainder
// when dividing the sum of its elements
// by K is equal to the number of its elements
int sub_arrays(int a[], int n, int k)
{

    // To store prefix sum
    int sum[n + 2] = { 0 };

    for (int i = 0; i < n; i++) {

        // We are dealing with zero
        // indexed array
        a[i]--;

        // Taking modulus value
        a[i] %= k;

        // Prefix sum
        sum[i + 1] += sum[i] + a[i];
        sum[i + 1] %= k;
    }

    // To store the required answer, the left
    // index and the right index
    int ans = 0, l = 0, r = 0;

    // To store si - i value
    map<int, int> mp;

    for (int i = 0; i < n + 1; i++) {

        // Include sum
        ans += mp[sum[i]];
        mp[sum[i]]++;

        // Increment the right index
        r++;

        // If subarray has at least
        // k elements
        if (r - l >= k) {
            mp[sum[l]]--;
            l++;
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int a[] = { 1, 4, 2, 3, 5 };
    int n = sizeof(a) / sizeof(a[0]);

    int k = 4;

    // Function call
    cout << sub_arrays(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class gfg
{

    // Function to return the number of subarrays
    // of the given array such that the remainder
    // when dividing the sum of its elements
    // by K is equal to the number of its elements
    static int sub_arrays(int []a, int n, int k)
    {

        // To store prefix sum
        int sum[] = new int[n + 2] ;

        for (int i = 0; i < n+2; i++)
        {
            sum[i] = 0;
        }

        for (int i = 0; i < n; i++)
        {

            // We are dealing with zero
            // indexed array
            a[i]--;

            // Taking modulus value
            a[i] %= k;

            // Prefix sum
            sum[i + 1] += sum[i] + a[i];
            sum[i + 1] %= k;
        }

        // To store the required answer, the left
        // index and the right index
        int ans = 0, l = 0, r = 0;

        // To store si - i value
        HashMap<Integer, Integer> mp = new HashMap<Integer, Integer>();

        for (int i = 0; i < n + 1; i++)
        {
            mp.put(sum[i], 0);
        }
        int temp;

        for (int i = 0; i < n + 1; i++)
        {

            // Include sum
            ans += (int)mp.get(sum[i]);
            temp =(int)mp.get(sum[i]) + 1;
            mp.put(sum[i], temp);

            // Increment the right index
            r++;

            // If subarray has at least
            // k elements
            if (r - l >= k)
            {
                //mp[sum[l]]--;
                temp = (int)mp.get(sum[l]) - 1;
                mp.put(sum[l], temp);
                l++;
            }
        }

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void main(String args[])
    {
        int []a = { 1, 4, 2, 3, 5 };

        int n = a.length;

        int k = 4;

        // Function call
        System.out.print(sub_arrays(a, n, k));

    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the number of
# subarrays of the given array
# such that the remainder when dividing
# the sum of its elements by K is
# equal to the number of its elements
def sub_arrays(a, n, k):

    # To store prefix sum
    sum = [0 for i in range(n + 2)]

    for i in range(n):

        # We are dealing with zero
        # indexed array
        a[i] -= 1

        # Taking modulus value
        a[i] %= k

        # Prefix sum
        sum[i + 1] += sum[i] + a[i]
        sum[i + 1] %= k

    # To store the required answer,
    # the left index and the right index
    ans = 0
    l = 0
    r = 0

    # To store si - i value
    mp = dict()

    for i in range(n + 1):

        # Include sum
        if sum[i] in mp:
            ans += mp[sum[i]]
        mp[sum[i]] = mp.get(sum[i], 0) + 1

        # Increment the right index
        r += 1

        # If subarray has at least
        # k elements
        if (r - l >= k):
            mp[sum[l]] -= 1
            l += 1

    # Return the required answer
    return ans

# Driver code
a = [1, 4, 2, 3, 5]
n = len(a)

k = 4

# Function call
print(sub_arrays(a, n, k))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class gfg
{
    // Function to return the number of subarrays
    // of the given array such that the remainder
    // when dividing the sum of its elements
    // by K is equal to the number of its elements
    static int sub_arrays(int []a, int n, int k)
    {

        // To store prefix sum
        int []sum = new int[n + 2] ;

        for (int i = 0; i < n + 2; i++)
        {
            sum[i] = 0;
        }

        for (int i = 0; i < n; i++)
        {

            // We are dealing with zero
            // indexed array
            a[i]--;

            // Taking modulus value
            a[i] %= k;

            // Prefix sum
            sum[i + 1] += sum[i] + a[i];
            sum[i + 1] %= k;
        }

        // To store the required answer, the left
        // index and the right index
        int ans = 0, l = 0, r = 0;

        // To store si - i value
        Dictionary<int, int> mp = new Dictionary<int, int>();

        for (int i = 0; i < n + 1; i++)
        {
            if(!mp.ContainsKey(sum[i]))
                mp.Add(sum[i], 0);
        }
        int temp;

        for (int i = 0; i < n + 1; i++)
        {

            // Include sum
            ans += (int)mp[sum[i]];
            temp =(int)mp[sum[i]] + 1;
            mp[sum[i]] = temp;

            // Increment the right index
            r++;

            // If subarray has at least
            // k elements
            if (r - l >= k)
            {
                //mp[sum[l]]--;
                temp = (int)mp[sum[l]] - 1;
                mp[sum[i]] = temp;
                l++;
            }
        }

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void Main(String []args)
    {
        int []a = { 1, 4, 2, 3, 5 };

        int n = a.Length;

        int k = 4;

        // Function call
        Console.Write(sub_arrays(a, n, k));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the number of subarrays
// of the given array such that the remainder
// when dividing the sum of its elements
// by K is equal to the number of its elements
function sub_arrays(a, n, k) {

    // To store prefix sum
    let sum = new Array(n + 2);

    for (let i = 0; i < n + 2; i++) {
        sum[i] = 0;
    }

    for (let i = 0; i < n; i++) {

        // We are dealing with zero
        // indexed array
        a[i]--;

        // Taking modulus value
        a[i] %= k;

        // Prefix sum
        sum[i + 1] += sum[i] + a[i];
        sum[i + 1] %= k;
    }

    // To store the required answer, the left
    // index and the right index
    let ans = 0, l = 0, r = 0;

    // To store si - i value
    let mp = new Map();

    for (let i = 0; i < n + 1; i++) {
        if (!mp.has(sum[i]))
            mp.set(sum[i], 0);
    }
    let temp;

    for (let i = 0; i < n + 1; i++) {

        // Include sum
        ans += mp.get(sum[i]);
        temp = mp.get(sum[i]) + 1;
        mp.set(sum[i], temp);

        // Increment the right index
        r++;

        // If subarray has at least
        // k elements
        if (r - l >= k) {
            //mp[sum[l]]--;
            temp = mp.get(sum[l]) - 1;
            mp.set(sum[i], temp);
            l++;
        }
    }

    // Return the required answer
    return ans;
}

// Driver code

let a = [1, 4, 2, 3, 5];

let n = a.length;

let k = 4;

// Function call
document.write(sub_arrays(a, n, k));

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
4
```

**时间复杂度:** O(N* log(N))
**辅助空间:** O(N)