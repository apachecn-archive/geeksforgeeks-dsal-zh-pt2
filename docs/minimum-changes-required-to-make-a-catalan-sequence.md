# 制作加泰罗尼亚语序列所需的最小变化

> 原文:[https://www . geeksforgeeks . org/make-a-Catalan-sequence 所需的最小更改数/](https://www.geeksforgeeks.org/minimum-changes-required-to-make-a-catalan-sequence/)

给定一个由 **N** 个整数元素组成的数组 **arr[]** ，任务是更改该数组的最小元素数，使其包含加泰罗尼亚序列的前 N 项。因此，找到所需的最小变化。
前几个加泰罗尼亚数字是 1，1，2，5，14，42，132，429，1430，4862，…..
**例:**

> **输入:** arr[] = {4，1，2，33，213，5}
> **输出:** 3
> 我们必须用 1，14，42 替换 4，33，213，才能构成加泰罗尼亚语序列的前 6 项。
> **输入:** arr[] = {1，1，2，5，41}
> **输出:** 1
> 只需将 41 换成 14

**进场:**

*   以无序多集为例。在这个多集合中插入加泰罗尼亚语序列的前 N 个术语。
*   从左到右遍历数组。检查数组元素是否存在于多集合中。如果存在，则从多集移除该元素。
*   遍历数组后，所需的最小更改将等于多集的大小。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 100000
#define ll long long int

// To store first N Catalan numbers
ll catalan[MAX];

// Function to find first n Catalan numbers
void catalanDP(ll n)
{

    // Initialize first two values in table
    catalan[0] = catalan[1] = 1;

    // Fill entries in catalan[] using recursive formula
    for (int i = 2; i <= n; i++) {
        catalan[i] = 0;
        for (int j = 0; j < i; j++)
            catalan[i] += catalan[j] * catalan[i - j - 1];
    }
}

// Function to return the minimum changes required
int CatalanSequence(int arr[], int n)
{

    // Find first n Catalan Numbers
    catalanDP(n);

    unordered_multiset<int> s;

    // a and b are first two
    // Catalan Sequence numbers
    int a = 1, b = 1;
    int c;

    // Insert first n catalan elements to set
    s.insert(a);
    if (n >= 2)
        s.insert(b);

    for (int i = 2; i < n; i++) {
        s.insert(catalan[i]);
    }

    unordered_multiset<int>::iterator it;

    for (int i = 0; i < n; i++) {

        // If catalan element is present
        // in the array then remove it from set
        it = s.find(arr[i]);
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
    int arr[] = { 1, 1, 2, 5, 41 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << CatalanSequence(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.HashSet;

// Java implementation of the approach
class GFG1
{

    static int MAX = 100000;

    // To store first N Catalan numbers
    static long catalan[] = new long[MAX];

    // Function to find first n Catalan numbers
    static void catalanDP(long n)
    {

        // Initialize first two values in table
        catalan[0] = catalan[1] = 1;

        // Filong entries in catalan[]
        // using recursive formula
        for (int i = 2; i <= n; i++)
        {
            catalan[i] = 0;
            for (int j = 0; j < i; j++)
            {
                catalan[i] += catalan[j] * catalan[i - j - 1];
            }
        }
    }

    // Function to return the minimum changes required
    static int CatalanSequence(int arr[], int n)
    {

        // Find first n Catalan Numbers
        catalanDP(n);

        HashSet<Integer> s = new HashSet<Integer>();

        // a and b are first two
        // Catalan Sequence numbers
        int a = 1, b = 1;
        int c;

        // Insert first n catalan elements to set
        s.add(a);
        if (n >= 2)
        {
            s.add(b);
        }

        for (int i = 2; i < n; i++)
        {
            s.add((int) catalan[i]);
        }

        for (int i = 0; i < n; i++)
        {

            // If catalan element is present
            // in the array then remove it from set
            if (s.contains(arr[i]))
            {
                s.remove(arr[i]);
            }
        }

        // Return the remaining number of
        // elements in the set
        return s.size();
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {1, 1, 2, 5, 41};
        int n = arr.length;

        System.out.print(CatalanSequence(arr, n));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of
# the approach
MAX = 100000;

# To store first N Catalan numbers
catalan = [0] * MAX;

# Function to find first n
# Catalan numbers
def catalanDP(n) :

    # Initialize first two values
    # in table
    catalan[0] = catalan[1] = 1;

    # Fill entries in catalan[]
    # using recursive formula
    for i in range(2, n + 1) :
        catalan[i] = 0;
        for j in range(i) :
            catalan[i] += (catalan[j] *
                           catalan[i - j - 1]);

# Function to return the minimum
# changes required
def CatalanSequence(arr, n) :

    # Find first n Catalan Numbers
    catalanDP(n);

    s = set();

    # a and b are first two
    # Catalan Sequence numbers
    a = 1 ; b = 1;

    # Insert first n catalan
    # elements to set
    s.add(a);
    if (n >= 2) :
        s.add(b);

    for i in range(2, n) :
        s.add(catalan[i]);

    temp = set()
    for i in range(n) :

        # If catalan element is present
        # in the array then remove it
        # from set
        if arr[i] in s :
            temp.add(arr[i])

    s = s - temp ;

    # Return the remaining number
    # of elements in the set
    return len(s);

# Driver code
if __name__ == "__main__" :

    arr = [1, 1, 2, 5, 41];
    n = len(arr)

    print(CatalanSequence(arr, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG1
{

    static int MAX = 100000;

    // To store first N Catalan numbers
    static long[] catalan = new long[MAX];

    // Function to find first n Catalan numbers
    static void catalanDP(long n)
    {

        // Initialize first two values in table
        catalan[0] = catalan[1] = 1;

        // Filong entries in catalan[]
        // using recursive formula
        for (int i = 2; i <= n; i++)
        {
            catalan[i] = 0;
            for (int j = 0; j < i; j++)
            {
                catalan[i] += catalan[j] * catalan[i - j - 1];
            }
        }
    }

    // Function to return the minimum changes required
    static int CatalanSequence(int []arr, int n)
    {

        // Find first n Catalan Numbers
        catalanDP(n);

        HashSet<int> s = new HashSet<int>();

        // a and b are first two
        // Catalan Sequence numbers
        int a = 1, b = 1;

        // Insert first n catalan elements to set
        s.Add(a);
        if (n >= 2)
        {
            s.Add(b);
        }

        for (int i = 2; i < n; i++)
        {
            s.Add((int)catalan[i]);
        }

        for (int i = 0; i < n; i++)
        {

            // If catalan element is present
            // in the array then remove it from set
            if (s.Contains(arr[i]))
            {
                s.Remove(arr[i]);
            }
        }

        // Return the remaining number of
        // elements in the set
        return s.Count;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {1, 1, 2, 5, 41};
        int n = arr.Length;

        Console.WriteLine(CatalanSequence(arr, n));
    }
}

// This code contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
$MAX = 1000;

// To store first N Catalan numbers
$catalan = array_fill(0, $MAX, 0);

// Function to find first n Catalan numbers
function catalanDP($n)
{
    global $catalan;

    // Initialize first two values in table
    $catalan[0] = $catalan[1] = 1;

    // Filong entries in catalan[]
    // using recursive formula
    for ($i = 2; $i <= $n; $i++)
    {
        $catalan[$i] = 0;
        for ($j = 0; $j < $i; $j++)
        {
            $catalan[$i] += $catalan[$j] *
                            $catalan[$i - $j - 1];
        }
    }
}

// Function to return the minimum
// changes required
function CatalanSequence($arr, $n)
{
    global $catalan;

    // Find first n Catalan Numbers
    catalanDP($n);

    $s = array();

    // a and b are first two
    // Catalan Sequence numbers
    $a = $b = 1;

    // Insert first n catalan elements to set
    array_push($s, $a);
    if ($n >= 2)
    {
        array_push($s, $b);
    }

    for ($i = 2; $i < $n; $i++)
    {
        array_push($s, $catalan[$i]);
    }

    $s = array_unique($s);
    for ($i = 0; $i < $n; $i++)
    {

        // If catalan element is present
        // in the array then remove it from set
        if (in_array($arr[$i], $s))
        {
            unset($s[array_search($arr[$i], $s)]);
        }
    }

    // Return the remaining number of
    // elements in the set
    return count($s);
}

// Driver code
$arr = array(1, 1, 2, 5, 41);
$n = count($arr);

print(CatalanSequence($arr, $n));

// This code contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var MAX = 100000

// To store first N Catalan numbers
var catalan = Array(MAX);

// Function to find first n Catalan numbers
function catalanDP(n)
{
    // Initialize first two values in table
    catalan[0] = catalan[1] = 1;

    // Fill entries in catalan[] using recursive formula
    for (var i = 2; i <= n; i++) {
        catalan[i] = 0;
        for (var j = 0; j < i; j++)
            catalan[i] += catalan[j] * catalan[i - j - 1];
    }
}

// Function to return the minimum changes required
function CatalanSequence(arr, n)
{
    // Find first n Catalan Numbers
    catalanDP(n);

    var s = [];

    // a and b are first two
    // Catalan Sequence numbers
    var a = 1, b = 1;
    var c;

    // push first n catalan elements to set
    s.push(a);
    if (n >= 2)
        s.push(b);

    for (var i = 2; i < n; i++) {
        s.push(catalan[i]);
    }

    s.sort((a,b)=>b-a);
    for(var i =0; i<n; i++)
    {
        // If catalan element is present
        // in the array then remove it from set
        if(s.includes(arr[i]))
        {
            s.pop(arr[i]);
        }
    }

    // Return the remaining number of
    // elements in the set
    return s.length;
}

// Driver code
var arr = [1, 1, 2, 5, 41 ];
var n = arr.length;
document.write( CatalanSequence(arr, n));

</script>   
```

**Output:** 

```
1
```