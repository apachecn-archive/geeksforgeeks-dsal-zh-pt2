# 按位“与”等于零的三倍计数

> 原文:[https://www . geesforgeks . org/count-triples-with-bitwise-and-equal-zero/](https://www.geeksforgeeks.org/count-triples-with-bitwise-and-equal-to-zero/)

给定一个由 **N** 个整数组成的[个整数数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**，求指数(I，j，k)的三元组数，使得**A【I】&A【j】&A【k】**为 **0** ( < 0 ≤ i，j，k ≤ N 且 **&** 表示[位“与”运算符](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

**示例:**

> **输入:** A[]={2，1，3}
> **输出:** 12
> **说明:**可以选择以下 I，j，k 三元组，其按位 AND 为零:
> (i=0，j=0，k=1) : 2 & 2 & 1
> (i=0，j=1，k=0) : 2 & 1 & 2
> (i=0，j=1，1 j=0，k=0) : 1 & 2 & 2
> (i=1，j=0，k=1) : 1 & 2 & 1
> (i=1，j=0，k=2) : 1 & 2 & 3
> (i=1，j=1，k=0) : 1 & 1 & 2
> (i=1，j=2，k=0) : 1 & 3
> 
> **输入:** A[]={21，15，6}
> **输出:** 0
> **说明:**不存在这样的三胞胎。

**方法:**解决这个问题的思路是用一张[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来处理数组求解元素。按照以下步骤解决问题:

*   初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来存储**A【I】&A【j】**的每个可能值的频率。另外，初始化一个变量**用 **0** 回答**，以存储所需的计数。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)对于每个数组元素，[遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)并检查每个地图是否有键，当前数组元素的**位“与”**是否为 0。对于发现为真的每个数组元素，将**答案**增加按键的**频率**。
*   完成数组遍历后，打印**答案**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function to find the number of
// triplets whose Bitwise AND is 0.
int countTriplets(vector<int>& A)
{
    // Stores the count of triplets
    // having bitwise AND equal to 0
    int cnt = 0;

    // Stores frequencies of all possible A[i] & A[j]
    unordered_map<int, int> tuples;

    // Traverse the array
    for (auto a : A)

        // Update frequency of Bitwise AND
        // of all array elements with a
        for (auto b : A)
            ++tuples[a & b];

    // Traverse the array
    for (auto a : A)

        // Iterate the map
        for (auto t : tuples)

            // If bitwise AND of triplet
            // is zero, increment cnt
            if ((t.first & a) == 0)
                cnt += t.second;

    // Return the number of triplets
    // whose Bitwise AND is 0.
    return cnt;
}

// Driver Code
int main()
{

    // Input Array
    vector<int> A = { 2, 1, 3 };

    // Function Call
    cout << countTriplets(A);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find the number of
// triplets whose Bitwise AND is 0.
static int countTriplets(int []A)
{

    // Stores the count of triplets
    // having bitwise AND equal to 0
    int cnt = 0;

    // Stores frequencies of all possible A[i] & A[j]
    HashMap<Integer,Integer> tuples = new HashMap<Integer,Integer>();

    // Traverse the array
    for (int a : A)

        // Update frequency of Bitwise AND
        // of all array elements with a
        for (int b : A)
        {
            if(tuples.containsKey(a & b))
                tuples.put(a & b, tuples.get(a & b) + 1);
            else
                tuples.put(a & b, 1);
        }

    // Traverse the array
    for (int a : A)

        // Iterate the map
        for (Map.Entry<Integer, Integer> t : tuples.entrySet())

            // If bitwise AND of triplet
            // is zero, increment cnt
            if ((t.getKey() & a) == 0)
                cnt += t.getValue();

    // Return the number of triplets
    // whose Bitwise AND is 0.
    return cnt;
}

// Driver Code
public static void main(String[] args)
{

    // Input Array
    int []A = { 2, 1, 3 };

    // Function Call
    System.out.print(countTriplets(A));
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number of
# triplets whose Bitwise AND is 0.
def countTriplets(A) :

    # Stores the count of triplets
    # having bitwise AND equal to 0
    cnt = 0;

    # Stores frequencies of all possible A[i] & A[j]
    tuples = {};

    # Traverse the array
    for a in A:

        # Update frequency of Bitwise AND
        # of all array elements with a
        for b in A:
            if (a & b) in tuples:
                tuples[a & b] += 1;               
            else:
                tuples[a & b] = 1;

    # Traverse the array
    for a in A:

        # Iterate the map
        for t in tuples:

            # If bitwise AND of triplet
            # is zero, increment cnt
            if ((t & a) == 0):
                cnt += tuples[t];

    # Return the number of triplets
    # whose Bitwise AND is 0.
    return cnt;

# Driver Code
if __name__ ==  "__main__" :

    # Input Array
    A = [ 2, 1, 3 ];

    # Function Call
    print(countTriplets(A));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the number of
// triplets whose Bitwise AND is 0.
static int countTriplets(int []A)
{

    // Stores the count of triplets
    // having bitwise AND equal to 0
    int cnt = 0;

    // Stores frequencies of all possible A[i] & A[j]
    Dictionary<int,int> tuples = new Dictionary<int,int>();

    // Traverse the array
    foreach (int a in A)

        // Update frequency of Bitwise AND
        // of all array elements with a
        foreach (int b in A)
        {
            if(tuples.ContainsKey(a & b))
                tuples[a & b] = tuples[a & b] + 1;
            else
                tuples.Add(a & b, 1);
        }

    // Traverse the array
    foreach (int a in A)

        // Iterate the map
        foreach (KeyValuePair<int, int> t in tuples)

            // If bitwise AND of triplet
            // is zero, increment cnt
            if ((t.Key & a) == 0)
                cnt += t.Value;

    // Return the number of triplets
    // whose Bitwise AND is 0.
    return cnt;
}

// Driver Code
public static void Main(String[] args)
{

    // Input Array
    int []A = { 2, 1, 3 };

    // Function Call
    Console.Write(countTriplets(A));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the number of
// triplets whose Bitwise AND is 0.
function countTriplets(A)
{
    // Stores the count of triplets
    // having bitwise AND equal to 0
    var cnt = 0;

    // Stores frequencies of all possible A[i] & A[j]
    var tuples = new Map();

    // Traverse the array
    A.forEach(a => {

        // Update frequency of Bitwise AND
        // of all array elements with a
        A.forEach(b => {

            if(tuples.has(a & b))
                tuples.set(a & b, tuples.get(a & b)+1)
            else
                tuples.set(a & b, 1)
        });
    });

    // Traverse the array
    A.forEach(a => {

        // Update frequency of Bitwise AND
        // of all array elements with a
        tuples.forEach((value, key) => {

            // If bitwise AND of triplet
            // is zero, increment cnt
            if ((key & a) == 0)
                cnt += value;
        });
    });

    // Return the number of triplets
    // whose Bitwise AND is 0.
    return cnt;
}

// Driver Code
// Input Array
var A = [2, 1, 3];
// Function Call
document.write( countTriplets(A));

</script>
```

**Output:** 

```
12
```

***时间复杂度:** O(max(M，N <sup>2</sup> )其中 **M** 是给定数组中存在的最大元素*
***辅助空间:** O(M)*