# 通过从给定的数组中选择边来最大化四边形的周长

> 原文:[https://www . geeksforgeeks . org/通过从给定数组中选择边来最大化四边形的周长/](https://www.geeksforgeeks.org/maximize-perimeter-of-quadrilateral-formed-by-choosing-sides-from-given-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **arr** ，其中每个元素代表一条边的长度，任务是找到使用给定数组中的边可以创建的最大周长四边形。如果不能形成四边形，打印-1。

**示例:**

> **输入:** arr[ ] = {3，1，2，4，2，1}
> **输出:** 11
> **说明:**可以形成周长为 4 + 3 + 2 + 2 = 11 的四边形，这是最大可能。
> 
> **输入:** arr[ ] = {1，1，2，2，20 }
> T3】输出: 6
> 
> **输入:** arr[ ] = {1，2，4，10}
> **输出:** -1

**方法:**给定的问题可以通过从给定的[数组](https://www.geeksforgeeks.org/array-data-structure/)中迭代所有可能的边的组合 **(a，b，c，d)** 来解决。可以观察到，只有当三条较小边之和大于或等于最大边，或者四边形的周长大于或等于(2 *最大边)时，a、b、c、d 边才构成有效的[四边形](https://www.geeksforgeeks.org/construction-of-a-quadrilateral/)。因此，从给定数组 **arr[]** 中迭代 **(a，b，c，d)** 的所有可能值，并检查它是否形成有效的四边形。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find largest perimeter
// of a possible quadrilateral
int largestPerimeterQuad(int* arr, int n)
{
    // Stores the final answer
    int ans = -1;

    // Loop to iterate over all possible
    // sides (a, b, c, d) that can be
    // formed from the given array
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            for (int k = j + 1; k < n; k++) {
                for (int l = k + 1; l < n; l++) {

                    // If a quadrilateral can
                    // be formed from current
                    // selected sides
                    if (arr[i] + arr[j]
                            + arr[k] + arr[l]
                        >= 2
                               * max(arr[i],
                                     max(arr[j],
                                         max(arr[k],
                                             arr[l]))))

                        // Update maximum
                        ans = max(ans, arr[i] + arr[j]
                                           + arr[k]
                                           + arr[l]);
                }
            }
        }
    }

    // Return Answer
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 3, 1, 2, 4, 2, 1 };
    int n = sizeof(arr) / sizeof(int);

    cout << largestPerimeterQuad(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

  // Function to find largest perimeter
  // of a possible quadrilateral
  static int largestPerimeterQuad(int []arr, int n)
  {

    // Stores the final answer
    int ans = -1;

    // Loop to iterate over all possible
    // sides (a, b, c, d) that can be
    // formed from the given array
    for (int i = 0; i < n; i++) {
      for (int j = i + 1; j < n; j++) {
        for (int k = j + 1; k < n; k++) {
          for (int l = k + 1; l < n; l++) {

            // If a quadrilateral can
            // be formed from current
            // selected sides
            if (arr[i] + arr[j]
                + arr[k] + arr[l]
                >= 2
                * Math.max(arr[i],
                           Math.max(arr[j],
                                    Math.max(arr[k],
                                             arr[l]))))

              // Update maximum
              ans = Math.max(ans, arr[i] + arr[j]
                             + arr[k]
                             + arr[l]);
          }
        }
      }
    }

    // Return Answer
    return ans;
  }

  // Driver Code
  public static void main(String args[])
  {
    int []arr = { 3, 1, 2, 4, 2, 1 };
    int n = arr.length;

    System.out.print(largestPerimeterQuad(arr, n));

  }
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find largest perimeter
# of a possible quadrilateral
def largestPerimeterQuad(arr, n):

    # Stores the final answer
    ans = -1

    # Loop to iterate over all possible
    # sides (a, b, c, d) that can be
    # formed from the given array
    for i in range(n):
        for j in range(i + 1, n):
            for k in range(j + 1, n):
                for l in range(k + 1, n):

                    # If a quadrilateral can
                    # be formed from current
                    # selected sides
                    if (arr[i] + arr[j]
                        + arr[k] + arr[l]
                        >= 2 * max(arr[i],
                                   max(arr[j],
                                       max(arr[k],
                                           arr[l])))):

                        # Update maximum
                        ans = max(ans, arr[i] + arr[j] + arr[k] + arr[l])
    # Return Answer
    return ans

# Driver Code
arr = [3, 1, 2, 4, 2, 1]
n = len(arr)

print(largestPerimeterQuad(arr, n))

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to find largest perimeter
// of a possible quadrilateral
static int largestPerimeterQuad(int []arr, int n)
{

    // Stores the final answer
    int ans = -1;

    // Loop to iterate over all possible
    // sides (a, b, c, d) that can be
    // formed from the given array
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            for (int k = j + 1; k < n; k++) {
                for (int l = k + 1; l < n; l++) {

                    // If a quadrilateral can
                    // be formed from current
                    // selected sides
                    if (arr[i] + arr[j]
                            + arr[k] + arr[l]
                        >= 2
                               * Math.Max(arr[i],
                                     Math.Max(arr[j],
                                         Math.Max(arr[k],
                                             arr[l]))))

                        // Update maximum
                        ans = Math.Max(ans, arr[i] + arr[j]
                                           + arr[k]
                                           + arr[l]);
                }
            }
        }
    }

    // Return Answer
    return ans;
}

// Driver Code
public static void Main()
{
    int []arr = { 3, 1, 2, 4, 2, 1 };
    int n = arr.Length;

    Console.Write(largestPerimeterQuad(arr, n));

}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to find largest perimeter
    // of a possible quadrilateral
    const largestPerimeterQuad = (arr, n) => {

        // Stores the final answer
        let ans = -1;

        // Loop to iterate over all possible
        // sides (a, b, c, d) that can be
        // formed from the given array
        for (let i = 0; i < n; i++) {
            for (let j = i + 1; j < n; j++) {
                for (let k = j + 1; k < n; k++) {
                    for (let l = k + 1; l < n; l++) {

                        // If a quadrilateral can
                        // be formed from current
                        // selected sides
                        if (arr[i] + arr[j]
                            + arr[k] + arr[l]
                            >= 2 * Math.max(arr[i],
                                Math.max(arr[j],
                                    Math.max(arr[k],
                                        arr[l]))))

                            // Update maximum
                            ans = Math.max(ans, arr[i] + arr[j]
                                + arr[k]
                                + arr[l]);
                    }
                }
            }
        }

        // Return Answer
        return ans;
    }

    // Driver Code
    let arr = [3, 1, 2, 4, 2, 1];
    let n = arr.length;

    document.write(largestPerimeterQuad(arr, n));

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
11
```

***时间复杂度:**O(N<sup>4</sup>)*
***辅助空间:** O(1)*