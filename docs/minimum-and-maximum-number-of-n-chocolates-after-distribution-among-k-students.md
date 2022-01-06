# 在 K 个学生中分发后 N 块巧克力的最小和最大数量

> 原文:[https://www . geeksforgeeks . org/k-学生分发 n-巧克力后的最小和最大数量/](https://www.geeksforgeeks.org/minimum-and-maximum-number-of-n-chocolates-after-distribution-among-k-students/)

给定 N 个巧克力和 K 个学生，任务是找到如何分割巧克力，使所有学生收到的最小和最大巧克力之间的差异最小化。打印最小和最大巧克力分配值。
**例** :

```
Input: N = 7, K = 3
Output: Min = 2, Max = 3
Distribution is 2 2 3

Input: N = 100, K = 10
Output: 10 10
Distribution is 10 10 10 10 10 10 10 10 10 10 
```

**方法:**只有当每个学生获得相同数量的糖果时，差异才会最小化，即 **N % k = 0** 但是如果 **N % K！= 0** 然后每个学生将首先获得 **(N-N%k)/k** 数量的糖果，然后剩余的 **N%k** 数量的糖果可以通过给他们每人 1 颗糖果的方式分配给 **N%K** 学生。这样就比**多一颗糖(N-N%k)/k，如果 N%k！= 0** 带学生。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Driver code
int main(){

    int n = 7, k = 3;

    if(n % k == 0)
        cout<<n/k<<" "<<n/k;
    else
        cout<<((n-(n % k))/k)<<" "
            <<(((n-(n % k))/k) + 1);

    return 0;
}

// This code is contributed by Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

public class Improve {

    // Driver code
    public static void main(String args[])
    {
            int n = 7 ;
            int k = 3 ;

            if (n % k == 0)
                System.out.println(n / k +" " + n / k);

            else
                System.out.println((n-(n % k)) / k + " "
                        + (((n-(n % k))/ k) + 1) ) ;

    }
    // This Code is contributed by ANKITRAI1
}
```

## 计算机编程语言

```
# Python implementation of the above approach

n, k = 7, 3
if(n % k == 0):
    print(n//k, n//k)

else:
    print((n-n % k)//k, (n-n % k)//k + 1)
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG
{

// Driver code
public static void Main()
{
    int n = 7 ;
    int k = 3 ;

    if (n % k == 0)
        Console.WriteLine(n / k +
                    " " + n / k);

    else
        Console.WriteLine((n - (n % k)) / k +
                  " " + (((n - (n % k)) / k) + 1));
}
}

// This code is contributed
// by inder_verama
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Driver code
$n = 7; $k = 3;

if($n % $k == 0)
    echo $n/$k . " " . $n/$k;
else
    echo (($n - ($n % $k)) / $k) . " " .
        ((($n - ($n % $k)) / $k) + 1);

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Driver code
var n = 7 ;
var k = 3 ;

if (n % k == 0)
    document.write(n / k +" " + n / k);

else
    document.write((n-(n % k)) / k + " "
            + (((n-(n % k))/ k) + 1) ) ;

// This code is contributed by 29AjayKumar

</script>
```

**Output:** 

```
2 3
```