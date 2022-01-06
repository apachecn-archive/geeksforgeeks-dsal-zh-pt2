# 从 N 个自然数中分离出偶数和奇数后，对第 k 个数中的设定位进行计数

> 原文:[https://www . geesforgeks . org/count-set-bits-in-kth-number-on-natural-numbers-separation-偶数和奇数/](https://www.geeksforgeeks.org/count-set-bits-in-the-kth-number-after-segregating-even-and-odd-from-n-natural-numbers/)

给定两个整数 **N** 和 **K** ，任务是在由范围**【1，N】**中的数字组成的奇偶序列中找到 **K <sup>第</sup>** 个数字中的设定位数。奇偶序列首先包含从 **1** 到 **N** 的所有奇数，然后包含从 **1** 到 **N** 的所有偶数。
**例:**

> **输入:** N = 8，K = 4
> **输出:** 3
> 顺序为 1、3、5、7、2、4、6、8。
> 第 4 个元素为 7，其中设置位的计数
> 为 3。
> **输入:** N = 18，K = 12
> **输出:** 2

**方法:**在[这篇](https://www.geeksforgeeks.org/find-kth-element-in-an-array-containing-odd-elements-first-and-then-even-elements/)文章中已经讨论了找到所需序列的第 k 个元素的方法。因此，找到所需的数字，然后使用 [__builtin_popcount()](https://www.geeksforgeeks.org/builtin-functions-gcc-compiler/) 找到其中设置的位数。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the kth element
// of the Odd-Even sequence
// of length n
int findK(int n, int k)
{
    int pos;

    // Finding the index from where the
    // even numbers will be stored
    if (n % 2 == 0) {
        pos = n / 2;
    }
    else {
        pos = (n / 2) + 1;
    }

    // Return the kth element
    if (k <= pos) {
        return (k * 2 - 1);
    }
    else

        return ((k - pos) * 2);
}

// Function to return the count of
// set bits in the kth number of the
// odd even sequence of length n
int countSetBits(int n, int k)
{

    // Required kth number
    int kth = findK(n, k);

    // Return the count of set bits
    return __builtin_popcount(kth);
}

// Driver code
int main()
{
    int n = 18, k = 12;

    cout << countSetBits(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the kth element
    // of the Odd-Even sequence
    // of length n
    static int findK(int n, int k)
    {
        int pos;

        // Finding the index from where the
        // even numbers will be stored
        if (n % 2 == 0)
        {
            pos = n / 2;
        }
        else
        {
            pos = (n / 2) + 1;
        }

        // Return the kth element
        if (k <= pos)
        {
            return (k * 2 - 1);
        }
        else
            return ((k - pos) * 2);
    }

    // Function to return the count of
    // set bits in the kth number of the
    // odd even sequence of length n
    static int countSetBits(int n, int k)
    {

        // Required kth number
        int kth = findK(n, k);

        int count = 0;

        while (kth > 0)
        {
            count += kth & 1;
            kth >>= 1;
        }

        // Return the count of set bits
        return count;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 18, k = 12;

        System.out.println(countSetBits(n, k));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the kth element
# of the Odd-Even sequence
# of length n
def findK(n, k) :

    # Finding the index from where the
    # even numbers will be stored
    if (n % 2 == 0) :
        pos = n // 2;
    else :
        pos = (n // 2) + 1;

    # Return the kth element
    if (k <= pos) :
        return (k * 2 - 1);
    else :
        return ((k - pos) * 2);

# Function to return the count of
# set bits in the kth number of the
# odd even sequence of length n
def countSetBits( n, k) :

    # Required kth number
    kth = findK(n, k);

    # Return the count of set bits
    return bin(kth).count('1');

# Driver code
if __name__ == "__main__" :
    n = 18; k = 12;
    print(countSetBits(n, k));

# This code is contributed by kanugargng
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the kth element
    // of the Odd-Even sequence
    // of length n
    static int findK(int n, int k)
    {
        int pos;

        // Finding the index from where the
        // even numbers will be stored
        if (n % 2 == 0)
        {
            pos = n / 2;
        }
        else
        {
            pos = (n / 2) + 1;
        }

        // Return the kth element
        if (k <= pos)
        {
            return (k * 2 - 1);
        }
        else
            return ((k - pos) * 2);
    }

    // Function to return the count of
    // set bits in the kth number of the
    // odd even sequence of length n
    static int countSetBits(int n, int k)
    {

        // Required kth number
        int kth = findK(n, k);

        int count = 0;

        while (kth > 0)
        {
            count += kth & 1;
            kth >>= 1;
        }

        // Return the count of set bits
        return count;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int n = 18, k = 12;

        Console.WriteLine(countSetBits(n, k));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the kth element 
    // of the Odd-Even sequence 
    // of length n 
    function findK(n, k) 
    { 
        let pos; 

        // Finding the index from where the 
        // even numbers will be stored 
        if (n % 2 == 0) 
        { 
            pos = parseInt(n / 2, 10); 
        } 
        else
        { 
            pos = parseInt(n / 2, 10) + 1; 
        } 

        // Return the kth element 
        if (k <= pos) 
        { 
            return (k * 2 - 1); 
        } 
        else
        {
            return ((k - pos) * 2);
        }
    } 

    // Function to return the count of 
    // set bits in the kth number of the 
    // odd even sequence of length n 
    function countSetBits(n, k) 
    { 
        // Required kth number 
        let kth = findK(n, k);

        let count = 0; 

        while (kth > 0) 
        { 
            count += kth & 1; 
            kth >>= 1; 
        } 

        // Return the count of set bits 
        return count;
    }

    let n = 18, k = 12; 
    document.write(countSetBits(n, k)); 

</script>
```

**Output:** 

```
2
```