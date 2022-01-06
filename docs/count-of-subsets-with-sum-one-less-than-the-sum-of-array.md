# 总和小于数组总和的子集计数

> 原文:[https://www . geeksforgeeks . org/小于数组和的子集计数/](https://www.geeksforgeeks.org/count-of-subsets-with-sum-one-less-than-the-sum-of-array/)

给定一个 **N** 大小的[阵](https://www.geeksforgeeks.org/introduction-to-arrays/)T2【arr】。任务是当数组中出现 0 时，找出**子集**的个数，其和为(****数组的**和–1**)如果没有可能的子集，则返回-1。****

****示例:****

> ****输入** : arr[ ] : {3，0，5，2，4}
> **输出** : -1
> **解释**:数组 arr[ ]的和为 14，没有和为 13 的子集。
> **输入** : arr[ ] : {0，0，2，1}
> **输出** : 4
> **说明**:数组 arr[ ]的和为 3，{0，2}、{0，2}、{0，0，2}、{2}为和为 2 的四个子集。**

****天真方法:**可以通过使用[递归](http://www.geeksforgeeks.org/recursion/)生成数组的所有可能的[子集](https://www.geeksforgeeks.org/count-of-subsets-with-sum-equal-to-x/)来解决该任务，如果遇到 sum 为(数组的 sum–1)的子集，则增加计数。
以下是上述方法的实现:**

## **C++**

```
// C++ program to print the count of
// subsets with sum equal to the given value X

#include <bits/stdc++.h>
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

    // Recursively calling the
    // function for two cases
    // Either the element can be
    // counted in the subset
    // If the element is counted,
    // then the remaining sum
    // to be checked is
    // sum - the selected element
    // If the element is not included,
    // then the remaining sum
    // to be checked is the total sum
    count = subsetSum(arr, n, i + 1,
                      sum - arr[i], count);
    count = subsetSum(arr, n, i + 1,
                      sum, count);
    return count == 0 ? -1 : count;
}

// Driver code
int main()
{
    int arr[] = { 0, 0, 2, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Sum of array - 1
    int sum = accumulate(arr, arr + n, 0) - 1;
    cout << subsetSum(arr, n, 0, sum, 0);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to print the count of
// subsets with sum equal to the given value X

public class GFG {

    // Recursive function to return the count
    // of subsets with sum equal to the given value
    static int subsetSum(int arr[], int n, int i,
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

        // Recursively calling the
        // function for two cases
        // Either the element can be
        // counted in the subset
        // If the element is counted,
        // then the remaining sum
        // to be checked is
        // sum - the selected element
        // If the element is not included,
        // then the remaining sum
        // to be checked is the total sum
        count = subsetSum(arr, n, i + 1,
                          sum - arr[i], count);
        count = subsetSum(arr, n, i + 1,
                          sum, count);
        return count == 0 ? -1 : count;
    }

    static int accumulate(int []arr)
    {
        int sum = 0;
        for(int i = 0; i < arr.length; i++)
            sum += arr[i];

        return sum;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 0, 0, 2, 1 };
        int n = arr.length;

        // Sum of array - 1
        int sum = accumulate(arr) - 1;

        System.out.println(subsetSum(arr, n, 0, sum, 0));
    }
}

// This code is contributed by AnkThon
```

## **蟒蛇 3**

```
# Python program to print the count of
# subsets with sum equal to the given value X

# Recursive function to return the count
# of subsets with sum equal to the given value
def subsetSum(arr, n, i, sum, count):

    # The recursion is stopped at N-th level
    # where all the subsets of the given array
    # have been checked
    if (i == n):

        # Incrementing the count if sum is
        # equal to 0 and returning the count
        if (sum == 0):
            count += 1
        return count

    # Recursively calling the
    # function for two cases
    # Either the element can be
    # counted in the subset
    # If the element is counted,
    # then the remaining sum
    # to be checked is
    # sum - the selected element
    # If the element is not included,
    # then the remaining sum
    # to be checked is the total sum
    count = subsetSum(arr, n, i + 1,
                      sum - arr[i], count)
    count = subsetSum(arr, n, i + 1,
                      sum, count)
    return - 1 if count == 0 else count

def accumulate(arr):
    sum = 0
    for i in range(len(arr)):
        sum += arr[i]
    return sum

# Driver code
arr = [0, 0, 2, 1]
n = len(arr)

# Sum of array - 1
sum = accumulate(arr) - 1
print(subsetSum(arr, n, 0, sum, 0))

# This code is contributed by gfgking
```

## **C#**

```
// C# program to print the count of
// subsets with sum equal to the given value X

using System;

public class GFG {

    // Recursive function to return the count
    // of subsets with sum equal to the given value
    static int subsetSum(int []arr, int n, int i,
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

        // Recursively calling the
        // function for two cases
        // Either the element can be
        // counted in the subset
        // If the element is counted,
        // then the remaining sum
        // to be checked is
        // sum - the selected element
        // If the element is not included,
        // then the remaining sum
        // to be checked is the total sum
        count = subsetSum(arr, n, i + 1,
                        sum - arr[i], count);
        count = subsetSum(arr, n, i + 1,
                        sum, count);
        return count == 0 ? -1 : count;
    }

    static int accumulate(int []arr)
    {
        int sum = 0;
        for(int i = 0; i < arr.Length; i++)
            sum += arr[i];

        return sum;
    }

    // Driver code
    public static void Main (string[] args)
    {
        int []arr = { 0, 0, 2, 1 };
        int n = arr.Length;

        // Sum of array - 1
        int sum = accumulate(arr) - 1;

        Console.WriteLine(subsetSum(arr, n, 0, sum, 0));
    }
}

// This code is contributed by AnkThon
```

## **java 描述语言**

```
<script>
        // JavaScript program to print the count of
        // subsets with sum equal to the given value X

        // Recursive function to return the count
        // of subsets with sum equal to the given value
        function subsetSum(arr, n, i,
            sum, count)
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

            // Recursively calling the
            // function for two cases
            // Either the element can be
            // counted in the subset
            // If the element is counted,
            // then the remaining sum
            // to be checked is
            // sum - the selected element
            // If the element is not included,
            // then the remaining sum
            // to be checked is the total sum
            count = subsetSum(arr, n, i + 1,
                sum - arr[i], count);
            count = subsetSum(arr, n, i + 1,
                sum, count);
            return count == 0 ? -1 : count;
        }

        function accumulate(arr) {
            let sum = 0;
            for (let i = 0; i < arr.length; i++) {
                sum += arr[i];
            }
            return sum;
        }

        // Driver code

        let arr = [0, 0, 2, 1];
        let n = arr.length;

        // Sum of array - 1
        let sum = accumulate(arr) - 1;
        document.write(subsetSum(arr, n, 0, sum, 0));

    // This code is contributed by Potta Lokesh
    </script>
```

****Output:** 

```
4
```** 

*****时间复杂度*** **:** O(2 <sup>n</sup> ，其中 n =数组长度
***辅助空间*** : O(n)，递归堆栈空间
**高效方法:**通过移除 **0s** 和**找到一个可能的和为**(array _ sum–1)**的子集，可以优化上述方法****

*   **如果数组中有 **k** 个零，那么就有 **2^k** (k 是零的个数)种方法可以将 **0** 从数组中移除。**
*   **这两个**的乘积**(去除 **0** 的方法数和去除 **1** 的方法数)导致可能的子集数。**

**下面是上面代码的实现:**

## **C++**

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the no of
// possible subsets
int subsetCount(int arr[], int n)
{
    // Count the no of 0s and 1s
    // in array
    int zeros = 0, ones = 0;

    for (int i = 0; i < n; i++) {
        if (arr[i] == 0) {
            zeros++;
        }
        else if (arr[i] == 1) {
            ones++;
        }
    }

    // Store no of ways to remove 0
    int no_of_ways_0 = pow(2, zeros);

    // Store no of ways to remove 1
    int no_of_ways_1 = ones;

    // Store the total count of subsets
    int count_subset = no_of_ways_0
                       * no_of_ways_1;

    // If there is no subset possible
    // with required sum, return -1
    if (count_subset == 0)
        return -1;
    return count_subset;
}

// Driver Code
int main()
{

    int arr[] = { 0, 0, 2, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << subsetCount(arr, n);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the above approach
import java.util.*;
public class GFG
{
// Function to find the no of
// possible subsets
static int subsetCount(int []arr, int n)
{
    // Count the no of 0s and 1s
    // in array
    int zeros = 0, ones = 0;

    for (int i = 0; i < n; i++) {
        if (arr[i] == 0) {
            zeros++;
        }
        else if (arr[i] == 1) {
            ones++;
        }
    }

    // Store no of ways to remove 0
    int no_of_ways_0 = (int)Math.pow(2, zeros);

    // Store no of ways to remove 1
    int no_of_ways_1 = ones;

    // Store the total count of subsets
    int count_subset = no_of_ways_0
                       * no_of_ways_1;

    // If there is no subset possible
    // with required sum, return -1
    if (count_subset == 0)
        return -1;
    return count_subset;
}

// Driver Code
public static void main(String args[])
{

    int []arr = { 0, 0, 2, 1 };
    int n = arr.length;
    System.out.println(subsetCount(arr, n));
}
}
// This code is contributed by Samim Hossain Mondal.
```

## **蟒蛇 3**

```
# Python 3 implementation of the above approach

# Function to find the no of
# possible subsets

def subsetCount(arr, n):

    # Count the no of 0s and 1s
    # in array
    zeros = 0
    ones = 0

    for i in range(n):
        if (arr[i] == 0):
            zeros += 1

        elif (arr[i] == 1):
            ones += 1

    # Store no of ways to remove 0
    no_of_ways_0 = pow(2, zeros)

    # Store no of ways to remove 1
    no_of_ways_1 = ones

    # Store the total count of subsets
    count_subset = no_of_ways_0 * no_of_ways_1

    # If there is no subset possible
    # with required sum, return -1
    if (count_subset == 0):
        return -1
    return count_subset

# Driver Code
if __name__ == "__main__":

    arr = [0, 0, 2, 1]
    n = len(arr)
    print(subsetCount(arr, n))

    # This code is contributed by ukasp.
```

## **C#**

```
// C# implementation of the above approach
using System;

class GFG
{
// Function to find the no of
// possible subsets
static int subsetCount(int []arr, int n)
{
    // Count the no of 0s and 1s
    // in array
    int zeros = 0, ones = 0;

    for (int i = 0; i < n; i++) {
        if (arr[i] == 0) {
            zeros++;
        }
        else if (arr[i] == 1) {
            ones++;
        }
    }

    // Store no of ways to remove 0
    int no_of_ways_0 = (int)Math.Pow(2, zeros);

    // Store no of ways to remove 1
    int no_of_ways_1 = ones;

    // Store the total count of subsets
    int count_subset = no_of_ways_0
                    * no_of_ways_1;

    // If there is no subset possible
    // with required sum, return -1
    if (count_subset == 0)
        return -1;
    return count_subset;
}

// Driver Code
public static void Main()
{

    int []arr = { 0, 0, 2, 1 };
    int n = arr.Length;
    Console.Write(subsetCount(arr, n));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## **java 描述语言**

```
<script>
// Javascript implementation of the above approach

// Function to find the no of
// possible subsets
function subsetCount(arr, n)
{
    // Count the no of 0s and 1s
    // in array
    let zeros = 0, ones = 0;

    for (let i = 0; i < n; i++) {
        if (arr[i] == 0) {
            zeros++;
        }
        else if (arr[i] == 1) {
            ones++;
        }
    }

    // Store no of ways to remove 0
    let no_of_ways_0 = Math.pow(2, zeros);

    // Store no of ways to remove 1
    let no_of_ways_1 = ones;

    // Store the total count of subsets
    let count_subset = no_of_ways_0
                       * no_of_ways_1;

    // If there is no subset possible
    // with required sum, return -1
    if (count_subset == 0)
        return -1;
    return count_subset;
}

// Driver Code
let arr = [ 0, 0, 2, 1 ];
let n = arr.length;
document.write(subsetCount(arr, n));

// This code is contributed by Samim Hossain Mondal.
</script>
```

****Output**

```
4
```** 

*****时间复杂度*** **:** O(n)，其中 n =阵长
***辅助空间*** : O(1)**