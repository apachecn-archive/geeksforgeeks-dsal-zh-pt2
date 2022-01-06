# 使用递归计算和等于 X 的子集的数量

> 原文:[https://www . geesforgeks . org/sum 等于 x 的子集计数使用递归/](https://www.geeksforgeeks.org/count-of-subsets-with-sum-equal-to-x-using-recursion/)

给定一个长度为 **N** 的数组**arr【】**和一个整数 **X** ，任务是使用[递归](https://www.geeksforgeeks.org/recursion/)找到和等于 **X** 的子集数量。
**举例:**

> **输入:** arr[] = {2，3，5，6，8，10}，X = 10
> **输出:** 3
> **解释:**
> 总和为 10 的所有可能子集为{2，3，5}、{2，8}、{10}
> **输入:** arr[] = {1，2，3，4，5}，X = 7
> **输出:** 3

**方法:**思路是递归检查所有子集。如果任何子集的和等于 N，则计数增加 1。否则，继续。
为了形成子集，每个元素有两种情况:

*   将元素包含在集合中。
*   排除集合中的元素。

因此，可以按照以下步骤计算答案:

1.  获取要为其找到和等于 K 的子集的数组。
2.  以下列方式递归计算总和等于 K 的子集:
    *   **基本情况:**基本情况是到达数组末尾时。如果这里的和被发现为 X，那么子集的计数增加 1。返回在基本条件下计算的计数。

```
if (n == 0) {
    if (sum == s)
        count++;
    return count;
}
```

*   **递归调用:**如果不满足基本情况，那么调用函数两次。一次是在索引“I”处包含元素，一次是不包含元素。找到这两种情况的计数，然后返回最终计数。

```
count = subsetSum(arr, n, sum , s , count);
count = subsetSum(arr, n, sum, s + arr[n-1 count);
```

*   **返回语句:**在每一步，返回包含特定元素或不包含特定元素的子集计数。最后，当执行整个递归堆栈时，返回总计数。

从上面的方法可以清楚地分析出，如果数组中有 N 个元素，那么总共会出现**2<sup>N</sup>T3】的情况。使用[递归](https://www.geeksforgeeks.org/recursion/)检查数组中的每个元素是否存在上述情况。
以下是上述方法的实现:** 

## C++

```
// C++ program to print the count of
// subsets with sum equal to the given value X

#include <iostream>
using namespace std;

// Recursive function to return the count
// of subsets with sum equal to the given value
int subsetSum(int arr[], int n, int i,
              int sum, int count)
{
    // The recursion is stopped at N-th level
    // where all the subsets of the given array
    // have been checked
    if (i == n) {

        // Incrementing the count if sum is
        // equal to 0 and returning the count
        if (sum == 0) {
            count++;
        }
        return count;
    }

    // Recursively calling the function for two cases
    // Either the element can be counted in the subset
    // If the element is counted, then the remaining sum
    // to be checked is sum - the selected element
    // If the element is not included, then the remaining sum
    // to be checked is the total sum
    count = subsetSum(arr, n, i + 1, sum - arr[i], count);
    count = subsetSum(arr, n, i + 1, sum, count);
    return count;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int sum = 10;
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << subsetSum(arr, n, 0, sum, 0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the count of
// subsets with sum equal to the given value X
import java.util.*;

class GFG {

    // Recursive function to return the count
    // of subsets with sum equal to the given value
    static int subsetSum(int arr[], int n, int sum, int s,
                         int count)
    {

        // The recursion is stopped at N-th level
        // where all the subsets of the given array
        // have been checked
        if (n == 0) {

            // Incrementing the count if sum is
            // equal to the subset and returning the count
            if (sum == s) {
                count++;
            }
            return count;
        }

        count = subsetSum(arr, n - 1, sum, s, count);
        count = subsetSum(arr, n - 1, sum, s + arr[n - 1],
                          count);
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5 };
        int sum = 10;
        int s = 0; // Initially assigning the sum of subset
                   // to be zero
        int n = arr.length;

        System.out.print(subsetSum(arr, n, sum, s, 0));
    }
}

// This code is contributed by Sparsh Choudhary
// (sparsht123t)
```

## 蟒蛇 3

```
# Python3 program to print the count of
# subsets with sum equal to the given value X

# Recursive function to return the count
# of subsets with sum equal to the given value
def subsetSum(arr, n, i,sum, count):

    # The recursion is stopped at N-th level
    # where all the subsets of the given array
    # have been checked
    if (i == n):

        # Incrementing the count if sum is
        # equal to 0 and returning the count
        if (sum == 0):
            count += 1
        return count

    # Recursively calling the function for two cases
    # Either the element can be counted in the subset
    # If the element is counted, then the remaining sum
    # to be checked is sum - the selected element
    # If the element is not included, then the remaining sum
    # to be checked is the total sum
    count = subsetSum(arr, n, i + 1, sum - arr[i], count)
    count = subsetSum(arr, n, i + 1, sum, count)
    return count

# Driver code
arr = [1, 2, 3, 4, 5]
sum = 10
n = len(arr)

print(subsetSum(arr, n, 0, sum, 0))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to print the count of
// subsets with sum equal to the given value X
using System;

class GFG
{

// Recursive function to return the count
// of subsets with sum equal to the given value
static int subsetSum(int []arr, int n, int i,
                    int sum, int count)
{
    // The recursion is stopped at N-th level
    // where all the subsets of the given array
    // have been checked
    if (i == n)
    {

        // Incrementing the count if sum is
        // equal to 0 and returning the count
        if (sum == 0)
        {
            count++;
        }
        return count;
    }

    // Recursively calling the function for two cases
    // Either the element can be counted in the subset
    // If the element is counted, then the remaining sum
    // to be checked is sum - the selected element
    // If the element is not included, then the remaining sum
    // to be checked is the total sum
    count = subsetSum(arr, n, i + 1, sum - arr[i], count);
    count = subsetSum(arr, n, i + 1, sum, count);
    return count;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5 };
    int sum = 10;
    int n = arr.Length;

    Console.Write(subsetSum(arr, n, 0, sum, 0));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to print the count of
// subsets with sum equal to the given value X

// Recursive function to return the count
// of subsets with sum equal to the given value
function subsetSum(arr, n, i, sum, count)
{
    // The recursion is stopped at N-th level
    // where all the subsets of the given array
    // have been checked
    if (i == n) {

        // Incrementing the count if sum is
        // equal to 0 and returning the count
        if (sum == 0) {
            count++;
        }
        return count;
    }

    // Recursively calling the function for two cases
    // Either the element can be counted in the subset
    // If the element is counted, then the remaining sum
    // to be checked is sum - the selected element
    // If the element is not included, then the remaining sum
    // to be checked is the total sum
    count = subsetSum(arr, n, i + 1, sum - arr[i], count);
    count = subsetSum(arr, n, i + 1, sum, count);
    return count;
}

// Driver code
var arr = [1, 2, 3, 4, 5];
var sum = 10;
var n = arr.length;
document.write( subsetSum(arr, n, 0, sum, 0));

</script>
```

**Output:** 

```
3
```

时间复杂度:O(n <sup>2</sup> )

辅助空间:O(n <sup>2</sup> )

**有效方法:**
在本文中已经讨论了使用动态规划解决问题的有效方法。