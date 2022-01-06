# 不使用或运算符的数组中一对的最大或值

> 原文:[https://www . geeksforgeeks . org/不使用或运算符的阵列对最大值或最大值/](https://www.geeksforgeeks.org/maximum-or-value-of-a-pair-in-an-array-without-using-or-operator/)

给定一个包含 **N** 正整数的数组 **arr[]** ，任务是在不使用按位或运算符的情况下找到给定数组中一对的最大按位或值。
**例:**

> **输入:** arr[] = {3，6，8，16}
> **输出:** 24
> **解释:**
> 给出最大 OR 值的对为(8，16) = > 8|16 = 24
> **输入:** arr[] = {8，7，3，12}
> **输出:** 15
> **解释:**T18 其中一个= > 8|7 = 15

**方法:**想法是在不同的索引处找到集合位数最多的两个数字。这样，结果数将所有这些索引作为一个设置位，这可以在不使用[或运算符](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的情况下完成。

*   找出数组中的最大元素，然后在剩余的数组中找到在索引处具有设置位的特定元素，其中最大元素具有未设置位。
*   为了最大化我们的输出，我们必须找到这样一个元素，它将有一个设置位，以最大化我们的输出。
*   计算数组中最大元素的补数，并用其他数字求出最大“与”值。
*   这个与其他数组元素的补码的最大“与”值将给出由于其他数组元素而可能在我们的答案中设置的最大未设置位。
*   用这个最大“与”值添加最大元素将会得到我们想要的最大“或”值对，而不使用“或”运算。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum bitwise OR
// for any pair of the given array
// without using bitwise OR operation
int maxOR(int arr[], int n)
{

    // find maximum element in the array
    int max_value
        = *max_element(arr, arr + n);

    int number_of_bits
        = floor(log2(max_value)) + 1;

    // finding complement will set
    // all unset bits in a number
    int complement
        = ((1 << number_of_bits) - 1)
          ^ max_value;

    int c = 0;

    // iterate through all other
    // array elements to find
    // maximum AND value
    for (int i = 0; i < n; i++) {
        if (arr[i] != max_value) {
            c = max(c, (complement & arr[i]));
        }
    }

    // c will give the maximum value
    // that could be added to max_value
    // to produce maximum OR value
    return (max_value + c);
}

// Driver code
int main()
{
    int arr[] = { 3, 6, 8, 16 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxOR(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// of the approach
import java.util.*;
class GFG{

// Function to return the maximum
// bitwise OR for any pair of the
// given array without using bitwise
// OR operation
static int maxOR(int arr[], int n)
{

    // find maximum element in the array
    int max_value =
        Arrays.stream(arr).max().getAsInt();

    int number_of_bits =
        (int)((Math.log(max_value))) + 2;

    // finding complement will set
    // all unset bits in a number
    int complement = ((1 << number_of_bits) - 1) ^
                       max_value;

    int c = 0;

    // iterate through all other
    // array elements to find
    // maximum AND value
    for (int i = 0; i < n; i++)
    {
        if (arr[i] != max_value)
        {
            c = Math.max(c,
                         (complement & arr[i]));
        }
    }

    // c will give the maximum value
    // that could be added to max_value
    // to produce maximum OR value
    return (max_value + c);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {3, 6, 8, 16};
    int n = arr.length;
    System.out.print(maxOR(arr, n));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import log2, floor

# Function to return the maximum bitwise OR
# for any pair of the given array
# without using bitwise OR operation
def maxOR(arr, n):

    # Find maximum element in the array
    max_value = max(arr)

    number_of_bits = floor(log2(max_value)) + 1

    # Finding complement will set
    # all unset bits in a number
    complement = (((1 << number_of_bits) - 1) ^
                 max_value)
    c = 0

    # Iterate through all other
    # array elements to find
    # maximum AND value
    for i in range(n):

        if (arr[i] != max_value):
            c = max(c, (complement & arr[i]))

    # c will give the maximum value
    # that could be added to max_value
    # to produce maximum OR value
    return (max_value + c)

# Driver code
if __name__ == '__main__':

    arr = [3, 6, 8, 16]
    n = len(arr)

    print(maxOR(arr, n))

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# program for the above approach
using System;
using System.Linq;

class GFG{

// Function to return the maximum
// bitwise OR for any pair of the
// given array without using bitwise
// OR operation
static int maxOR(int[] arr, int n)
{

    // Find maximum element in the array
    int max_value = arr.Max();

    int number_of_bits = (int)(Math.Log(max_value)) + 2;

    // Finding complement will set
    // all unset bits in a number
    int complement = ((1 << number_of_bits) - 1) ^
                      max_value;

    int c = 0;

    // Iterate through all other
    // array elements to find
    // maximum AND value
    for(int i = 0; i < n; i++)
    {
        if (arr[i] != max_value)
        {
            c = Math.Max(c,
                        (complement & arr[i]));
        }
    }

    // c will give the maximum value
    // that could be added to max_value
    // to produce maximum OR value
    return (max_value + c);
}

// Driver code
public static void Main()
{
    int[] arr = { 3, 6, 8, 16 };
    int n = arr.Length;

    Console.Write(maxOR(arr, n));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>
// javascript implementation
// of the approach

    // Function to return the maximum
    // bitwise OR for any pair of the
    // given array without using bitwise
    // OR operation
    function maxOR(arr , n) {

        // find maximum element in the array
        var max_value = Math.max.apply(Math,arr);

        var number_of_bits = parseInt( ((Math.log(max_value)))) + 2;

        // finding complement will set
        // all unset bits in a number
        var complement = ((1 << number_of_bits) - 1) ^ max_value;

        var c = 0;

        // iterate through all other
        // array elements to find
        // maximum AND value
        for (i = 0; i < n; i++) {
            if (arr[i] != max_value) {
                c = Math.max(c, (complement & arr[i]));
            }
        }

        // c will give the maximum value
        // that could be added to max_value
        // to produce maximum OR value
        return (max_value + c);
    }

    // Driver code

        var arr = [ 3, 6, 8, 16 ];
        var n = arr.length;
        document.write(maxOR(arr, n));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
24
```

***时间复杂度:** O(N)*

***辅助空间:** O(1)*