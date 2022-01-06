# 二进制字符串回文所需的最小位翻转数

> 原文:[https://www . geeksforgeeks . org/最小位翻转数-需要生成二进制字符串-回文/](https://www.geeksforgeeks.org/minimum-count-of-bit-flips-required-to-make-a-binary-string-palindromic/)

给定一个整数 **N** ，任务是找到将 **N** 的二进制表示转换为回文所需的最小翻转位数。

**示例:**

> **输入:** N = 12
> **输出:** 2
> **解释:**
> 代表 12 的二进制字符串=“1100”。
> 要使“1100”成为回文，请将字符串转换为“0110”。
> 因此，需要翻转的最小位数为 2。
> **输入:** N = 7
> **输出:** 0
> **解释:**
> 代表 7 = 111 的二进制字符串，已经是回文了。

**天真方法:**最简单的方法是检查每个可能的子集，即具有相同位数的回文。
***时间复杂度:** O(N)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过以下步骤进行优化:

1.  首先，检查给定数字的二进制形式的长度。
2.  将两个指针分别指向 **L.S.B** 和 **M.S.B** 。
3.  现在继续递减第一个指针，递增第二个指针。
4.  检查第一个和第二个指针位置的位是否相同。如果不是，增加要更改的位数。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the
// length of the binary string
int check_length(int n)
{
    // Length
    int ans = 0;
    while (n) {

        // Right shift of n
        n = n >> 1;

        // Increment the length
        ans++;
    }

    // Return the length
    return ans;
}

// Function to check if the bit present
// at i-th position is a set bit or not
int check_ith_bit(int n, int i)
{
    // Returns true if the bit is set
    return (n & (1 << (i - 1)))
               ? true
               : false;
}

// Function to count the minimum
// number of bit flips required
int no_of_flips(int n)
{
    // Length of the binary form
    int len = check_length(n);

    // Number of flips
    int ans = 0;

    // Pointer to the LSB
    int right = 1;

    // Pointer to the MSB
    int left = len;

    while (right < left) {

        // Check if the bits are equal
        if (check_ith_bit(n, right)
            != check_ith_bit(n, left))
            ans++;

        // Decrementing the
        // left pointer
        left--;

        // Incrementing the
        // right pointer
        right++;
    }

    // Returns the number of
    // bits to flip.
    return ans;
}

// Driver Code
int main()
{

    int n = 12;

    cout << no_of_flips(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to calculate the
// length of the binary string
static int check_length(int n)
{

    // Length
    int ans = 0;

    while (n != 0)
    {

        // Right shift of n
        n = n >> 1;

        // Increment the length
        ans++;
    }

    // Return the length
    return ans;
}

// Function to check if the bit present
// at i-th position is a set bit or not
static boolean check_ith_bit(int n, int i)
{

    // Returns true if the bit is set
    return (n & (1<< (i - 1))) != 0 ? true : false;
}

// Function to count the minimum
// number of bit flips required
static int no_of_flips(int n)
{

    // Length of the binary form
    int len = check_length(n);

    // Number of flips
    int ans = 0;

    // Pointer to the LSB
    int right = 1;

    // Pointer to the MSB
    int left = len;

    while (right < left)
    {

        // Check if the bits are equal
        if (check_ith_bit(n, right) !=
            check_ith_bit(n, left))
            ans++;

        // Decrementing the
        // left pointer
        left--;

        // Incrementing the
        // right pointer
        right++;
    }

    // Returns the number of
    // bits to flip.
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int n = 12;

    System.out.println(no_of_flips(n));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate the
# length of the binary string
def check_length(n):

    # Length
    ans = 0

    while (n):

        # Right shift of n
        n = n >> 1

        # Increment the length
        ans += 1

    # Return the length
    return ans

# Function to check if the bit present
# at i-th position is a set bit or not
def check_ith_bit(n, i):

    # Returns true if the bit is set
    if (n & (1 << (i - 1))):
        return True
    else:
        return False

# Function to count the minimum
# number of bit flips required
def no_of_flips(n):

    # Length of the binary form
    ln = check_length(n)

    # Number of flips
    ans = 0

    # Pointer to the LSB
    right = 1

    # Pointer to the MSB
    left = ln

    while (right < left):

        # Check if the bits are equal
        if (check_ith_bit(n, right) !=
            check_ith_bit(n, left)):
            ans += 1

        # Decrementing the
        # left pointer
        left -= 1

        # Incrementing the
        # right pointer
        right += 1

    # Returns the number of
    # bits to flip.
    return ans

# Driver Code
n = 12

print(no_of_flips(n))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to calculate the
// length of the binary string
static int check_length(int n)
{

    // Length
    int ans = 0;

    while (n != 0)
    {

        // Right shift of n
        n = n >> 1;

        // Increment the length
        ans++;
    }

    // Return the length
    return ans;
}

// Function to check if the bit present
// at i-th position is a set bit or not
static bool check_ith_bit(int n, int i)
{

    // Returns true if the bit is set
    return (n & (1 << (i - 1))) != 0 ?
                                true : false;
}

// Function to count the minimum
// number of bit flips required
static int no_of_flips(int n)
{

    // Length of the binary form
    int len = check_length(n);

    // Number of flips
    int ans = 0;

    // Pointer to the LSB
    int right = 1;

    // Pointer to the MSB
    int left = len;

    while (right < left)
    {

        // Check if the bits are equal
        if (check_ith_bit(n, right) !=
            check_ith_bit(n, left))
            ans++;

        // Decrementing the
        // left pointer
        left--;

        // Incrementing the
        // right pointer
        right++;
    }

    // Returns the number of
    // bits to flip.
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 12;

    Console.WriteLine(no_of_flips(n));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to calculate the
// length of the binary string
function check_length(n)
{

    // Length
    let ans = 0;

    while (n != 0)
    {

        // Right shift of n
        n = n >> 1;

        // Increment the length
        ans++;
    }

    // Return the length
    return ans;
}

// Function to check if the bit present
// at i-th position is a set bit or not
function check_ith_bit(n, i)
{

    // Returns true if the bit is set
    return (n & (1<< (i - 1))) != 0 ? true : false;
}

// Function to count the minimum
// number of bit flips required
function no_of_flips(n)
{

    // Length of the binary form
    let len = check_length(n);

    // Number of flips
    let ans = 0;

    // Pointer to the LSB
    let right = 1;

    // Pointer to the MSB
    let left = len;

    while (right < left)
    {

        // Check if the bits are equal
        if (check_ith_bit(n, right) !=
            check_ith_bit(n, left))
            ans++;

        // Decrementing the
        // left pointer
        left--;

        // Incrementing the
        // right pointer
        right++;
    }

    // Returns the number of
    // bits to flip.
    return ans;
}

// Driver Code

       let n = 12;

    document.write(no_of_flips(n));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(log N)*
***辅助空间:** O(1)*