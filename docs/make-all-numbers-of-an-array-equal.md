# 使数组的所有数字相等

> 原文:[https://www . geesforgeks . org/make-all-numbers-of-a-array-equal/](https://www.geeksforgeeks.org/make-all-numbers-of-an-array-equal/)

给定一个数组 **arr[]** ，任务是用给定的运算使所有数组元素相等。在单次操作中，数组的任何元素都可以乘以 **2** 或 **3** 。如果可以用给定的操作使所有的数组元素相等，那么打印**是**否则打印**否**。

**示例:**

> **输入:** arr[] = {50，75，100 }
> T3】输出:是
> {50 * 2 * 3，75 * 2 * 2，100 * 3} = {300，300，300}
> 
> **输入:** arr[] = {10，14 }
> T3】输出:否

**逼近:**任意正整数可因式分解写成 2<sup>a</sup>* 3<sup>b</sup>* 5<sup>c</sup>* 7<sup>d</sup>*…..
我们可以将给定的数字乘以 **2** 和 **3** ，这样我们就可以为它们增加 **a** 和 **b** 。因此，我们可以通过将所有 **a** 和 **b** 增加到相同的大值(例如 100)来使它们相等。但是我们不能改变其他质数的幂，所以它们从一开始就必须相等。我们可以通过尽可能多地将输入的所有数字乘以 2 和乘以 3 来检查它。那么他们都必须是平等的。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if all
// the array elements can be made equal
// with the given operation
bool EqualNumbers(int a[], int n)
{
    for (int i = 0; i < n; i++) {

        // Divide number by 2
        while (a[i] % 2 == 0)
            a[i] /= 2;

        // Divide number by 3
        while (a[i] % 3 == 0)
            a[i] /= 3;

        if (a[i] != a[0]) {
            return false;
        }
    }

    return true;
}

// Driver code
int main()
{
    int a[] = { 50, 75, 150 };

    int n = sizeof(a) / sizeof(a[0]);

    if (EqualNumbers(a, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

    // Function that returns true if all
    // the array elements can be made equal
    // with the given operation
    static boolean EqualNumbers(int a[], int n)
    {
        for (int i = 0; i < n; i++)
        {

            // Divide number by 2
            while (a[i] % 2 == 0)
            {
                a[i] /= 2;
            }

            // Divide number by 3
            while (a[i] % 3 == 0)
            {
                a[i] /= 3;
            }

            if (a[i] != a[0])
            {
                return false;
            }
        }

        return true;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = {50, 75, 150};

        int n = a.length;

        if (EqualNumbers(a, n))
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }
    }
}

// This code is contributed by Rajput-JI
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if all
# the array elements can be made equal
# with the given operation
def EqualNumbers(a, n):

    for i in range(0, n):

        # Divide number by 2
        while a[i] % 2 == 0:
            a[i] //= 2

        # Divide number by 3
        while a[i] % 3 == 0:
            a[i] //= 3

        if a[i] != a[0]:
            return False

    return True

# Driver code
if __name__ == "__main__":

    a = [50, 75, 150]
    n = len(a)

    if EqualNumbers(a, n):
        print("Yes")
    else:
        print("No")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

    // Function that returns true if all
    // the array elements can be made equal
    // with the given operation
    static bool EqualNumbers(int []a, int n)
    {
        for (int i = 0; i < n; i++)
        {

            // Divide number by 2
            while (a[i] % 2 == 0)
            {
                a[i] /= 2;
            }

            // Divide number by 3
            while (a[i] % 3 == 0)
            {
                a[i] /= 3;
            }

            if (a[i] != a[0])
            {
                return false;
            }

        }

        return true;
    }

    // Driver code
    public static void Main()
    {
        int []a = {50, 75, 150};

        int n = a.Length;

        if (EqualNumbers(a, n))
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
// Function that returns true if all
// the array elements can be made equal
// with the given operation

function EqualNumbers($a, $n)
{
    for ($i = 0; $i < $n; $i++)
    {

        // Divide number by 2
        while ($a[$i] % 2 == 0)
            $a[$i] /= 2;

        // Divide number by 3
        while ($a[$i] % 3 == 0)
            $a[$i] /= 3;

        if ($a[$i] != $a[0])
        {
            return false;
        }
    }

    return true;
}

    // Driver code
    $a = array(50, 75, 150 );
    $n = sizeof($a) / sizeof($a[0]);
    if (EqualNumbers($a, $n))
        echo "Yes";
    else
        echo "No";

#This code is contributed by ajit..
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function that returns true if all
// the array elements can be made equal
// with the given operation
function EqualNumbers(a, n)
{
    for(let i = 0; i < n; i++)
    {

        // Divide number by 2
        while (a[i] % 2 == 0)
        {
            a[i] = parseInt(a[i] / 2, 10);
        }

        // Divide number by 3
        while (a[i] % 3 == 0)
        {
            a[i] = parseInt(a[i] / 3, 10); 
        }

        if (a[i] != a[0])
        {
            return false;
        }
    }
    return true;
}

// Driver code
let a = [ 50, 75, 150 ];
let n = a.length;

if (EqualNumbers(a, n))
{
    document.write("Yes");
}
else
{
    document.write("No");
}

// This code is contributed by divyeshrabadiya07  

</script>
```

**Output:** 

```
Yes
```