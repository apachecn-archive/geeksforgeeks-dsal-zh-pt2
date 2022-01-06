# 最大化形成的组的数量，其大小不小于其最大元素

> 原文:[https://www . geeksforgeeks . org/最大化大小不小于其最大元素的组数/](https://www.geeksforgeeks.org/maximize-number-of-groups-formed-with-size-not-smaller-than-its-largest-element/)

给定一个正整数(1 ≤ arr[i] ≤ N)的数组 **arr[]** ，将数组的元素分成组，使得每组的大小大于或等于该组的最大元素。也有可能一个元素不能加入任何组。任务是最大化组的数量。

**示例:**

> **输入:** arr = {2，3，1，2，2}
> **输出:** 2
> **说明:**
> 第一组我们可以取{1，2}
> 第二组我们可以取{2，2，3}
> 因此，最多可以取 2 组。
> 
> **输入:** arr = {1，1，1 }
> T3】输出: 3

**进场:**

*   首先存储数组中每个元素出现的次数。
*   现在，将相似的元素分组。例如:如果数组中有三个 1，那么为每个 1 创建三个组。
*   然后存储剩余的元素，并从最低的元素开始分组。

下面是上述方法的实现。

## C++

```
// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

// Function that prints the number
// of maximum groups
void makeGroups(int a[], int n)
{
    vector<int> v(n + 1, 0);

    // Store the number of
    // occurrence of elements
    for (int i = 0; i < n; i++) {
        v[a[i]]++;
    }

    int no_of_groups = 0;

    // Make all groups of similar
    // elements and store the
    // left numbers
    for (int i = 1; i <= n; i++) {
        no_of_groups += v[i] / i;

        v[i] = v[i] % i;
    }

    int i = 1;
    int total = 0;

    for (i = 1; i <= n; i++) {
        // Condition for finding first
        // leftover element
        if (v[i] != 0) {
            total = v[i];
            break;
        }
    }

    i++;

    while (i <= n) {
        // Condition for current
        // leftover element
        if (v[i] != 0) {
            total += v[i];

            // Condition if group size
            // is equal to or more than
            // current element
            if (total >= i) {
                int rem = total - i;
                no_of_groups++;
                total = rem;
            }
        }
        i++;
    }

    // Printing maximum
    // number of groups
    cout << no_of_groups << "\n";
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 1, 2, 2 };

    int size = sizeof(arr) / sizeof(arr[0]);

    makeGroups(arr, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
class GFG{

// Function that prints the number
// of maximum groups
static void makeGroups(int a[], int n)
{
    int []v = new int[n + 1];

    // Store the number of
    // occurrence of elements
    for (int i = 0; i < n; i++)
    {
        v[a[i]]++;
    }

    int no_of_groups = 0;

    // Make all groups of similar
    // elements and store the
    // left numbers
    for (int i = 1; i <= n; i++)
    {
        no_of_groups += v[i] / i;

        v[i] = v[i] % i;
    }

    int i = 1;
    int total = 0;

    for (i = 1; i <= n; i++)
    {
        // Condition for finding first
        // leftover element
        if (v[i] != 0)
        {
            total = v[i];
            break;
        }
    }

    i++;

    while (i <= n)
    {
        // Condition for current
        // leftover element
        if (v[i] != 0)
        {
            total += v[i];

            // Condition if group size
            // is equal to or more than
            // current element
            if (total >= i)
            {
                int rem = total - i;
                no_of_groups++;
                total = rem;
            }
        }
        i++;
    }

    // Printing maximum
    // number of groups
    System.out.print(no_of_groups + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 1, 2, 2 };

    int size = arr.length;

    makeGroups(arr, size);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# python3 implementation of above approach
# Function that prints the number
# of maximum groups
def makeGroups(a, n):
    v = [0] * (n + 1)

    # Store the number of
    # occurrence of elements
    for i in range (n):
        v[a[i]] += 1

    no_of_groups = 0

    # Make all groups of similar
    # elements and store the
    # left numbers
    for i in range (1, n + 1):
        no_of_groups += v[i] // i
        v[i] = v[i] % i

    i = 1
    total = 0
    for i in range ( 1, n + 1):

        # Condition for finding first
        # leftover element
        if (v[i] != 0):
            total = v[i]
            break

    i += 1
    while (i <= n):

        # Condition for current
        # leftover element
        if (v[i] != 0):
            total += v[i]

            # Condition if group size
            # is equal to or more than
            # current element
            if (total >= i):
                rem = total - i
                no_of_groups += 1
                total = rem

        i += 1

    # Printing maximum
    # number of groups
    print (no_of_groups)

# Driver Code
if __name__ == "__main__": 
    arr = [2, 3, 1, 2, 2]
    size = len(arr)
    makeGroups(arr, size)

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation of above approach
using System;
class GFG{

// Function that prints the number
// of maximum groups
static void makeGroups(int []a, int n)
{
    int []v = new int[n + 1];
    int i = 0;

    // Store the number of
    // occurrence of elements
    for(i = 0; i < n; i++)
    {
       v[a[i]]++;
    }

    int no_of_groups = 0;

    // Make all groups of similar
    // elements and store the
    // left numbers
    for(i = 1; i <= n; i++)
    {
       no_of_groups += v[i] / i;
       v[i] = v[i] % i;
    }

    i = 1;
    int total = 0;
    for(i = 1; i <= n; i++)
    {

       // Condition for finding first
       // leftover element
       if (v[i] != 0)
       {
           total = v[i];
           break;
       }
    }
    i++;

    while (i <= n)
    {

        // Condition for current
        // leftover element
        if (v[i] != 0)
        {
            total += v[i];

            // Condition if group size
            // is equal to or more than
            // current element
            if (total >= i)
            {
                int rem = total - i;
                no_of_groups++;
                total = rem;
            }
        }
        i++;
    }

    // Printing maximum
    // number of groups
    Console.Write(no_of_groups + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 2, 3, 1, 2, 2 };
    int size = arr.Length;

    makeGroups(arr, size);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function that prints the number
// of maximum groups
function makeGroups(a, n)
{
    let v = Array.from({length: n+1}, (_, i) => 0);

    // Store the number of
    // occurrence of elements
    for (let i = 0; i < n; i++)
    {
        v[a[i]]++;
    }

    let no_of_groups = 0;

    // Make all groups of similar
    // elements and store the
    // left numbers
    for (let i = 1; i <= n; i++)
    {
        no_of_groups += Math.floor(v[i] / i);

        v[i] = v[i] % i;
    }

    let i = 1;
    let total = 0;

    for (i = 1; i <= n; i++)
    {
        // Condition for finding first
        // leftover element
        if (v[i] != 0)
        {
            total = v[i];
            break;
        }
    }

    i++;

    while (i <= n)
    {
        // Condition for current
        // leftover element
        if (v[i] != 0)
        {
            total += v[i];

            // Condition if group size
            // is equal to or more than
            // current element
            if (total >= i)
            {
                let rem = total - i;
                no_of_groups++;
                total = rem;
            }
        }
        i++;
    }

    // Printing maximum
    // number of groups
    document.write(no_of_groups + "\n");
}

// Driver Code

   let arr = [ 2, 3, 1, 2, 2 ];

    let size = arr.length;

    makeGroups(arr, size);

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)*