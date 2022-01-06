# 计算给定数组中不相等的元素对

> 原文:[https://www . geesforgeks . org/count-不等元素对-来自给定数组/](https://www.geeksforgeeks.org/count-unequal-element-pairs-from-the-given-array/)

给定一个由 **N** 元素组成的数组 **arr[]** 。任务是统计指数总数 **(i，j)** 这样**arr【I】！= arr[j]** 和 **i < j** 。
**举例:**

> **输入:** arr[] = {1，1，2}
> **输出:** 2
> (1，2)和(1，2)是唯一有效的对。
> **输入:** arr[] = {1，2，3}
> **输出:** 3
> **输入:** arr[] = {1，1，1}
> **输出:** 0

**方法:**初始化一个计数变量 **cnt = 0** 并运行两个嵌套循环来检查每个可能的对当前对是否有效。如果有效，则递增计数变量。最后，打印有效对的计数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the
// count of valid pairs
int countPairs(int arr[], int n)
{

    // To store the required count
    int cnt = 0;

    // For each index pair (i, j)
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // If current pair is valid
            // then increment the count
            if (arr[i] != arr[j])
                cnt++;
        }
    }
    return cnt;
}

// Driven code
int main()
{
    int arr[] = { 1, 1, 2 };
    int n = sizeof(arr) / sizeof(int);

    cout << countPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the
    // count of valid pairs
    static int countPairs(int arr[], int n)
    {

        // To store the required count
        int cnt = 0;

        // For each index pair (i, j)
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
            {

                // If current pair is valid
                // then increment the count
                if (arr[i] != arr[j])
                    cnt++;
            }
        }
        return cnt;
    }

    // Driven code
    public static void main (String[] args)
    {
        int arr[] = { 1, 1, 2 };
        int n = arr.length;

        System.out.println(countPairs(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the
# count of valid pairs
def countPairs(arr, n):

    # To store the required count
    cnt = 0;

    # For each index pair (i, j)
    for i in range(n):
        for j in range(i + 1, n):

            # If current pair is valid
            # then increment the count
            if (arr[i] != arr[j]):
                cnt += 1;

    return cnt;

# Driver code
if __name__ == '__main__':
    arr = [ 1, 1, 2 ];
    n = len(arr);

    print(countPairs(arr, n));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the
    // count of valid pairs
    static int countPairs(int []arr, int n)
    {

        // To store the required count
        int cnt = 0;

        // For each index pair (i, j)
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
            {

                // If current pair is valid
                // then increment the count
                if (arr[i] != arr[j])
                    cnt++;
            }
        }
        return cnt;
    }

    // Driven code
    public static void Main()
    {
        int []arr = { 1, 1, 2 };
        int n = arr.Length;

        Console.WriteLine(countPairs(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the
// count of valid pairs
function countPairs(arr, n)
{

    // To store the required count
    var cnt = 0;

    // For each index pair (i, j)
    for (var i = 0; i < n; i++) {
        for (var j = i + 1; j < n; j++) {

            // If current pair is valid
            // then increment the count
            if (arr[i] != arr[j])
                cnt++;
        }
    }
    return cnt;
}

// Driven code
var arr = [ 1, 1, 2 ];
var n = arr.length;
document.write(countPairs(arr, n));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N <sup>2</sup> )