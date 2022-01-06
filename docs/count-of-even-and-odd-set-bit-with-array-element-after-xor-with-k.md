# 与 K

异或后数组元素的偶奇设定位计数

> 原文:[https://www . geeksforgeeks . org/用 k 异或后的数组元素设置奇偶位计数/](https://www.geeksforgeeks.org/count-of-even-and-odd-set-bit-with-array-element-after-xor-with-k/)

给定一个[阵](https://www.geeksforgeeks.org/introduction-to-arrays/)T2【arr】和一个号 **K** 。任务是在将 **K** 与给定的**arr【】**的每个元素进行异或运算后，找到具有奇数和偶数设定位的元素的计数。
**举例:**

> **输入:** arr[] = {4，2，15，9，8，8}，K = 3
> T3】输出:偶数= 2， Odd = 4
> **解释:**
> 元素与 k 取 XOR 后的二进制表示为:
> 4 ^ 3 = 7(111)
> 2 ^ 3 = 1(1)
> 15 ^ 3 = 12(1100)
> 9 ^ 3 = 10(1010)
> 8 ^ 3 = 11(1011)
> 8 ^ 3 = 11(1011)
> 否 10)
> 二进制表示中奇数为 1 的元素个数:4 (7，1，11，11)
> **输入:** arr[] = {4，2，15，9，8，8}，K = 6
> **输出:**偶数= 4，奇数= 2

**朴素方法:**朴素方法是将 **K** 与给定的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**的每个元素进行按位异或，然后在与 **K** 进行异或后，计算[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中每个元素的设置位。
**时间复杂度:** O(N*K)
**高效逼近:**
借助以下观察，我们有:

> 例如:
> 如果 A = 4 且 K = 3
> 二进制表示:
> a = 100
> k = 011
> a^k = 111
> 因此，数 **A** (其具有奇数个设定位)与数 **K** (其具有偶数个设定位)的异或运算产生奇数个设定位。
> 并且如果 A = 4 并且 K = 7
> 二进制表示:
> a = 100
> k = 111
> a^k = 011
> 因此，数 **A** (其具有奇数个设定位)与数 **K** (其具有奇数个设定位)的异或产生偶数个设定位。

从以上观察:

*   如果 **K** 有奇数个置位，那么与 **K** 异或后的偶置位和奇置位的[阵](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【】**的元素个数将与异或前的[阵](https://www.geeksforgeeks.org/introduction-to-arrays/)中偶置位和奇置位的个数相同。
*   如果 **K** 有偶数个置位，那么与 **K** 异或后的[阵](https://www.geeksforgeeks.org/introduction-to-arrays/)T4【arr】【】偶置位奇置位的元素个数将与异或前的[阵](https://www.geeksforgeeks.org/introduction-to-arrays/)偶置位奇置位的个数相反。

**步骤**:T2

1.  存储给定[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**中具有偶设定位和奇设定位的元素的计数。
2.  如果 **K** 有奇数置位，那么与 K 异或后的奇偶置位计数将与上面计算的奇偶置位计数相同。
3.  如果 **K** 有偶设定位，那么与 K 异或后的偶、奇设定位的计数就是上面计算的奇、偶设定位的计数。

以下是上述方法的实现:

## C++

```
// C++ program to count the set
// bits after taking XOR with a
// number K
#include <bits/stdc++.h>
using namespace std;

// Function to store EVEN and odd variable
void countEvenOdd(int arr[], int n, int K)
{
    int even = 0, odd = 0;

    // Store the count of even and
    // odd set bit
    for (int i = 0; i < n; i++) {

        // Count the set bit using
        // in built function
        int x = __builtin_popcount(arr[i]);
        if (x % 2 == 0)
            even++;
        else
            odd++;
    }

    int y;

    // Count of set-bit of K
    y = __builtin_popcount(K);

    // If y is odd then, count of
    // even and odd set bit will
    // be interchanged
    if (y & 1) {
        cout << "Even = " << odd
             << ", Odd = " << even;
    }

    // Else it will remain same as
    // the original array
    else {
        cout << "Even = " << even
             << ", Odd = " << odd;
    }
}

// Driver's Code
int main(void)
{
    int arr[] = { 4, 2, 15, 9, 8, 8 };
    int K = 3;
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call to count even
    // and odd
    countEvenOdd(arr, n, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the set
// bits after taking XOR with a
// number K
class GFG {

    /* Function to get no of set 
    bits in binary representation 
    of positive integer n */
    static int __builtin_popcount(int n)
    {
        int count = 0;
        while (n > 0) {
            count += n & 1;
            n >>= 1;
        }
        return count;
    }

    // Function to store EVEN and odd variable
    static void countEvenOdd(int arr[], int n, int K)
    {
        int even = 0, odd = 0;

        // Store the count of even and
        // odd set bit
        for (int i = 0; i < n; i++) {

            // Count the set bit using
            // in built function
            int x = __builtin_popcount(arr[i]);
            if (x % 2 == 0)
                even++;
            else
                odd++;
        }

        int y;

        // Count of set-bit of K
        y = __builtin_popcount(K);

        // If y is odd then, count of
        // even and odd set bit will
        // be interchanged
        if ((y & 1) != 0) {
            System.out.println("Even = "+ odd + ", Odd = " + even);
        }

        // Else it will remain same as
        // the original array
        else {
            System.out.println("Even = " + even + ", Odd = " + odd);
        }
    }

    // Driver's Code
    public static void main (String[] args)
    {
        int arr[] = { 4, 2, 15, 9, 8, 8 };
        int K = 3;
        int n = arr.length;

        // Function call to count even
        // and odd
        countEvenOdd(arr, n, K);
    }

}
// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python3 program to count the set
# bits after taking XOR with a
# number K

# Function to store EVEN and odd variable
def countEvenOdd(arr, n, K) :

    even = 0; odd = 0;

    # Store the count of even and
    # odd set bit
    for i in range(n) :

        # Count the set bit using
        # in built function
        x = bin(arr[i]).count('1');
        if (x % 2 == 0) :
            even += 1;
        else :
            odd += 1;

    # Count of set-bit of K
    y = bin(K).count('1');

    # If y is odd then, count of
    # even and odd set bit will
    # be interchanged
    if (y & 1) :
        print("Even =",odd ,", Odd =", even);

    # Else it will remain same as
    # the original array
    else :
        print("Even =" , even ,", Odd =", odd);

# Driver's Code
if __name__ == "__main__" :

    arr = [ 4, 2, 15, 9, 8, 8 ];
    K = 3;
    n = len(arr);

    # Function call to count even
    # and odd
    countEvenOdd(arr, n, K);

# This code is contributed by Yash_R
```

## C#

```
// C# program to count the set
// bits after taking XOR with a
// number K
using System;

public class GFG {

    /* Function to get no of set 
    bits in binary representation 
    of positive integer n */
    static int __builtin_popcount(int n)
    {
        int count = 0;
        while (n > 0) {
            count += n & 1;
            n >>= 1;
        }
        return count;
    }

    // Function to store EVEN and odd variable
    static void countEvenOdd(int []arr, int n, int K)
    {
        int even = 0, odd = 0;

        // Store the count of even and
        // odd set bit
        for (int i = 0; i < n; i++) {

            // Count the set bit using
            // in built function
            int x = __builtin_popcount(arr[i]);
            if (x % 2 == 0)
                even++;
            else
                odd++;
        }

        int y;

        // Count of set-bit of K
        y = __builtin_popcount(K);

        // If y is odd then, count of
        // even and odd set bit will
        // be interchanged
        if ((y & 1) != 0) {
            Console.WriteLine("Even = "+ odd + ", Odd = " + even);
        }

        // Else it will remain same as
        // the original array
        else {
            Console.WriteLine("Even = " + even + ", Odd = " + odd);
        }
    }

    // Driver's Code
    public static void Main (string[] args)
    {
        int []arr = { 4, 2, 15, 9, 8, 8 };
        int K = 3;
        int n = arr.Length;

        // Function call to count even
        // and odd
        countEvenOdd(arr, n, K);
    }

}
// This code is contributed by Yash_R
```

## java 描述语言

```
<script>
// Javascript program to count the set
// bits after taking XOR with a
// number K

/* Function to get no of set
bits in binary representation
of positive integer n */
function __builtin_popcount(n) {
    let count = 0;
    while (n > 0) {
        count += n & 1;
        n >>= 1;
    }
    return count;
}

// Function to store EVEN and odd variable
function countEvenOdd(arr, n, K) {
    let even = 0, odd = 0;

    // Store the count of even and
    // odd set bit
    for (let i = 0; i < n; i++) {

        // Count the set bit using
        // in built function
        let x = __builtin_popcount(arr[i]);
        if (x % 2 == 0)
            even++;
        else
            odd++;
    }

    let y;

    // Count of set-bit of K
    y = __builtin_popcount(K);

    // If y is odd then, count of
    // even and odd set bit will
    // be interchanged
    if ((y & 1) != 0) {
        document.write("Even = " + odd + ", Odd = " + even);
    }

    // Else it will remain same as
    // the original array
    else {
        document.write("Even = " + even + ", Odd = " + odd);
    }
}

// Driver's Code

let arr = [4, 2, 15, 9, 8, 8];
let K = 3;
let n = arr.length;

// Function call to count even
// and odd
countEvenOdd(arr, n, K);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
Even = 2, Odd = 4
```

**时间复杂度:** O(N)