# 计算从 L 到 R 范围内所有数字的总设定位

> 原文:[https://www . geesforgeks . org/count-total-set-bit-in-all-numbers-from-l-to-r/](https://www.geeksforgeeks.org/count-total-set-bits-in-all-numbers-from-range-l-to-r/)

给定两个正整数 **L** 和 **R** ，任务是计算从 **L** 到 **R** 的所有数字的二进制表示中的设定位总数。

**示例:**

> **输入:** L = 3，R = 5
> **输出:** 5
> **解释:** (3)10 = (11)2，(4)10 = (100)2，(5)10 = (101)2
> 所以，3 到 5 范围内的总设置位为 5
> 
> **输入:** L = 10，R = 15
> T3】输出: 17

**方法 1–天真方法:**想法是运行从 **L 到 R** 的循环，并对从 **L 到 R** 的所有数字中的设置位计数求和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count set bits in x
unsigned int
countSetBitsUtil(unsigned int x)
{
    // Base Case
    if (x <= 0)
        return 0;

    // Recursive Call
    return ((x % 2 == 0 ? 0 : 1)
            + countSetBitsUtil(x / 2));
}

// Function that returns count of set bits
// present in all numbers from 1 to N
unsigned int countSetBits(unsigned int L,
                          unsigned int R)
{
    // Initialize the result
    int bitCount = 0;

    for (int i = L; i <= R; i++) {
        bitCount += countSetBitsUtil(i);
    }

    // Return the setbit count
    return bitCount;
}

// Driver Code
int main()
{
    // Given L and R
    int L = 3, R = 5;

    // Function Call
    printf("Total set bit count is %d",
           countSetBits(L, R));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to count set bits in x
static int countSetBitsUtil(int x)
{
    // Base Case
    if (x <= 0)
        return 0;

    // Recursive Call
    return ((x % 2 == 0 ? 0 : 1) +
             countSetBitsUtil(x / 2));
}

// Function that returns count of set bits
// present in all numbers from 1 to N
static int countSetBits(int L, int R)
{
    // Initialize the result
    int bitCount = 0;

    for (int i = L; i <= R; i++)
    {
        bitCount += countSetBitsUtil(i);
    }

    // Return the setbit count
    return bitCount;
}

// Driver Code
public static void main(String[] args)
{
    // Given L and R
    int L = 3, R = 5;

    // Function Call
    System.out.printf("Total set bit count is %d",
                                 countSetBits(L, R));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count set bits in x
def countSetBitsUtil(x):

    # Base Case
    if (x < 1):
        return 0;

    # Recursive Call
    if (x % 2 == 0):
        return 0;
    else:
        return 1 + (countSetBitsUtil(x / 2));

# Function that returns count of set bits
# present in all numbers from 1 to N
def countSetBits(L, R):

    # Initialize the result
    bitCount = 0;

    for i in range(L, R + 1):
        bitCount += countSetBitsUtil(i);

    # Return the setbit count
    return bitCount;

# Driver Code
if __name__ == '__main__':

    # Given L and R
    L = 3;
    R = 5;

    # Function Call
    print("Total set bit count is ",
                countSetBits(L, R));

# This code is contributed by Princi Singh
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to count set bits in x
static int countSetBitsUtil(int x)
{
    // Base Case
    if (x <= 0)
        return 0;

    // Recursive Call
    return ((x % 2 == 0 ? 0 : 1) +
             countSetBitsUtil(x / 2));
}

// Function that returns count of set bits
// present in all numbers from 1 to N
static int countSetBits(int L, int R)
{
    // Initialize the result
    int bitCount = 0;

    for (int i = L; i <= R; i++)
    {
        bitCount += countSetBitsUtil(i);
    }

    // Return the setbit count
    return bitCount;
}

// Driver Code
public static void Main(String[] args)
{
    // Given L and R
    int L = 3, R = 5;

    // Function Call
    Console.Write("Total set bit count is {0}",
                           countSetBits(L, R));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count set bits in x
function countSetBitsUtil(x)
{
    // Base Case
    if (x <= 0)
        return 0;

    // Recursive Call
    return ((x % 2 == 0 ? 0 : 1)
            + countSetBitsUtil(parseInt(x / 2)));
}

// Function that returns count of set bits
// present in all numbers from 1 to N
function countSetBits(L, R)
{
    // Initialize the result
    var bitCount = 0;

    for (var i = L; i <= R; i++) {
        bitCount += countSetBitsUtil(i);
    }

    // Return the setbit count
    return bitCount;
}

// Driver Code
// Given L and R
var L = 3, R = 5;

// Function Call
document.write("Total set bit count is "+
       countSetBits(L, R));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
Total set bit count is 5
```

***时间复杂度:** O(N*Log N)*
***辅助空间:** O(1)*

**方法 2–更好的方法:**想法是从最右侧远处观察位 **i** ，然后位在垂直顺序中的 **2 <sup>i</sup>** 位置之后反转。

**示例:**

```
L = 3, R = 5
0 = 0000
1 = 0001
2 = 0010
3 = 0011
4 = 0100
5 = 0101
```

观察最右边的位(i = 0)位在( **2 <sup>0</sup>** = 1)
之后翻转。
因此，我们可以以垂直方式计数位，使得在**最右侧的**位置，位将在 **2 <sup>i</sup> 迭代**后翻转。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that counts the set bits
// from 0 to N
int countSetBit(int n)
{
    int i = 0;

    // To store sum of set bits from 0 - N
    int ans = 0;

    // Until n >= to 2^i
    while ((1 << i) <= n) {

        // This k will get flipped after
        // 2^i iterations
        bool k = 0;

        // Change is iterator from 2^i to 1
        int change = 1 << i;

        // This will loop from 0 to n for
        // every bit position
        for (int j = 0; j <= n; j++) {

            ans += k;

            if (change == 1) {

                // When change = 1 flip the bit
                k = !k;

                // Again set change to 2^i
                change = 1 << i;
            }
            else {
                change--;
            }
        }

        // Increment the position
        i++;
    }

    return ans;
}

// Function that counts the set bit
// in the range (L, R)
int countSetBits(int L, int R)
{

    // Return the count
    return abs(countSetBit(R)
               - countSetBit(L - 1));
}

// Driver Code
int main()
{
    // Given L and R
    int L = 3, R = 5;

    // Function Call
    cout << "Total set bit count is "
         << countSetBits(L, R) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function that counts the set bits
// from 0 to N
static int countSetBit(int n)
{
    int i = 0;

    // To store sum of set bits from 0 - N
    int ans = 0;

    // Until n >= to 2^i
    while ((1 << i) <= n)
    {

        // This k will get flipped after
        // 2^i iterations
        boolean k = true;

        // Change is iterator from 2^i to 1
        int change = 1 << i;

        // This will loop from 0 to n for
        // every bit position
        for (int j = 0; j <= n; j++)
        {
            ans += k==true?0:1;

            if (change == 1)
            {

                // When change = 1 flip the bit
                k = !k;

                // Again set change to 2^i
                change = 1 << i;
            }
            else
            {
                change--;
            }
        }

        // Increment the position
        i++;
    }

    return ans;
}

// Function that counts the set bit
// in the range (L, R)
static int countSetBits(int L, int R)
{

    // Return the count
    return Math.abs(countSetBit(R) -
                    countSetBit(L - 1));
}

// Driver Code
public static void main(String[] args)
{
    // Given L and R
    int L = 3, R = 5;

    // Function Call
    System.out.print("Total set bit count is " +
                      countSetBits(L, R) +"\n");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that counts the set bits
# from 0 to N
def countSetBit(n):
    i = 0;

    # To store sum of set bits from 0 - N
    ans = 0;

    # Until n >= to 2^i
    while ((1 << i) <= n):

        # This k will get flipped after
        # 2^i iterations
        k = True;

        # Change is iterator from 2^i to 1
        change = 1 << i;

        # This will loop from 0 to n for
        # every bit position
        for j in range(n+1):
            ans += 0 if k == True else 1;

            if (change == 1):

                # When change = 1 flip the bit
                k = False if k == True else True;

                # Again set change to 2^i
                change = 1 << i;
            else:
                change -=1;

        # Increment the position
        i += 1;

    return ans;

# Function that counts the set bit
# in the range (L, R)
def countSetBits(L, R):

    # Return the count
    return abs(countSetBit(R) -
               countSetBit(L - 1));

# Driver Code
if __name__ == '__main__':

    # Given L and R
    L = 3;
    R = 5;

    # Function Call
    print("Total set bit count is ", 
          countSetBits(L, R));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function that counts the set bits
// from 0 to N
static int countSetBit(int n)
{
    int i = 0;

    // To store sum of set bits from 0 - N
    int ans = 0;

    // Until n >= to 2^i
    while ((1 << i) <= n)
    {

        // This k will get flipped after
        // 2^i iterations
        bool k = true;

        // Change is iterator from 2^i to 1
        int change = 1 << i;

        // This will loop from 0 to n for
        // every bit position
        for (int j = 0; j <= n; j++)
        {
            ans += k==true?0:1;

            if (change == 1)
            {

                // When change = 1 flip the bit
                k = !k;

                // Again set change to 2^i
                change = 1 << i;
            }
            else
            {
                change--;
            }
        }

        // Increment the position
        i++;
    }

    return ans;
}

// Function that counts the set bit
// in the range (L, R)
static int countSetBits(int L, int R)
{

    // Return the count
    return Math.Abs(countSetBit(R) -
                    countSetBit(L - 1));
}

// Driver Code
public static void Main(String[] args)
{
    // Given L and R
    int L = 3, R = 5;

    // Function Call
    Console.Write("Total set bit count is " +
                   countSetBits(L, R) +"\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function that counts the set bits
// from 0 to N
function countSetBit(n)
{
    var i = 0;

    // To store sum of set bits from 0 - N
    var ans = 0;

    // Until n >= to 2^i
    while ((1 << i) <= n) {

        // This k will get flipped after
        // 2^i iterations
        var k = 0;

        // Change is iterator from 2^i to 1
        var change = 1 << i;

        // This will loop from 0 to n for
        // every bit position
        for (var j = 0; j <= n; j++) {

            ans += k;

            if (change == 1) {

                // When change = 1 flip the bit
                k = !k;

                // Again set change to 2^i
                change = 1 << i;
            }
            else {
                change--;
            }
        }

        // Increment the position
        i++;
    }

    return ans;
}

// Function that counts the set bit
// in the range (L, R)
function countSetBits(L, R)
{

    // Return the count
    return Math.abs(countSetBit(R)
               - countSetBit(L - 1));
}

// Driver Code

// Given L and R
var L = 3, R = 5;

// Function Call
document.write( "Total set bit count is "
     + countSetBits(L, R) );

</script>
```

**Output:** 

```
Total set bit count is 5
```