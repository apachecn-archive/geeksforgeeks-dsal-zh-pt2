# 仅由素数组成的子阵列的计数

> 原文:[https://www . geesforgeks . org/子数组计数-仅由素数组成/](https://www.geeksforgeeks.org/count-of-subarrays-consisting-of-only-prime-numbers/)

给定一个长度为 **N** 的数组 **A[]** ，任务是找出仅由素数组成的子数组的数量。

**示例:**

> **输入:** arr[] = {2，3，4，5，7}
> **输出:** 6
> **解释:**
> 仅由素数组成的所有可能的子阵为{{2}、{3}、{2，3}、{5}、{7}、{5，7}}
> 
> **输入:** arr[] = {2，3，5，6，7，11，3，5，9，3}
> **输出:** 17

**天真方法:**解决问题最简单的方法是[从给定的数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)中生成所有可能的子阵，并检查它是否只由[素数](https://www.geeksforgeeks.org/prime-numbers/)组成。

***时间复杂度:** O(N <sup>3</sup> * √max(数组))，其中 **√M** 是检查一个数是否为素数所需的时间，这个 **M** 的范围可以是**【min(arr)，max(arr)】***

***辅助空间:** O(1)*

**双指针进场:**

取两个指针**‘I’**和**‘j’**指向数组的第一个元素 **(arr[0]** )。将**和**初始化为 0。如果索引“j”处的元素是质数，则将**和**增加 1，并将 j 增加 1。如果索引“j”处的元素不是素数，则将“I”增加 1，并将 j 的值更新为 I。重复上述步骤，直到“I”到达数组末尾。返回 **ans** 。

给定方法的实现如下所示。

## C++

```
// C++ program to implement the above approach

#include <bits/stdc++.h>
using namespace std;

bool is_prime(int n)
{
    if (n <= 1)
        return 0;

    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0)
            return 0;
    }

    return 1;
}

int count_prime_subarrays(int arr[], int n)
{
    int ans = 0;
    int i = 0;
    int j = 0;
    while (i < n) {
        // If 'j' reaches the end of array but 'i' does not
        // , then change the value of 'j' to 'i'
        if (j == n) {
            i++;
            j = i;
            if (i
                == n) // if both 'i' and 'j' reaches the end
                      // of array, we will break the loop
                break;
        }

        if (is_prime(arr[j])) {
            ans++; // we will increment the count if 'j' is
                   // prime
            j++; // we will increment 'j' by 1
        }
        // if arr[j] is not prime
        else {
            i++; // we will increment i by 1
            j = i; // assign the value of i to j
        }
    }

    return ans;
}

// Driver Code
int main()
{
    int N = 10;
    int ar[] = { 2, 3, 5, 6, 7, 11, 3, 5, 9, 3 };
    cout << count_prime_subarrays(ar, N);
}
```

**Output**

```
17
```

**高效方法:**需要进行以下观察来优化上述方法:

> [长度为 **M** 的阵列的子阵列计数等于 **M * (M + 1) / 2**](https://www.geeksforgeeks.org/count-of-possible-subarrays-and-subsequences-using-given-length-of-array/) 。

因此，从一个给定的数组中，一个长度为 **M** 的仅由素数组成的连续子数组将生成长度为 **M * (M + 1) / 2** 的子数组。

按照以下步骤解决问题:

*   遍历数组，检查每个元素[是否是素数](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-prime-or-not/)。
*   对于找到的每个质数，继续递增**计数**。
*   对于每个非素数元素，通过添加**计数*(计数+ 1) / 2** 并将**计数**重置为 **0** 来更新所需答案。
*   最后，打印所需的子阵列。

以下执行上述方法:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a number
// is prime or not.
bool is_prime(int n)
{
    if (n <= 1)
        return 0;

    for (int i = 2; i * i <= n; i++) {

        // If n has any factor other than 1,
        // then n is non-prime.
        if (n % i == 0)
            return 0;
    }

    return 1;
}

// Function to return the count of
// subarrays made up of prime numbers only
int count_prime_subarrays(int ar[], int n)
{

    // Stores the answer
    int ans = 0;

    // Stores the count of continuous
    // prime numbers in an array
    int count = 0;

    for (int i = 0; i < n; i++) {

        // If the current array
        // element is prime
        if (is_prime(ar[i]))

            // Increase the count
            count++;
        else {

            if (count) {

                // Update count of subarrays
                ans += count * (count + 1)
                       / 2;
                count = 0;
            }
        }
    }

    // If the array ended with a
    // continuous prime sequence
    if (count)
        ans += count * (count + 1) / 2;

    return ans;
}

// Driver Code
int main()
{
    int N = 10;
    int ar[] = { 2, 3, 5, 6, 7,
                 11, 3, 5, 9, 3 };
    cout << count_prime_subarrays(ar, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Function to check if a number
// is prime or not.
static boolean is_prime(int n)
{
    if (n <= 1)
         return false;

    for (int i = 2; i * i <= n; i++)
    {

        // If n has any factor other than 1,
        // then n is non-prime.
        if (n % i == 0)
             return false; 
    }
    return true;
}

// Function to return the count of
// subarrays made up of prime numbers only
static int count_prime_subarrays(int ar[], int n)
{

    // Stores the answer
    int ans = 0;

    // Stores the count of continuous
    // prime numbers in an array
    int count = 0;

    for (int i = 0; i < n; i++)
    {

        // If the current array
        // element is prime
        if (is_prime(ar[i]))

            // Increase the count
            count++;
        else
        {
            if (count != 0)
            {

                // Update count of subarrays
                ans += count * (count + 1) / 2;
                count = 0;
            }
        }
    }

    // If the array ended with a
    // continuous prime sequence
    if (count != 0)
        ans += count * (count + 1) / 2;

    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int N = 10;
    int []ar = { 2, 3, 5, 6, 7,
                11, 3, 5, 9, 3 };
    System.out.print(count_prime_subarrays(ar, N));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to check if a number
# is prime or not.
def is_prime(n):

    if(n <= 1):
        return 0

    i = 2
    while(i * i <= n):

        # If n has any factor other than 1,
        # then n is non-prime.
        if(n % i == 0):
            return 0

        i += 1

    return 1

# Function to return the count of
# subarrays made up of prime numbers only
def count_prime_subarrays(ar, n):

    # Stores the answer
    ans = 0

    # Stores the count of continuous
    # prime numbers in an array
    count = 0

    for i in range(n):

        # If the current array
        # element is prime
        if(is_prime(ar[i])):

            # Increase the count
            count += 1

        else:
            if(count):

                # Update count of subarrays
                ans += count * (count + 1) // 2
                count = 0

    # If the array ended with a
    # continuous prime sequence
    if(count):
        ans += count * (count + 1) // 2

    return ans

# Driver Code
N = 10
ar = [ 2, 3, 5, 6, 7,
       11, 3, 5, 9, 3 ]

# Function call
print(count_prime_subarrays(ar, N))

# This code is contributed by Shivam Singh
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

// Function to check if a number
// is prime or not.
static bool is_prime(int n)
{
    if (n <= 1)
         return false;

    for (int i = 2; i * i <= n; i++)
    {

        // If n has any factor other than 1,
        // then n is non-prime.
        if (n % i == 0)
             return false; 
    }
    return true;
}

// Function to return the count of
// subarrays made up of prime numbers only
static int count_prime_subarrays(int []ar, int n)
{

    // Stores the answer
    int ans = 0;

    // Stores the count of continuous
    // prime numbers in an array
    int count = 0;

    for (int i = 0; i < n; i++)
    {

        // If the current array
        // element is prime
        if (is_prime(ar[i]))

            // Increase the count
            count++;
        else
        {
            if (count != 0)
            {

                // Update count of subarrays
                ans += count * (count + 1) / 2;
                count = 0;
            }
        }
    }

    // If the array ended with a
    // continuous prime sequence
    if (count != 0)
        ans += count * (count + 1) / 2;

    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 10;
    int []ar = { 2, 3, 5, 6, 7,
                11, 3, 5, 9, 3 };
    Console.Write(count_prime_subarrays(ar, N));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

      // JavaScript Program to implement
      // the above approach

      // Function to check if a number
      // is prime or not.
      function is_prime(n) {
        if (n <= 1) return 0;

        for (var i = 2; i * i <= n; i++) {

          // If n has any factor other than 1,
          // then n is non-prime.
          if (n % i == 0) return 0;
        }

        return 1;
      }

      // Function to return the count of
      // subarrays made up of prime numbers only
      function count_prime_subarrays(ar, n) {
        // Stores the answer
        var ans = 0;

        // Stores the count of continuous
        // prime numbers in an array
        var count = 0;

        for (var i = 0; i < n; i++) {
          // If the current array
          // element is prime
          if (is_prime(ar[i]))
            // Increase the count
            count++;
          else {
            if (count) {
              // Update count of subarrays
              ans += (count * (count + 1)) / 2;
              count = 0;
            }
          }
        }

        // If the array ended with a
        // continuous prime sequence
        if (count) ans += (count * (count + 1)) / 2;

        return ans;
      }

      // Driver Code

      var N = 10;
      var ar = [2, 3, 5, 6, 7, 11, 3, 5, 9, 3];
      document.write(count_prime_subarrays(ar, N));

</script>
```

**Output**

```
17
```

***时间复杂度:** O(N * √max(arr))，其中 **√M** 是检查一个数是否为素数所需的时间，这个 **M** 可以范围**【min(arr)，max(arr)】***
***辅助空间:** O(1)*