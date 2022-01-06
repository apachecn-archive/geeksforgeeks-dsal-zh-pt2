# 计数成对的指数乘积等于这些指数上元素的乘积

> 原文:[https://www . geesforgeks . org/count-pairs-with-product-of-index-等于-product-of-elements-present-at-the-index/](https://www.geeksforgeeks.org/count-pairs-with-product-of-indices-equal-to-the-product-of-elements-present-at-those-indices/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是计算不同数组元素对的数量，这些数组元素的指数乘积等于该指数处元素的[乘积。对 **(x，y)** 和 **(y，x)** 视为同一对。](https://www.geeksforgeeks.org/product-2-numbers-using-recursion/)

**示例:**

> ***输入:** arr[] = {1，0，3，2，6}*
> ***输出:** 3*
> ***解释:**满足给定标准的所有可能对为:*
> 
> *   ***(0，1):** 指数的乘积= 1 * 0 = 0。元素的乘积= 1 * 0 = 0。*
> *   ***(2，3):** 指数的乘积= 2 * 3 = 6。元素的乘积= 3 * 2 = 6。*
> *   ***(3，4):** 指数的乘积= 3 * 4 = 12。元素的乘积= 2 * 6 = 12。*
> 
> *因此，对的总数为 3。*
> 
> ***输入:** arr[] = {4，-1，2，6，2，10}*
> ***输出:** 2*

**方法:**给定的问题可以通过[从给定的数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)生成所有可能的不同元素对 **(arr[i]，arr[j])** 来解决，如果 **i** 和 **j** 的乘积等于数组元素 **arr[i]** 和 **arr[j]** 的乘积，则增加这些对的计数。检查所有不同对后，打印总计**计数**作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to count the number of pairs
// having product of indices equal to the
// product of elements at that indices
int CountPairs(int arr[], int n)
{
    // Stores the count of valid pairs
    int count = 0;

    // Generate all possible pairs
    for (int i = 0; i < n - 1; i++) {

        for (int j = i + 1; j < n; j++) {

            // If the condition is satisfied
            if ((i * j) == (arr[i] * arr[j]))

                // Increment the count
                count++;
        }
    }

    // Return the total count
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 1, 0, 3, 2, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << CountPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count the number of pairs
// having product of indices equal to the
// product of elements at that indices
static int CountPairs(int[] arr, int n)
{

    // Stores the count of valid pairs
    int count = 0;

    // Generate all possible pairs
    for(int i = 0; i < n - 1; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // If the condition is satisfied
            if ((i * j) == (arr[i] * arr[j]))

                // Increment the count
                count++;
        }
    }

    // Return the total count
    return count;
}

// Driver Code
public static void main (String[] args)
{
    int[] arr = { 1, 0, 3, 2, 6 };
    int N = arr.length;

    System.out.println(CountPairs(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of pairs
# having product of indices equal to the
# product of elements at that indices
def CountPairs(arr, n):

    # Stores the count of valid pairs
    count = 0

    # Generate all possible pairs
    for i in range(n - 1):
        for j in range(i + 1, n):

            # If the condition is satisfied
            if ((i * j) == (arr[i] * arr[j])):

                # Increment the count
                count += 1

    # Return the total count
    return count

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 0, 3, 2, 6 ]
    N = len(arr)

    print(CountPairs(arr, N))

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the number of pairs
// having product of indices equal to the
// product of elements at that indices
static int CountPairs(int[] arr, int n)
{

    // Stores the count of valid pairs
    int count = 0;

    // Generate all possible pairs
    for(int i = 0; i < n - 1; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // If the condition is satisfied
            if ((i * j) == (arr[i] * arr[j]))

                // Increment the count
                count++;
        }
    }

    // Return the total count
    return count;
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 0, 3, 2, 6 };
    int N = arr.Length;

    Console.Write(CountPairs(arr, N));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to count the number of pairs
    // having product of indices equal to the
    // product of elements at that indices
    function CountPairs(arr , n) {

        // Stores the count of valid pairs
        var count = 0;

        // Generate all possible pairs
        for (i = 0; i < n - 1; i++) {
            for (j = i + 1; j < n; j++) {

                // If the condition is satisfied
                if ((i * j) == (arr[i] * arr[j]))

                    // Increment the count
                    count++;
            }
        }

        // Return the total count
        return count;
    }

    // Driver Code

        var arr = [ 1, 0, 3, 2, 6 ];
        var N = arr.length;

        document.write(CountPairs(arr, N));
// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*