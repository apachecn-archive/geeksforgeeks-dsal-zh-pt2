# 给定数组的所有非空子序列中不同 gcd 的计数

> 原文:[https://www . geeksforgeeks . org/count-of-distinct-gcds-in-all-non-empty-subseries-of-给定数组/](https://www.geeksforgeeks.org/count-of-distinct-gcds-among-all-the-non-empty-subsequences-of-given-array/)

给定一个大小为 **N** 的整数数组 **arr[]** ，任务是计算 **arr[]** 的所有非空子序列中不同的 [**最大公约数(GCDs)**](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 的总数。

**示例:**

> **输入:** arr[]={3，4，8} N=3
> **输出:**
> 4
> **解释:**
> 不同的非空子序列可能是{3}、{4}、{8}、{3，4}、{4，8}、{3，8}、{3，4，8}，它们对应的 GCDs 是 3，4，8，1，1。
> 因此，不同 gcd 的总数为 4 (1，3，4，8)。
> 
> **输入:** arr[]={3，11，14，6，12}，N = 5
> T3】输出:T5】7

**天真方法:**天真方法是找到所有子序列，计算每个子序列的 **GCDs** ，最后计算不同的 **GCDs** 的总数。

***时间复杂度:** O(2 <sup>N</sup> 。Log(M))，其中 M 是数组中最大的元素。*

**方法:**给定的问题可以基于以下观察来解决:

1.  最大可能的 **GCD** 不能超过数组的最大元素(比如 **M** )。因此，所有可能的 **GCDs** 位于 **1** 至 **M** 之间。
2.  通过迭代 **GCD** 的所有可能值，即从 **1** 到 **M** ，并检查数组中是否存在任何倍数的 **i** ，并且其 **GCD** 等于 **i** ，问题就可以解决了。

按照以下步骤解决问题:

1.  将变量**和**初始化为 0。
2.  计算**中的[最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)并将**存储在一个变量中，比如 **M** 。
3.  将 **arr** 的所有元素存储在[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **地图**中，以便进行定时访问。
4.  使用变量 **i** 遍历 **GCD** 的所有可能值，即从 **1** 到 **M** ，并执行以下操作:
    *   使用变量 **j** 遍历 **arr** 中出现的 **M** 的倍数，并执行以下操作:
    *   如果 **GCD** 在任一点变为 **i** ，则增加 **ans** 并断开。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the number
// of distinct GCDs among all
// non-empty subsequences of an array
int distinctGCDs(int arr[], int N)
{
    // variables to store the largest element
// in array and the required count
    int M = -1, ans = 0;

    // Map to store whether
// a number is present in A
    map<int, int> Mp;

    // calculate largest number
// in A and mapping A to Mp
    for (int i = 0; i < N; i++) {
        M = max(M, arr[i]);
        Mp[arr[i]] = 1;
    }

    // iterate over all possible values of GCD
    for (int i = 1; i <= M; i++) {

        // variable to check current GCD
        int currGcd = 0;

        // iterate over all multiples of i
        for (int j = i; j <= M; j += i) {

            // If j is present in A
            if (Mp[j]) {

                // calculate gcd of all encountered
                // multiples of i
                currGcd = __gcd(currGcd, j);

                // current GCD is possible
                if (currGcd == i) {
                    ans++;
                    break;
                }
            }
        }
    }
    // return answer
    return ans;
}
// Driver code
int main()
{
    // Input
    int arr[] = { 3, 11, 14, 6, 12 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function calling
    cout << distinctGCDs(arr, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

static int gcd(int a, int b)
{
    return b == 0 ? a : gcd(b, a % b);
}

// Function to calculate the number
// of distinct GCDs among all
// non-empty subsequences of an array
static int distinctGCDs(int []arr, int N)
{

    // Variables to store the largest element
    // in array and the required count
    int M = -1, ans = 0;

    // Map to store whether
    // a number is present in A
    HashMap<Integer,
               Integer> Mp = new HashMap<Integer,
                                        Integer>();

    // Calculate largest number
    // in A and mapping A to Mp
    for(int i = 0; i < N; i++)
    {
        M = Math.max(M, arr[i]);

        if (Mp.containsKey(arr[i]))
            Mp.put(arr[i],1);
        else
            Mp.put(arr[i],0);
    }

    // Iterate over all possible values of GCD
    for(int i = 1; i <= M; i++)
    {

        // Variable to check current GCD
        int currGcd = 0;

        // Iterate over all multiples of i
        for(int j = i; j <= M; j += i)
        {

            // If j is present in A
            if (Mp.containsKey(j))
            {

                // Calculate gcd of all encountered
                // multiples of i
                currGcd = gcd(currGcd, j);

                // Current GCD is possible
                if (currGcd == i)
                {
                    ans++;
                    break;
                }
            }
        }
    }

    // Return answer
    return ans;
}

// Driver code
public static void main(String [] args)
{

    // Input
    int []arr = { 3, 11, 14, 6, 12 };
    int N = arr.length;

    // Function calling
    System.out.println(distinctGCDs(arr, N));
}
}

// This code is contributed by ukasp.
```

## 蟒蛇 3

```
# Python 3 program for the above approach
from math import gcd

# Function to calculate the number
# of distinct GCDs among all
# non-empty subsequences of an array
def distinctGCDs(arr, N):

    # variables to store the largest element
    # in array and the required count
    M = -1
    ans = 0

    # Map to store whether
    # a number is present in A
    Mp = {}

    # calculate largest number
    # in A and mapping A to Mp
    for i in range(N):
        M = max(M, arr[i])
        Mp[arr[i]] = 1

    # iterate over all possible values of GCD
    for i in range(1, M + 1, 1):

        # variable to check current GCD
        currGcd = 0

        # iterate over all multiples of i
        for j in range(i, M + 1, i):

            # If j is present in A
            if (j in Mp):

                # calculate gcd of all encountered
                # multiples of i
                currGcd = gcd(currGcd, j)

                # current GCD is possible
                if (currGcd == i):
                    ans += 1
                    break

    # return answer
    return ans

# Driver code
if __name__ == '__main__':
    # Input
    arr = [3, 11, 14, 6, 12]
    N = len(arr)

    # Function calling
    print(distinctGCDs(arr, N))

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static int gcd(int a, int b)
{
    return b == 0 ? a : gcd(b, a % b);
}

// Function to calculate the number
// of distinct GCDs among all
// non-empty subsequences of an array
static int distinctGCDs(int []arr, int N)
{

    // Variables to store the largest element
    // in array and the required count
    int M = -1, ans = 0;

    // Map to store whether
    // a number is present in A
    Dictionary<int,
               int> Mp = new Dictionary<int,
                                        int>();

    // Calculate largest number
    // in A and mapping A to Mp
    for(int i = 0; i < N; i++)
    {
        M = Math.Max(M, arr[i]);

        if (Mp.ContainsKey(arr[i]))
            Mp[arr[i]] = 1;
        else
            Mp.Add(arr[i],1);
    }

    // Iterate over all possible values of GCD
    for(int i = 1; i <= M; i++)
    {

        // Variable to check current GCD
        int currGcd = 0;

        // Iterate over all multiples of i
        for(int j = i; j <= M; j += i)
        {

            // If j is present in A
            if (Mp.ContainsKey(j))
            {

                // Calculate gcd of all encountered
                // multiples of i
                currGcd = gcd(currGcd, j);

                // Current GCD is possible
                if (currGcd == i)
                {
                    ans++;
                    break;
                }
            }
        }
    }

    // Return answer
    return ans;
}

// Driver code
public static void Main()
{

    // Input
    int []arr = { 3, 11, 14, 6, 12 };
    int N = arr.Length;

    // Function calling
    Console.Write(distinctGCDs(arr, N));
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>
        // JavaScript program for the above approach

        // Function to calculate gcd
        function gcd(a, b)
        {
            if (b == 0)
                return a;
            return gcd(b, a % b);
        }

        // Function to calculate the number
        // of distinct GCDs among all
        // non-empty subsequences of an array
        function distinctGCDs(arr, N)
        {

            // variables to store the largest element
            // in array and the required count
            let M = -1, ans = 0;

            // Map to store whether
            // a number is present in A
            var Mp = new Map();

            // calculate largest number
            // in A and mapping A to Mp
            for (let i = 0; i < N; i++) {
                M = Math.max(M, arr[i]);
                Mp.set(arr[i], 1);
            }

            // iterate over all possible values of GCD
            for (let i = 1; i <= M; i++) {

                // variable to check current GCD
                let currGcd = 0;

                // iterate over all multiples of i
                for (let j = i; j <= M; j += i) {

                    // If j is present in A
                    if (Mp.has(j)) {

                        // calculate gcd of all encountered
                        // multiples of i
                        currGcd = gcd(currGcd, j);

                        // current GCD is possible
                        if (currGcd == i) {
                            ans++;
                            break;
                        }
                    }
                }
            }
            // return answer
            return ans;
        }
        // Driver code

        // Input
        let arr = [3, 11, 14, 6, 12];
        let N = arr.length;

        // Function calling
        document.write(distinctGCDs(arr, N) + '<br>');

  // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
7
```

***时间复杂度:** O(M*log(M))，其中 M 是数组中最大的元素*
***辅助空间:** O(M)*