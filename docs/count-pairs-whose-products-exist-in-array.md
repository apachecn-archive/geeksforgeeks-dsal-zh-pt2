# 计数成阵列存在产品的对

> 原文:[https://www . geesforgeks . org/count-pairs-其产品存在于阵列中/](https://www.geeksforgeeks.org/count-pairs-whose-products-exist-in-array/)

给定一个数组，计算那些乘积值出现在数组中的对。
**例:**

```
Input : arr[] = {6, 2, 4, 12, 5, 3}
Output : 3
       All pairs whose product exist in array 
       (6 , 2) (2, 3) (4, 3)   

Input :  arr[] = {3, 5, 2, 4, 15, 8}
Output : 2 
```

一个**简单的解决方案**是生成给定数组的所有对，并检查数组中是否存在乘积。如果存在，则递增计数。最后返回计数。
以下是上述想法的实现

## C++

```
// C++ program to count pairs whose product exist in array
#include<bits/stdc++.h>
using namespace std;

// Returns count of pairs whose product exists in arr[]
int countPairs( int arr[] ,int n)
{
    int result = 0;
    for (int i = 0; i < n ; i++)
    {
        for (int j = i+1 ; j < n ; j++)
        {
            int product = arr[i] * arr[j] ;

            // find product in an array
            for (int k = 0; k < n; k++)
            {
                // if product found increment counter
                if (arr[k] == product)
                {
                    result++;
                    break;
                }
            }
        }
    }

    // return Count of all pair whose product exist in array
    return result;
}

//Driver program
int main()
{
    int arr[] = {6 ,2 ,4 ,12 ,5 ,3} ;
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << countPairs(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pairs
// whose product exist in array
import java.io.*;

class GFG
{

// Returns count of pairs
// whose product exists in arr[]
static int countPairs(int arr[],
                      int n)
{
    int result = 0;
    for (int i = 0; i < n ; i++)
    {
        for (int j = i + 1 ; j < n ; j++)
        {
            int product = arr[i] * arr[j] ;

            // find product
            // in an array
            for (int k = 0; k < n; k++)
            {
                // if product found
                // increment counter
                if (arr[k] == product)
                {
                    result++;
                    break;
                }
            }
        }
    }

    // return Count of all pair
    // whose product exist in array
    return result;
}

// Driver Code
public static void main (String[] args)
{
int arr[] = {6, 2, 4, 12, 5, 3} ;
int n = arr.length;
System.out.println(countPairs(arr, n));
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python program to count pairs whose
# product exist in array

# Returns count of pairs whose
# product exists in arr[]
def countPairs(arr, n):

    result = 0;
    for i in range (0, n):

        for j in range(i + 1, n):

            product = arr[i] * arr[j] ;

            # find product in an array
            for k in range (0, n):

                # if product found increment counter
                if (arr[k] == product):
                    result = result + 1;
                    break;

    # return Count of all pair whose
    # product exist in array
    return result;

# Driver program
arr = [6, 2, 4, 12, 5, 3] ;
n = len(arr);
print(countPairs(arr, n));

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// C# program to count pairs
// whose product exist in array
using System;

class GFG
{

// Returns count of pairs
// whose product exists in arr[]
public static int countPairs(int[] arr,
                             int n)
{
    int result = 0;
    for (int i = 0; i < n ; i++)
    {
        for (int j = i + 1 ; j < n ; j++)
        {
            int product = arr[i] * arr[j];

            // find product in an array
            for (int k = 0; k < n; k++)
            {
                // if product found
                // increment counter
                if (arr[k] == product)
                {
                    result++;
                    break;
                }
            }
        }
    }

    // return Count of all pair
    // whose product exist in array
    return result;
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = new int[] {6, 2, 4, 12, 5, 3};
    int n = arr.Length;
    Console.WriteLine(countPairs(arr, n));
}
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count pairs
// whose product exist in array

// Returns count of pairs whose
// product exists in arr[]
function countPairs($arr, $n)
{
    $result = 0;
    for ($i = 0; $i < $n ; $i++)
    {
        for ($j = $i + 1 ; $j < $n ; $j++)
        {
            $product = $arr[$i] * $arr[$j] ;

            // find product in an array
            for ($k = 0; $k < $n; $k++)
            {
                // if product found increment counter
                if ($arr[$k] == $product)
                {
                    $result++;
                    break;
                }
            }
        }
    }

    // return Count of all pair whose
    // product exist in array
    return $result;
}

// Driver Code
$arr = array(6, 2, 4, 12, 5, 3);
$n = sizeof($arr);
echo countPairs($arr, $n);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
// javascript program to count pairs
// whose product exist in array

    // Returns count of pairs
    // whose product exists in arr
    function countPairs(arr, n)
    {
        var result = 0;
        for (i = 0; i < n; i++)
        {
            for (j = i + 1; j < n; j++)
            {
                var product = arr[i] * arr[j];

                // find product
                // in an array
                for (k = 0; k < n; k++)
                {

                    // if product found
                    // increment counter
                    if (arr[k] == product)
                    {
                        result++;
                        break;
                    }
                }
            }
        }

        // return Count of all pair
        // whose product exist in array
        return result;
    }

    // Driver Code
        var arr = [ 6, 2, 4, 12, 5, 3 ];
        var n = arr.length;
        document.write(countPairs(arr, n));

// This code is contributed by Rajput-Ji
</script>
```

**输出:**

```
3
```

**时间复杂度:** O(n <sup>3</sup> )
一个**高效的解决方案**是使用存储所有数组元素的‘hash’。生成给定数组“arr”所有可能的对，并检查每对的乘积是否在“hash”中。如果存在，则递增计数。最终返回计数。
以下是上述想法的实现

## C++

```
// A hashing based C++ program to count pairs whose product
// exists in arr[]
#include<bits/stdc++.h>
using namespace std;

// Returns count of pairs whose product exists in arr[]
int countPairs(int arr[] , int n)
{
    int result = 0;

    // Create an empty hash-set that store all array element
    set< int > Hash;

    // Insert all array element into set
    for (int i = 0 ; i < n; i++)
        Hash.insert(arr[i]);

    // Generate all pairs and check is exist in 'Hash' or not
    for (int i = 0 ; i < n; i++)
    {
        for (int j = i + 1; j<n ; j++)
        {
            int product = arr[i]*arr[j];

            // if product exists in set then we increment
            // count by 1
            if (Hash.find(product) != Hash.end())
                result++;
        }
    }

    // return count of pairs whose product exist in array
    return result;
}

// Driver program
int main()
{
    int arr[] = {6 ,2 ,4 ,12 ,5 ,3};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << countPairs(arr, n) ;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A hashing based Java program to count pairs whose product
// exists in arr[]
import java.util.*;

class GFG
{

    // Returns count of pairs whose product exists in arr[]
    static int countPairs(int arr[], int n) {
        int result = 0;

        // Create an empty hash-set that store all array element
        HashSet< Integer> Hash = new HashSet<>();

        // Insert all array element into set
        for (int i = 0; i < n; i++)
        {
            Hash.add(arr[i]);
        }

        // Generate all pairs and check is exist in 'Hash' or not
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                int product = arr[i] * arr[j];

                // if product exists in set then we increment
                // count by 1
                if (Hash.contains(product))
                {
                    result++;
                }
            }
        }

        // return count of pairs whose product exist in array
        return result;
    }

    // Driver program
    public static void main(String[] args)
    {
        int arr[] = {6, 2, 4, 12, 5, 3};
        int n = arr.length;
        System.out.println(countPairs(arr, n));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# A hashing based C++ program to count
# pairs whose product exists in arr[]

# Returns count of pairs whose product
# exists in arr[]
def countPairs(arr, n):
    result = 0

    # Create an empty hash-set that
    # store all array element
    Hash = set()

    # Insert all array element into set
    for i in range(n):
        Hash.add(arr[i])

    # Generate all pairs and check is
    # exist in 'Hash' or not
    for i in range(n):
        for j in range(i + 1, n):
            product = arr[i] * arr[j]

            # if product exists in set then
            # we increment count by 1
            if product in(Hash):
                result += 1

    # return count of pairs whose
    # product exist in array
    return result

# Driver Code
if __name__ == '__main__':
    arr = [6, 2, 4, 12, 5, 3]
    n = len(arr)
    print(countPairs(arr, n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// A hashing based C# program to count pairs whose product
// exists in arr[]
using System;
using System.Collections.Generic;

class GFG
{

    // Returns count of pairs whose product exists in arr[]
    static int countPairs(int []arr, int n)
    {
        int result = 0;

        // Create an empty hash-set that store all array element
        HashSet<int> Hash = new HashSet<int>();

        // Insert all array element into set
        for (int i = 0; i < n; i++)
        {
            Hash.Add(arr[i]);
        }

        // Generate all pairs and check is exist in 'Hash' or not
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                int product = arr[i] * arr[j];

                // if product exists in set then we increment
                // count by 1
                if (Hash.Contains(product))
                {
                    result++;
                }
            }
        }

        // return count of pairs whose product exist in array
        return result;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {6, 2, 4, 12, 5, 3};
        int n = arr.Length;
        Console.WriteLine(countPairs(arr, n));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
// A hashing based javascript program to count pairs whose product
// exists in arr

    // Returns count of pairs whose product exists in arr
    function countPairs(arr , n) {
        var result = 0;

        // Create an empty hash-set that store all array element
        var Hash = new Set();

        // Insert all array element into set
        for (i = 0; i < n; i++) {
            Hash.add(arr[i]);
        }

        // Generate all pairs and check is exist in 'Hash' or not
        for (i = 0; i < n; i++) {
            for (j = i + 1; j < n; j++) {
                var product = arr[i] * arr[j];

                // if product exists in set then we increment
                // count by 1
                if (Hash.has(product)) {
                    result++;
                }
            }
        }

        // return count of pairs whose product exist in array
        return result;
    }

    // Driver program

        var arr = [ 6, 2, 4, 12, 5, 3 ];
        var n = arr.length;
        document.write(countPairs(arr, n));

// This code contributed by Rajput-Ji
</script>
```

**输出:**

```
3
```

**时间复杂度:** O(n <sup>2</sup> )【假设插入下，查找操作取 O(1)时间】
本文由[**Nishant _ Singh(Pintu)**](https://practice.geeksforgeeks.org/user-profile.php?user=_code)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。