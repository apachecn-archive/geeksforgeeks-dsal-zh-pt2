# 奇数和数组中三元组的计数

> 原文:[https://www . geesforgeks . org/带奇数和的数组中的三元组计数/](https://www.geeksforgeeks.org/count-of-triplets-in-an-array-with-odd-sum/)

给定一个带有 **N** 整数的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，求 **i** 、 **j** 和 **k** 的三元组个数，使得**1<= I<j<k<= N**和 **arr[i] + arr[j] + arr[k]** 为奇数。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 4
> **解释:**给定数组包含 4 个奇数和的三元组。它们是{1，2，4}、{1，3，5}、{2，3，4}和{2，4，5}。
> 
> **输入:** arr[] ={4，5，6，4，5，10，1，7}
> **输出:** 28

**天真方法:**给定的问题可以通过迭代数组中所有可能的无序三元组并跟踪三元组的数量以使它们的和为奇数来解决。
**时间复杂度:** *O(N <sup>3</sup> )*

**有效方法:**可以使用整数的以下属性来优化上述方法:

*   **奇数+偶数+偶数=奇数**
*   **奇数+奇数+奇数=奇数**

因此，为了实现上述思想，我们可以[统计数组中偶数和奇数的个数](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)。假设奇数的计数为 **O** ，偶数的计数为 **E** 。所以排列一个奇数和两个偶数的不同方式是**<sup>O</sup>C<sub>1</sub>*<sup>E</sup>C<sub>2</sub>->(O * E *(E-1))/2**排列三个奇数的不同方式是**<sup>O</sup>C<sub>3</sub>->(O *(O-1)*(O-2))/6【6 最终答案将是上述两个值的总和。**

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <iostream>
using namespace std;

// Function to count the number of
// unordered triplets such that their
// sum is an odd integer
int countTriplets(int arr[], int n)
{
    // Count the number of odd and
    // even integers in the array
    int odd = 0, even = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] & 1)
            odd++;
        else
            even++;
    }

    // Number of ways to create triplets
    // using one odd and two even integers
    int c1 = odd * (even * (even - 1)) / 2;

    // Number of ways to create triplets
    // using three odd integers
    int c2 = (odd * (odd - 1) * (odd - 2)) / 6;

    // Return answer
    return c1 + c2;
}

// Driver Code
int main()
{
    int arr[] = { 4, 5, 6, 4, 5, 10, 1, 7 };
    int n = sizeof(arr) / sizeof(int);

    // Function Call
    int ans = countTriplets(arr, n);

    // Print Answer
    cout << ans;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

// Function to count the number of
// unordered triplets such that their
// sum is an odd integer
static int countTriplets(int arr[], int n)
{
    // Count the number of odd and
    // even integers in the array
    int odd = 0, even = 0;
    for (int i = 0; i < n; i++) {
        if ((arr[i] & 1) != 0)
            odd++;
        else
            even++;
    }

    // Number of ways to create triplets
    // using one odd and two even integers
    int c1 = odd * (even * (even - 1)) / 2;

    // Number of ways to create triplets
    // using three odd integers
    int c2 = (odd * (odd - 1) * (odd - 2)) / 6;

    // Return answer
    return c1 + c2;
}

// Driver code
public static void main(String[] args)
{
     int arr[] = { 4, 5, 6, 4, 5, 10, 1, 7 };
    int n = arr.length;

    // Function Call
    int ans = countTriplets(arr, n);

    // Print Answer
    System.out.println(ans);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python Program for the above approach

# Function to count the number of
# unordered triplets such that their
# sum is an odd integer
def countTriplets(arr, n):

    # Count the number of odd and
    # even integers in the array
    odd = 0
    even = 0
    for i in range(n):
        if (arr[i] & 1):
            odd+=1
        else:
            even+=1

    # Number of ways to create triplets
    # using one odd and two even integers
    c1 = odd * (even * (even - 1)) // 2

    # Number of ways to create triplets
    # using three odd integers
    c2 = (odd * (odd - 1) * (odd - 2)) // 6

    # Return answer
    return c1 + c2

# Driver Code

arr = [4, 5, 6, 4, 5, 10, 1, 7]
n = len(arr)

# Function Call
ans = countTriplets(arr, n)

# Print Answer
print(ans)

# This code is contributed by Shivani
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the number of unordered
// triplets such that their sum is an odd integer
static int countTriplets(int []arr, int n)
{

    // Count the number of odd and
    // even integers in the array
    int odd = 0, even = 0;
    for(int i = 0; i < n; i++)
    {
        if ((arr[i] & 1) != 0)
            odd++;
        else
            even++;
    }

    // Number of ways to create triplets
    // using one odd and two even integers
    int c1 = odd * (even * (even - 1)) / 2;

    // Number of ways to create triplets
    // using three odd integers
    int c2 = (odd * (odd - 1) * (odd - 2)) / 6;

    // Return answer
    return c1 + c2;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 4, 5, 6, 4, 5, 10, 1, 7 };
    int n = arr.Length;

    // Function Call
    int ans = countTriplets(arr, n);

    // Print Answer
    Console.Write(ans);
}
}

// This code is contributed by shivanisinghss2110.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach;

        // Function to count the number of
        // unordered triplets such that their
        // sum is an odd integer
        function countTriplets(arr, n)
        {

            // Count the number of odd and
            // even integers in the array
            let odd = 0, even = 0;
            for (let i = 0; i < n; i++) {
                if (arr[i] & 1)
                    odd++;
                else
                    even++;
            }

            // Number of ways to create triplets
            // using one odd and two even integers
            let c1 = Math.floor(odd * (even * (even - 1)) / 2);

            // Number of ways to create triplets
            // using three odd integers
            let c2 = Math.floor((odd * (odd - 1) * (odd - 2)) / 6);

            // Return answer

            return c1 + c2;
        }

        // Driver Code

        let arr = [4, 5, 6, 4, 5, 10, 1, 7];
        let n = arr.length;
        // Function Call
        let ans = countTriplets(arr, n);

        // Print Answer
        document.write(ans);

   // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
28
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*