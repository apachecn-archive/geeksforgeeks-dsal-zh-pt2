# 包含给定数组的所有元素所需的小数组的最小容量

> 原文:[https://www . geeksforgeeks . org/需要包含给定阵列所有元素的小阵列最小容量/](https://www.geeksforgeeks.org/minimum-capacity-of-small-arrays-needed-to-contain-all-element-of-the-given-array/)

给定一个正整数的**数组**和值 **K** ，任务是在小于或等于 K 个小数组中清空数组，使得每个小数组最多只能包含给定数组的单个槽/索引中的 **P** 元素。求 p 的最小值
**例:**

> **输入:** arr[] = {1，2，3，4，5}，K = 7
> **输出:** 3
> **解释:**
> 我们把 1 放入第一个小数组，
> 2 放入第二个数组，
> 3 放入第三个数组，
> 之后，我们把其他元素分为 1 + 3 和 2 + 3
> 这 4 个元素可以放入剩下的 4 个框中。
> 所以，P 的要求值是 3。
> **输入:** arr[] = {23，1，43，66，220}，K = 102
> **输出:** 4

**方法:**要解决这个问题我们需要[二分搜索法](https://www.geeksforgeeks.org/binary-search/)的答案。

1.  首先，我们将下限设置为 1，上限设置为给定数组的最大值。
2.  现在，我们可以在这个范围内表演二分搜索法。对于容量的特定值，我们计算包含项目中所有值所需的小数组的数量。
3.  如果所需的小数组数量大于 K，答案肯定更大。因此，我们修剪搜索的左侧。如果它小于或等于 K，我们将此值保留为潜在答案，并修剪搜索的右侧。

下面是上述方法的实现。

## C++

```
// C++ program to find the Minimum
// capacity of small arrays needed
// to contain all element of
// the given array
#include <bits/stdc++.h>
using namespace std;

// Function returns the value
// of Minimum capacity needed
int MinimumCapacity(vector<int> arr,
                    int K)
{
    // Initializing maximum
    // value
    int maxVal = arr[0];

    // Finding maximum value
    // in arr
    for (auto x : arr)
        maxVal = max(maxVal, x);

    int l = 1, r = maxVal, m;
    int ans, req;

    // Binary Search the answer
    while (l <= r)
    {

        // m is the mid-point
        // of the range
        m = l + (r - l) / 2;

        req = 0;

        // Finding the total number of
        // arrays needed to completely
        // contain the items array
        // with P = req
        for (auto x : arr)
            req += x / m + (x % m > 0);

        // If the required number of
        // arrays is more than K, it
        // means we need to increase
        // the value of P
        if (req > K)
            l = m + 1;

        else
            // If the required number of
            // arrays is less than or equal
            // to K, it means this is a
            // possible answer and we go to
            // check if any smaller possible
            // value exists for P
            ans = m, r = m - 1;
    }

    return ans;
}

// Driver Code
int main()
{

    // Given array
    vector<int> arr = { 1, 2, 3, 4, 5 };

    // Number of available small arrays
    int K = 7;

    cout << MinimumCapacity(arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the Minimum
// capacity of small arrays needed
// to contain all element of
// the given array
class GFG{

// Function returns the value
// of Minimum capacity needed
static int MinimumCapacity(int []arr,
                           int K)
{
    // Initializing maximum
    // value
    int maxVal = arr[0];

    // Finding maximum value
    // in arr
    for (int x : arr)
        maxVal = Math.max(maxVal, x);

    int l = 1, r = maxVal, m;
    int ans = 0, req;

    // Binary Search the answer
    while (l <= r)
    {

        // m is the mid-point
        // of the range
        m = l + (r - l) / 2;

        req = 0;

        // Finding the total number of
        // arrays needed to completely
        // contain the items array
        // with P = req
        for (int x : arr)
            req += x / m + (x % m > 0 ? 1 : 0);

        // If the required number of
        // arrays is more than K, it
        // means we need to increase
        // the value of P
        if (req > K)
            l = m + 1;

        else
        {
            // If the required number of
            // arrays is less than or equal
            // to K, it means this is a
            // possible answer and we go to
            // check if any smaller possible
            // value exists for P
            ans = m;
            r = m - 1;
        }
    }

    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int []arr = { 1, 2, 3, 4, 5 };

    // Number of available small arrays
    int K = 7;

    System.out.print(MinimumCapacity(arr, K));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the Minimum
# capacity of small arrays needed
# to contain all element of
# the given array

# Function returns the value
# of Minimum capacity needed
def MinimumCapacity(arr, K):

    # Initializing maximum
    # value
    maxVal = arr[0]

    # Finding maximum value
    # in arr
    for x in arr:
        maxVal = max(maxVal, x)

    l = 1
    r = maxVal
    m = 0
    ans = 0
    req = 0

    # Binary Search the answer
    while l <= r:

        # m is the mid-point
        # of the range
        m = l + (r - l) // 2

        req = 0

        # Finding the total number of
        # arrays needed to completely
        # contain the items array
        # with P = req
        for x in arr:
            req += x // m + (x % m > 0)

        # If the required number of
        # arrays is more than K, it
        # means we need to increase
        # the value of P
        if req > K:
            l = m + 1

        else:

            # If the required number of
            # arrays is less than or equal
            # to K, it means this is a
            # possible answer and we go to
            # check if any smaller possible
            # value exists for P
            ans = m
            r = m - 1

    return ans

#Driver Code
# Given array
arr = [ 1, 2, 3, 4, 5 ]

# Number of available small arrays
K = 7
print(MinimumCapacity(arr, K))

# This code is contributed by divyamohan123
```

## C#

```
// C# program to find the minimum
// capacity of small arrays needed
// to contain all element of
// the given array
using System;

class GFG{

// Function returns the value
// of minimum capacity needed
static int MinimumCapacity(int []arr,
                           int K)
{

    // Initializing maximum
    // value
    int maxVal = arr[0];

    // Finding maximum value
    // in arr
    foreach (int x in arr)
        maxVal = Math.Max(maxVal, x);

    int l = 1, r = maxVal, m;
    int ans = 0, req;

    // Binary Search the answer
    while (l <= r)
    {

        // m is the mid-point
        // of the range
        m = l + (r - l) / 2;

        req = 0;

        // Finding the total number of
        // arrays needed to completely
        // contain the items array
        // with P = req
        foreach (int x in arr)
            req += x / m + (x % m > 0 ? 1 : 0);

        // If the required number of
        // arrays is more than K, it
        // means we need to increase
        // the value of P
        if (req > K)
            l = m + 1;

        else
        {

            // If the required number of
            // arrays is less than or equal
            // to K, it means this is a
            // possible answer and we go to
            // check if any smaller possible
            // value exists for P
            ans = m;
            r = m - 1;
        }
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array
    int []arr = { 1, 2, 3, 4, 5 };

    // Number of available small arrays
    int K = 7;

    Console.Write(MinimumCapacity(arr, K));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // JavaScript program to find the minimum
    // capacity of small arrays needed
    // to contain all element of
    // the given array

    // Function returns the value
    // of minimum capacity needed
    function MinimumCapacity(arr, K)
    {

        // Initializing maximum
        // value
        let maxVal = arr[0];

        // Finding maximum value
        // in arr
        for(let x = 0; x < arr.length; x++)
            maxVal = Math.max(maxVal, arr[x]);

        let l = 1, r = maxVal, m;
        let ans = 0, req;

        // Binary Search the answer
        while (l <= r)
        {

            // m is the mid-point
            // of the range
            m = l + parseInt((r - l) / 2, 10);

            req = 0;

            // Finding the total number of
            // arrays needed to completely
            // contain the items array
            // with P = req
            for(let x = 0; x < arr.length; x++)
                req +=
                parseInt(arr[x] / m, 10) + (arr[x] % m > 0 ? 1 : 0);

            // If the required number of
            // arrays is more than K, it
            // means we need to increase
            // the value of P
            if (req > K)
                l = m + 1;

            else
            {

                // If the required number of
                // arrays is less than or equal
                // to K, it means this is a
                // possible answer and we go to
                // check if any smaller possible
                // value exists for P
                ans = m;
                r = m - 1;
            }
        }
        return ans;
    }

    // Given array
    let arr = [ 1, 2, 3, 4, 5 ];

    // Number of available small arrays
    let K = 7;

    document.write(MinimumCapacity(arr, K));

</script>
```

**Output:** 

```
3
```