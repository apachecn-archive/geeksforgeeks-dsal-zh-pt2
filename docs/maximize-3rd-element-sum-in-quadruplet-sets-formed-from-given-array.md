# 最大化由给定数组形成的四元组中的第三元素和

> 原文:[https://www . geeksforgeeks . org/maximum-第三元素-四个小集合中的和-从给定数组形成/](https://www.geeksforgeeks.org/maximize-3rd-element-sum-in-quadruplet-sets-formed-from-given-array/)

给定一个数组 **arr** 包含描述 N 个作业优先级的 **N** 值。任务是形成每天要做的四胞胎组(W，X，Y，Z)，使得 W > = X > = Y > = Z，并且在这样做时，最大化所有四胞胎组的所有 Y 的总和。
**注** : N 永远是 4 的倍数。
**示例:**

> **输入:** Arr[] = {2，1，7，5，5，4，1，1，3，3，2，2}
> **输出:** 10
> **解释:**
> 我们可以组成 3 个四胞胎集合为【7，5，5，1】、【4，3，3，1】、【2，2，2，1】。
> 所有 Y 的总和为 5 + 3 + 2 = 10，这是最大可能值。
> **输入:** arr[] = {1，51，91，1，1，16，1，51，48，16，1，49}
> **输出:** 68

**方法:**为了解决上述问题，我们可以观察到:

1.  不考虑 Y，(W，X) >= Y，即 W 和 X 的较高值总是丢失，对答案没有贡献。因此，我们必须保持这些值尽可能低，但大于或等于 y。
2.  同样，Z 的值总是丢失，并且必须小于 y。因此，它必须尽可能低。

因此，为了满足上述条件，我们必须:

*   首先[给定数组按降序排序](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   初始化一个[指针](https://www.geeksforgeeks.org/pointers-in-c-and-c-set-1-introduction-arithmetic-and-array/)，该指针从索引 0 指向每对的第三个元素。
*   从数组的大小中减去这种对的计数，即 n

**以下是上述方法的实施:**

## C++

```
// C++ code to Maximize 3rd element
// sum in quadruplet sets formed
// from given Array

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// possible value of Y
int formQuadruplets(int arr[], int n)
{

    int ans = 0, pairs = 0;

    // pairs contain count
    // of minimum elements
    // that will be utilized
    // at place of Z.
    // it is equal to count of
    // possible pairs that
    // is size of array divided by 4
    pairs = n / 4;

    // sorting the array in descending order
    // so as to bring values with minimal
    // difference closer to arr[i]
    sort(arr, arr + n, greater<int>());

    for (int i = 0; i < n - pairs; i += 3) {

        // here, i+2 acts as a
        // pointer that points
        // to the third value of
        // every possible quadruplet
        ans += arr[i + 2];
    }

    // returning the optimally
    // maximum possible value
    return ans;
}

// Driver code
int main()
{
    // array declaration
    int arr[] = { 2, 1, 7, 5, 5,
                  4, 1, 1, 3, 3,
                  2, 2 };

    // size of array
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << formQuadruplets(arr, n)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to Maximize 3rd element
// sum in quadruplet sets formed
// from given Array
import java.util.*;
class GFG{

// Function to find the maximum
// possible value of Y
static int formQuadruplets(Integer arr[], int n)
{
    int ans = 0, pairs = 0;

    // pairs contain count
    // of minimum elements
    // that will be utilized
    // at place of Z.
    // it is equal to count of
    // possible pairs that
    // is size of array divided by 4
    pairs = n / 4;

    // sorting the array in descending order
    // so as to bring values with minimal
    // difference closer to arr[i]
    Arrays.sort(arr, Collections.reverseOrder());

    for (int i = 0; i < n - pairs; i += 3)
    {

        // here, i+2 acts as a
        // pointer that points
        // to the third value of
        // every possible quadruplet
        ans += arr[i + 2];
    }

    // returning the optimally
    // maximum possible value
    return ans;
}

// Driver code
public static void main(String[] args)
{
    // array declaration
    Integer arr[] = { 2, 1, 7, 5, 5, 4,
                      1, 1, 3, 3, 2, 2 };

    // size of array
    int n = arr.length;

    System.out.print(
           formQuadruplets(arr, n) + "\n");

}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 code to maximize 3rd element
# sum in quadruplet sets formed
# from given Array

# Function to find the maximum
# possible value of Y
def formQuadruplets(arr, n):

    ans = 0
    pairs = 0

    # Pairs contain count of minimum
    # elements that will be utilized
    # at place of Z. It is equal to 
    # count of possible pairs that
    # is size of array divided by 4
    pairs = n // 4

    # Sorting the array in descending order
    # so as to bring values with minimal
    # difference closer to arr[i]
    arr.sort(reverse = True)

    for i in range(0, n - pairs, 3):

        # Here, i+2 acts as a pointer that 
        # points to the third value of
        # every possible quadruplet
        ans += arr[i + 2]

    # Returning the optimally
    # maximum possible value
    return ans

# Driver code

# Array declaration
arr = [ 2, 1, 7, 5, 5, 4, 1, 1, 3, 3, 2, 2 ]

# Size of array
n = len(arr)

print(formQuadruplets(arr, n))

# This code is contributed by divyamohan123
```

## C#

```
// C# code to maximize 3rd element
// sum in quadruplet sets formed
// from given Array
using System;

class GFG{

// Function to find the maximum
// possible value of Y
static int formQuadruplets(int []arr, int n)
{
    int ans = 0, pairs = 0;

    // Pairs contain count of minimum 
    // elements that will be utilized at
    // place of Z. It is equal to count of
    // possible pairs that is size of
    // array divided by 4
    pairs = n / 4;

    // Sorting the array in descending order
    // so as to bring values with minimal
    // difference closer to arr[i]
    Array.Sort(arr);
    Array.Reverse(arr);
    for(int i = 0; i < n - pairs; i += 3)
    {

       // Here, i+2 acts as a
       // pointer that points
       // to the third value of
       // every possible quadruplet
       ans += arr[i + 2];
    }

    // Returning the optimally
    // maximum possible value
    return ans;
}

// Driver code
public static void Main(String[] args)
{

    // Array declaration
    int []arr = { 2, 1, 7, 5, 5, 4,
                  1, 1, 3, 3, 2, 2 };

    // Size of array
    int n = arr.Length;

    Console.Write(formQuadruplets(arr, n) + "\n");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

      // JavaScript code to maximize 3rd element
      // sum in quadruplet sets formed
      // from given Array

      // Function to find the maximum
      // possible value of Y
      function formQuadruplets(arr, n) {
        var ans = 0,
          pairs = 0;

        // Pairs contain count of minimum
        // elements that will be utilized at
        // place of Z. It is equal to count of
        // possible pairs that is size of
        // array divided by 4
        pairs = parseInt(n / 4);

        // Sorting the array in descending order
        // so as to bring values with minimal
        // difference closer to arr[i]
        arr.sort().reverse();
        for (var i = 0; i < n - pairs; i += 3) {
          // Here, i+2 acts as a
          // pointer that points
          // to the third value of
          // every possible quadruplet
          ans += arr[i + 2];
        }

        // Returning the optimally
        // maximum possible value
        return ans;
      }

      // Driver code
      // Array declaration
      var arr = [2, 1, 7, 5, 5, 4, 1, 1, 3, 3, 2, 2];

      // Size of array
      var n = arr.length;

      document.write(formQuadruplets(arr, n) + "<br>");

</script>
```

**Output:** 

```
10
```