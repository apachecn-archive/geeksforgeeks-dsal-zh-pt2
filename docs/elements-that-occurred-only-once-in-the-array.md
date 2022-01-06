# 数组中只出现一次的元素

> 原文:[https://www . geesforgeks . org/elements-发生在阵列中的唯一一次/](https://www.geeksforgeeks.org/elements-that-occurred-only-once-in-the-array/)

给定一个数字出现两次或一次的数组 *arr* 。任务是识别在数组中只出现一次的数字。

**注意:**重复项每次并排出现。可能一次会出现几个数字，假设这是一个向右旋转的数组(假设一个数组可以向右旋转 k 次)。输出中元素的顺序并不重要。

**示例:**

```
Input: arr[] = { 7, 7, 8, 8, 9, 1, 1, 4, 2, 2 }
Output: 9 4

Input: arr[] = {-9, -8, 4, 4, 5, 5, -1}
Output: -9 -8 -1
```

**方法-1:** *使用* [*排序*](https://www.geeksforgeeks.org/sort-c-stl/) *。*

*   对数组排序。
*   检查索引 I 处的每个元素(第一个和最后一个元素除外)，如果

```
arr[i] != arr[i-1] && arr [i] != arr[i+1]
```

*   对于第一个元素，检查 ***是否 arr[0]！= arr[1]*** 。
*   最后一个元素，检查 ***是否 arr[n-1]！= arr[n-2]** 。*

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the elements that
// appeared only once in the array
void occurredOnce(int arr[], int n)
{
    // Sort the array
    sort(arr, arr + n);

    // Check for first element
    if (arr[0] != arr[1])
        cout << arr[0] << " ";

    // Check for all the elements if it is different
    // its adjacent elements
    for (int i = 1; i < n - 1; i++)
        if (arr[i] != arr[i + 1] && arr[i] != arr[i - 1])
            cout << arr[i] << " ";

    // Check for the last element
    if (arr[n - 2] != arr[n - 1])
        cout << arr[n - 1] << " ";
}

// Driver code
int main()
{

    int arr[] = { 7, 7, 8, 8, 9, 1, 1, 4, 2, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    occurredOnce(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// of above approach
import java.util.*;

class GFG
{

// Function to find the elements that
// appeared only once in the array
static void occurredOnce(int arr[], int n)
{
    // Sort the array
    Arrays.sort(arr);

    // Check for first element
    if (arr[0] != arr[1])
        System.out.println(arr[0] + " ");

    // Check for all the elements
    // if it is different
    // its adjacent elements
    for (int i = 1; i < n - 1; i++)
        if (arr[i] != arr[i + 1] &&
            arr[i] != arr[i - 1])
            System.out.print(arr[i] + " ");

    // Check for the last element
    if (arr[n - 2] != arr[n - 1])
        System.out.print(arr[n - 1] + " ");
}

// Driver code
public static void main(String args[])
{
    int arr[] = {7, 7, 8, 8, 9,
                 1, 1, 4, 2, 2};
    int n = arr.length;

    occurredOnce(arr, n);
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation
# of above approach

# Function to find the elements
# that appeared only once in
# the array
def occurredOnce(arr, n):

    # Sort the array
    arr.sort()

    # Check for first element
    if arr[0] != arr[1]:
        print(arr[0], end = " ")

    # Check for all the elements
    # if it is different its
    # adjacent elements
    for i in range(1, n - 1):
        if (arr[i] != arr[i + 1] and
            arr[i] != arr[i - 1]):
            print( arr[i], end = " ")

    # Check for the last element
    if arr[n - 2] != arr[n - 1]:
        print(arr[n - 1], end = " ")

# Driver code
if __name__ == "__main__":

    arr = [ 7, 7, 8, 8, 9,
            1, 1, 4, 2, 2 ]
    n = len(arr)
    occurredOnce(arr, n)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation
// of above approach
using System;

class GFG
{

// Function to find the elements that
// appeared only once in the array
static void occurredOnce(int[] arr, int n)
{
    // Sort the array
    Array.Sort(arr);

    // Check for first element
    if (arr[0] != arr[1])
        Console.Write(arr[0] + " ");

    // Check for all the elements
    // if it is different
    // its adjacent elements
    for (int i = 1; i < n - 1; i++)
        if (arr[i] != arr[i + 1] &&
            arr[i] != arr[i - 1])
            Console.Write(arr[i] + " ");

    // Check for the last element
    if (arr[n - 2] != arr[n - 1])
        Console.Write(arr[n - 1] + " ");
}

// Driver code
public static void Main()
{
    int[] arr = {7, 7, 8, 8, 9,
                1, 1, 4, 2, 2};
    int n = arr.Length;

    occurredOnce(arr, n);
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation
// of above approach

// Function to find the elements
// that appeared only once in
// the array
function occurredOnce(&$arr, $n)
{
    // Sort the array
    sort($arr);

    // Check for first element
    if ($arr[0] != $arr[1])
        echo $arr[0]." ";

    // Check for all the elements
    // if it is different its
    // adjacent elements
    for ($i = 1; $i < $n - 1; $i++)
        if ($arr[$i] != $arr[$i + 1] &&
            $arr[$i] != $arr[$i - 1])
            echo $arr[$i]." ";

    // Check for the last element
    if ($arr[$n - 2] != $arr[$n - 1])
        echo $arr[$n - 1]." ";
}

// Driver code
$arr = array(7, 7, 8, 8, 9,
             1, 1, 4, 2, 2);
$n = sizeof($arr);
occurredOnce($arr, $n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript implementation
// of above approach

// Function to find the elements that
// appeared only once in the array
function occurredOnce(arr,n)
{
    // Sort the array
    arr.sort(function(a,b){return a-b;});

    // Check for first element
    if (arr[0] != arr[1])
        document.write(arr[0] + " ");

    // Check for all the elements
    // if it is different
    // its adjacent elements
    for (let i = 1; i < n - 1; i++)
        if (arr[i] != arr[i + 1] &&
            arr[i] != arr[i - 1])
            document.write(arr[i] + " ");

    // Check for the last element
    if (arr[n - 2] != arr[n - 1])
        document.write(arr[n - 1] + " ");
}

// Driver code
let arr=[7, 7, 8, 8, 9,
                 1, 1, 4, 2, 2];
let n = arr.length;
occurredOnce(arr, n);

// This code is contributed by rag2127

</script>
```

**Output**

```
4 9 
```

**时间复杂度:**O(Nlogn)
T3】空间复杂度: O(1)

**方法-2:** *(使用* [*哈希*](https://www.geeksforgeeks.org/hashing-set-1-introduction/) *)* :在 C++中，[无序 _ 映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)可以用于哈希。

*   遍历数组。
*   将每个元素及其出现位置存储在无序映射中。
*   遍历无序映射，打印出现次数为 1 的所有元素。

下面是上述方法的实现:

## C++

```
// C++ implementation to find elements
// that appeared only once
#include <bits/stdc++.h>
using namespace std;

// Function to find the elements that
// appeared only once in the array
void occurredOnce(int arr[], int n)
{
    unordered_map<int, int> mp;

    // Store all the elements in the map with
    // their occurrence
    for (int i = 0; i < n; i++)
        mp[arr[i]]++;

    // Traverse the map and print all the
    // elements with occurrence 1
    for (auto it = mp.begin(); it != mp.end(); it++)
        if (it->second == 1)
            cout << it->first << " ";
}

// Driver code
int main()
{

    int arr[] = { 7, 7, 8, 8, 9, 1, 1, 4, 2, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    occurredOnce(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find elements
// that appeared only once
import java.util.*;
import java.io.*;

class GFG
{
    // Function to find the elements that
    // appeared only once in the array
    static void occurredOnce(int[] arr, int n)
    {
            HashMap<Integer, Integer> mp = new HashMap<>();

            // Store all the elements in the map with
            // their occurrence
            for (int i = 0; i < n; i++)
            {
                if (mp.containsKey(arr[i]))
                    mp.put(arr[i], 1 + mp.get(arr[i]));
                else
                    mp.put(arr[i], 1);
            }

            // Traverse the map and print all the
            // elements with occurrence 1
            for (Map.Entry entry : mp.entrySet())
            {
                if (Integer.parseInt(String.valueOf(entry.getValue())) == 1)
                    System.out.print(entry.getKey() + " ");
            }
    }

    // Driver code
    public static void main(String args[])
    {
            int[] arr = { 7, 7, 8, 8, 9, 1, 1, 4, 2, 2 };
            int n = arr.length;

            occurredOnce(arr, n);
    }
}

// This code is contributed by rachana soma
```

## 蟒蛇 3

```
# Python3 implementation to find elements
# that appeared only once
import math as mt

# Function to find the elements that
# appeared only once in the array
def occurredOnce(arr, n):

    mp = dict()

    # Store all the elements in the
    # map with their occurrence
    for i in range(n):
        if arr[i] in mp.keys():
            mp[arr[i]] += 1
        else:
            mp[arr[i]] = 1

    # Traverse the map and print all
    # the elements with occurrence 1
    for it in mp:
        if mp[it] == 1:
            print(it, end = " ")

# Driver code
arr = [7, 7, 8, 8, 9, 1, 1, 4, 2, 2]
n = len(arr)

occurredOnce(arr, n)

# This code is contributed by
# Mohit Kumar 29
```

## C#

```
// C# implementation to find elements
// that appeared only once
using System;
using System.Collections.Generic;
class GFG
{
    // Function to find the elements that
    // appeared only once in the array
    static void occurredOnce(int[] arr, int n)
    {
      Dictionary<int, int> mp = new Dictionary<int, int>();

      // Store all the elements in the map with
      // their occurrence
      for (int i = 0; i < n; i++)
      {
        if (mp.ContainsKey(arr[i]))
          mp[arr[i]] = 1 + mp[arr[i]];
        else
          mp.Add(arr[i], 1);
      }

      // Traverse the map and print all the
      // elements with occurrence 1
      foreach(KeyValuePair<int, int> entry in mp)
      {
        if (Int32.Parse(String.Join("", entry.Value)) == 1)
          Console.Write(entry.Key + " ");
      }
    }

    // Driver code
    public static void Main(String []args)
    {
      int[] arr = { 7, 7, 8, 8, 9, 1, 1, 4, 2, 2 };
      int n = arr.Length;
      occurredOnce(arr, n);
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript implementation to find elements
// that appeared only once

// Function to find the elements that
// appeared only once in the array
function occurredOnce(arr, n)
{
    let mp = new Map();

    // Store all the elements in the map
    // with their occurrence
    for(let i = 0; i < n; i++)
    {
        if (mp.has(arr[i]))
            mp.set(arr[i], 1 + mp.get(arr[i]));
        else
            mp.set(arr[i], 1);
    }

    // Traverse the map and print all the
    // elements with occurrence 1
    for(let [key, value] of mp.entries())
    {
        if (value == 1)
            document.write(key + " ");
    }
}

// Driver code
let arr = [ 7, 7, 8, 8, 9,
            1, 1, 4, 2, 2 ];
let n = arr.length;

occurredOnce(arr, n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
4 9 
```

**时间复杂度:**O(N)
T3】空间复杂度: O(N)

**方法-3:** *使用给定的假设。*
给定一个数组可以随时旋转，每次都会并排出现副本。所以，旋转之后，第一个和最后一个元素会并排出现。

*   检查第一个和最后一个元素是否相等。如果是，那么开始遍历它们之间的元素。
*   检查当前元素是否等于前一个索引中的元素。如果是，对下一个元素进行同样的检查。
*   如果没有，打印当前元素。

## C++

```
// C++ implementation to find elements
// that appeared only once
#include <bits/stdc++.h>
using namespace std;

// Function to find the elements that
// appeared only once in the array
void occurredOnce(int arr[], int n)
{
    int i = 1, len = n;

    // Check if the first and last element is equal
    // If yes, remove those elements
    if (arr[0] == arr[len - 1]) {
        i = 2;
        len--;
    }

    // Start traversing the remaining elements
    for (; i < n; i++)

        // Check if current element is equal to
        // the element at immediate previous index
        // If yes, check the same for next element
        if (arr[i] == arr[i - 1])
            i++;

        // Else print the current element
        else
            cout << arr[i - 1] << " ";

    // Check for the last element
    if (arr[n - 1] != arr[0] && arr[n - 1] != arr[n - 2])
        cout << arr[n - 1];
}

// Driver code
int main()
{

    int arr[] = { 7, 7, 8, 8, 9, 1, 1, 4, 2, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    occurredOnce(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// elements that appeared only once
class GFG
{
// Function to find the elements that
// appeared only once in the array
static void occurredOnce(int arr[], int n)
{
    int i = 1, len = n;

    // Check if the first and last
    // element is equal. If yes,
    // remove those elements
    if (arr[0] == arr[len - 1])
    {
        i = 2;
        len--;
    }

    // Start traversing the
    // remaining elements
    for (; i < n; i++)

        // Check if current element is
        // equal to the element at
        // immediate previous index
        // If yes, check the same
        // for next element
        if (arr[i] == arr[i - 1])
            i++;

        // Else print the current element
        else
            System.out.print(arr[i - 1] + " ");

    // Check for the last element
    if (arr[n - 1] != arr[0] &&
        arr[n - 1] != arr[n - 2])
        System.out.print(arr[n - 1]);
}

// Driver code
public static void main(String args[])
{
    int arr[] = {7, 7, 8, 8, 9,
                 1, 1, 4, 2, 2};
    int n = arr.length;

    occurredOnce(arr, n);
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 implementation to find
# elements that appeared only once

# Function to find the elements that
# appeared only once in the array
def occurredOnce(arr, n):
    i = 1
    len = n

    # Check if the first and
    # last element is equal
    # If yes, remove those elements
    if arr[0] == arr[len - 1]:
        i = 2
        len -= 1

    # Start traversing the
    # remaining elements
    while i < n:

        # Check if current element is
        # equal to the element at
        # immediate previous index
        # If yes, check the same for
        # next element
        if arr[i] == arr[i - 1]:
            i += 1

        # Else print the current element
        else:
            print(arr[i - 1], end = " ")

        i += 1

    # Check for the last element
    if (arr[n - 1] != arr[0] and
        arr[n - 1] != arr[n - 2]):
        print(arr[n - 1])

# Driver code
if __name__ == "__main__":
    arr = [ 7, 7, 8, 8, 9, 1, 1, 4, 2, 2 ]
    n = len(arr)

    occurredOnce(arr, n)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation to find
// elements that appeared only once
using System;

class GFG
{
// Function to find the elements that
// appeared only once in the array
static void occurredOnce(int[] arr, int n)
{
    int i = 1, len = n;

    // Check if the first and last
    // element is equal. If yes,
    // remove those elements
    if (arr[0] == arr[len - 1])
    {
        i = 2;
        len--;
    }

    // Start traversing the
    // remaining elements
    for (; i < n; i++)

        // Check if current element is
        // equal to the element at
        // immediate previous index
        // If yes, check the same
        // for next element
        if (arr[i] == arr[i - 1])
            i++;

        // Else print the current element
        else
            Console.Write(arr[i - 1] + " ");

    // Check for the last element
    if (arr[n - 1] != arr[0] &&
        arr[n - 1] != arr[n - 2])
        Console.Write(arr[n - 1]);
}

// Driver code
public static void Main()
{
    int[] arr = {7, 7, 8, 8, 9,
                1, 1, 4, 2, 2};
    int n = arr.Length;

    occurredOnce(arr, n);
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// elements that appeared only once

// Function to find the elements that
// appeared only once in the array
function occurredOnce(&$arr, $n)
{
    $i = 1;
    $len = $n;

    // Check if the first and last
    // element is equal. If yes,
    // remove those elements
    if ($arr[0] == $arr[$len - 1])
    {
        $i = 2;
        $len--;
    }

    // Start traversing the
    // remaining elements
    for (; $i < $n; $i++)

        // Check if current element is
        // equal to the element at
        // immediate previous index
        // If yes, check the same for
        // next element
        if ($arr[$i] == $arr[$i - 1])
            $i++;

        // Else print the current element
        else
            echo $arr[$i - 1] . " ";

    // Check for the last element
    if ($arr[$n - 1] != $arr[0] &&
        $arr[$n - 1] != $arr[$n - 2])
        echo $arr[$n - 1];
}

// Driver code
$arr = array(7, 7, 8, 8, 9,
             1, 1, 4, 2, 2);
$n = sizeof($arr);

occurredOnce($arr, $n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript implementation to find
// elements that appeared only once

// Function to find the elements that
// appeared only once in the array
function occurredOnce(arr, n)
{
    var i = 1, len = n;

    // Check if the first and last
    // element is equal. If yes,
    // remove those elements
    if (arr[0] == arr[len - 1])
    {
        i = 2;
        len--;
    }

    // Start traversing the
    // remaining elements
    for(; i < n; i++)

        // Check if current element is
        // equal to the element at
        // immediate previous index
        // If yes, check the same
        // for next element
        if (arr[i] == arr[i - 1])
            i++;

        // Else print the current element
        else
            document.write(arr[i - 1] + " ");

    // Check for the last element
    if (arr[n - 1] != arr[0] &&
        arr[n - 1] != arr[n - 2])
        document.write(arr[n - 1]);
}

// Driver code
var arr = [ 7, 7, 8, 8, 9,
            1, 1, 4, 2, 2 ];
var n = arr.length;

occurredOnce(arr, n);

// This code is contributed by Ankita saini

</script>
```

**Output**

```
9 4 
```

**时间复杂度:**O(N)
T3】空间复杂度: O(1)

#### 方法 4:使用内置的 Python 函数:

*   使用计数器函数计算每个元素的频率
*   遍历频率数组，打印出现次数为 1 的所有元素。

下面是实现

## 蟒蛇 3

```
# Python3 implementation to find elements
# that appeared only once
from collections import Counter

# Function to find the elements that
# appeared only once in the array
def occurredOnce(arr, n):

    #counting frequency of every element using Counter
    mp=Counter(arr)
    # Traverse the map and print all
    # the elements with occurrence 1
    for it in mp:
        if mp[it] == 1:
            print(it, end = " ")

# Driver code
arr = [7, 7, 8, 8, 9, 1, 1, 4, 2, 2]
n = len(arr)

occurredOnce(arr, n)

# This code is contributed by vikkycirus
```

**Output**

```
9 4 
```

**时间复杂度:** O(n)