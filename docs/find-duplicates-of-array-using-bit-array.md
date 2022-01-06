# 使用位数组找到数组的副本

> 原文:[https://www . geeksforgeeks . org/find-使用位数组的数组副本/](https://www.geeksforgeeks.org/find-duplicates-of-array-using-bit-array/)

你有一个 N 个数的数组，其中 N 最多是 32，000。数组可能有重复的条目，并且您不知道 N 是什么。只有 4 千字节的可用内存，如何打印数组中所有重复的元素？。

**示例:**

```
Input : arr[] = {1, 5, 1, 10, 12, 10}
Output : 1 10
1 and 10 appear more than once in given
array.

Input : arr[] = {50, 40, 50}
Output : 50

```

问于:亚马逊

我们有 4 千字节的内存，这意味着我们最多可以寻址 8 * 4 * 2 <sup>10</sup> 位。注意 32 * 2 <sup>10</sup> 位大于 32000。我们可以创建一个 32000 位的位，其中每个位代表一个整数。

注意:如果需要创建 32000 位以上的位，那么可以轻松创建 32000 以上的位；

使用这个位向量，我们可以迭代数组，通过将位 v 设置为 1 来标记每个元素 v。当我们遇到重复的元素时，我们会打印它。

下面是这个想法的实现。

## C++

```
// C++ program to print all Duplicates in array
#include <bits/stdc++.h>
using namespace std;

// A class to represent an array of bits using
// array of integers
class BitArray
{
    int *arr;

    public:
    BitArray() {}

    // Constructor
    BitArray(int n)
    {
        // Divide by 32\. To store n bits, we need
        // n/32 + 1 integers (Assuming int is stored
        // using 32 bits)
        arr = new int[(n >> 5) + 1];
    }

    // Get value of a bit at given position
    bool get(int pos)
    {
        // Divide by 32 to find position of
        // integer.
        int index = (pos >> 5);

        // Now find bit number in arr[index]
        int bitNo = (pos & 0x1F);

        // Find value of given bit number in
        // arr[index]
        return (arr[index] & (1 << bitNo)) != 0;
    }

    // Sets a bit at given position
    void set(int pos)
    {
        // Find index of bit position
        int index = (pos >> 5);

        // Set bit number in arr[index]
        int bitNo = (pos & 0x1F);
        arr[index] |= (1 << bitNo);
    }

    // Main function to print all Duplicates
    void checkDuplicates(int arr[], int n)
    {
        // create a bit with 32000 bits
        BitArray ba = BitArray(320000);

        // Traverse array elements
        for (int i = 0; i < n; i++)
        {
            // Index in bit array
            int num = arr[i];

            // If num is already present in bit array
            if (ba.get(num))
                cout << num << " ";

            // Else insert num
            else
                ba.set(num);
        }
    }
};

// Driver code
int main()
{
    int arr[] = {1, 5, 1, 10, 12, 10};
    int n = sizeof(arr) / sizeof(arr[0]);
    BitArray obj = BitArray();
    obj.checkDuplicates(arr, n);
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all Duplicates in array
import java.util.*;
import java.lang.*;
import java.io.*;

// A class to represent array of bits using
// array of integers
class BitArray
{
    int[] arr;

    // Constructor
    public BitArray(int n)
    {
        // Divide by 32\. To store n bits, we need
        // n/32 + 1 integers (Assuming int is stored
        // using 32 bits)
        arr = new int[(n>>5) + 1];
    }

    // Get value of a bit at given position
    boolean get(int pos)
    {
        // Divide by 32 to find position of
        // integer.
        int index = (pos >> 5);

        // Now find bit number in arr[index]
        int bitNo  = (pos & 0x1F);

        // Find value of given bit number in
        // arr[index]
        return (arr[index] & (1 << bitNo)) != 0;
    }

    // Sets a bit at given position
    void set(int pos)
    {
        // Find index of bit position
        int index = (pos >> 5);

        // Set bit number in arr[index]
        int bitNo = (pos & 0x1F);
        arr[index] |= (1 << bitNo);
    }

    // Main function to print all Duplicates
    static void checkDuplicates(int[] arr)
    {
        // create a bit with 32000 bits
        BitArray ba = new BitArray(320000);

        // Traverse array elements
        for (int i=0; i<arr.length; i++)
        {
            // Index in bit array
            int num  = arr[i] - 1;

            // If num is already present in bit array
            if (ba.get(num))
                System.out.print(num +" ");

            // Else insert num
            else
                ba.set(num);
        }
    }

    // Driver code
    public static void main(String[] args) throws
                              java.lang.Exception
    {
        int[] arr = {1, 5, 1, 10, 12, 10};
        checkDuplicates(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program to print all Duplicates in array

# A class to represent array of bits using
# array of integers
class BitArray:

    # Constructor
    def __init__(self, n):

        # Divide by 32\. To store n bits, we need
        # n/32 + 1 integers (Assuming int is stored
        # using 32 bits)
        self.arr = [0] * ((n >> 5) + 1)

    # Get value of a bit at given position
    def get(self, pos):

        # Divide by 32 to find position of
        # integer.
        self.index = pos >> 5

        # Now find bit number in arr[index]
        self.bitNo = pos & 0x1F

        # Find value of given bit number in
        # arr[index]
        return (self.arr[self.index] & 
                   (1 << self.bitNo)) != 0

    # Sets a bit at given position
    def set(self, pos):

        # Find index of bit position
        self.index = pos >> 5

        # Set bit number in arr[index]
        self.bitNo = pos & 0x1F
        self.arr[self.index] |= (1 << self.bitNo)

# Main function to print all Duplicates
def checkDuplicates(arr):

    # create a bit with 32000 bits
    ba = BitArray(320000)

    # Traverse array elements
    for i in range(len(arr)):

        # Index in bit array
        num = arr[i]

        # If num is already present in bit array
        if ba.get(num):
            print(num, end = " ")

        # Else insert num
        else:
            ba.set(num)

# Driver Code
if __name__ == "__main__":
    arr = [1, 5, 1, 10, 12, 10]
    checkDuplicates(arr)

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to print all Duplicates in array

// A class to represent array of bits using 
// array of integers 
using System;

class BitArray 
{ 
    int[] arr; 

    // Constructor 
    public BitArray(int n) 
    { 
        // Divide by 32\. To store n bits, we need 
        // n/32 + 1 integers (Assuming int is stored 
        // using 32 bits) 
        arr = new int[(int)(n >> 5) + 1]; 
    } 

    // Get value of a bit at given position 
    bool get(int pos) 
    { 
        // Divide by 32 to find position of 
        // integer. 
        int index = (pos >> 5); 

        // Now find bit number in arr[index] 
        int bitNo = (pos & 0x1F); 

        // Find value of given bit number in 
        // arr[index] 
        return (arr[index] & (1 << bitNo)) != 0; 
    } 

    // Sets a bit at given position 
    void set(int pos) 
    { 
        // Find index of bit position 
        int index = (pos >> 5); 

        // Set bit number in arr[index] 
        int bitNo = (pos & 0x1F); 
        arr[index] |= (1 << bitNo); 
    } 

    // Main function to print all Duplicates 
    static void checkDuplicates(int[] arr) 
    { 
        // create a bit with 32000 bits 
        BitArray ba = new BitArray(320000); 

        // Traverse array elements 
        for (int i = 0; i < arr.Length; i++) 
        { 
            // Index in bit array 
            int num = arr[i]; 

            // If num is already present in bit array 
            if (ba.get(num)) 
                Console.Write(num + " "); 

            // Else insert num 
            else
                ba.set(num); 
        } 
    } 

    // Driver code 
    public static void Main()
    { 
        int[] arr = {1, 5, 1, 10, 12, 10}; 
        checkDuplicates(arr); 
    } 
} 

// This code is contributed by Rajput-Ji
```

**Output:**

```
1 10 

```

本文由 Somesh Awasthi 先生供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。