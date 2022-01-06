# 最大上一个和下一个元素乘积

> 原文:[https://www . geesforgeks . org/maximum-previous-and-next-element-product/](https://www.geeksforgeeks.org/maximum-previous-and-next-element-product/)

给定一个整数数组，任务是打印数组中的最大乘积，使得它的前一个和下一个元素乘积最大。
**注:**阵可以按循环顺序考虑。第一个元素的前一个元素将等于最后一个元素，最后一个元素的下一个元素将是第一个元素。
**示例:**

> **输入:** a[ ] = { 5，6，4，3，2}
> **输出:** 20
> 对于 5:上一个元素是 2，下一个元素是 6 所以，积将是 12。
> 对于 6:上一个元素是 5，下一个元素是 4 所以，积将是 20。
> 对于 4:上一个元素是 6，下一个元素是 3 所以，积将是 18。
> 对于 3:上一个元素是 4，下一个元素是 2 所以，乘积将是 8。
> 对于 2:上一个元素是 3，下一个元素是 5 所以，积将是 15。
> 最大可能乘积为 20
> ，数组中最大元素为 6。
> **输入:** a[ ] = {9，2，3，1，5，17}
> **输出:** 45

**进场:**

*   想法是先找到上一个元素和下一个元素。
*   找到两个元素后，取乘积，找到其中最大的乘积。

以下是上述方法的实现:

## C++

```

// C++ program to print maximum product
// such that its previous and next
// element product is maximum.
#include<bits/stdc++.h>
using namespace std;
    // function to return largest element
    // such that its previous and next
    // element product is maximum.
     int maxProduct(int a[], int n)
    {

        int product[n];

        int maxA[n];
        int maxProd = 0;
        int maxArr = 0;
        for (int i = 0; i < n; i++) {

            // product of previous and next
            // element and stored into an
            // array product[i]
            product[i] = a[(i + 1) % n] *
                          a[(i + (n - 1)) % n];

            // find maximum product 
            // in product[i] array
            if (maxProd < product[i]) {
                maxProd = product[i];
            }
        }
        return maxProd;
    }

    // Driver program
   int main()
    {
        int a[] = { 5, 6, 4, 3, 2 };

        int n = sizeof(a)/sizeof(a[0]);

        cout<<(maxProduct(a, n));
    }

// This code contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print maximum product
// such that its previous and next
// element product is maximum.
import java.io.*;

class GFG
{
    // function to return largest element
    // such that its previous and next
    // element product is maximum.
    static int maxProduct(int a[], int n)
    {

        int[] product = new int[n];

        int maxA[] = new int[n];

        int maxProd = 0;
        int maxArr = 0;
        for (int i = 0; i < n; i++)
        {

            // product of previous and next
            // element and stored into an
            // array product[i]
            product[i] = a[(i + 1) % n] *
                        a[(i + (n - 1)) % n];

            // find maximum product
            // in product[i] array
            if (maxProd < product[i])
            {
                maxProd = product[i];
            }
        }
        return maxProd;
    }

    // Driver code
    public static void main(String[] args)

    {
        int[] a = { 5, 6, 4, 3, 2 };

        int n = a.length;

        System.out.println(maxProduct(a, n));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to print maximum product
# such that its previous and next
# element product is maximum.

# function to return largest element
# such that its previous and next
# element product is maximum.
def maxProduct(a, n) :

    product = [0]*n;
    maxA = [0]*n;
    maxProd = 0;
    maxArr = 0;

    for i in range(n) :

        # product of previous and next
        # element and stored into an
        # array product[i]
        product[i] = a[(i + 1) % n] * a[(i + (n - 1)) % n];

        # find maximum product
        # in product[i] array
        if (maxProd < product[i]) :
            maxProd = product[i];

    return maxProd;

# Driver code
if __name__ == "__main__" :

    a = [ 5, 6, 4, 3, 2 ];
    n = len(a);

    print(maxProduct(a, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to print maximum product
// such that its previous and next
// element product is maximum.
using System;

class GFG
{
    // function to return largest element
    // such that its previous and next
    // element product is maximum.
    static int maxProduct(int []a, int n)
    {

        int[] product = new int[n];

        //int []maxA = new int[n];

         int maxProd = 0;
        //int maxArr = 0;
        for (int i = 0; i < n; i++)
        {

            // product of previous and next
            // element and stored into an
            // array product[i]
            product[i] = a[(i + 1) % n] *
                        a[(i + (n - 1)) % n];

            // find maximum product
            // in product[i] array
            if (maxProd < product[i])
            {
                maxProd = product[i];
            }
        }
        return maxProd;
    }

    // Driver code
    public static void Main()

    {
        int[] a = { 5, 6, 4, 3, 2 };

        int n = a.Length;

        Console.WriteLine(maxProduct(a, n));
    }
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
    // Javascript program to print maximum product
    // such that its previous and next
    // element product is maximum.

    // function to return largest element
    // such that its previous and next
    // element product is maximum.
    function maxProduct(a, n)
    {

        let product = new Array(n);

        //int []maxA = new int[n];

        let maxProd = 0;
        //int maxArr = 0;
        for (let i = 0; i < n; i++)
        {

            // product of previous and next
            // element and stored into an
            // array product[i]
            product[i] = a[(i + 1) % n] *
                        a[(i + (n - 1)) % n];

            // find maximum product
            // in product[i] array
            if (maxProd < product[i])
            {
                maxProd = product[i];
            }
        }
        return maxProd;
    }

    let a = [ 5, 6, 4, 3, 2 ];

    let n = a.length;

    document.write(maxProduct(a, n));

</script>
```

**Output:** 

```
20
```

**时间复杂度:** O(N)