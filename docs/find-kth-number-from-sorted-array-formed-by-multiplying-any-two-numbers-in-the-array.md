# 从数组中任意两个数相乘形成的排序数组中找出第 k 个数

> 原文:[https://www . geeksforgeeks . org/find-kth-number-from-sorted-array-formed-乘任意两个数组中的数字/](https://www.geeksforgeeks.org/find-kth-number-from-sorted-array-formed-by-multiplying-any-two-numbers-in-the-array/)

给定一个大小为 **N** 的数组**arr【】**和一个整数 **K** ，任务是从产品数组中找到第**K**号。
**注:**数组的积数组 **prod[]** 是大小为 **(N*(N-1))/2** 的排序数组，其中每个元素组成为 **prod[k] = arr[i] * arr[j]** ，其中 *0 ≤ i < j < N* 。
**例:**

> **输入:** arr[] = {-4，-2，3，3}，K = 3
> **输出:** -6
> 最终 prod[]数组= {-12，-12，-6，-6，8，9}
> 其中 prod[K] = -6
> **输入:**arr[= { 5，4，3，2，-1，0，0}，K = 20
> **输出:** 15

**天真方法:**通过迭代给定数组两次来生成 prod[]数组，然后对 prod[]数组进行排序，并从数组中找到第 K <sup>个</sup>元素。
**时间复杂度:**O(N<sup>2</sup>* log(N))
**高效方法:**负、零、正对的个数很容易确定，所以可以分辨出答案是负、零、还是正。如果答案是否定的，可以通过逐个选择负数和正数来测量大于或等于 K 的对的数量，因此答案是使用二分搜索法得到的。当答案是肯定的时候，答案是完全一样的，但是考虑两次选择相同的元素，减去它将每对精确计数两次。
以下是上述方法的实施:

## C++

```
// C++ implementation to find the
// Kth number in the list formed
// from product of any two numbers
// in the array and sorting them

#include <bits/stdc++.h>
using namespace std;

// Function to find number of pairs
bool check(long long x,
           vector<int>& pos,
           vector<int>& neg, int k)
{
    long long pairs = 0;

    int p = neg.size() - 1;
    int nn = neg.size() - 1;
    int pp = pos.size() - 1;

    // Negative and Negative
    for (int i = 0; i < neg.size(); i++) {
        while (p >= 0 and neg[i] * neg[p] <= x)
            p--;

        // Add Possible Pairs
        pairs += min(nn - p, nn - i);
    }

    // Positive and Positive
    p = 0;
    for (int i = pos.size() - 1; i >= 0; i--) {
        while (p < pos.size() and pos[i] * pos[p] <= x)
            p++;

        // Add Possible pairs
        pairs += min(p, i);
    }

    // Negative and Positive
    p = pos.size() - 1;
    for (int i = neg.size() - 1;
         i >= 0;
         i--) {
        while (p >= 0 and neg[i] * pos[p] <= x)
            p--;

        // Add Possible pairs
        pairs += pp - p;
    }

    return (pairs >= k);
}

// Function to find the kth
// element in the list
long long kth_element(int a[],
                      int n, int k)
{
    vector<int> pos, neg;

    // Separate Positive and
    // Negative elements
    for (int i = 0; i < n; i++) {
        if (a[i] >= 0)
            pos.push_back(a[i]);
        else
            neg.push_back(a[i]);
    }

    // Sort the Elements
    sort(pos.begin(), pos.end());
    sort(neg.begin(), neg.end());

    long long l = -1e18,
              ans = 0, r = 1e18;

    // Binary search
    while (l <= r) {
        long long mid = (l + r) >> 1;
        if (check(mid, pos, neg, k)) {
            ans = mid;
            r = mid - 1;
        }
        else
            l = mid + 1;
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int a[] = { -4, -2, 3, 3 }, k = 3;

    int n = sizeof(a) / sizeof(a[0]);

    // Function call
    cout << kth_element(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// Kth number in the list formed
// from product of any two numbers
// in the array and sorting them
import java.util.*;

class GFG
{

    // Function to find number of pairs
    static boolean check(int x, Vector pos, Vector neg, int k)
    {
        int pairs = 0;

        int p = neg.size() - 1;
        int nn = neg.size() - 1;
        int pp = pos.size() - 1;

        // Negative and Negative
        for (int i = 0; i < neg.size(); i++)
        {
            while ((p >= 0) && ((int)neg.get(i) *
                    (int)neg.get(p) <= x))
                p--;

            // Add Possible Pairs
            pairs += Math.min(nn - p, nn - i);
        }

        // Positive and Positive
        p = 0;
        for (int i = pos.size() - 1; i >= 0; i--)
        {
            while ((p < pos.size()) && ((int)pos.get(i) *
                    (int)pos.get(p) <= x))
                p++;

            // Add Possible pairs
            pairs += Math.min(p, i);
        }

        // Negative and Positive
        p = pos.size() - 1;
        for (int i = neg.size() - 1;
            i >= 0; i--) {
            while ((p >= 0) && ((int)neg.get(i) *
                    (int)pos.get(p) <= x))
                p--;

            // Add Possible pairs
            pairs += pp - p;
        }

        return (pairs >= k);
    }

    // Function to find the kth
    // element in the list
    static int kth_element(int a[], int n, int k)
    {
        Vector pos = new Vector();
        Vector neg = new Vector();;

        // Separate Positive and
        // Negative elements
        for (int i = 0; i < n; i++)
        {
            if (a[i] >= 0)
                pos.add(a[i]);
            else
                neg.add(a[i]);
        }

        // Sort the Elements
        //sort(pos.begin(), pos.end());
        //sort(neg.begin(), neg.end());
        Collections.sort(pos);
        Collections.sort(neg);

        int l = (int)-1e8, ans = 0, r = (int)1e8;

        // Binary search
        while (l <= r)
        {
            int mid = (l + r) >> 1;
            if (check(mid, pos, neg, k))
            {
                ans = mid;
                r = mid - 1;
            }
            else
                l = mid + 1;
        }

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void main (String[] args)
    {
        int a[] = { -4, -2, 3, 3 }, k = 3;
        int n = a.length;

        // Function call
        System.out.println(kth_element(a, n, k));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation to find the
# Kth number in the list formed
# from product of any two numbers
# in the array and sorting them

# Function to find number of pairs
def check(x, pos, neg, k):
    pairs = 0

    p = len(neg) - 1
    nn = len(neg) - 1
    pp = len(pos) - 1

    # Negative and Negative
    for i in range(len(neg)):
        while (p >= 0 and neg[i] * neg[p] <= x):
            p -= 1

        # Add Possible Pairs
        pairs += min(nn - p, nn - i)

    # Positive and Positive
    p = 0
    for i in range(len(pos) - 1, -1, -1):
        while (p < len(pos) and pos[i] * pos[p] <= x):
            p += 1

        # Add Possible pairs
        pairs += min(p, i)

    # Negative and Positive
    p = len(pos) - 1
    for i in range(len(neg) - 1, -1, -1):
        while (p >= 0 and neg[i] * pos[p] <= x):
            p -= 1

        # Add Possible pairs
        pairs += pp - p

    return (pairs >= k)

# Function to find the kth
# element in the list
def kth_element(a, n, k):
    pos, neg = [],[]

    # Separate Positive and
    # Negative elements
    for i in range(n):
        if (a[i] >= 0):
            pos.append(a[i])
        else:
            neg.append(a[i])

    # Sort the Elements
    pos = sorted(pos)
    neg = sorted(neg)

    l = -10**18
    ans = 0
    r = 10**18

    # Binary search
    while (l <= r):
        mid = (l + r) >> 1
        if (check(mid, pos, neg, k)):
            ans = mid
            r = mid - 1
        else:
            l = mid + 1

    # Return the required answer
    return ans

# Driver code
a = [-4, -2, 3, 3]
k = 3

n = len(a)

# Function call
print(kth_element(a, n, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find the
// Kth number in the list formed
// from product of any two numbers
// in the array and sorting them
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find number of pairs
    static bool check(int x, List<int> pos, List<int> neg, int k)
    {
        int pairs = 0;

        int p = neg.Count - 1;
        int nn = neg.Count - 1;
        int pp = pos.Count - 1;

        // Negative and Negative
        for (int i = 0; i < neg.Count; i++)
        {
            while ((p >= 0) && ((int)neg[i] *
                    (int)neg[p] <= x))
                p--;

            // Add Possible Pairs
            pairs += Math.Min(nn - p, nn - i);
        }

        // Positive and Positive
        p = 0;
        for (int i = pos.Count - 1; i >= 0; i--)
        {
            while ((p < pos.Count) && ((int)pos[i] *
                    (int)pos[p] <= x))
                p++;

            // Add Possible pairs
            pairs += Math.Min(p, i);
        }

        // Negative and Positive
        p = pos.Count - 1;
        for (int i = neg.Count - 1; i >= 0; i--)
        {
            while ((p >= 0) && ((int)neg[i] *
                    (int)pos[p] <= x))
                p--;

            // Add Possible pairs
            pairs += pp - p;
        }

        return (pairs >= k);
    }

    // Function to find the kth
    // element in the list
    static int kth_element(int []a, int n, int k)
    {
        List<int> pos = new List<int>();
        List<int> neg = new List<int>();;

        // Separate Positive and
        // Negative elements
        for (int i = 0; i < n; i++)
        {
            if (a[i] >= 0)
                pos.Add(a[i]);
            else
                neg.Add(a[i]);
        }

        // Sort the Elements
        //sort(pos.begin(), pos.end());
        //sort(neg.begin(), neg.end());
        pos.Sort();
        neg.Sort();

        int l = (int)-1e8, ans = 0, r = (int)1e8;

        // Binary search
        while (l <= r)
        {
            int mid = (l + r) >> 1;
            if (check(mid, pos, neg, k))
            {
                ans = mid;
                r = mid - 1;
            }
            else
                l = mid + 1;
        }

        // Return the required answer
        return ans;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []a = { -4, -2, 3, 3 };
        int k = 3;
        int n = a.Length;

        // Function call
        Console.WriteLine(kth_element(a, n, k));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript implementation to find the
    // Kth number in the list formed
    // from product of any two numbers
    // in the array and sorting them

    // Function to find number of pairs
    function check(x, pos, neg, k)
    {
        let pairs = 0;

        let p = neg.length - 1;
        let nn = neg.length - 1;
        let pp = pos.length - 1;

        // Negative and Negative
        for (let i = 0; i < neg.length; i++)
        {
            while ((p >= 0) && (neg[i] * neg[p] <= x))
                p--;

            // Add Possible Pairs
            pairs += Math.min(nn - p, nn - i);
        }

        // Positive and Positive
        p = 0;
        for (let i = pos.length - 1; i >= 0; i--)
        {
            while ((p < pos.length) && (pos[i] * pos[p] <= x))
                p++;

            // Add Possible pairs
            pairs += Math.min(p, i);
        }

        // Negative and Positive
        p = pos.length - 1;
        for (let i = neg.length - 1; i >= 0; i--)
        {
            while ((p >= 0) && (neg[i] * pos[p] <= x))
                p--;

            // Add Possible pairs
            pairs += pp - p;
        }

        return (pairs >= k);
    }

    // Function to find the kth
    // element in the list
    function kth_element(a, n, k)
    {
        let pos = [];
        let neg = [];

        // Separate Positive and
        // Negative elements
        for (let i = 0; i < n; i++)
        {
            if (a[i] >= 0)
                pos.push(a[i]);
            else
                neg.push(a[i]);
        }

        // Sort the Elements
        //sort(pos.begin(), pos.end());
        //sort(neg.begin(), neg.end());
        pos.sort(function(a, b){return a - b});
        neg.sort(function(a, b){return a - b});

        let l = -1e8, ans = 0, r = 1e8;

        // Binary search
        while (l <= r)
        {
            let mid = (l + r) >> 1;
            if (check(mid, pos, neg, k))
            {
                ans = mid;
                r = mid - 1;
            }
            else
                l = mid + 1;
        }

        // Return the required answer
        return ans;
    }

    let a = [ -4, -2, 3, 3 ];
    let k = 3;
    let n = a.length;

    // Function call
    document.write(kth_element(a, n, k));

// This coe is contributed by divyesh072019.
</script>
```

**Output:** 

```
-6
```