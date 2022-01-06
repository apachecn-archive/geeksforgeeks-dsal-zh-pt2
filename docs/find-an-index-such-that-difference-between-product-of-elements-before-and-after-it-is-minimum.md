# 找到一个指数，使前后元素乘积之差最小

> 原文:[https://www . geeksforgeeks . org/find-a-index-a-elements-product-of-before-it-before-minimum/](https://www.geeksforgeeks.org/find-an-index-such-that-difference-between-product-of-elements-before-and-after-it-is-minimum/)

给定一个整数**arr【】**，任务是找到一个索引，使得达到该索引的元素的乘积(包括该索引)与其余元素的乘积之差最小。如果存在多个这样的索引，则返回最小索引作为答案。

**示例:**

> **输入:** arr[] = { 2，2，1 }
> **输出:** 0
> 对于指数 0:ABS((2)–(2 * 1))= 0
> 对于指数 1:ABS((2 * 2)–(1))= 3
> 
> **输入:** arr[] = { 3，2，5，7，2，9 }
> T3】输出: 2

一个**简单的解决方案**是从第一个到第二个最后一个元素开始遍历所有元素。对于每个元素，找到元素的乘积，直到这个元素(包括这个元素)。然后在它之后找到元素的乘积。最后计算差异。如果到目前为止差异最小，请更新结果。

**更好的方法:**使用前缀乘积数组*prod【】*可以很容易地解决这个问题，其中**prod【I】**存储从**arr【0】**到**arr【I】**的元素乘积。因此，通过将数组的总积除以到当前索引的积，可以很容易地找到其余元素的积。现在，迭代乘积数组以找到差异最小的索引。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to return the index i such that
// the absolute difference between product
// of elements up to that index and the
// product of rest of the elements
// of the array is minimum
int findIndex(int a[], int n)
{
    // To store the required index
    int res;

    ll min_diff = INT_MAX;

    // Prefix product array
    ll prod[n];
    prod[0] = a[0];

    // Compute the product array
    for (int i = 1; i < n; i++)
        prod[i] = prod[i - 1] * a[i];

    // Iterate the product array to find the index
    for (int i = 0; i < n - 1; i++) {
        ll curr_diff = abs((prod[n - 1] / prod[i]) - prod[i]);

        if (curr_diff < min_diff) {
            min_diff = curr_diff;
            res = i;
        }
    }

    return res;
}

// Driver code
int main()
{
    int arr[] = { 3, 2, 5, 7, 2, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << findIndex(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG{

// Function to return the index i such that
// the absolute difference between product
// of elements up to that index and the
// product of rest of the elements
// of the array is minimum
static int findIndex(int a[], int n)
{
    // To store the required index
    int res = 0;

    long min_diff = Long.MAX_VALUE;

    // Prefix product array
    long prod[] = new long[n];
    prod[0] = a[0];

    // Compute the product array
    for (int i = 1; i < n; i++)
        prod[i] = prod[i - 1] * a[i];

    // Iterate the product array to find the index
    for (int i = 0; i < n - 1; i++)
    {
        long curr_diff = Math.abs((prod[n - 1] /
                                   prod[i]) - prod[i]);

        if (curr_diff < min_diff)
        {
            min_diff = curr_diff;
            res = i;
        }
    }

    return res;
}

// Driver code
public static void main(String arg[])
{
    int arr[] = { 3, 2, 5, 7, 2, 9 };
    int N = arr.length;

    System.out.println(findIndex(arr, N));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the index i such that
# the absolute difference between product of
# elements up to that index and the product of
# rest of the elements of the array is minimum
def findIndex(a, n):

    # To store the required index
    res, min_diff = None, float('inf')

    # Prefix product array
    prod = [None] * n
    prod[0] = a[0]

    # Compute the product array
    for i in range(1, n):
        prod[i] = prod[i - 1] * a[i]

    # Iterate the product array to find the index
    for i in range(0, n - 1): 
        curr_diff = abs((prod[n - 1] // prod[i]) - prod[i])

        if curr_diff < min_diff: 
            min_diff = curr_diff
            res = i

    return res

# Driver code
if __name__ == "__main__":

    arr = [3, 2, 5, 7, 2, 9] 
    N = len(arr)

    print(findIndex(arr, N))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to return the index i such that 
    // the absolute difference between product 
    // of elements up to that index and the 
    // product of rest of the elements 
    // of the array is minimum 
    static int findIndex(int[] a, int n) 
    { 
        // To store the required index 
        int res = 0; 

        long min_diff = Int64.MaxValue; 

        // Prefix product array 
        long[] prod = new long[n]; 
        prod[0] = a[0]; 

        // Compute the product array 
        for (int i = 1; i < n; i++) 
            prod[i] = prod[i - 1] * a[i]; 

        // Iterate the product array to find the index 
        for (int i = 0; i < n - 1; i++)
        { 
            long curr_diff = Math.Abs((prod[n - 1] / 
                                       prod[i]) - prod[i]); 

            if (curr_diff < min_diff) 
            { 
                min_diff = curr_diff; 
                res = i; 
            } 
        } 

        return res; 
    } 

  // Driver code
  static void Main()
  {
        int[] arr = { 3, 2, 5, 7, 2, 9 }; 
        int N = arr.Length; 

        Console.WriteLine(findIndex(arr, N)); 
  }
}

// This code is contributed by divyeshrabadiya07
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the index i such that
// the absolute difference between product
// of elements up to that index and the
// product of rest of the elements
// of the array is minimum
function findIndex($a, $n)
{
    $min_diff = PHP_INT_MAX;

    // Prefix product array
    $prod = array();
    $prod[0] = $a[0];

    // Compute the product array
    for ($i = 1; $i < $n; $i++)
        $prod[$i] = $prod[$i - 1] * $a[$i];

    // Iterate the product array to find the index
    for ($i = 0; $i < $n - 1; $i++)
    {
        $curr_diff = abs(($prod[$n - 1] /
                    $prod[$i]) - $prod[$i]);

        if ($curr_diff < $min_diff)
        {
            $min_diff = $curr_diff;
            $res = $i;
        }
    }

    return $res;
}

    // Driver code
    $arr = array( 3, 2, 5, 7, 2, 9 );
    $N = count($arr);

    echo findIndex($arr, $N);

    // This code is contributed by AnkitRai01
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the index i such that
    // the absolute difference between product
    // of elements up to that index and the
    // product of rest of the elements
    // of the array is minimum
    function findIndex(a, n)
    {
        // To store the required index
        let res = 0;

        let min_diff = Number.MAX_VALUE;

        // Prefix product array
        let prod = new Array(n);
        prod[0] = a[0];

        // Compute the product array
        for (let i = 1; i < n; i++)
            prod[i] = prod[i - 1] * a[i];

        // Iterate the product array to find the index
        for (let i = 0; i < n - 1; i++)
        {
            let curr_diff = Math.abs(parseInt(prod[n - 1] / prod[i], 10) - prod[i]);

            if (curr_diff < min_diff)
            {
                min_diff = curr_diff;
                res = i;
            }
        }

        return res;
    }

    let arr = [ 3, 2, 5, 7, 2, 9 ];
    let N = arr.length;

    document.write(findIndex(arr, N));

        // This code is contributed by suresh07.
</script>
```

**Output:** 

```
2
```

**无溢流进场**
以上解决方案可能会造成溢流。为了防止溢出问题，记录数组的所有值。现在，问题归结为用和的绝对差将数组分成两半是最小可能的。现在，数组包含每个索引处元素的日志值。维护一个前缀和数组 B，它保存所有值的和，直到索引 I。检查所有索引，ABS(B[n-1]–2 * B[I])并找到具有最小可能绝对值的索引。

## C++

```
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Function to find index
void solve(int Array[], int N)
{
    // Array to store log values of elements
    double Arraynew[N];
    for (int i = 0; i < N; i++) {
        Arraynew[i] = log(Array[i]);
    }

    // Prefix Array to Maintain Sum of log values till index i
    double prefixsum[N];
    prefixsum[0] = Arraynew[0];

    for (int i = 1; i < N; i++) {
        prefixsum[i] = prefixsum[i - 1] + Arraynew[i];
    }

    // Answer Index
    int answer = 0;
    double minabs = abs(prefixsum[N - 1] - 2 * prefixsum[0]);

    for (int i = 1; i < N - 1; i++) {
        double ans1 = abs(prefixsum[N - 1] - 2 * prefixsum[i]);

        // Find minimum absolute value
        if (ans1 < minabs) {
            minabs = ans1;
            answer = i;
        }
    }

    cout << "Index is: " << answer << endl;
}

// Driver Code
int main()
{
    int Array[5] = { 1, 4, 12, 2, 6 };
    int N = 5;
    solve(Array, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
public class Main
{
    // Function to find index
    public static void solve(int Array[], int N)
    {
        // Array to store log values of elements
        double Arraynew[] = new double[N];
        for (int i = 0; i < N; i++) {
            Arraynew[i] = Math.log(Array[i]);
        }

        // Prefix Array to Maintain Sum of log values till index i
        double prefixsum[] = new double[N];
        prefixsum[0] = Arraynew[0];

        for (int i = 1; i < N; i++)
        {
            prefixsum[i] = prefixsum[i - 1] + Arraynew[i];
        }

        // Answer Index
        int answer = 0;
        double minabs = Math.abs(prefixsum[N - 1] - 2 *
                                 prefixsum[0]);

        for (int i = 1; i < N - 1; i++)
        {
            double ans1 = Math.abs(prefixsum[N - 1] - 2 *
                                   prefixsum[i]);

            // Find minimum absolute value
            if (ans1 < minabs)
            {
                minabs = ans1;
                answer = i;
            }
        }

        System.out.println("Index is: " + answer);
    }

 // Driver code
    public static void main(String[] args)
    {
        int Array[] = { 1, 4, 12, 2, 6 };
        int N = 5;
        solve(Array, N);
    }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
import math

# Function to find index
def solve( Array,  N):

    # Array to store log values of elements
    Arraynew = [0]*N
    for i in range( N ) :
        Arraynew[i] = math.log(Array[i])

    # Prefix Array to Maintain Sum of log values till index i
    prefixsum = [0]*N
    prefixsum[0] = Arraynew[0]

    for i in range( 1,  N) :
        prefixsum[i] = prefixsum[i - 1] + Arraynew[i]

    # Answer Index
    answer = 0
    minabs = abs(prefixsum[N - 1] - 2 * prefixsum[0])

    for i in range(1, N - 1):
        ans1 = abs(prefixsum[N - 1] - 2 * prefixsum[i])

        # Find minimum absolute value
        if (ans1 < minabs):
            minabs = ans1
            answer = i

    print("Index is: " ,answer)

# Driver Code
if __name__ == "__main__":
    Array = [ 1, 4, 12, 2, 6 ]
    N = 5
    solve(Array, N)

# This code is contributed by chitranayal
```

## C#

```
using System;
using System.Collections;

class GFG{

// Function to find index
public static void solve(int []Array, int N)
{

    // Array to store log values of elements
    double []Arraynew = new double[N];
    for(int i = 0; i < N; i++)
    {
        Arraynew[i] = Math.Log(Array[i]);
    }

    // Prefix Array to Maintain Sum of
    // log values till index i
    double []prefixsum = new double[N];
    prefixsum[0] = Arraynew[0];

    for(int i = 1; i < N; i++)
    {
        prefixsum[i] = prefixsum[i - 1] +
                        Arraynew[i];
    }

    // Answer Index
    int answer = 0;
    double minabs = Math.Abs(prefixsum[N - 1] - 2 *
                             prefixsum[0]);

    for(int i = 1; i < N - 1; i++)
    {
        double ans1 = Math.Abs(prefixsum[N - 1] - 2 *
                               prefixsum[i]);

        // Find minimum absolute value
        if (ans1 < minabs)
        {
            minabs = ans1;
            answer = i;
        }
    }

    Console.WriteLine("Index is: " + answer);
}

// Driver code
public static void Main(string []args)
{
    int []Array = { 1, 4, 12, 2, 6 };
    int N = 5;

    solve(Array, N);
}
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>

    // Function to find index
    function solve(array, N)
    {

        // Array to store log values of elements
        let Arraynew = new Array(N);
        for(let i = 0; i < N; i++)
        {
            Arraynew[i] = Math.log(array[i]);
        }

        // Prefix Array to Maintain Sum of
        // log values till index i
        let prefixsum = new Array(N);
        prefixsum[0] = Arraynew[0];

        for(let i = 1; i < N; i++)
        {
            prefixsum[i] = prefixsum[i - 1] +
                            Arraynew[i];
        }

        // Answer Index
        let answer = 0;
        let minabs = Math.abs(prefixsum[N - 1] - 2 *
                                 prefixsum[0]);

        for(let i = 1; i < N - 1; i++)
        {
            let ans1 = Math.abs(prefixsum[N - 1] - 2 *
                                   prefixsum[i]);

            // Find minimum absolute value
            if (ans1 < minabs)
            {
                minabs = ans1;
                answer = i;
            }
        }

        document.write("Index is: " + answer + "</br>");
    }

    let array = [ 1, 4, 12, 2, 6 ];
    let N = 5;

    solve(array, N);

</script>
```

**Output:** 

```
Index is: 2
```