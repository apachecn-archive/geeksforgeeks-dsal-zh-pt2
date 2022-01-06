# 通过仅移除一个元素使数组求和的方法计数

> 原文:[https://www . geeksforgeeks . org/仅移除一个元素来进行数组求和的方法计数/](https://www.geeksforgeeks.org/count-of-ways-to-make-array-sum-even-by-removing-only-one-element/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**正整数，任务是找到转换数组和的方法数量，即使我们只被允许移除一个元素。
**例:**

> **输入:** arr[] = { 1，3，3，2 }
> **输出:** 3
> **解释:**
> 1。去掉 1，那么和就是 3 + 3 + 2 = 8。
> 2。去掉 3，那么和就是 1 + 3 + 2 = 6。
> 3。去掉 3，那么和就是 1 + 3 + 2 = 6。
> **输入:** arr[] = { 4，8，3，3，6 }
> **输出:** 3
> **解释:**
> 1。去掉 4，那么和就是 8 + 3 + 3 + 6 = 20。
> 2。去掉 8，那么和就是 4 + 3 + 3 + 6 = 16。
> 3。去掉 6，那么和就是 4 + 8 + 3 + 3 = 18。

**方法:**对上述问题陈述的关键观察是:

1.  如果我们有奇数个奇数元素，那么和总是奇数，那么我们必须从数组中移除一个奇数 **arr[]** 以使和为偶数。由于我们必须移除一个元素，因此，使总和为偶数的方法总数是数组中奇数元素的**计数**arr【】**。**
2.  如果我们有偶数个奇数元素，那么和总是偶数。由于我们必须移除一个元素才能使和为偶数，因此，使和为偶数的方法总数是数组**arr【】**中偶数元素的**计数**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find a number of ways
// to make array element sum even by
// removing one element
int find_num_of_ways(int arr[], int N)
{
    int count_even = 0, count_odd = 0;

    // Finding the count of even
    // and odd elements
    for (int i = 0; i < N; i++) {
        if (arr[i] % 2) {
            count_odd++;
        }
        else {
            count_even++;
        }
    }

    // If count_odd is odd then
    // no. of ways is count_odd
    if (count_odd % 2) {
        return count_odd;
    }

    // Else no. of ways is count_even
    else {
        return count_even;
    }
}

// Driver Code
int main()
{

    // Given array arr[]
    int arr[] = { 1, 3, 3, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << find_num_of_ways(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find a number of ways
// to make array element sum even by
// removing one element
static int find_num_of_ways(int arr[], int N)
{
    int count_even = 0, count_odd = 0;

    // Finding the count of even
    // and odd elements
    for(int i = 0; i < N; i++)
    {
        if (arr[i] % 2 == 1)
        {
            count_odd++;
        }
        else
        {
            count_even++;
        }
    }

    // If count_odd is odd then
    // no. of ways is count_odd
    if (count_odd % 2 == 1)
    {
        return count_odd;
    }

    // Else no. of ways is count_even
    else
    {
        return count_even;
    }
}

// Driver Code
public static void main (String[] args)
{

    // Given array arr[]
    int arr[] = { 1, 3, 3, 2 };
    int N = 4;

    // Function call
    System.out.print(find_num_of_ways(arr, N));
}
}

// This code is contributed by Ritik Bansal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find a number of ways
# to make array element sum even by
# removing one element
def find_num_of_ways(arr, N):

    count_even = 0
    count_odd = 0

    # Finding the count of even
    # and odd elements
    for i in range(N):
        if (arr[i] % 2):
            count_odd += 1
        else:
            count_even += 1

    # If count_odd is odd then
    # no. of ways is count_odd
    if (count_odd % 2):
        return count_odd

    # Else no. of ways is count_even
    else:
        return count_even

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 1, 3, 3, 2 ]
    N = len(arr)

    # Function call
    print(find_num_of_ways(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find a number of ways
// to make array element sum even by
// removing one element
static int find_num_of_ways(int []arr, int N)
{
    int count_even = 0, count_odd = 0;

    // Finding the count of even
    // and odd elements
    for(int i = 0; i < N; i++)
    {
        if (arr[i] % 2 == 1)
        {
            count_odd++;
        }
        else
        {
            count_even++;
        }
    }

    // If count_odd is odd then
    // no. of ways is count_odd
    if (count_odd % 2 == 1)
    {
        return count_odd;
    }

    // Else no. of ways is count_even
    else
    {
        return count_even;
    }
}

// Driver Code
public static void Main(string[] args)
{

    // Given array arr[]
    int []arr = { 1, 3, 3, 2 };
    int N = 4;

    // Function call
    Console.Write(find_num_of_ways(arr, N));
}
}

// This code is contributed by Rutvik
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function to find a number of ways
// to make array element sum even by
// removing one element
function find_num_of_ways(arr , N)
{
    var count_even = 0, count_odd = 0;

    // Finding the count of even
    // and odd elements
    for(i = 0; i < N; i++)
    {
        if (arr[i] % 2 == 1)
        {
            count_odd++;
        }
        else
        {
            count_even++;
        }
    }

    // If count_odd is odd then
    // no. of ways is count_odd
    if (count_odd % 2 == 1)
    {
        return count_odd;
    }

    // Else no. of ways is count_even
    else
    {
        return count_even;
    }
}

// Driver Code

// Given array arr
var arr = [ 1, 3, 3, 2 ];
var N = 4;

// Function call
document.write(find_num_of_ways(arr, N));

// This code is contributed by Amit Katiyar
</script>
```

**Output:** 

```
3
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*