# 包含卢卡斯数的数组的最长子序列

> 原文:[https://www . geeksforgeeks . org/包含 lucas 数的最长子数组序列/](https://www.geeksforgeeks.org/longest-sub-sequence-of-array-containing-lucas-numbers/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是找出 **arr[]** 中最长子序列的长度，这样序列的所有元素都是[卢卡斯数](https://www.geeksforgeeks.org/lucas-numbers/)。
**举例:**

> **输入:** arr[] = {2，3，55，6，1，18}
> **输出:** 4
> 1，2，3 和 18 是卢卡斯序列中唯一的元素。
> **输入:** arr[] = {22，33，2，123}
> **输出:** 2

**进场:**

*   找到数组中的最大元素。
*   生成最大的卢卡斯数字，并将其存储在一个集合中。
*   遍历数组 **arr[]** 并检查集合中是否存在当前元素。
*   如果它存在于集合中，则增加计数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the length of
// the longest required sub-sequence
int LucasSequence(int arr[], int n)
{
    // Find the maximum element from
    // the array
    int max = *max_element(arr, arr+n);

    // Insert all lucas numbers
    // below max to the set
    // a and b are first two elements
    // of the Lucas sequence
    unordered_set<int> s;
    int a = 2, b = 1, c;
    s.insert(a);
    s.insert(b);
    while (b < max) {
        int c = a + b;
        a = b;
        b = c;
        s.insert(b);
    }

    int count = 0;
    for (int i = 0; i < n; i++) {

        // If current element is a Lucas
        // number, increment count
        auto it = s.find(arr[i]);
        if (it != s.end())
            count++;
    }

    // Return the count
    return count;
}

// Driver code
int main()
{
    int arr[] = { 7, 11, 22, 4, 2, 1, 8, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << LucasSequence(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the length of
    // the longest required sub-sequence
    static int LucasSequence(int[] arr, int n)
    {
        // Find the maximum element from
        // the array
        int max = Arrays.stream(arr).max().getAsInt();
        int counter = 0;

        // Insert all lucas numbers
        // below max to the set
        // a and b are first two elements
        // of the Lucas sequence
        HashSet<Integer> s = new HashSet<>();

        int a = 2, b = 1;
        s.add(a);
        s.add(b);

        while (b < max)
        {
            int c = a + b;
            a = b;
            b = c;
            s.add(b);
        }

        for (int i = 0; i < n; i++)
        {

            // If current element is a Lucas
            // number, increment count
            if (s.contains(arr[i]))
            {
                counter++;
            }
        }

        // Return the count
        return counter;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = {7, 11, 22, 4, 2, 1, 8, 9};
        int n = arr.length;

        System.out.println(LucasSequence(arr, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the length of
# the longest required sub-sequence
def LucasSequence(arr, n):

    # Find the maximum element from
    # the array
    max = arr[0]
    for i in range(len(arr)):
        if(arr[i] > max):
            max = arr[i]

    # Insert all lucas numbers below max
    # to the set a and b are first two
    # elements of the Lucas sequence
    s = set()
    a = 2
    b = 1
    s.add(a)
    s.add(b)
    while (b < max):
        c = a + b
        a = b
        b = c
        s.add(b)

    count = 0
    for i in range(n):

        # If current element is a Lucas
        # number, increment count
        if(arr[i] in s):
            count += 1

    # Return the count
    return count

# Driver code
if __name__ == '__main__':
    arr = [7, 11, 22, 4, 2, 1, 8, 9]
    n = len(arr)

    print(LucasSequence(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
using System.Linq;

class GFG
{

    // Function to return the length of
    // the longest required sub-sequence
    static int LucasSequence(int []arr, int n)
    {
        // Find the maximum element from
        // the array
        int max = arr.Max();
        int counter = 0;

        // Insert all lucas numbers
        // below max to the set
        // a and b are first two elements
        // of the Lucas sequence
        HashSet<int> s = new HashSet<int>() ;

        int a = 2, b = 1 ;
        s.Add(a);
        s.Add(b);

        while (b < max)
        {
            int c = a + b;
            a = b;
            b = c;
            s.Add(b);
        }

        for (int i = 0; i < n; i++)
        {

            // If current element is a Lucas
            // number, increment count
            if (s.Contains(arr[i]))
                counter++;
        }

        // Return the count
        return counter;
    }

    // Driver code
    static public void Main()
    {
        int []arr = { 7, 11, 22, 4, 2, 1, 8, 9 };
        int n = arr.Length ;

        Console.WriteLine(LucasSequence(arr, n)) ;
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the length of
// the longest required sub-sequence
function LucasSequence(arr, n)
{
    // Find the maximum element from
    // the array
    var max = arr.reduce((a,b)=> Math.max(a,b));

    // push all lucas numbers
    // below max to the set
    // a and b are first two elements
    // of the Lucas sequence
    var s = [];
    var a = 2, b = 1, c;
    s.push(a);
    s.push(b);
    while (b < max) {
        var c = a + b;
        a = b;
        b = c;
        s.push(b);
    }

    s.sort((a,b) => a-b)
    var count = 0;
    for (var i = 0; i < n; i++) {

        // If current element is a Lucas
        // number, increment count
        if(s.includes(arr[i]))
        {
            s.pop(arr[i]);
            count++;
        }
    }

    // Return the count
    return count;
}

// Driver code
var arr = [7, 11, 22, 4, 2, 1, 8, 9 ];
var n = arr.length;
document.write( LucasSequence(arr, n));

</script>
```

**Output:** 

```
5
```