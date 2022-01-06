# 求积和最大等于 N 的 N 的四个因子

> 原文:[https://www . geeksforgeeks . org/find-四因子 n 与最大积和等于 n/](https://www.geeksforgeeks.org/find-four-factors-of-n-with-maximum-product-and-sum-equal-to-n/)

给定一个整数![N](img/19e409e13c1238e1f3ff3dbd06cdd45e.png "Rendered by QuickLaTeX.com")。任务是找到 N 的所有因子打印 N 的四个因子的乘积，这样:

*   四个因素之和等于 n。
*   四个因素的乘积最大。

如果找不到 4 个这样的因素，则打印**“不可能”**。

**注:**四个因素都可以相等，使产品最大化。

**示例**:

```
Input : 24
Output : Product -> 1296
All factors are -> 1 2 3 4 6 8 12 24 
Choose the factor 6 four times,
Therefore, 6+6+6+6 = 24 and product is maximum.

Input : 100
Output : Product -> 390625
All the factors are -> 1 2 4 5 10 10 20 25 50 100 
Choose the factor 25 four times.
```

在第二个例子中，当四个因子等于 25 时，乘积最大。四个因素之和等于‘N’。虽然我们可以选择四次相同的因子来最大化产品。

下面是解决这个问题的分步算法:

1.  首先通过从 1 遍历到“N”的平方根来找到数字“N”的因子，并检查“I”和“n/i”是否除以 N，并将它们存储在向量中。
2.  对向量排序并打印每个元素。
3.  用三个循环找出三个数字，用第四个数字最大化产品。
4.  用上一个产品替换下一个最大产品。
5.  当你找到四个因素时，打印产品。

下面是上述方法的实现:

## C++

```
// C++ program to find four factors of N
// with maximum product and sum equal to N
#include <bits/stdc++.h>

using namespace std;

// Function to find factors
// and to print those four factors
void findfactors(int n)
{
    vector<int> vec;

    // inserting all the factors in a vector s
    for (int i = 1; i * i <= n; i++) {
        if (n % i == 0) {
            vec.push_back(i);
            vec.push_back(n / i);
        }
    }

    // sort the vector
    sort(vec.begin(), vec.end());

    // print all the factors
    cout << "All the factors are -> ";
    for (int i = 0; i < vec.size(); i++)
        cout << vec[i] << " ";
    cout << endl;

    // Any elements is divisible by 1
    int maxProduct = 1;
    bool flag = 1;

    // using three loop we'll find
    // the three maximum factors
    for (int i = 0; i < vec.size(); i++) {
        for (int j = i; j < vec.size(); j++) {
            for (int k = j; k < vec.size(); k++) {
                // storing the fourth factor in y
                int y = n - vec[i] - vec[j] - vec[k];

                // if the fourth factor become negative
                // then break
                if (y <= 0)
                    break;

                // we will replace more optimum number
                // than the previous one
                if (n % y == 0) {
                    flag = 0;
                    maxProduct = max(vec[i] * vec[j] * vec[k] * y,
                                                    maxProduct);
                }
            }
        }
    }

    // print the product if the numbers exist
    if (flag == 0)
        cout << "Product is -> " << maxProduct << endl;

    else
        cout << "Not possible" << endl;
}

// Driver code
int main()
{
    int n;
    n = 50;

    findfactors(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Collections;
import java.util.Vector;

// Java program to find four factors of N
// with maximum product and sum equal to N
class GFG
{

    // Function to find factors
    // and to print those four factors
    static void findfactors(int n)
    {
        Vector<Integer> vec = new Vector<Integer>();

        // inserting all the factors in a vector s
        for (int i = 1; i * i <= n; i++)
        {
            if (n % i == 0)
            {
                vec.add(i);
                vec.add(n / i);
            }
        }

        // sort the vector
        Collections.sort(vec);

        // print all the factors
        System.out.println("All the factors are -> ");
        for (int i = 0; i < vec.size(); i++)
        {
            System.out.print(vec.get(i) + " ");
        }
        System.out.println();

        // Any elements is divisible by 1
        int maxProduct = 1;
        boolean flag = true;

        // using three loop we'll find
        // the three maximum factors
        for (int i = 0; i < vec.size(); i++)
        {
            for (int j = i; j < vec.size(); j++)
            {
                for (int k = j; k < vec.size(); k++)
                {
                    // storing the fourth factor in y
                    int y = n - vec.get(i) - vec.get(j) -
                                    vec.get(k);

                    // if the fourth factor become negative
                    // then break
                    if (y <= 0)
                    {
                        break;
                    }

                    // we will replace more optimum number
                    // than the previous one
                    if (n % y == 0)
                    {
                        flag = false;
                        maxProduct = Math.max(vec.get(i) * vec.get(j) *
                                            vec.get(k) * y, maxProduct);
                    }
                }
            }
        }

        // print the product if the numbers exist
        if (flag == false)
        {
            System.out.println("Product is -> " + maxProduct);
        }
        else
        {
            System.out.println("Not possible");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int n;
        n = 50;
        findfactors(n);
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python 3 to find four factors
# of N with maximum product and
# sum equal to N

# import every thing from
# math library
from math import *

# Function to find factors
# and to print those four factors
def findfactors(n) :
    vec = []

    # inserting all the factors
    # in a list vec
    for i in range(1, int(sqrt(n)) + 1) :
        if n % i == 0 :
            vec.append(i)
            vec.append(n // i)

    # sort the list
    vec.sort()

    print("All the factors are -> ",
                           end = "")

    # print all the factors
    for i in range(len(vec)) :
        print(vec[i], end = " ")
    print()

    # Any elements is divisible by 1
    maxProduct = 1
    flag = 1

    # using three loop we'll find
    # the three maximum factors
    for i in range(0, len(vec)) :
        for j in range(i, len(vec)) :
            for k in range(j, len(vec)) :

                # storing the fourth factor in y
                y = n - vec[i] - vec[j] - vec[k]

                # if the fourth factor become
                # negative then break
                if y <= 0 :
                    break

                # we will replace more optimum
                # number than the previous one
                if n % y == 0 :
                    flag = 0
                    maxProduct = max(vec[i] * vec[j] *
                                     vec[k] * y , maxProduct)

    # print the product if the numbers exist
    if flag == 0 :
        print("Product is - >", maxProduct)
    else :
        print("Not possible")

# Driver Code
if __name__ == "__main__" :
    n = 50

    # function calling
    findfactors(n)

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find four factors of N
// with maximum product and sum equal to N
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find factors
    // and to print those four factors
    static void findfactors(int n)
    {
        List<int> vec = new List<int>();

        // inserting all the factors in a vector s
        for (int i = 1; i * i <= n; i++)
        {
            if (n % i == 0)
            {
                vec.Add(i);
                vec.Add(n / i);
            }
        }

        // sort the vector
        vec.Sort();

        // print all the factors
        Console.WriteLine("All the factors are -> ");
        for (int i = 0; i < vec.Count; i++)
        {
            Console.Write(vec[i] + " ");
        }
        Console.WriteLine();

        // Any elements is divisible by 1
        int maxProduct = 1;
        Boolean flag = true;

        // using three loop we'll find
        // the three maximum factors
        for (int i = 0; i < vec.Count; i++)
        {
            for (int j = i; j < vec.Count; j++)
            {
                for (int k = j; k < vec.Count; k++)
                {
                    // storing the fourth factor in y
                    int y = n - vec[i] - vec[j] -
                                         vec[k];

                    // if the fourth factor become negative
                    // then break
                    if (y <= 0)
                    {
                        break;
                    }

                    // we will replace more optimum number
                    // than the previous one
                    if (n % y == 0)
                    {
                        flag = false;
                        maxProduct = Math.Max(vec[i] * vec[j] *
                                              vec[k] * y, maxProduct);
                    }
                }
            }
        }

        // print the product if the numbers exist
        if (flag == false)
        {
            Console.WriteLine("Product is -> " +
                                    maxProduct);
        }
        else
        {
            Console.WriteLine("Not possible");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n;
        n = 50;
        findfactors(n);
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find four factors
// of N with maximum product and
// sum equal to N

// Function to find factors
// and to print those four factors
function findfactors($n)
{
    $vec = array();

    // inserting all the
    // factors in a vector s
    for ($i = 1; $i * $i <= $n; $i++)
    {
        if ($n % $i == 0)
        {
            array_push($vec, $i);
            array_push($vec, ($n / $i));
        }
    }

    // sort the vector
    sort($vec);

    // print all the factors
    echo "All the factors are -> ";
    for ($i = 0; $i < sizeof($vec); $i++)
        echo $vec[$i] . " ";
    echo "\n";

    // Any elements is divisible by 1
    $maxProduct = 1;
    $flag = 1;

    // using three loop we'll find
    // the three maximum factors
    for ($i = 0; $i < sizeof($vec); $i++)
    {
        for ($j = $i;
             $j < sizeof($vec); $j++)
        {
            for ($k = $j;
                 $k < sizeof($vec); $k++)
            {
                // storing the fourth factor in y
                $y = $n - $vec[$i] -
                          $vec[$j] - $vec[$k];

                // if the fourth factor become
                // negative then break
                if ($y <= 0)
                    break;

                // we will replace more optimum
                // number than the previous one
                if ($n % $y == 0)
                {
                    $flag = 0;
                    $maxProduct = max($vec[$i] * $vec[$j] *
                                      $vec[$k] * $y, $maxProduct);
                }
            }
        }
    }

    // print the product if
    // the numbers exist
    if ($flag == 0)
        echo "Product is -> " .
             $maxProduct ."\n";

    else
        echo "Not possible" ."\n";
}

// Driver code
$n = 50;
findfactors($n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to find four factors of N
// with maximum product and sum equal to N

    // Function to find factors
    // and to print those four factors
    function findfactors(n)
    {
        let vec = [];
        // inserting all the factors in a vector s
        for (let i = 1; i * i <= n; i++)
        {
            if (n % i == 0)
            {
                vec.push(i);
                vec.push(Math.floor(n / i));
            }
        }

        // sort the vector
        vec.sort(function(a,b){return a-b;});

        // print all the factors
        document.write("All the factors are -> ");
        for (let i = 0; i < vec.length; i++)
        {
            document.write(vec[i] + " ");
        }
        document.write("<br>");

        // Any elements is divisible by 1
        let maxProduct = 1;
        let flag = true;

        // using three loop we'll find
        // the three maximum factors
        for (let i = 0; i < vec.length; i++)
        {
            for (let j = i; j < vec.length; j++)
            {
                for (let k = j; k < vec.length; k++)
                {
                    // storing the fourth factor in y
                    let y = n - vec[i] - vec[j] -
                                    vec[k];

                    // if the fourth factor
                    // become negative
                    // then break
                    if (y <= 0)
                    {
                        break;
                    }

                    // we will replace more
                    // optimum number
                    // than the previous one
                    if (n % y == 0)
                    {
                        flag = false;
                        maxProduct = Math.max(vec[i] *
                        vec[j] * vec[k] * y, maxProduct);
                    }
                }
            }
        }

        // print the product if the numbers exist
        if (flag == false)
        {
            document.write("Product is -> " + maxProduct);
        }
        else
        {
            document.write("Not possible");
        }
    }

    // Driver code
    let n = 50;
    findfactors(n);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
All the factors are -> 1 2 5 10 25 50 
Product is -> 12500
```