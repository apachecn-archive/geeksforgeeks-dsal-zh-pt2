# 在交替的步骤中删除奇数和偶数，使得剩余元素的总和最小

> 原文:[https://www . geesforgeks . org/delete-奇数和偶数-交替步长-这样剩余元素的总和被最小化/](https://www.geeksforgeeks.org/delete-odd-and-even-numbers-at-alternate-step-such-that-sum-of-remaining-elements-is-minimized/)

给定一个由 **N** 元素组成的数组 **arr[]** 。在任何一步中，我们都可以从上一步中删除一个不同的**奇偶校验**的数字，即如果在上一步中删除了一个奇数，则在当前步骤中删除一个偶数，反之亦然。
允许删除任意数字开始。删除是可能的，直到我们可以在每一步删除不同奇偶数。任务是找到末尾剩余元素的最小可能和。

**示例:**

> **输入:** arr[] = {1，5，7，8，2}
> **输出:** 0
> 删除顺序为 1，2，5，8，最后是 7 的元素。
> 有多种删除方式，
> 导致相同的最小化总和。
> 
> **输入:** arr[] = {2，2，2，2}
> **输出:** 6
> 第一步删除 2。
> 不能删除任何数字，因为已经没有奇数了。
> 因此，剩余元素之和为 6。

**方法:**解决上述问题可以遵循以下方式:

*   计算奇数和偶数元素的数量，并存储在向量 **v1** 和 **v2** 中。
*   检查奇数和偶数元素的数量是否相同或相差 **1** ，然后我们可以执行 N 个步骤，导致剩余和为 0。
*   如果大小相差超过 1，那么只有剩余的元素。
*   为了最小化剩余的元素总和，我们首先选择较大的元素。
*   因此，X 个较小元素的总和将是答案，其中 X 是**v2 . size()–v1 . size()–1**或**v1 . size()–v2 . size()–1**取决于偶数和奇数元素的计数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimized sum
int MinimizeleftOverSum(int a[], int n)
{
    vector<int> v1, v2;
    for (int i = 0; i < n; i++) {

        if (a[i] % 2)
            v1.push_back(a[i]);
        else
            v2.push_back(a[i]);
    }

    // If more odd elements
    if (v1.size() > v2.size()) {

        // Sort the elements
        sort(v1.begin(), v1.end());
        sort(v2.begin(), v2.end());

        // Left-over elements
        int x = v1.size() - v2.size() - 1;

        int sum = 0;
        int i = 0;

        // Find the sum of leftover elements
        while (i < x) {
            sum += v1[i++];
        }

        // Return the sum
        return sum;
    }

    // If more even elements
    else if (v2.size() > v1.size()) {

        // Sort the elements
        sort(v1.begin(), v1.end());
        sort(v2.begin(), v2.end());

        // Left-over elements
        int x = v2.size() - v1.size() - 1;

        int sum = 0;
        int i = 0;

        // Find the sum of leftover elements
        while (i < x) {
            sum += v2[i++];
        }

        // Return the sum
        return sum;
    }

    // If same elements
    else
        return 0;
}

// Driver code
int main()
{

    int a[] = { 2, 2, 2, 2 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << MinimizeleftOverSum(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to find the minimized sum
static int MinimizeleftOverSum(int a[], int n)
{
    Vector<Integer> v1 = new Vector<Integer>(),
                    v2 = new Vector<Integer>();
    for (int i = 0; i < n; i++)
    {

        if (a[i] % 2 == 1)
            v1.add(a[i]);
        else
            v2.add(a[i]);
    }

    // If more odd elements
    if (v1.size() > v2.size())
    {

        // Sort the elements
        Collections.sort(v1);
        Collections.sort(v2);

        // Left-over elements
        int x = v1.size() - v2.size() - 1;

        int sum = 0;
        int i = 0;

        // Find the sum of leftover elements
        while (i < x)
        {
            sum += v1.get(i++);
        }

        // Return the sum
        return sum;
    }

    // If more even elements
    else if (v2.size() > v1.size())
    {

        // Sort the elements
        Collections.sort(v1);
        Collections.sort(v2);

        // Left-over elements
        int x = v2.size() - v1.size() - 1;

        int sum = 0;
        int i = 0;

        // Find the sum of leftover elements
        while (i < x)
        {
            sum += v2.get(i++);
        }

        // Return the sum
        return sum;
    }

    // If same elements
    else
        return 0;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 2, 2, 2, 2 };
    int n = a.length;
    System.out.println(MinimizeleftOverSum(a, n));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the minimized sum
def MinimizeleftOverSum(a, n) :

    v1, v2 = [], [];
    for i in range(n) :

        if (a[i] % 2) :
            v1.append(a[i]);
        else :
            v2.append(a[i]);

    # If more odd elements
    if (len(v1) > len(v2)) :

        # Sort the elements
        v1.sort();
        v2.sort();

        # Left-over elements
        x = len(v1) - len(v2) - 1;

        sum = 0;
        i = 0;

        # Find the sum of leftover elements
        while (i < x) :
            sum += v1[i];
            i += 1

        # Return the sum
        return sum;

    # If more even elements
    elif (len(v2) > len(v1)) :

        # Sort the elements
        v1.sort();
        v2.sort();

        # Left-over elements
        x = len(v2) - len(v1) - 1;

        sum = 0;
        i = 0;

        # Find the sum of leftover elements
        while (i < x) :
            sum += v2[i];
            i += 1

        # Return the sum
        return sum;

    # If same elements
    else :
        return 0;

# Driver code
if __name__ == "__main__" :

    a = [ 2, 2, 2, 2 ];
    n = len(a);

    print(MinimizeleftOverSum(a, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the minimized sum
static int MinimizeleftOverSum(int []a,
                               int n)
{
    List<int> v1 = new List<int>(),
              v2 = new List<int>();
    for (int i = 0; i < n; i++)
    {

        if (a[i] % 2 == 1)
            v1.Add(a[i]);
        else
            v2.Add(a[i]);
    }

    // If more odd elements
    if (v1.Count > v2.Count)
    {

        // Sort the elements
        v1.Sort();
        v2.Sort();

        // Left-over elements
        int x = v1.Count - v2.Count - 1;

        int sum = 0;
        int i = 0;

        // Find the sum of leftover elements
        while (i < x)
        {
            sum += v1[i++];
        }

        // Return the sum
        return sum;
    }

    // If more even elements
    else if (v2.Count > v1.Count)
    {

        // Sort the elements
        v1.Sort();
        v2.Sort();

        // Left-over elements
        int x = v2.Count - v1.Count - 1;

        int sum = 0;
        int i = 0;

        // Find the sum of leftover elements
        while (i < x)
        {
            sum += v2[i++];
        }

        // Return the sum
        return sum;
    }

    // If same elements
    else
        return 0;
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 2, 2, 2, 2 };
    int n = a.Length;
    Console.WriteLine(MinimizeleftOverSum(a, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// javascript implementation of the approach

// Function to find the minimized sum
function MinimizeleftOverSum(a , n)
{
   var v1 = [], v2 =[];
    for (i = 0; i < n; i++)
    {

        if (a[i] % 2 == 1)
            v1.push(a[i]);
        else
            v2.push(a[i]);
    }

    // If more odd elements
    if (v1.length > v2.length)
    {

        // Sort the elements
        v1.sort();
        v2.sort();

        // Left-over elements
        var x = v1.length - v2.length - 1;

        var sum = 0;
        var i = 0;

        // Find the sum of leftover elements
        while (i < x)
        {
            sum += v1[i++];
        }

        // Return the sum
        return sum;
    }

    // If more even elements
    else if (v2.length > v1.length)
    {

        // Sort the elements
        v1.sort();
        v2.sort();

        // Left-over elements
        var x = v2.length - v1.length - 1;

        var sum = 0;
        var i = 0;

        // Find the sum of leftover elements
        while (i < x)
        {
            sum += v2[i++];
        }

        // Return the sum
        return sum;
    }

    // If same elements
    else
        return 0;
}

// Driver code
    var a = [ 2, 2, 2, 2 ];
    var n = a.length;
    document.write(MinimizeleftOverSum(a, n));

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
6
```