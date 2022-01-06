# 执行给定操作后数组中剩余的最小元素

> 原文:[https://www . geeksforgeeks . org/执行给定操作后从数组中留下的最小元素/](https://www.geeksforgeeks.org/minimum-element-left-from-the-array-after-performing-given-operations/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是从数组的两端移除元素，即在一次操作中，可以从数组的当前剩余元素中移除第一个或最后一个元素。此操作需要以这样的方式执行，即剩下的最后一个元素将具有最小可能值。打印此最小值。
**例:**

> **输入:** arr[] = {5，3，1，6，9}
> **输出:** 1
> 操作 1: arr[] = {5，3，1，6}
> 操作 2: arr[] = {5，3，1}
> 操作 3: arr[] = {3，1}
> 操作 4: arr[] = {1}
> **输入:** arr[] = {2，6，4，8，2，6}

**方法:**这个问题可以贪婪地解决，需要在一次操作中移除任一端值最大的元素。按照这种方法，直到数组中只剩下一个元素，最后会给出原始数组中的最小元素。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum possible
// value of the last element left after
// performing the given operations
int getMin(int arr[], int n)
{
    int minVal = *min_element(arr, arr + n);
    return minVal;
}

// Driver code
int main()
{
    int arr[] = { 5, 3, 1, 6, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << getMin(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
class GFG
{

// Function to return the minimum possible
// value of the last element left after
// performing the given operations
static int getMin(int arr[], int n)
{
    int minVal = Arrays.stream(arr).min().getAsInt();
    return minVal;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 5, 3, 1, 6, 9 };
    int n = arr.length;

    System.out.println(getMin(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum possible
# value of the last element left after
# performing the given operations
def getMin(arr, n) :

    minVal = min(arr);
    return minVal;

# Driver code
if __name__ == "__main__" :

    arr = [ 5, 3, 1, 6, 9 ];
    n = len(arr);

    print(getMin(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;
using System.Linq;

class GFG
{

// Function to return the minimum possible
// value of the last element left after
// performing the given operations
static int getMin(int []arr, int n)
{
    int minVal = arr.Min();
    return minVal;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 5, 3, 1, 6, 9 };
    int n = arr.Length;

    Console.WriteLine(getMin(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript implementation of the above approach

    // Function to return the minimum possible
    // value of the last element left after
    // performing the given operations
    function getMin(arr, n)
    {
        var minVal = Math.min.apply(Math, arr);
        return minVal;
    }

    // Driver code
        var arr = [ 5, 3, 1, 6, 9 ];
        var n = arr.length;
        document.write(getMin(arr, n));

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
1
```