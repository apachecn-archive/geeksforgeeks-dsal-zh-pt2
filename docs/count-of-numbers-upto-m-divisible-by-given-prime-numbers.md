# 可被给定素数整除的 M 以内的数的计数

> 原文:[https://www . geesforgeks . org/numbers-up-m-可被给定素数整除/](https://www.geeksforgeeks.org/count-of-numbers-upto-m-divisible-by-given-prime-numbers/)

给定一个由[质数](https://www.geeksforgeeks.org/prime-numbers/)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个数 **M** ，任务是计算范围**【1，M】**中可被任意给定质数整除的元素数。

**示例:**

> **输入:** arr[] = {2，3，5，7} M = 100
> **输出:** 78
> **解释:**
> 总共有 78 个数字可以被 2，3，5 或 7 整除。
> 
> **输入:** arr[] = {2，5，7，11} M = 200
> **输出:** 137
> **解释:**
> 总共有 137 个数字可以被 2，5，7 或 11 整除。

**天真方法:**想法是迭代范围**【1，M】**并检查是否有任何数组元素在范围**【1，M】**内划分元素，然后计数元素否则检查范围内的下一个数字。
以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to count the numbers that
// are divisible by the numbers in
// the array from range 1 to M
int count(int a[], int M, int N)
{
    // Initialize the count variable
    int cnt = 0;

    // Iterate over [1, M]
    for (int i = 1; i <= M; i++) {

        // Iterate over array elements arr[]
        for (int j = 0; j < N; j++) {

            // Check if i is divisible by a[j]
            if (i % a[j] == 0) {

                // Increment the count
                cnt++;
                break;
            }
        }
    }

    // Return the answer
    return cnt;
}

// Driver code
int main()
{
    // Given array arr[]
    int arr[] = { 2, 3, 5, 7 };

    // Given Number M
    int m = 100;
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << count(arr, m, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to count the numbers that
// are divisible by the numbers in
// the array from range 1 to M
static int count(int a[], int M, int N)
{

    // Initialize the count variable
    int cnt = 0;

    // Iterate over [1, M]
    for(int i = 1; i <= M; i++)
    {

        // Iterate over array elements arr[]
        for(int j = 0; j < N; j++)
        {

            // Check if i is divisible by a[j]
            if (i % a[j] == 0)
            {

                // Increment the count
                cnt++;
                break;
            }
        }
    }

    // Return the answer
    return cnt;
}

// Driver code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 2, 3, 5, 7 };

    // Given number M
    int m = 100;
    int n = arr.length;

    // Function call
    System.out.print(count(arr, m, n));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the numbers that
# are divisible by the numbers in
# the array from range 1 to M
def count(a, M, N):

    # Initialize the count variable
    cnt = 0

    # Iterate over [1, M]
    for i in range(1, M + 1):

        # Iterate over array elements arr[]
        for j in range(N):

            # Check if i is divisible by a[j]
            if (i % a[j] == 0):

                # Increment the count
                cnt += 1
                break

    # Return the answer
    return cnt

# Driver code

# Given list lst
lst = [ 2, 3, 5, 7 ]

# Given number M
m = 100
n = len(lst)

# Function call
print(count(lst, m, n))

# This code is contributed by vishu2908   
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the numbers that
// are divisible by the numbers in
// the array from range 1 to M
static int count(int []a, int M, int N)
{

    // Initialize the count variable
    int cnt = 0;

    // Iterate over [1, M]
    for(int i = 1; i <= M; i++)
    {

        // Iterate over array elements []arr
        for(int j = 0; j < N; j++)
        {

            // Check if i is divisible by a[j]
            if (i % a[j] == 0)
            {

                // Increment the count
                cnt++;
                break;
            }
        }
    }

    // Return the answer
    return cnt;
}

// Driver code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 2, 3, 5, 7 };

    // Given number M
    int m = 100;
    int n = arr.Length;

    // Function call
    Console.Write(count(arr, m, n));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Function to count the numbers that
    // are divisible by the numbers in
    // the array from range 1 to M
    function count(a, M, N)
    {
        // Initialize the count variable
        let cnt = 0;

        // Iterate over [1, M]
        for (let i = 1; i <= M; i++) {

            // Iterate over array elements arr[]
            for (let j = 0; j < N; j++) {

                // Check if i is divisible by a[j]
                if (i % a[j] == 0) {

                    // Increment the count
                    cnt++;
                    break;
                }
            }
        }

        // Return the answer
        return cnt;
    }

    // Given array arr[]
    let arr = [ 2, 3, 5, 7 ];

    // Given Number M
    let m = 100;
    let n = arr.length;

    // Function Call
    document.write(count(arr, m, n));

</script>
```

**Output**

```
78
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(1)*
**另一种方法:**解决这个问题的另一种方法是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)和[筛选](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)。标记数组中可被任意素数整除的 M 以内的所有数字。然后统计所有标记的数字并打印出来。