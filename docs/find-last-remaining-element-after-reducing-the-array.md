# 缩小数组后找到最后一个剩余元素

> 原文:[https://www . geesforgeks . org/find-数组约简后的最后剩余元素/](https://www.geeksforgeeks.org/find-last-remaining-element-after-reducing-the-array/)

给定一个大小为 **N** 的数组 **arr[]** 和一个整数 **K** 。任务是在缩小数组后找到数组中最后剩余的元素。减少数组的规则是:

*   第一个和最后一个元素，比如 X 和 Y，被选择并从数组 arr[]中移除。
*   值 X 和 Y 相加。Z = X + Y。
*   将 **Z % K** 的值插入数组 arr【】中的 **((N/2) + 1) <sup>第</sup>** 个位置，其中 N 表示数组的当前长度。

示例:

> **输入:** N = 5，arr[] = {1，2，3，4，5}，K = 7
> **输出:** 1
> **解释:**
> 给定数组 arr[]，减少如下:
> {1，2，3，4，5} - > {2，6，3，4}
> {2，6，3，4} - > {6，6，3}
> {6，6，6
> **输入:** N = 5，arr[] = {2，4，7，11，3}，K = 12
> **输出:** 3
> **解释:**
> 给定数组 arr[]，减少如下:
> {2，4，7，11，3} - > {4，5，7，11}
> {4，5，7，11 }->{ 0 }

**天真法:**这个问题的天真法是在每一步找到数组中的第一个元素和最后一个元素，计算 **(X + Y) % K** ，其中 X 是每一步数组的第一个元素，Y 是最后一个元素。计算该值后，在给定位置插入该值。
**时间复杂度:** O(N <sup>2</sup> )
**高效方法:**

*   仔细观察，可以说数组中以 K 为模的元素之和在数组中始终没有变化。
*   这是因为我们基本上是将值 **X + Y % K** 插回数组中。
*   所以这个问题可以通过直接求数组的和，求值**和% K** 在线性时间内解决。

以下是上述方法的实现:

## C++

```
// C++ program to find the value of the
// reduced Array by reducing the array
// based on the given conditions

#include <iostream>
using namespace std;

// Function to find the value of the
// reduced Array by reducing the array
// based on the given conditions
int find_value(int a[], int n, int k)
{
    // Variable to store the sum
    int sum = 0;

    // For loop to iterate through the
    // given array and find the sum
    for (int i = 0; i < n; i++) {
        sum += a[i];
    }

    // Return the required value
    return sum % k;
}

// Driver code
int main()
{
    int n = 5, k = 3;
    int a[] = { 12, 4, 13, 0, 5 };
    cout << find_value(a, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the value of the
// reduced Array by reducing the array
// based on the given conditions

public class GFG {

    // Function to find the value of the
    // reduced Array by reducing the array
    // based on the given conditions
    public static int find_value(int a[], int n, int k)
    {
        // Variable to store the sum
        int sum = 0;

        // For loop to iterate through the
        // given array and find the sum
        for (int i = 0; i < n; i++) {
            sum += a[i];
        }

        // Return the required value
        return sum % k;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 5, k = 3;
        int a[] = { 12, 4, 13, 0, 5 };
        System.out.println(find_value(a, n, k));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the value of the
# reduced Array by reducing the array
# based on the given conditions

# Function to find the value of the
# reduced Array by reducing the array
# based on the given conditions
def find_value(a, n, k):

    # Variable to store the sum
    sum = 0

    # For loop to iterate through the
    # given array and find the sum
    for i in range(n):
        sum += a[i]

    # Return the required value
    return sum % k

# Driver code
if __name__ == "__main__":
    n, k = 5, 3;
    a = [12, 4, 13, 0, 5];
    print(find_value(a, n, k))
```

## C#

```
// C# program to find the value of the
// reduced Array by reducing the array
// based on the given conditions
using System;

class GFG {

    // Function to find the value of the
    // reduced Array by reducing the array
    // based on the given conditions
    public static int find_value(int []a, int n, int k)
    {
        // Variable to store the sum
        int sum = 0;

        // For loop to iterate through the
        // given array and find the sum
        for (int i = 0; i < n; i++) {
            sum += a[i];
        }

        // Return the required value
        return sum % k;
    }

    // Driver code
    public static void Main(string[] args)
    {
        int n = 5, k = 3;
        int []a = { 12, 4, 13, 0, 5 };
        Console.WriteLine(find_value(a, n, k));
    }
}

// This code is contributed  by AnkitRai01
```

## java 描述语言

```
<script>

// Js program to find the value of the
// reduced Array by reducing the array
// based on the given conditions

// Function to find the value of the
// reduced Array by reducing the array
// based on the given conditions
function find_value( a, n, k)
{
    // Variable to store the sum
    let sum = 0;

    // For loop to iterate through the
    // given array and find the sum
    for (let i = 0; i < n; i++) {
        sum += a[i];
    }

    // Return the required value
    return sum % k;
}

// Driver code
let n = 5, k = 3;
    let a = [ 12, 4, 13, 0, 5 ];
document.write(find_value(a, n, k));

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(N)