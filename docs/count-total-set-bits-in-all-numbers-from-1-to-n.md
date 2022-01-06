# 从 1 到 n 对所有数字中的总设定位进行计数

> 原文:[https://www . geesforgeks . org/count-total-set-bit-in-all-numbers-from-1-n/](https://www.geeksforgeeks.org/count-total-set-bits-in-all-numbers-from-1-to-n/)

给定一个正整数 n，计算从 1 到 n 的所有数字的二进制表示中的总位数。

**示例:**

```
Input: n = 3
Output:  4

Input: n = 6
Output: 9

Input: n = 7
Output: 12

Input: n = 8
Output: 13
```

来源:亚马逊面试问题

**方法 1(简单)**
一个简单的解决方案是运行一个从 1 到 n 的循环，并对从 1 到 n 的所有数字中的设置位计数求和

## C++

```
// A simple program to count set bits
// in all numbers from 1 to n.
#include <iostream>
using namespace std;

// A utility function to count set bits
// in a number x
unsigned int countSetBitsUtil(unsigned int x);

// Returns count of set bits present in all
// numbers from 1 to n
unsigned int countSetBits(unsigned int n)
{
    int bitCount = 0; // initialize the result

    for (int i = 1; i <= n; i++)
        bitCount += countSetBitsUtil(i);

    return bitCount;
}

// A utility function to count set bits
// in a number x
unsigned int countSetBitsUtil(unsigned int x)
{
    if (x <= 0)
        return 0;
    return (x % 2 == 0 ? 0 : 1) + countSetBitsUtil(x / 2);
}

// Driver program to test above functions
int main()
{
    int n = 4;
    cout <<"Total set bit count is " <<countSetBits(n);
    return 0;
}

// This code is contributed by shivanisinghss2110.
```

## C

```
// A simple program to count set bits
// in all numbers from 1 to n.
#include <stdio.h>

// A utility function to count set bits
// in a number x
unsigned int countSetBitsUtil(unsigned int x);

// Returns count of set bits present in all
// numbers from 1 to n
unsigned int countSetBits(unsigned int n)
{
    int bitCount = 0; // initialize the result

    for (int i = 1; i <= n; i++)
        bitCount += countSetBitsUtil(i);

    return bitCount;
}

// A utility function to count set bits
// in a number x
unsigned int countSetBitsUtil(unsigned int x)
{
    if (x <= 0)
        return 0;
    return (x % 2 == 0 ? 0 : 1) + countSetBitsUtil(x / 2);
}

// Driver program to test above functions
int main()
{
    int n = 4;
    printf("Total set bit count is %d", countSetBits(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple program to count set bits
// in all numbers from 1 to n.

class GFG{

    // Returns count of set bits present
    //  in all numbers from 1 to n
    static int countSetBits( int n)
    {
        // initialize the result
        int bitCount = 0;

        for (int i = 1; i <= n; i++)
            bitCount += countSetBitsUtil(i);

        return bitCount;
    }

    // A utility function to count set bits
    // in a number x
    static int countSetBitsUtil( int x)
    {
        if (x <= 0)
            return 0;
        return (x % 2 == 0 ? 0 : 1) +
               countSetBitsUtil(x / 2);
    }

    // Driver program
    public static void main(String[] args)
    {
        int n = 4;
        System.out.print("Total set bit count is ");
        System.out.print(countSetBits(n));
    }
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# A simple program to count set bits
# in all numbers from 1 to n.

# Returns count of set bits present in all
# numbers from 1 to n
def countSetBits(n):

    # initialize the result
    bitCount = 0

    for i in range(1, n + 1):
        bitCount += countSetBitsUtil(i)

    return bitCount

# A utility function to count set bits
# in a number x
def countSetBitsUtil(x):

    if (x <= 0):
        return 0
    return (0 if int(x % 2) == 0 else 1) +  countSetBitsUtil(int(x / 2))

# Driver program
if __name__=='__main__':
    n = 4
    print("Total set bit count is", countSetBits(n))

# This code is contributed by
# Smitha Dinesh Semwal   
```

## C#

```
// A simple C# program to count set bits
// in all numbers from 1 to n.
using System;

class GFG
{
    // Returns count of set bits present
    // in all numbers from 1 to n
    static int countSetBits( int n)
    {
        // initialize the result
        int bitCount = 0;

        for (int i = 1; i <= n; i++)
            bitCount += countSetBitsUtil(i);

        return bitCount;
    }

    // A utility function to count set bits
    // in a number x
    static int countSetBitsUtil( int x)
    {
        if (x <= 0)
            return 0;
        return (x % 2 == 0 ? 0 : 1) +
            countSetBitsUtil(x / 2);
    }

    // Driver program
    public static void Main()
    {
        int n = 4;
        Console.Write("Total set bit count is ");
        Console.Write(countSetBits(n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple program to count set bits
// in all numbers from 1 to n.

// Returns count of set bits present
// in all numbers from 1 to n
function countSetBits($n)
{
    $bitCount = 0; // initialize the result

    for ($i = 1; $i <= $n; $i++)
        $bitCount += countSetBitsUtil($i);

    return $bitCount;
}

// A utility function to count
// set bits in a number x
function countSetBitsUtil($x)
{
    if ($x <= 0)
        return 0;
    return ($x % 2 == 0 ? 0 : 1) +
            countSetBitsUtil($x / 2);
}

// Driver Code
$n = 4;
echo "Total set bit count is " .
               countSetBits($n);

// This code is contributed by ChitraNayal
?>
```

## java 描述语言

```
<script>
// A simple program to count set bits
// in all numbers from 1 to n.

    // Returns count of set bits present
    //  in all numbers from 1 to n
    function countSetBits(n)
    {
        // initialize the result
        let bitCount = 0;
        for (let i = 1; i <= n; i++)
        {
            bitCount += countSetBitsUtil(i);
        }
        return bitCount;
    }

    // A utility function to count set bits
    // in a number x
    function countSetBitsUtil(x)
    {
        if (x <= 0)
        {
            return 0;
        }
        return (x % 2 == 0 ? 0 : 1) + countSetBitsUtil(Math.floor(x/2));
    }

    // Driver program
    let n = 4;
    document.write("Total set bit count is ");
    document.write(countSetBits(n));

    // This code is contributed by rag2127
</script>
```

**Output**

```
Total set bit count is 5
```

时间复杂性

**方法 2(比方法 1 简单有效)**
如果我们在距离 I 处从最右侧观察比特，则比特在垂直序列中的 2^i 位置之后被反转。
例如 n = 5；
0 = 0000
1 = 0001
2 = 0010
3 = 0011
4 = 0100
5 = 0101
观察最右边的位(i = 0)这些位在(2^0 = 1)
之后翻转观察第三个最右边的位(i = 2)这些位在(2^2 = 4)
之后翻转，因此我们可以以垂直方式计数位，使得在最右边的位置

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function which counts set bits from 0 to n
int countSetBits(int n)
{
    int i = 0;

    // ans store sum of set bits from 0 to n 
    int ans = 0;

    // while n greater than equal to 2^i
    while ((1 << i) <= n) {

        // This k will get flipped after
        // 2^i iterations
        bool k = 0;

        // change is iterator from 2^i to 1
        int change = 1 << i;

        // This will loop from 0 to n for
        // every bit position
        for (int j = 0; j <= n; j++) {

            ans += k;

            if (change == 1) {
                k = !k; // When change = 1 flip the bit
                change = 1 << i; // again set change to 2^i
            }
            else {
                change--;
            }
        }

        // increment the position
        i++;
    }

    return ans;
}

// Main Function
int main()
{
    int n = 17;
    cout << countSetBits(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
public class GFG {

    // Function which counts set bits from 0 to n
    static int countSetBits(int n)
    {
        int i = 0;

        // ans store sum of set bits from 0 to n
        int ans = 0;

        // while n greater than equal to 2^i
        while ((1 << i) <= n) {

            // This k will get flipped after
            // 2^i iterations
            boolean k = false;

            // change is iterator from 2^i to 1
            int change = 1 << i;

            // This will loop from 0 to n for
            // every bit position
            for (int j = 0; j <= n; j++) {

                if (k == true)
                    ans += 1;
                else
                    ans += 0;

                if (change == 1) {

                    // When change = 1 flip the bit
                    k = !k;

                    // again set change to 2^i
                    change = 1 << i;
                }
                else {
                    change--;
                }
            }

            // increment the position
            i++;
        }

        return ans;
    }

    // Driver program
    public static void main(String[] args)
    {
        int n = 17;

        System.out.println(countSetBits(n));
    }
}

// This code is contributed by Sam007.
```

## 蟒蛇 3

```
# Function which counts set bits from 0 to n
def countSetBits(n) :
    i = 0

    # ans store sum of set bits from 0 to n 
    ans = 0

    # while n greater than equal to 2^i
    while ((1 << i) <= n) :

        # This k will get flipped after 
        # 2^i iterations
        k = 0

        # change is iterator from 2^i to 1
        change = 1 << i

        # This will loop from 0 to n for
        # every bit position
        for j in range(0, n+1) :
            ans += k

            if change == 1 :

                #  When change = 1 flip the bit
                k = not k

                # again set change to 2^i
                change = 1 << i

            else :
                change -= 1

        # increment the position
        i += 1

    return ans

# Driver code
if __name__ == "__main__" :

    n = 17
    print(countSetBits(n))

# This code is contributed by ANKITRAI1
```

## C#

```
using System;

class GFG
{
    static int countSetBits(int n)
    {
        int i = 0;

        // ans store sum of set bits from 0 to n
        int ans = 0;

        // while n greater than equal to 2^i
        while ((1 << i) <= n) {

            // This k will get flipped after
            // 2^i iterations
            bool k = false;

            // change is iterator from 2^i to 1
            int change = 1 << i;

            // This will loop from 0 to n for
            // every bit position
            for (int j = 0; j <= n; j++) {

                if (k == true)
                    ans += 1;
                else
                    ans += 0;

                if (change == 1) {

                    // When change = 1 flip the bit
                    k = !k;

                    // again set change to 2^i
                    change = 1 << i;
                }
                else {
                    change--;
                }
            }

            // increment the position
            i++;
        }

        return ans;
    }

    // Driver program
    static void Main()
    {
        int n = 17;
        Console.Write(countSetBits(n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Function which counts
// set bits from 0 to n
function countSetBits($n)
{
    $i = 0;

    // ans store sum of set
    // bits from 0 to n
    $ans = 0;

    // while n greater than
    // equal to 2^i
    while ((1 << $i) <= $n)
    {

        // This k will get flipped
        // after 2^i iterations
        $k = 0;

        // change is iterator
        // from 2^i to 1
        $change = 1 << $i;

        // This will loop from 0 to n
        // for every bit position
        for ($j = 0; $j <= $n; $j++)
        {
            $ans += $k;

            if ($change == 1)
            {
                // When change = 1 flip
                // the bit
                $k = !$k;

                // again set change to 2^i
                $change = 1 << $i;
            }
            else
            {
                $change--;
            }
        }

        // increment the position
        $i++;
    }

    return $ans;
}

// Driver code
$n = 17;
echo(countSetBits($n));

// This code is contributed by Smitha
?>
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function which counts set bits from 0 to n
function countSetBits(n)
{
    let i = 0;

    // ans store sum of set bits from 0 to n 
    let ans = 0;

    // while n greater than equal to 2^i
    while ((1 << i) <= n) {

        // This k will get flipped after
        // 2^i iterations
        let k = 0;

        // change is iterator from 2^i to 1
        let change = 1 << i;

        // This will loop from 0 to n for
        // every bit position
        for (let j = 0; j <= n; j++) {

            ans += k;

            if (change == 1) {
                // When change = 1 flip the bit
                k = !k;
                // again set change to 2^i
                change = 1 << i;
            }
            else {
                change--;
            }
        }

        // increment the position
        i++;
    }

    return ans;
}

// Driver Code

    let n = 17;
    document.write(countSetBits(n));

</script>
```

**Output**

```
35
```

时间复杂度:O(k*n)
其中 k =代表数字 n 的位数
k < = 64

**方法 3(棘手)**
如果输入的数字是 2^b -1 的形式，例如 1、3、7、15..等等，设置的位数是 b * 2^(b-1).这是因为对于所有的数字 0 到(2^b)-1，如果你补充和翻转列表，你会得到相同的列表(一半的位是开的，一半是关的)。
如果数字没有全部设置位，那么某个位置 m 就是最左边设置位的位置。该位置的设置位数为 n –( 1<<m)+1。剩余的设置位分为两部分:
1)在(m-1)位置的位向下到最左边的位变为 0 的点，以及
2)在该点之下的 2^(m-1 数，这是上面的封闭形式。
一个简单的方法是考虑数字 6:

```
0|0 0
0|0 1
0|1 0
0|1 1
-|--
1|0 0
1|0 1
1|1 0
```

最左边的设置位在位置 2(位置被认为是从 0 开始)。如果我们屏蔽掉它，剩下的就是 2(最后一行右边的“1 0”)。)所以第二个位置(左下框)的位数是 3(即 2 + 1)。从 0-3(右上框)设置的位是 2*2^(2-1) = 4。右下角的框是我们还没有统计的剩余位，是所有数字的设置位数，最多为 2(右下角框中最后一个条目的值)，可以递归计算。

## C++

```
#include <bits/stdc++.h>

// A O(Logn) complexity program to count
// set bits in all numbers from 1 to n
using namespace std;

/* Returns position of leftmost set bit.
The rightmost position is considered
as 0 */
unsigned int getLeftmostBit(int n)
{
    int m = 0;
    while (n > 1)
    {
        n = n >> 1;
        m++;
    }
    return m;
}

/* Given the position of previous leftmost
set bit in n (or an upper bound on
leftmost position) returns the new
position of leftmost set bit in n */
unsigned int getNextLeftmostBit(int n, int m)
{
    unsigned int temp = 1 << m;
    while (n < temp) {
        temp = temp >> 1;
        m--;
    }
    return m;
}

// The main recursive function used by countSetBits()
unsigned int _countSetBits(unsigned int n, int m);

// Returns count of set bits present in
// all numbers from 1 to n
unsigned int countSetBits(unsigned int n)
{
    // Get the position of leftmost set
    // bit in n. This will be used as an
    // upper bound for next set bit function
    int m = getLeftmostBit(n);

    // Use the position
    return _countSetBits(n, m);
}

unsigned int _countSetBits(unsigned int n, int m)
{
    // Base Case: if n is 0, then set bit
    // count is 0
    if (n == 0)
        return 0;

    /* get position of next leftmost set bit */
    m = getNextLeftmostBit(n, m);

    // If n is of the form 2^x-1, i.e., if n
    // is like 1, 3, 7, 15, 31, .. etc,
    // then we are done.
    // Since positions are considered starting
    // from 0, 1 is added to m
    if (n == ((unsigned int)1 << (m + 1)) - 1)
        return (unsigned int)(m + 1) * (1 << m);

    // update n for next recursive call
    n = n - (1 << m);
    return (n + 1) + countSetBits(n) + m * (1 << (m - 1));
}

// Driver code
int main()
{
    int n = 17;
    cout<<"Total set bit count is "<< countSetBits(n);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// A O(Logn) complexity program to count
// set bits in all numbers from 1 to n
#include <stdio.h>

/* Returns position of leftmost set bit.
   The rightmost position is considered
   as 0 */
unsigned int getLeftmostBit(int n)
{
    int m = 0;
    while (n > 1) {
        n = n >> 1;
        m++;
    }
    return m;
}

/* Given the position of previous leftmost
   set bit in n (or an upper bound on
   leftmost position) returns the new
   position of leftmost set bit in n  */
unsigned int getNextLeftmostBit(int n, int m)
{
    unsigned int temp = 1 << m;
    while (n < temp) {
        temp = temp >> 1;
        m--;
    }
    return m;
}

// The main recursive function used by countSetBits()
unsigned int _countSetBits(unsigned int n, int m);

// Returns count of set bits present in
// all numbers from 1 to n
unsigned int countSetBits(unsigned int n)
{
    // Get the position of leftmost set
    // bit in n. This will be used as an
    // upper bound for next set bit function
    int m = getLeftmostBit(n);

    // Use the position
    return _countSetBits(n, m);
}

unsigned int _countSetBits(unsigned int n, int m)
{
    // Base Case: if n is 0, then set bit
    // count is 0
    if (n == 0)
        return 0;

    /* get position of next leftmost set bit */
    m = getNextLeftmostBit(n, m);

    // If n is of the form 2^x-1, i.e., if n
    // is like 1, 3, 7, 15, 31, .. etc,
    // then we are done.
    // Since positions are considered starting
    // from 0, 1 is added to m
    if (n == ((unsigned int)1 << (m + 1)) - 1)
        return (unsigned int)(m + 1) * (1 << m);

    // update n for next recursive call
    n = n - (1 << m);
    return (n + 1) + countSetBits(n) + m * (1 << (m - 1));
}

// Driver program to test above functions
int main()
{
    int n = 17;
    printf("Total set bit count is %d", countSetBits(n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java A O(Logn) complexity program to count
// set bits in all numbers from 1 to n
import java.io.*;

class GFG
{

/* Returns position of leftmost set bit.
The rightmost position is considered
as 0 */
static int getLeftmostBit(int n)
{
    int m = 0;
    while (n > 1)
    {
        n = n >> 1;
        m++;
    }
    return m;
}

/* Given the position of previous leftmost
set bit in n (or an upper bound on
leftmost position) returns the new
position of leftmost set bit in n */
static int getNextLeftmostBit(int n, int m)
{
    int temp = 1 << m;
    while (n < temp)
    {
        temp = temp >> 1;
        m--;
    }
    return m;
}

// The main recursive function used by countSetBits()
// Returns count of set bits present in
// all numbers from 1 to n

static int countSetBits(int n)
{
    // Get the position of leftmost set
    // bit in n. This will be used as an
    // upper bound for next set bit function
    int m = getLeftmostBit(n);

    // Use the position
    return countSetBits(n, m);
}

static int countSetBits( int n, int m)
{
    // Base Case: if n is 0, then set bit
    // count is 0
    if (n == 0)
        return 0;

    /* get position of next leftmost set bit */
    m = getNextLeftmostBit(n, m);

    // If n is of the form 2^x-1, i.e., if n
    // is like 1, 3, 7, 15, 31, .. etc,
    // then we are done.
    // Since positions are considered starting
    // from 0, 1 is added to m
    if (n == ((int)1 << (m + 1)) - 1)
        return (int)(m + 1) * (1 << m);

    // update n for next recursive call
    n = n - (1 << m);
    return (n + 1) + countSetBits(n) + m * (1 << (m - 1));
}

// Driver code
public static void main (String[] args)
{

    int n = 17;
    System.out.println ("Total set bit count is " + countSetBits(n));
}
}

// This code is contributed by ajit..
```

## 蟒蛇 3

```
# A O(Logn) complexity program to count
# set bits in all numbers from 1 to n

"""
/* Returns position of leftmost set bit.
The rightmost position is considered
as 0 */
"""
def getLeftmostBit(n):

    m = 0
    while (n > 1) :

        n = n >> 1
        m += 1

    return m

"""
/* Given the position of previous leftmost
set bit in n (or an upper bound on
leftmost position) returns the new
position of leftmost set bit in n */
"""
def getNextLeftmostBit(n, m) :

    temp = 1 << m
    while (n < temp) :
        temp = temp >> 1
        m -= 1

    return m

# The main recursive function used by countSetBits()
# def _countSetBits(n, m)

# Returns count of set bits present in
# all numbers from 1 to n
def countSetBits(n) :

    # Get the position of leftmost set
    # bit in n. This will be used as an
    # upper bound for next set bit function
    m = getLeftmostBit(n)

    # Use the position
    return _countSetBits(n, m)

def _countSetBits(n, m) :

    # Base Case: if n is 0, then set bit
    # count is 0
    if (n == 0) :
        return 0

    # /* get position of next leftmost set bit */
    m = getNextLeftmostBit(n, m)

    # If n is of the form 2^x-1, i.e., if n
    # is like 1, 3, 7, 15, 31, .. etc,
    # then we are done.
    # Since positions are considered starting
    # from 0, 1 is added to m
    if (n == (1 << (m + 1)) - 1) :
        return ((m + 1) * (1 << m))

    # update n for next recursive call
    n = n - (1 << m)
    return (n + 1) + countSetBits(n) + m * (1 << (m - 1))

# Driver code
n = 17
print("Total set bit count is", countSetBits(n))

# This code is contributed by rathbhupendra
```

## C#

```
// C# A O(Logn) complexity program to count
// set bits in all numbers from 1 to n
using System;

class GFG
{

/* Returns position of leftmost set bit.
The rightmost position is considered
as 0 */
static int getLeftmostBit(int n)
{
    int m = 0;
    while (n > 1)
    {
        n = n >> 1;
        m++;
    }
    return m;
}

/* Given the position of previous leftmost
set bit in n (or an upper bound on
leftmost position) returns the new
position of leftmost set bit in n */
static int getNextLeftmostBit(int n, int m)
{
    int temp = 1 << m;
    while (n < temp)
    {
        temp = temp >> 1;
        m--;
    }
    return m;
}

// The main recursive function used by countSetBits()
// Returns count of set bits present in
// all numbers from 1 to n
static int countSetBits(int n)
{
    // Get the position of leftmost set
    // bit in n. This will be used as an
    // upper bound for next set bit function
    int m = getLeftmostBit(n);

    // Use the position
    return countSetBits(n, m);
}

static int countSetBits( int n, int m)
{
    // Base Case: if n is 0,
    // then set bit count is 0
    if (n == 0)
        return 0;

    /* get position of next leftmost set bit */
    m = getNextLeftmostBit(n, m);

    // If n is of the form 2^x-1, i.e., if n
    // is like 1, 3, 7, 15, 31, .. etc,
    // then we are done.
    // Since positions are considered starting
    // from 0, 1 is added to m
    if (n == ((int)1 << (m + 1)) - 1)
        return (int)(m + 1) * (1 << m);

    // update n for next recursive call
    n = n - (1 << m);
    return (n + 1) + countSetBits(n) +
                  m * (1 << (m - 1));
}

// Driver code
static public void Main ()
{
    int n = 17;
    Console.Write("Total set bit count is " +
                            countSetBits(n));
}
}

// This code is contributed by Tushil.
```

## java 描述语言

```
<script>

// JavaScript A O(Logn) complexity program to count
// set bits in all numbers from 1 to n

/* Returns position of leftmost set bit.
The rightmost position is considered
as 0 */
function getLeftmostBit(n)
{
    let m = 0;
    while (n > 1)
    {
        n = n >> 1;
        m++;
    }
    return m;
}

/* Given the position of previous leftmost
set bit in n (or an upper bound on
leftmost position) returns the new
position of leftmost set bit in n */
function getNextLeftmostBit(n,m)
{
    let temp = 1 << m;
    while (n < temp)
    {
        temp = temp >> 1;
        m--;
    }
    return m;
}

// The main recursive function used by countSetBits()
// Returns count of set bits present in
// all numbers from 1 to n
function countSetBits(n)
{
    // Get the position of leftmost set
    // bit in n. This will be used as an
    // upper bound for next set bit function
    let m = getLeftmostBit(n);

    // Use the position
    return _countSetBits(n, m);
}

function _countSetBits(n,m)
{
    // Base Case: if n is 0, then set bit
    // count is 0
    if (n == 0)
        return 0;

    /* get position of next leftmost set bit */
    m = getNextLeftmostBit(n, m);

    // If n is of the form 2^x-1, i.e., if n
    // is like 1, 3, 7, 15, 31, .. etc,
    // then we are done.
    // Since positions are considered starting
    // from 0, 1 is added to m
    if (n == (1 << (m + 1)) - 1)
        return (m + 1) * (1 << m);

    // update n for next recursive call
    n = n - (1 << m);
    return (n + 1) + countSetBits(n) + m * (1 << (m - 1));
}

// Driver code
let n = 17;
document.write("Total set bit count is " + countSetBits(n));

// This code is contributed by ab2127

</script>
```

**Output**

```
Total set bit count is 35
```