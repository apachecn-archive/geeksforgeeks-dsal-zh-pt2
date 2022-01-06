# 计算给定数组中 K 的因子

> 原文:[https://www . geeksforgeeks . org/给定数组中 k 的计数因子/](https://www.geeksforgeeks.org/count-the-factors-of-k-present-in-the-given-array/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是计算数组中存在的 **K** 的因子。
**举例:**

> **输入:** arr[] = {1，2，4，5，6}，K = 6
> **输出:** 3
> **解释:**
> 数组中有三个数字，它们是 K = 6 –{ 1，2，6}
> **输入:**arr[= { 1，2，12，24}，K = 20
> **输出:** 2

****天真方法:**这个问题的一个简单解决方案是[找到 K 的所有因子](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)，然后对每个因子迭代数组并检查它是否存在于数组中。如果是，则将因子的计数增加 1。
**有效方法:**想法是代替[找到数字 K 的所有因子](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)迭代数组，并在[模运算符](https://www.geeksforgeeks.org/modulo-operator-in-c-cpp-with-examples/)的帮助下检查每个元素是否是 K 的因子。如果是，则增加因子 k 的计数。
下面是上述方法的实现:** 

## **C++**

```
// C++ implementation to find the count
// of factors of K present in array

#include <iostream>
using namespace std;

// Function to find the count
// of factors of K present in array
int calcCount(int arr[], int n, int k)
{
    int count = 0;

    // Loop to consider every
    // element of array
    for (int i = 0; i < n; i++) {
        if (k % arr[i] == 0)
            count++;
    }

    return count;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 6;

    // Function Call
    cout << calcCount(arr, n, k);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation to find the count
// of factors of K present in array
class GFG{

// Function to find the count
// of factors of K present in array
static int calcCount(int arr[], int n, int k)
{
    int count = 0;

    // Loop to consider every
    // element of array
    for(int i = 0; i < n; i++)
    {
       if (k % arr[i] == 0)
           count++;
    }
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 4, 5, 6 };
    int n = arr.length;
    int k = 6;

    // Function Call
    System.out.print(calcCount(arr, n, k));
}
}

// This code is contributed by gauravrajput1
```

## **蟒蛇 3**

```
# Python3 implementation to find the count
# of factors of K present in array

# Function to find the count
# of factors of K present in array
def calcCount(arr, n, k):

    count = 0

    # Loop to consider every
    # element of array
    for i in range(0, n):
        if (k % arr[i] == 0):
            count = count + 1

    return count

# Driver Code
arr = [ 1, 2, 4, 5, 6 ]
n = len(arr)
k = 6

# Function Call
print(calcCount(arr, n, k))

# This code is contributed by PratikBasu   
```

## **C#**

```
// C# implementation to find the count
// of factors of K present in array
using System;

class GFG{

// Function to find the count
// of factors of K present in array
static int calcCount(int []arr, int n, int k)
{
    int count = 0;

    // Loop to consider every
    // element of array
    for(int i = 0; i < n; i++)
    {
       if (k % arr[i] == 0)
           count++;
    }
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 4, 5, 6 };
    int n = arr.Length;
    int k = 6;

    // Function Call
    Console.Write(calcCount(arr, n, k));
}
}

// This code is contributed by Amit Katiyar
```

## **java 描述语言**

```
<script>

// Javascript implementation to find the count
// of factors of K present in array

// Function to find the count
// of factors of K present in array
function calcCount(arr, n, k)
{
    var count = 0;

    // Loop to consider every
    // element of array
    for (var i = 0; i < n; i++) {
        if (k % arr[i] == 0)
            count++;
    }

    return count;
}

// Driver Code
var arr = [ 1, 2, 4, 5, 6 ];
var n = arr.length;
var k = 6;

// Function Call
document.write( calcCount(arr, n, k));

</script>
```

****Output:** 

```
3
```** 

*****时间复杂度:** O(N)***

*****辅助空间:**O(1)*T4】**