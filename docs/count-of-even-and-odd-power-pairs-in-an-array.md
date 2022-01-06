# 阵列中偶数和奇数功率对的计数

> 原文:[https://www . geeksforgeeks . org/阵列中奇偶幂对的计数/](https://www.geeksforgeeks.org/count-of-even-and-odd-power-pairs-in-an-array/)

给定一个长度为 **N** 的数组**arr【】**，任务是计算对的数量 **(X，Y)** 使得**X<sup>Y</sup>T9】为偶数，并且计算对的数量使得**X<sup>Y</sup>T13】为奇数。
**举例:****** 

> **输入:** arr[] = {2，3，4，5}
> **输出:**
> 6
> 6
> **说明:** (2，3)、(2，4)、(2，5)、(4，2)、(4，3)和(4，5)为偶数值对
> 和(3，2)、(3，4)、(3，5)、(5)、(2)、(5，3)和(5，4)为奇数值对。
> **输入:** arr[] = {10，11，20，60，70}
> **输出:**
> 16
> 4
> **解释:** (10，11)，(10，20)，(10，60)，(10，70)，(20，10)，(20，11)，(20，60)，(20，70)，(60，10)，(60，10)

**天真的方法:**计算每一个可能的单对的幂，并找出计算值是偶数还是奇数。
**高效做法:**统计数组中的偶、奇元素，然后使用幂(偶，除自身外的任意元素)为偶，幂(奇，除自身外的任意元素)为奇的概念。
所以，对(X，Y)的数量是，

*   幂(X，Y)为偶数=(偶数计数*(n–1))
*   幂(X，Y)是奇数=(奇数的计数*(n–1))

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to find and print the
// required count of pairs
void countPairs(int arr[], int n)
{

    // Find the count of even and
    // odd elements in the array
    int even = 0, odd = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] % 2 == 0)
            even++;
        else
            odd++;
    }

    // Print the required count of pairs
    cout << (even) * (n - 1) << endl;
    cout << (odd) * (n - 1) << endl;
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    countPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to find and print the
    // required count of pairs
    static void countPairs(int arr[], int n)
    {

        // Find the count of even and
        // odd elements in the array
        int even = 0, odd = 0;
        for (int i = 0; i < n; i++)
        {
            if (arr[i] % 2 == 0)
                even++;
            else
                odd++;
        }

        // Print the required count of pairs
        System.out.println((even) * (n - 1));
        System.out.println((odd) * (n - 1));
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 2, 3, 4, 5 };
        int n = arr.length;

        countPairs(arr, n);
    }
}

// This code is contributed by ANKITUMAR34
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find and print the
# required count of pairs
def countPairs(arr, n):

    # Find the count of even and
    # odd elements in the array
    odd = 0
    even = 0
    for i in range(n):
        if (arr[i] % 2 == 0):
            even += 1
        else:
            odd += 1

    # Count the number of odd pairs
    odd_pairs = odd*(n-1)

    # Count the number of even pairs
    even_pairs = even*(n-1)

    print(odd_pairs)
    print(even_pairs)

# Driver code
if __name__ == '__main__':
    arr = [2, 3, 4, 5]
    n = len(arr)
    countPairs(arr, n)
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to find and print the
    // required count of pairs
    static void countPairs(int []arr, int n)
    {

        // Find the count of even and
        // odd elements in the array
        int even = 0, odd = 0;
        for (int i = 0; i < n; i++)
        {
            if (arr[i] % 2 == 0)
                even++;
            else
                odd++;
        }

        // Print the required count of pairs
        Console.WriteLine((even) * (n - 1));
        Console.WriteLine((odd) * (n - 1));
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 2, 3, 4, 5 };
        int n = arr.Length;

        countPairs(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

    // Javascript implementation of the approach

    // Function to find and print the
    // required count of pairs
    function countPairs(arr, n)
    {

        // Find the count of even and
        // odd elements in the array
        let even = 0, odd = 0;
        for (let i = 0; i < n; i++)
        {
            if (arr[i] % 2 == 0)
                even++;
            else
                odd++;
        }

        // Print the required count of pairs
        document.write((even) * (n - 1) + "</br>");
        document.write((odd) * (n - 1));
    }

    let arr = [ 2, 3, 4, 5 ];
    let n = arr.length;

    countPairs(arr, n);

</script>
```

**Output:** 

```
6
6
```