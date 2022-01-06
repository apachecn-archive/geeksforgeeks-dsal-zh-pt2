# 两个数组的元素态和的数字组成一个新的数组

> 原文:[https://www . geeksforgeeks . org/以元素为单位将两个数组之和转换为新数组/](https://www.geeksforgeeks.org/digits-of-element-wise-sum-of-two-arrays-into-a-new-array/)

给定两个大小分别为 **M** 和 **N** 的正整数数组 **A** 和 **B** ，任务是每 **i = 0 到 min(M，N)** 将 **A[i] + B[i]** 推入一个新数组，最后打印新生成的数组。如果总和是一个两位数，那么将数字分成两个元素，也就是说，结果数组的每个元素都必须是一个位数。
**示例:**

> **输入:** A = {2，3，4，5}，B = {1，12，3}
> **输出:**3 1 5 7 5
> 2+1 = 3
> 3+12 = 15 = 1 5
> 4+3 = 7
> 5
> 因此得到的数组将是{3，1，5，7，5}
> **输入:** A = {23，5，2，7，80

**方法:**创建一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)来存储每次加法的结果。如果相加的是一个位数，那么就把这个数推进向量中，否则就把这个数分解成不同的位数，然后把数组中的位数一个一个推进去。最后打印矢量的内容。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
#include <vector>
using namespace std;

// Utility function to print the contents of the vector
void printVector(vector<int>& result)
{
    for (int i : result)
        cout << i << " ";
}

// Recursive function to separate the digits of a positive
// integer and add them to the given vector
void split_number(int num, vector<int>& result)
{
    if (num > 0) {
        split_number(num / 10, result);
        result.push_back(num % 10);
    }
}

// Function to add two arrays
void add(vector<int> a, vector<int> b)
{
    // Vector to store the output
    vector<int> result;
    int m = a.size(), n = b.size();

    // Loop till a or b runs out
    int i = 0;
    while (i < m && i < n) {

        // Get sum of next element from each array
        int sum = a[i] + b[i];

        // Separate the digits of sum and add them to
        // the resultant vector
        split_number(sum, result);
        i++;
    }

    // Process remaining elements of first vector, if any
    while (i < m) {
        split_number(a[i++], result);
    }

    // Process remaining elements of second vector, if any
    while (i < n) {
        split_number(b[i++], result);
    }

    // Print the resultant vector
    printVector(result);
}

// Driver code
int main()
{
    // input vectors
    vector<int> a = { 23, 5, 2, 7, 87 };
    vector<int> b = { 4, 67, 2, 8 };

    add(a, b);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

    // Utility function to print
    // the contents of the vector
    static void printVector(Vector<Integer> result)
    {
        for (int i : result)
        {
            System.out.print(i + " ");
        }
    }

    // Recursive function to separate
    // the digits of a positive integer
    // and add them to the given vector
    static void split_number(int num, Vector<Integer> result)
    {
        if (num > 0)
        {
            split_number(num / 10, result);
            result.add(num % 10);
        }
    }

    // Function to add two arrays
    static void add(Vector<Integer> a, Vector<Integer> b)
    {
        // Vector to store the output
        Vector<Integer> result = new Vector<Integer>();
        int m = a.size(), n = b.size();

        // Loop till a or b runs out
        int i = 0;
        while (i < m && i < n)
        {

            // Get sum of next element from each array
            int sum = a.get(i) + b.get(i);

            // Separate the digits of sum and add them to
            // the resultant vector
            split_number(sum, result);
            i++;
        }

        // Process remaining elements
        // of first vector, if any
        while (i < m)
        {
            split_number(a.get(i++), result);
        }

        // Process remaining elements
        // of second vector, if any
        while (i < n)
        {
            split_number(b.get(i++), result);
        }

        // Print the resultant vector
        printVector(result);
    }

    // Driver code
    public static void main(String[] args)
    {
        // input vectors
        int[] arr1 = {23, 5, 2, 7, 87};
        Vector<Integer> a = new Vector<>();
        for(Integer i:arr1)
            a.add(i);

        int[] arr2 = {4, 67, 2, 8};
        Vector<Integer> b = new Vector<Integer>();
        for(Integer i:arr2)
            b.add(i);

        add(a, b);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Utility function to print the
# contents of the list
def printVector(result):

    for i in result:
        print(i, end = " ")

# Recursive function to separate the
# digits of a positive integer and
# add them to the given list
def split_number(num, result):

    if num > 0:
        split_number(num // 10, result)
        result.append(num % 10)

# Function to add two lists
def add(a, b):

    # List to store the output
    result = []
    m, n = len(a), len(b)

    # Loop till a or b runs out
    i = 0
    while i < m and i < n:

        # Get sum of next element from
        # each array
        sum = a[i] + b[i]

        # Separate the digits of sum and
        # add them to the resultant list
        split_number(sum, result)
        i += 1

    # Process remaining elements of
    # first list, if any
    while i < m:
        split_number(a[i], result)
        i += 1

    # Process remaining elements of
    # second list, if any
    while i < n:
        split_number(b[i], result)
        i += 1   

    # Print the resultant list
    printVector(result)

# Driver Code
if __name__ == "__main__":

    # input lists
    a = [23, 5, 2, 7, 87]
    b = [4, 67, 2, 8]

    add(a, b)

# This code is contributed by rituraj_jain
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{

    // Utility function to print
    // the contents of the vector
    static void printVector(List<int> result)
    {
        foreach (int i in result)
        {
            Console.Write(i + " ");
        }
    }

    // Recursive function to separate
    // the digits of a positive integer
    // and add them to the given vector
    static void split_number(int num, List<int> result)
    {
        if (num > 0)
        {
            split_number(num / 10, result);
            result.Add(num % 10);
        }
    }

    // Function to add two arrays
    static void add(List<int> a, List<int> b)
    {
        // Vector to store the output
        List<int> result = new List<int>();
        int m = a.Count, n = b.Count;

        // Loop till a or b runs out
        int i = 0;
        while (i < m && i < n)
        {

            // Get sum of next element from each array
            int sum = a[i] + b[i];

            // Separate the digits of sum and add them to
            // the resultant vector
            split_number(sum, result);
            i++;
        }

        // Process remaining elements
        // of first vector, if any
        while (i < m)
        {
            split_number(a[i++], result);
        }

        // Process remaining elements
        // of second vector, if any
        while (i < n)
        {
            split_number(b[i++], result);
        }

        // Print the resultant vector
        printVector(result);
    }

    // Driver code
    public static void Main(String[] args)
    {
        // input vectors
        int[] arr1 = {23, 5, 2, 7, 87};
        List<int> a = new List<int>();
        foreach(int i in arr1)
            a.Add(i);

        int[] arr2 = {4, 67, 2, 8};
        List<int> b = new List<int>();
        foreach(int i in arr2)
            b.Add(i);

        add(a, b);
    }
}

// This code is contributed by princiraj1992
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Utility function to print the contents of the vector
function printVector(result)
{
    for (let i = 0; i < result.length; i++)
        document.write(result[i] + " ");
}

// Recursive function to separate the digits of a positive
// integer and add them to the given vector
function split_number(num, result)
{
    if (num > 0) {
        split_number(parseInt(num / 10), result);
        result.push(num % 10);
    }
}

// Function to add two arrays
function add(a, b)
{
    // Vector to store the output
    let result = [];
    let m = a.length, n = b.length;

    // Loop till a or b runs out
    let i = 0;
    while (i < m && i < n) {

        // Get sum of next element from each array
        let sum = a[i] + b[i];

        // Separate the digits of sum and add them to
        // the resultant vector
        split_number(sum, result);
        i++;
    }

    // Process remaining elements of first vector, if any
    while (i < m) {
        split_number(a[i++], result);
    }

    // Process remaining elements of second vector, if any
    while (i < n) {
        split_number(b[i++], result);
    }

    // Print the resultant vector
    printVector(result);
}

// Driver code
// input vectors
let a = [ 23, 5, 2, 7, 87 ];
let b = [ 4, 67, 2, 8 ];

add(a, b);

// This code is contributed by souravmahato348.
</script>
```

**Output:** 

```
2 7 7 2 4 1 5 8 7
```

**时间复杂度:** O(max(m，n))