# 数组子集均匀分布后大于 X 的最大元素个数

> 原文:[https://www . geeksforgeeks . org/最大元素数-大于-x-平均分布-数组子集/](https://www.geeksforgeeks.org/maximum-number-of-elements-greater-than-x-after-equally-distributing-subset-of-array/)

给定一个数组， **arr[]** 和一个整数 **X** ，任务是在等分元素子集后计算大于 X 的元素数量。也就是说，子集的每个元素都将等于![\frac{Sum of Subset}{Number of Elements}  ](img/2c792f331e4f128a0f44ab9f381368d3.png "Rendered by QuickLaTeX.com")

**示例:**

> **输入:** arr[] = {5，1，2，1}，X = 3
> **输出:** 2
> **说明:**
> 平均分布的子集为{5，2}。
> 之后元素各为 3.5。
> 数组= > {3.5，1，3.5，1}
> 大于 X 的元素总数= 2
> 
> **输入:** arr[] = {3，4，5}，X = 6
> **输出:** 0
> **解释:**
> 没有办法分配数组的任何子集使元素大于 6。

**方法:**思路是[对数组](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)进行排序，包含数组中最大的元素，使得它们的平均值大于或等于 X，平均值大于或等于 X 的这类元素的个数是可以等分的期望子集，每个元素都大于 X

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum number of elements greater
// than X by equally distributing

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// maximum number of elements greater
// than X by equally distributing
void redistribute(int arr[], int n, int x)
{
    // Sorting the array
    sort(arr, arr + n, greater<int>());

    int i, sum = 0;

    // Loop to iterate over the elements
    // of the array
    for (i = 0; i < n; i++) {
        sum += arr[i];

        // If no more elements can
        // become larger than x
        if (sum / (i + 1) < x) {
            cout << i << endl;
            break;
        }
    }
    if (i == n)
        cout << n << endl;
}

// Driver Code
int main()
{
    int arr[] = { 5, 1, 2, 1 };
    int x = 3;
    redistribute(arr, 4, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum number of elements greater
// than X by equally distributing
import java.util.*;

class GFG{

// Function to find the maximum
// number of elements greater
// than X by equally distributing
static void redistribute(Integer arr[], int n,
                                        int x)
{

    // Sorting the array
    Arrays.sort(arr, Collections.reverseOrder());

    int i, sum = 0;

    // Loop to iterate over the elements
    // of the array
    for(i = 0; i < n; i++)
    {
       sum += arr[i];

       // If no more elements can
       // become larger than x
       if (sum / (i + 1) < x)
       {
           System.out.print(i + "\n");
           break;
       }
    }
    if (i == n)
        System.out.print(n + "\n");
}

// Driver Code
public static void main(String[] args)
{
    Integer arr[] = { 5, 1, 2, 1 };
    int x = 3;

    redistribute(arr, 4, x);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum number of elements greater
# than X by equally distributing

# Function to find the
# maximum number of elements greater
# than X by equally distributing
def redistribute(arr, n, x):

    # Sorting the array
    arr.sort(reverse = True)

    sum = 0

    # Loop to iterate over the
    # elements of the array
    for i in range(n):
        sum += arr[i]

        # If no more elements can
        # become larger than x
        if (sum / (i + 1) < x):
            print(i)
            break

    if (i == n):
        print(n)

# Driver Code
arr = [ 5, 1, 2, 1 ]
x = 3

# Function call
redistribute(arr, 4, x)

# This code is contributed by Vishal Maurya.
```

## C#

```
// C# implementation to find the
// maximum number of elements greater
// than X by equally distributing
using System;

class GFG{

// Function to find the maximum
// number of elements greater
// than X by equally distributing
static void redistribute(int []arr, int n,
                                    int x)
{

    // Sorting the array
    Array.Sort(arr);
    Array.Reverse(arr);

    int i, sum = 0;

    // Loop to iterate over the elements
    // of the array
    for(i = 0; i < n; i++)
    {
       sum += arr[i];

       // If no more elements can
       // become larger than x
       if (sum / (i + 1) < x)
       {
           Console.Write(i + "\n");
           break;
       }
    }
    if (i == n)
        Console.Write(n + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 5, 1, 2, 1 };
    int x = 3;

    redistribute(arr, 4, x);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation to find the
// maximum number of elements greater
// than X by equally distributing

// Function to find the maximum
// number of elements greater
// than X by equally distributing
function redistribute(arr, n, x)
{

    // Sorting the array
    arr.sort();
    arr.reverse();

    let i, sum = 0;

    // Loop to iterate over the elements
    // of the array
    for(i = 0; i < n; i++)
    {
        sum += arr[i];

        // If no more elements can
        // become larger than x
        if ((sum / (i + 1)) < x)
        {
            document.write(i );
            break;
        }
    }
    if (i == n)
        document.write(n);
}

// Driver Code
let arr = [ 5, 1, 2, 1 ];
let x = 3;

redistribute(arr, 4, x);

// This code is contributed by sanjoy_62

</script>
```

**Output:** 

```
2
```