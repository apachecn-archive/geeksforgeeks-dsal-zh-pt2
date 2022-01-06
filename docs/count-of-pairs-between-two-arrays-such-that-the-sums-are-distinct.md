# 计算两个数组之间的对，使得和不同

> 原文:[https://www . geeksforgeeks . org/两个数组之间的对计数-这样总和就不同了/](https://www.geeksforgeeks.org/count-of-pairs-between-two-arrays-such-that-the-sums-are-distinct/)

给定两个数组 **a[]** 和 **b[]** ，任务是找到所有对的计数 **(a[i]，b[j])** ，使得 **a[i] + b[j]** 在所有对中是唯一的，即如果两个对具有相等的和，那么结果中将只计数一个。
**举例:**

> **输入:** a[] = {3，3}，b[] = {3}
> **输出:** 1
> 两个可能的对是(a[0]，b[0])和(a[1]，b[0])。
> 对 1: 3 + 3 = 6
> 对 2: 3 + 3 = 6
> **输入:** a[] = {12，2，7}，b[] = {4，3，8}
> **输出:** 7

**方法:**初始化**计数= 0** 并运行两个循环来考虑所有可能的对，并将每对的和存储在[无序 _ 集合](https://www.geeksforgeeks.org/unorderd_set-stl-uses/)中，以检查之前是否已经获得和。如果有，则忽略当前对，否则增加**计数**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of pairs with distinct sum
int countPairs(int a[], int b[], int n, int m)
{

    // To store the required count
    int cnt = 0;

    // Set to store the sum
    // obtained for each pair
    unordered_set<int> s;

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            // Sum of the current pair
            int sum = a[i] + b[j];

            // If the sum obtained is distinct
            if (s.count(sum) == 0) {

                // Increment the count
                cnt++;

                // Insert sum in the set
                s.insert(sum);
            }
        }
    }

    return cnt;
}

// Driver code
int main()
{
    int a[] = { 12, 2, 7 };
    int n = sizeof(a) / sizeof(a[0]);
    int b[] = { 4, 3, 8 };
    int m = sizeof(b) / sizeof(b[0]);

    cout << countPairs(a, b, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the count
    // of pairs with distinct sum
    static int countPairs(int a[], int b[], int n, int m)
    {

        // To store the required count
        int cnt = 0;

        // Set to store the sum
        // obtained for each pair
        HashSet<Integer> s = new HashSet<Integer>();

        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {

                // Sum of the current pair
                int sum = a[i] + b[j];

                // If the sum obtained is distinct
                if (s.contains(sum) == false)
                {

                    // Increment the count
                    cnt++;

                    // Insert sum in the set
                    s.add(sum);
                }
            }
        }

        return cnt;
    }

    // Driver code
    static public void main (String args[])
    {
        int a[] = { 12, 2, 7 };
        int n = a.length;
        int b[] = { 4, 3, 8 };
        int m = b.length;

        System.out.println(countPairs(a, b, n, m));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of pairs with distinct sum
def countPairs(a, b, n, m):

    # To store the required count
    cnt = 0

    # Set to store the sum
    # obtained for each pair
    s=dict()

    for i in range(n):
        for j in range(m):

            # Sum of the current pair
            sum = a[i] + b[j]

            # If the sum obtained is distinct
            if (sum not in s.keys()):
                # Increment the count
                cnt+=1

                # Insert sum in the set
                s[sum]=1

    return cnt

# Driver code

a =[ 12, 2, 7]
n = len(a)
b =[ 4, 3, 8 ]
m = len(b)

print(countPairs(a, b, n, m))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return the count
    // of pairs with distinct sum
    static int countPairs(int []a, int []b,
                          int n, int m)
    {

        // To store the required count
        int cnt = 0;

        // Set to store the sum
        // obtained for each pair
        HashSet<int> s = new HashSet<int>();

        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {

                // Sum of the current pair
                int sum = a[i] + b[j];

                // If the sum obtained is distinct
                if (s.Contains(sum) == false)
                {

                    // Increment the count
                    cnt++;

                    // Insert sum in the set
                    s.Add(sum);
                }
            }
        }

        return cnt;
    }

    // Driver code
    static public void Main (String []args)
    {
        int []a = { 12, 2, 7 };
        int n = a.Length;
        int []b = { 4, 3, 8 };
        int m = b.Length;

        Console.WriteLine(countPairs(a, b, n, m));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to return the count
    // of pairs with distinct sum
    function countPairs(a, b, n, m)
    {

        // To store the required count
        let cnt = 0;

        // Set to store the sum
        // obtained for each pair
        let s = new Set();

        for (let i = 0; i < n; i++)
        {
            for (let j = 0; j < m; j++)
            {

                // Sum of the current pair
                let sum = a[i] + b[j];

                // If the sum obtained is distinct
                if (s.has(sum) == false)
                {

                    // Increment the count
                    cnt++;

                    // Insert sum in the set
                    s.add(sum);
                }
            }
        }

        return cnt;
    }

    // Driver code

        let a = [ 12, 2, 7 ];
        let n = a.length;
        let b = [ 4, 3, 8 ];
        let m = b.length;

        document.write(countPairs(a, b, n, m));

    // This code is contributed by susmitakundugoaldanga.     
</script>
```

**Output:** 

```
7
```

**时间复杂度:** O(N * M)。
**辅助空间** : O(1)。