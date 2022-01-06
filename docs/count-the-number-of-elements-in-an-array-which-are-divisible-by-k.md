# 计算一个数组中可被 k 整除的元素个数

> 原文:[https://www . geesforgeks . org/count-数组中可被 k 整除的元素个数/](https://www.geeksforgeeks.org/count-the-number-of-elements-in-an-array-which-are-divisible-by-k/)

给定一个整数数组。任务是计算可被给定数 k 整除的元素数。

**示例:**

```
Input: arr[] = { 2, 6, 7, 12, 14, 18 }, k = 3
Output: 3
Numbers which are divisible by k are { 6, 12, 18 }

Input: arr[] = { 2, 6, 7, 12, 14, 18 }, k = 2
Output: 5
```

**方法-1:** 开始遍历数组，检查当前元素是否可被 k 整除，如果是，则递增计数。遍历所有元素时打印计数。

下面是上述方法的实现:

## C++

```
// C++ program to Count the number of elements
// in an array which are divisible by k
#include <iostream>
using namespace std;

// Function to count the elements
int CountTheElements(int arr[], int n, int k)
{
    int counter = 0;

    for (int i = 0; i < n; i++) {
        if (arr[i] % k == 0)
            counter++;
    }

    return counter;
}

// Driver code
int main()
{
    int arr[] = { 2, 6, 7, 12, 14, 18 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    cout << CountTheElements(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Count the number of elements
// in an array which are divisible by k
import java.util.*;

class Geeks {

// Function to count the elements
static int CountTheElements(int arr[], int n, int k)
{
    int counter = 0;

    for (int i = 0; i < n; i++) {
        if (arr[i] % k == 0)
            counter++;
    }

    return counter;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 2, 6, 7, 12, 14, 18 };
    int n = arr.length;
    int k = 3;

    System.out.println(CountTheElements(arr, n, k));
}
}

// This code is contributed by ankita_saini
```

## 蟒蛇 3

```
# Python 3 program to Count the
# number of elements in an array
# which are divisible by k

# Function to count the elements
def CountTheElements(arr, n, k):
    counter = 0

    for i in range(0, n, 1):
        if (arr[i] % k == 0):
            counter = counter+1

    return counter

# Driver code
if __name__ == '__main__':
    arr = [2, 6, 7, 12, 14, 18];
    n = len(arr)
    k = 3

    print(CountTheElements(arr, n, k))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to Count the number of elements
// in an array which are divisible by k
using System;

class Geeks {

// Function to count the elements
static int CountTheElements(int []arr, int n, int k)
{
    int counter = 0;

    for (int i = 0; i < n; i++) {
        if (arr[i] % k == 0)
            counter++;
    }

    return counter;
}

// Driver code
public static void Main()
{
    int []arr = { 2, 6, 7, 12, 14, 18 };
    int n = arr.Length;
    int k = 3;

    Console.WriteLine(CountTheElements(arr, n, k));
}
}
//This code is contributed by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Count the number of elements
// in an array which are divisible by k

// Function to count the elements
function CountTheElements($arr, $n, $k)
{
    $counter = 0;

    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] % $k == 0)
            $counter++;
    }

    return $counter;
}

// Driver code
$arr = array( 2, 6, 7, 12, 14, 18 );
$n = count($arr);
$k = 3;

echo CountTheElements($arr, $n, $k);

// This code is contributed by inder_verma
?>
```

## java 描述语言

```
<script>

// Javascript program to Count the number
// of elements in an array which are
// divisible by k

// Function to count the elements
function CountTheElements(arr, n, k)
{
    let counter = 0;

    for(let i = 0; i < n; i++)
    {
        if (arr[i] % k == 0)
            counter++;
    }

    return counter;
}

// Driver code
let arr = [ 2, 6, 7, 12, 14, 18 ];
let n = arr.length;
let k = 3;

document.write(CountTheElements(arr, n, k));

// This code is contributed by subhammahato348

</script>
```

**Output:** 

```
3
```

**方法-2:** 另一种方法是使用内置函数–[Count _ if](https://www.geeksforgeeks.org/count_if-in-c/)。这个函数接受指向包含元素和辅助函数的容器的开始和结束的指针。它将返回函数将返回 true 的元素计数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
int main()
{
    vector<int> v{ 2, 6, 7, 12, 14, 18 };

    // Count the number elements which when passed
    // through the function (3rd argument) returns true
    int res = count_if(v.begin(), v.end(),
                       [](int i, int k = 3) { return i % k == 0; });
    cout << res;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{
public static void main(String[] args)
{
   int []v = { 2, 6, 7, 12, 14, 18 };

    // Count the number elements which when passed
    // through the function (3rd argument) returns true
    int res = 0;
    for(int i = 0; i < v.length; i++) {
        if(v[i] % 3 == 0)
            res++;
    }
     System.out.print(res);

}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Java implementation of the above approach
v = [ 2, 6, 7, 12, 14, 18 ];

# Count the number elements which when passed
# through the function (3rd argument) returns true
res = 0
for i in range(0,len(v)):
    if(v[i] % 3 == 0):
        res+=1

print(res)
# This code is contributed by shivanisinghss2110
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
public static void Main(String[] args)
{
   int []v = { 2, 6, 7, 12, 14, 18 };

    // Count the number elements which when passed
    // through the function (3rd argument) returns true
    int res = 0;
    for(int i = 0; i < v.Length; i++) {
        if(v[i] % 3 == 0)
            res++;
    }
     Console.Write(res);

}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach
var v = [ 2, 6, 7, 12, 14, 18 ];

    // Count the number elements which when passed
    // through the function (3rd argument) returns true
    var res = 0;
    for(var i = 0; i < v.length; i++) {
        if(v[i] % 3 == 0)
            res++;
    }
     document.write(res);

// This code is contributed by shivanisinghss2110

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)