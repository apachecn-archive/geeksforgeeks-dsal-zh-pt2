# 用和 S 创建一个大小为 N 的数组，这样就不存在和 S 或 S-K 的子数组

> 原文:[https://www . geesforgeks . org/create-a-size-n-with-sum-s-so-not-subarray-exists-with-sum-s-k/](https://www.geeksforgeeks.org/create-an-array-of-size-n-with-sum-s-such-that-no-subarray-exists-with-sum-s-or-s-k/)

给定一个数字 **N** 和一个整数 **S** ，任务是创建一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，使得所有元素的和等于 **S** ，并打印一个元素 **K** ，其中 0 ≤ K ≤ S，使得不存在和等于 **K** 或**(S–K)**的子阵列。
如果没有这样的数组，则打印**-1”**。
**注意:**的 **K** 可以有多个值。你可以打印任何一个。
**举例:**

> **输入:** N = 1，S = 4
> **输出:** {4}
> K = 2
> **说明:**
> 存在一个和为 4 的数组{4}。
> 从所有可能的 K 值，即 0 ≤ K ≤ 4，K = 1、2 和 3 满足给定条件。
> 对于 K = 2，不存在和为 2 或 S–K 的子阵，即 4–2 = 2。
> **输入:** N = 3，S = 8
> **输出:** {2，2，4}
> K = 1
> **解释:**
> 存在一个数组{2，2，4}，K 作为 1 存在，因此不存在和为 1 和 S–K 的子数组，即 8–1 = 7。

**方法:**要解决上述问题，我们必须观察:

1.  如果 **2 * N > S** 那么就没有数组可能。
    **例如:**

> 对于 N = 3 和 S = 4，则可能的数组是{1，2，1}、{1，1，2}、{2，1，1}。
> 可能的 **K** 值为 0、1、2、3 (0 < = k < = S)。
> 但是满足条件的 **K** 没有值。
> 所以解决这个是不可能的。

1.  只有当 **2 * N < = S** 时，数组才是可能的，并且可以使用元素 **(N-1)乘以 2** 来创建数组，并且最后一个元素作为**S –( 2 *(N-1))**和 K 将始终为 1。

以下是上述方法的实现:

## C++

```
// C++ for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to create an array with
// N elements with sum as S such that
// the given conditions satisfy
void createArray(int n, int s)
{

    // Check if the solution exists
    if (2 * n <= s)
    {

        // Print the array as
        // print (n-1) elements
        // of array as 2
        for(int i = 0; i < n - 1; i++)
        {
           cout << "2" << " ";
           s -= 2;
        }

        // Print the last element
        // of the array
        cout << s << endl;

        // Print the value of k
        cout << "1" << endl;
    }
    else

        // If solution doesnot exists
        cout << "-1" << endl;
}

// Driver Code
int main()
{

    // Given N and sum S
    int N = 1;
    int S = 4;

    // Function call
    createArray(N, S);
}

// This code is contributed by Ritik Bansal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java for the above approach
class GFG{

// Function to create an array with
// N elements with sum as S such that
// the given conditions satisfy
static void createArray(int n, int s)
{

    // Check if the solution exists
    if (2 * n <= s)
    {

        // Print the array as
        // print (n-1) elements
        // of array as 2
        for (int i = 0; i < n - 1; i++)
        {
            System.out.print(2 + " ");
            s -= 2;
        }

        // Print the last element
        // of the array
        System.out.println(s);

        // Print the value of k
        System.out.println(1);
    }
    else

        // If solution doesnot exists
        System.out.print("-1");
}

// Driver Code
public static void main(String[] args)
{

    // Given N and sum S
    int N = 1;
    int S = 4;

    // Function call
    createArray(N, S);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 for the above approach

# Function to create an array with
# N elements with sum as S such that
# the given conditions satisfy
def createArray(n, s):

    # Check if the solution exists
    if (2 * n<= s):            

        # Print the array as
        # print (n-1) elements
        # of array as 2
        for i in range(n-1):
            print(2, end =" ")
            s-= 2

        # Print the last element
        # of the array
        print(s)

        # Print the value of k
        print(1)
    else:
        # If solution doesnot exists
        print('-1')

# Driver Code

# Given N and sum S 
N = 1
S = 4

# Function call
createArray(N, S)
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to create an array with
// N elements with sum as S such that
// the given conditions satisfy
static void createArray(int n, int s)
{

    // Check if the solution exists
    if (2 * n <= s)
    {

        // Print the array as
        // print (n-1) elements
        // of array as 2
        for(int i = 0; i < n - 1; i++)
        {
           Console.Write(2 + " ");
           s -= 2;
        }

        // Print the last element
        // of the array
        Console.WriteLine(s);

        // Print the value of k
        Console.WriteLine(1);
    }
    else

        // If solution doesnot exists
        Console.Write("-1");
}

// Driver Code
public static void Main()
{

    // Given N and sum S
    int N = 1;
    int S = 4;

    // Function call
    createArray(N, S);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to create an array with
// N elements with sum as S such that
// the given conditions satisfy
function createArray(n, s)
{

    // Check if the solution exists
    if (2 * n <= s)
    {

        // Print the array as
        // print (n-1) elements
        // of array as 2
        for (let i = 0; i < n - 1; i++)
        {
             document.write(2 + " ");
            s -= 2;
        }

        // Print the last element
        // of the array
         document.write(s + "<br/>");

        // Print the value of k
         document.write(1);
    }
    else

        // If solution doesnot exists
         document.write("-1");
}

// Driver code

   // Given N and sum S
    let N = 1;
    let S = 4;

    // Function call
    createArray(N, S);

// This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
4
1
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*