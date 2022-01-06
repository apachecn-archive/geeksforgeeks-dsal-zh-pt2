# 要改变的最小数组元素，以形成重铸人的序列

> 原文:[https://www . geeksforgeeks . org/最小数组-要更改的元素-制作-重铸-序列/](https://www.geeksforgeeks.org/minimum-array-elements-to-be-changed-to-make-recamans-sequence/)

给定一个由 **N** 元素组成的数组 **arr[]** 。任务是找到数组中需要改变的元素的最小数量，使得数组首先包含**N**T6】重铸人序列项。**注意**重铸人术语可以在数组中以任何顺序出现。
雷卡曼序列的前几个术语是:

> 0, 1, 3, 6, 2, 7, 13, 20, 12, 21, 11, 22, 10, 23, 9, 24, 8, … ..

**例:**

> **输入:** arr[] = {44，0，2，3，9}
> **输出:** 2
> N = 5 且前 5 个重铸人编号为 0，1，3，6 和 2
> 44 和 9 必须替换为 6 和 1
> 因此需要进行 2 次更改。
> **输入:** arr[] = {0，33，3，1}
> **输出:** 1

**进场:**

*   在[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中插入第一个 N 重铸人的序列术语。
*   从左到右遍历数组，检查数组元素是否存在于集合中。
*   如果当前元素存在于集合中，则将其从集合中移除。
*   所需的最小变化是最终缩减集的大小。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int recamanGenerator(int arr[], int n)
{
    // First term of the sequence is always 0
    arr[0] = 0;

    // Fill remaining terms using recursive
    // formula
    for (int i = 1; i <= n; i++) {
        int temp = arr[i - 1] - i;
        int j;

        for (j = 0; j < i; j++) {

            // If arr[i-1] - i is negative or
            // already exists
            if ((arr[j] == temp) || temp < 0) {
                temp = arr[i - 1] + i;
                break;
            }
        }

        arr[i] = temp;
    }
}

// Function that returns minimum changes required
int recamanArray(int arr[], int n)
{

    // Set to store first n Recaman numbers
    unordered_set<int> s;

    // Generate and store
    // first n Recaman numbers
    int recaman[n];
    recamanGenerator(recaman, n);

    // Insert first n Recaman numbers to set
    for (int i = 0; i < n; i++)
        s.insert(recaman[i]);

    for (int i = 0; i < n; i++) {

        // If current element of the array
        // is present in the set
        auto it = s.find(arr[i]);
        if (it != s.end())
            s.erase(it);
    }

    // Return the remaining number of
    // elements in the set
    return s.size();
}

// Driver code
int main()
{

    int arr[] = { 7, 11, 20, 4, 2, 1, 8, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << recamanArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int recamanGenerator(int arr[], int n)
{
    // First term of the sequence is always 0
    arr[0] = 0;

    // Fill remaining terms using recursive
    // formula
    for (int i = 1; i <= n; i++)
    {
        int temp = arr[i - 1] - i;
        int j;

        for (j = 0; j < i; j++)
        {

            // If arr[i-1] - i is negative or
            // already exists
            if ((arr[j] == temp) || temp < 0)
            {
                temp = arr[i - 1] + i;
                break;
            }
        }

        arr[i] = temp;
    }
    return 0;
}

// Function that returns minimum changes required
static int recamanArray(int arr[], int n)
{

    // Set to store first n Recaman numbers
    Set<Integer> s=new HashSet<Integer>();

    // Generate and store
    // first n Recaman numbers
    int recaman[]=new int[n+1];
    recamanGenerator(recaman, n);

    // Insert first n Recaman numbers to set
    for (int i = 0; i < n; i++)
        s.add(recaman[i]);

    for (int i = 0; i < n; i++)
    {
        // If current element of the array
        // is present in the set
        if (s.contains(arr[i]))
            s.remove(arr[i]);
    }

    // Return the remaining number of
    // elements in the set
    return s.size();
}

// Driver code
public static void main(String args[])
{

    int arr[] = { 7, 11, 20, 4, 2, 1, 8, 6 };
    int n = arr.length;

    System.out.print( recamanArray(arr, n));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
def recamanGenerator(arr, n):

    # First term of the sequence
    # is always 0
    arr[0] = 0

    # Fill remaining terms using
    # recursive formula
    for i in range(1, n):
        temp = arr[i - 1] - i
        j = 0

        for j in range(i):

            # If arr[i-1] - i is negative or
            # already exists
            if ((arr[j] == temp) or temp < 0):
                temp = arr[i - 1] + i
                break

        arr[i] = temp

# Function that returns minimum
# changes required
def recamanArray(arr, n):

    # Set to store first n Recaman numbers
    s = dict()

    # Generate and store
    # first n Recaman numbers
    recaman = [0 for i in range(n)]
    recamanGenerator(recaman, n)

    # Insert first n Recaman numbers to set
    for i in range(n):
        s[recaman[i]] = s.get(recaman[i], 0) + 1

    for i in range(n):

        # If current element of the array
        # is present in the set
        if arr[i] in s.keys():
            del s[arr[i]]

    # Return the remaining number of
    # elements in the set
    return len(s)

# Driver code
arr = [7, 11, 20, 4, 2, 1, 8, 6 ]
n = len(arr)

print(recamanArray(arr, n))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

static int recamanGenerator(int []arr, int n)
{
    // First term of the sequence is always 0
    arr[0] = 0;

    // Fill remaining terms using recursive
    // formula
    for (int i = 1; i <= n; i++)
    {
        int temp = arr[i - 1] - i;
        int j;

        for (j = 0; j < i; j++)
        {

            // If arr[i-1] - i is negative or
            // already exists
            if ((arr[j] == temp) || temp < 0)
            {
                temp = arr[i - 1] + i;
                break;
            }
        }

        arr[i] = temp;
    }
    return 0;
}

// Function that returns minimum changes required
static int recamanArray(int []arr, int n)
{

    // Set to store first n Recaman numbers
    HashSet<int> s=new HashSet<int>();

    // Generate and store
    // first n Recaman numbers
    int[] recaman=new int[n+1];
    recamanGenerator(recaman, n);

    // Insert first n Recaman numbers to set
    for (int i = 0; i < n; i++)
        s.Add(recaman[i]);

    for (int i = 0; i < n; i++)
    {
        // If current element of the array
        // is present in the set
        if (s.Contains(arr[i]))
            s.Remove(arr[i]);
    }

    // Return the remaining number of
    // elements in the set
    return s.Count;
}

// Driver code
static void Main()
{

    int []arr = { 7, 11, 20, 4, 2, 1, 8, 6 };
    int n = arr.Length;

    Console.Write( recamanArray(arr, n));
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

function recamanGenerator(arr, n)
{
    // First term of the sequence is always 0
    arr[0] = 0;

    // Fill remaining terms using recursive
    // formula
    for (var i = 1; i <= n; i++) {
        var temp = arr[i - 1] - i;
        var j;

        for (j = 0; j < i; j++) {

            // If arr[i-1] - i is negative or
            // already exists
            if ((arr[j] == temp) || temp < 0) {
                temp = arr[i - 1] + i;
                break;
            }
        }

        arr[i] = temp;
    }
}

// Function that returns minimum changes required
function recamanArray(arr, n)
{

    // Set to store first n Recaman numbers
    var s = [];

    // Generate and store
    // first n Recaman numbers
    var recaman = Array(n).fill(0);
    recamanGenerator(recaman, n);

    // push first n Recaman numbers to set
    for (var i = 0; i < n; i++)
        s.push(recaman[i]);

    s.sort((a,b)=> b-a)

    for (var i = 0; i < n; i++) {

        // If current element of the array
        // is present in the set
        if(s.includes(arr[i]))
        {
            s.splice(s.indexOf(arr[i]), 1);
        }  
    }

    // Return the remaining number of
    // elements in the set
    return s.length;
}

// Driver code
var arr = [7, 11, 20, 4, 2, 1, 8, 6 ];
var n = arr.length;
document.write( recamanArray(arr, n));

</script>
```

**Output:** 

```
3
```