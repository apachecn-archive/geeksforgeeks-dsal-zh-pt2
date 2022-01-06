# 找出数组中最大的 d，使得 a + b + c = d

> 原文:[https://www . geesforgeks . org/find-最大阵列中的 d-a-B- c-d/](https://www.geeksforgeeks.org/find-largest-d-in-array-such-that-a-b-c-d/)

给定一组 S(所有不同的元素)整数，找出最大的 d，使得 a + b + c = d
，其中 a、b、c 和 d 是 S 的不同元素

```
Constraints:
1 ≤ number of elements in the set ≤ 1000
INT_MIN ≤ each element in the set ≤ INT_MAX
```

**例:**

> 输入:S[] = {2，3，5，7，12}
> 输出:12
> **说明:** 12 是最大的 d，可以表示为 12 = 2 + 3 + 7
> 输入:S[] = {2，16，64，256，1024}
> 输出:无解

**方法 1(蛮力)**
我们可以使用简单的蛮力方法来解决这个问题，这种方法的效率不是很高，因为|S|可能高达 1000。我们将对元素集进行排序，并从找到最大的 d 开始，方法是将其与 a、b 和 c 的所有可能组合的总和相等。
下面是上述想法的实现:

## C++

```
// CPP Program to find the largest d
// such that d = a + b + c
#include <bits/stdc++.h>
using namespace std;

int findLargestd(int S[], int n)
{
    bool found = false;

    // sort the array in
    // ascending order
    sort(S, S + n);

    // iterating from backwards to
    // find the required largest d
    for (int i = n - 1; i >= 0; i--)
    {
        for (int j = 0; j < n; j++)
        {

            // since all four a, b, c,
            // d should be distinct
            if (i == j)
                continue;

            for (int k = j + 1; k < n; k++)
            {
                if (i == k)
                    continue;

                for (int l = k + 1; l < n; l++)
                {
                    if (i == l)
                        continue;

                    // if the current combination 
                    // of j, k, l in the set is
                    // equal to S[i] return this
                    // value as this would be the
                    // largest d since we are
                    //  iterating in descending order
                    if (S[i] == S[j] + S[k] + S[l])
                    {
                        found = true;
                        return S[i];
                    }
                }
            }
        }
    }
    if (found == false)
        return INT_MIN;
}

// Driver Code
int main()
{
    // Set of distinct Integers
    int S[] = { 2, 3, 5, 7, 12 };
    int n = sizeof(S) / sizeof(S[0]);

    int ans = findLargestd(S, n);
    if (ans == INT_MIN)
        cout << "No Solution" << endl;
    else
        cout << "Largest d such that a + b + "
             << "c = d is " << ans << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the largest
// such that d = a + b + c
import java.io.*;
import java.util.Arrays;

class GFG
{

// function to find largest d
static int findLargestd(int []S, int n)
{
    boolean found = false;

    // sort the array in
    // ascending order
    Arrays.sort(S);

    // iterating from backwards to
    // find the required largest d
    for (int i = n - 1; i >= 0; i--)
    {
        for (int j = 0; j < n; j++)
        {

            // since all four a, b, c,
            // d should be distinct
            if (i == j)
                continue;

            for (int k = j + 1; k < n; k++)
            {
                if (i == k)
                    continue;

                for (int l = k + 1; l < n; l++)
                {
                    if (i == l)
                        continue;

                    // if the current combination 
                    // of j, k, l in the set is
                    // equal to S[i] return this
                    // value as this would be the
                    // largest d since we are 
                    // iterating in descending order
                    if (S[i] == S[j] + S[k] + S[l])
                    {
                        found = true;
                        return S[i];
                    }
                }
            }
        }
    }
    if (found == false)
        return Integer.MAX_VALUE;

    return -1;
}

// Driver Code
public static void main(String []args)
{
    // Set of distinct Integers
    int []S = new int[]{ 2, 3, 5, 7, 12 };
    int n = S.length;

    int ans = findLargestd(S, n);
    if (ans == Integer.MAX_VALUE)
        System.out.println("No Solution");
    else
        System.out.println("Largest d such that " +
                         "a + " + "b + c = d is " +
                                             ans );

}
}

// This code is contributed by Sam007
```

## 蟒蛇 3

```
# Python Program to find the largest
# d such that d = a + b + c

def findLargestd(S, n) :
    found = False

    # sort the array in ascending order
    S.sort()

    # iterating from backwards to
    # find the required largest d
    for i in range(n-1, -1, -1) :
        for j in range(0, n) :

            # since all four a, b, c,
            # d should be distinct
            if (i == j) :
                continue

            for k in range(j + 1, n) :
                if (i == k) :
                    continue

                for l in range(k+1, n) :
                    if (i == l) :
                        continue

                    # if the current combination
                    # of j, k, l in the set is
                    # equal to S[i] return this
                    # value as this would be the
                    # largest d since we are
                    # iterating in descending order
                    if (S[i] == S[j] + S[k] + S[l]) :
                        found = True
                        return S[i]                

    if (found == False) :
        return -1

# Driver Code

# Set of distinct Integers
S = [ 2, 3, 5, 7, 12 ]
n = len(S)

ans = findLargestd(S, n)
if (ans == -1) :
    print ("No Solution")
else :
    print ("Largest d such that a + b +" ,
        "c = d is" ,ans)

# This code is contributed by Manish Shaw
# (manishshaw1)
```

## C#

```
// C# Program to find the largest
// such that d = a + b + c
using System;

class GFG
{

// function to find largest d
static int findLargestd(int []S,
                        int n)
{
    bool found = false;

    // sort the array
    // in ascending order
    Array.Sort(S);

    // iterating from backwards to
    // find the required largest d
    for (int i = n - 1; i >= 0; i--)
    {
        for (int j = 0; j < n; j++)
        {

            // since all four a, b, c,
            // d should be distinct
            if (i == j)
                continue;

            for (int k = j + 1; k < n; k++)
            {
                if (i == k)
                    continue;

                for (int l = k + 1; l < n; l++)
                {
                    if (i == l)
                        continue;

                    // if the current combination
                    // of j, k, l in the set is
                    // equal to S[i] return this
                    // value as this would be the
                    // largest dsince we are 
                    // iterating in descending order
                    if (S[i] == S[j] + S[k] + S[l])
                    {
                        found = true;
                        return S[i];
                    }
                }
            }
        }
    }
    if (found == false)
        return int.MaxValue;

    return -1;
}

// Driver Code
public static void Main()
{
    // Set of distinct Integers
    int []S = new int[]{ 2, 3, 5, 7, 12 };
    int n = S.Length;

    int ans = findLargestd(S, n);
    if (ans == int.MaxValue)
        Console.WriteLine( "No Solution");
    else
        Console.Write("Largest d such that a + " +
                          "b + c = d is " + ans );

}
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the largest
// d such that d = a + b + c

function findLargestd( $S, $n)
{
$found = false;

    // sort the array in
    // ascending order
    sort($S);

    // iterating from backwards to
    // find the required largest d
    for ( $i = $n - 1; $i >= 0; $i--)
    {
        for ( $j = 0; $j < $n; $j++)
        {

            // since all four a, b, c, 
            // d should be distinct
            if ($i == $j)
                continue;

            for ( $k = $j + 1; $k < $n; $k++)
            {
                if ($i == $k)
                    continue;

                for ( $l = $k + 1; $l < $n; $l++)
                {
                    if ($i == $l)
                        continue;

                    // if the current combination
                    // of j, k, l in the set is
                    // equal to S[i] return this
                    // value as this would be the
                    // largest d since we are 
                    // iterating in descending order
                    if ($S[$i] == $S[$j] + $S[$k] + $S[$l])
                    {
                        $found = true;
                        return $S[$i];
                    }
                }
            }
        }
    }
    if ($found == false)
        return PHP_INT_MIN;
}

// Driver Code

// Set of distinct Integers
$S = array( 2, 3, 5, 7, 12 );
$n = count($S);

$ans = findLargestd($S, $n);
if ($ans == PHP_INT_MIN)
    echo "No Solution" ;
else
    echo "Largest d such that a + b + " ,
         "c = d is " , $ans ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript Program to find the largest
    // such that d = a + b + c

    // function to find largest d
    function findLargestd(S, n)
    {
        let found = false;

        // sort the array
        // in ascending order
        S.sort();

        // iterating from backwards to
        // find the required largest d
        for (let i = n - 1; i >= 0; i--)
        {
            for (let j = 0; j < n; j++)
            {

                // since all four a, b, c,
                // d should be distinct
                if (i == j)
                    continue;

                for (let k = j + 1; k < n; k++)
                {
                    if (i == k)
                        continue;

                    for (let l = k + 1; l < n; l++)
                    {
                        if (i == l)
                            continue;

                        // if the current combination
                        // of j, k, l in the set is
                        // equal to S[i] return this
                        // value as this would be the
                        // largest dsince we are 
                        // iterating in descending order
                        if (S[i] == S[j] + S[k] + S[l])
                        {
                            found = true;
                            return S[i];
                        }
                    }
                }
            }
        }
        if (found == false)
            return Number.MAX_VALUE;

        return -1;
    }

    // Set of distinct Integers
    let S = [ 2, 3, 5, 7, 12 ];
    let n = S.length;

    let ans = findLargestd(S, n);
    if (ans == Number.MAX_VALUE)
        document.write( "No Solution");
    else
        document.write("Largest d such that a + " +
                          "b + c = d is " + ans );

</script>
```

**Output :** 

```
Largest d such that a + b + c = d is 12
```

这个强力解决方案的时间复杂度为 0((集合的大小) <sup>4</sup> )。
**方法 2(高效方法–使用哈希)**
上述问题陈述(a + b + c = d)可以重述为寻找 a、b、c、d，使得 a+b = d–c。因此，这个问题可以使用哈希有效地解决。

1.  将所有对(a + b)的总和存储在哈希表中
2.  再次遍历所有对(c，d)，并在哈希表中搜索(d–c)。
3.  如果找到具有所需总和的对，则确保所有元素都是不同的数组元素，并且一个元素不会被考虑多次。

下面是上述方法的实现。

## C++

```
// A hashing based CPP program to find largest d
// such that a + b + c = d.
#include <bits/stdc++.h>
using namespace std;

// The function finds four elements with given sum X
int findFourElements(int arr[], int n)
{
    // Store sums  (a+b) of all pairs (a,b) in a
    // hash table
    unordered_map<int, pair<int, int> > mp;
    for (int i = 0; i < n - 1; i++)
        for (int j = i + 1; j < n; j++)
            mp[arr[i] + arr[j]] = { i, j };

    // Traverse through all pairs and find (d -c)
    // is present in hash table
    int d = INT_MIN;
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            int abs_diff = abs(arr[i] - arr[j]);

            // If d - c is present in hash table,
            if (mp.find(abs_diff) != mp.end()) {

                // Making sure that all elements are
                // distinct array elements and an element
                // is not considered more than once.
                pair<int, int> p = mp[abs_diff];
                if (p.first != i && p.first != j &&
                    p.second != i && p.second != j)
                    d = max(d, max(arr[i], arr[j]));
            }
        }
    }
    return d;
}

// Driver program to test above function
int main()
{
    int arr[] = { 2, 3, 5, 7, 12 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int res = findFourElements(arr, n);
    if (res == INT_MIN)
        cout << "No Solution.";
    else
        cout << res;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A hashing based Java program to find largest d
// such that a + b + c = d.
import java.util.HashMap;
import java.lang.Math;

// To store and retrieve indices pair i & j
class Indexes
{
    int i, j;

    Indexes(int i, int j)
    {
        this.i = i;
        this.j = j;
    }

    int getI()
    {
        return i;
    }

    int getJ()
    {
        return j;
    }
}

class GFG {

    // The function finds four elements with given sum X
    static int findFourElements(int[] arr, int n)
    {
        HashMap<Integer, Indexes> map = new HashMap<>();

        // Store sums (a+b) of all pairs (a,b) in a
        // hash table
        for (int i = 0; i < n - 1; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                map.put(arr[i] + arr[j], new Indexes(i, j));
            }
        }

        int d = Integer.MIN_VALUE;

        // Traverse through all pairs and find (d -c)
        // is present in hash table
        for (int i = 0; i < n - 1; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                int abs_diff = Math.abs(arr[i] - arr[j]);

                // If d - c is present in hash table,
                if (map.containsKey(abs_diff))
                {
                    Indexes indexes = map.get(abs_diff);

                    // Making sure that all elements are
                    // distinct array elements and an element
                    // is not considered more than once.
                    if (indexes.getI() != i && indexes.getI() != j &&
                    indexes.getJ() != i && indexes.getJ() != j)
                    {
                        d = Math.max(d, Math.max(arr[i], arr[j]));
                    }
                }
            }
        }
        return d;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 3, 5, 7, 12 };
        int n = arr.length;
        int res = findFourElements(arr, n);
        if (res == Integer.MIN_VALUE)
            System.out.println("No Solution");
        else
            System.out.println(res);
    }
}

// This code is contributed by Vivekkumar Singh
```

## 蟒蛇 3

```
# A hashing based Python3 program to find
# largest d, such that a + b + c = d.

# The function finds four elements
# with given sum X
def findFourElements(arr, n):

    # Store sums (a+b) of all pairs (a,b) in a
    # hash table
    mp = dict()
    for i in range(n - 1):
        for j in range(i + 1, n):
            mp[arr[i] + arr[j]] =(i, j)

    # Traverse through all pairs and find (d -c)
    # is present in hash table
    d = -10**9
    for i in range(n - 1):
        for j in range(i + 1, n):
            abs_diff = abs(arr[i] - arr[j])

            # If d - c is present in hash table,
            if abs_diff in mp.keys():

                # Making sure that all elements are
                # distinct array elements and an element
                # is not considered more than once.
                p = mp[abs_diff]
                if (p[0] != i and p[0] != j and
                    p[1] != i and p[1] != j):
                    d = max(d, max(arr[i], arr[j]))

    return d

# Driver Code
arr = [2, 3, 5, 7, 12]
n = len(arr)
res = findFourElements(arr, n)
if (res == -10**9):
    print("No Solution.")
else:
    print(res)

# This code is contributed by Mohit Kumar
```

## C#

```
// A hashing based C# program to find
// largest d such that a + b + c = d.
using System;
using System.Collections.Generic;

// To store and retrieve
// indices pair i & j
public class Indexes
{
    int i, j;

    public Indexes(int i, int j)
    {
        this.i = i;
        this.j = j;
    }

    public int getI()
    {
        return i;
    }

    public int getJ()
    {
        return j;
    }
}

public class GFG
{

    // The function finds four elements
    // with given sum X
    static int findFourElements(int[] arr, int n)
    {
        Dictionary<int, Indexes> map =
                    new Dictionary<int, Indexes>();

        // Store sums (a+b) of all pairs
        // (a,b) in a hash table
        for (int i = 0; i < n - 1; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                map.Add(arr[i] + arr[j],
                        new Indexes(i, j));
            }
        }

        int d = int.MinValue;

        // Traverse through all pairs and
        // find (d -c) is present in hash table
        for (int i = 0; i < n - 1; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                int abs_diff = Math.Abs(arr[i] - arr[j]);

                // If d - c is present in hash table,
                if (map.ContainsKey(abs_diff))
                {
                    Indexes indexes = map[abs_diff];

                    // Making sure that all elements are
                    // distinct array elements and an element
                    // is not considered more than once.
                    if (indexes.getI() != i &&
                        indexes.getI() != j &&
                        indexes.getJ() != i &&
                        indexes.getJ() != j)
                    {
                        d = Math.Max(d, Math.Max(arr[i],
                                                 arr[j]));
                    }
                }
            }
        }
        return d;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 2, 3, 5, 7, 12 };
        int n = arr.Length;
        int res = findFourElements(arr, n);
        if (res == int.MinValue)
            Console.WriteLine("No Solution");
        else
            Console.WriteLine(res);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// A hashing based Javascript program to find largest d
// such that a + b + c = d.

// To store and retrieve indices pair i & j
class Indexes
{
       constructor(i,j)
    {
        this.i = i;
        this.j = j;
    }

    getI()
    {
        return this.i;
    }

    getJ()
    {
        return this.j;
    }
}

// The function finds four elements with given sum X
function findFourElements(arr,n)
{
    let map = new Map();

        // Store sums (a+b) of all pairs (a,b) in a
        // hash table
        for (let i = 0; i < n - 1; i++)
        {
            for (let j = i + 1; j < n; j++)
            {
                map.set(arr[i] + arr[j], new Indexes(i, j));
            }
        }

        let d = Number.MIN_VALUE;

        // Traverse through all pairs and find (d -c)
        // is present in hash table
        for (let i = 0; i < n - 1; i++)
        {
            for (let j = i + 1; j < n; j++)
            {
                let abs_diff = Math.abs(arr[i] - arr[j]);

                // If d - c is present in hash table,
                if (map.has(abs_diff))
                {
                    let indexes = map.get(abs_diff);

                    // Making sure that all elements are
                    // distinct array elements and an element
                    // is not considered more than once.
                    if (indexes.getI() != i && indexes.getI() != j &&
                    indexes.getJ() != i && indexes.getJ() != j)
                    {
                        d = Math.max(d, Math.max(arr[i], arr[j]));
                    }
                }
            }
        }
        return d;
}

// Driver code
let arr=[ 2, 3, 5, 7, 12];
let n = arr.length;
let res = findFourElements(arr, n);
if (res == Number.MIN_VALUE)
    document.write("No Solution");
else
    document.write(res);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
12
```

这种有效方法的总时间复杂度是 **O(N <sup>2</sup> )** (其中 N 是集合的大小)。