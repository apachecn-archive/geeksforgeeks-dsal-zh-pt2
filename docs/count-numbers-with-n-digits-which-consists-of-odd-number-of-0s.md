# 计数由奇数个 0 组成的 N 位数字

> 原文:[https://www . geesforgeks . org/count-numbers-with-n-digits-其中-由-奇数-0 组成/](https://www.geeksforgeeks.org/count-numbers-with-n-digits-which-consists-of-odd-number-of-0s/)

给我们一个数字 N，任务是找出有 N 个数字和奇数个零的数字的个数。
**注**:数字前面可以有 0

**示例**:

```
Input : N = 2
Output : Count = 18

Input : N = 3
Output : Count = 244
```

假设一个数字有 N 个数字，其中只包含一个零。所以数字 0 中的数字只能用 1 种方式填充，其余的位置可以用 9 种不同的方式用 1 到 9 的数字填充。所以用 N 个数字计算所有这些数字，只有 1 个零=**<sup>N</sup>C<sub>1</sub>*(9<sup>N-1</sup>)**。

同样，用 N 位数字和 3 个零计算所有这些数字=**<sup>N</sup>C<sub>3</sub>*(9<sup>N-3</sup>)**。
以此类推。

所以，所有这些数字的计数，如果有 N 个数字和奇数个零，

> **<sup>N</sup>C<sub>1</sub>*(9<sup>N-1</sup>)**+**T9】NC<sub>3</sub>*(9<sup>N-3</sup>)**+**T17】NC<sub>5</sub>*(9<sup>N-5</sup>)**+……。+**<sup>N</sup>C<sub>K</sub>*(9<sup>N-K</sup>)**
> 其中，K 为小于 N 的奇数

上面的等式可以写成，

> **(9<sup>n</sup>)(<sup>n</sup>c<sub>1</sub>*(1/9))+(<sup>n</sup>c<sub>3</sub>*(1/9^3))+(<sup>n</sup>c<sub>5</sub>*(1/9^5))+…**

上式可以表示为两个级数的减法，(9<sup>N</sup>)* {(1+x)<sup>N</sup>-(1-x)<sup>N</sup>}/2，其中 **x = 1/9**
等于，

```
(10<sup>N - 8N)/2</sup>
```

下面是上述方法的实现:

## C++

```
// C++ program to count numbers with N digits
// which consists of odd number of 0's
#include <bits/stdc++.h>
using namespace std;

// Function to count Numbers with N digits
// which consists of odd number of 0's
int countNumbers(int N)
{
    return (pow(10, N) - pow(8, N)) / 2;
}

// Driver code
int main()
{
    int n = 5;

    cout << countNumbers(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count numbers
// with N digits which consists
// of odd number of 0's
import java.io.*;

class GFG {

    // Function to count Numbers
    // with N digits which consists
    // of odd number of 0's
    static int countNumbers(int N)
    {
        return (int)(Math.pow(10, N)
                     - Math.pow(8, N)) / 2;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 5;
        System.out.println(countNumbers(n));
    }
}

// This code is contributed by Shashank
```

## 蟒蛇 3

```
# Python 3 program to count numbers
# with N digits which consists of
# odd number of 0's

# Function to count Numbers with
# N digits which consists of odd
# number of 0's

def countNumbers(N):

    return (pow(10, N) - pow(8, N)) // 2

# Driver code
if __name__ == "__main__":

    n = 5

    print(countNumbers(n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to count numbers
// with N digits which consists
// of odd number of 0's
using System;

class GFG {

    // Function to count Numbers
    // with N digits which consists
    // of odd number of 0's
    static int countNumbers(int N)
    {
        return (int)(Math.Pow(10, N)
                     - Math.Pow(8, N)) / 2;
    }

    // Driver code
    public static void Main()
    {
        int n = 5;
        Console.WriteLine(countNumbers(n));
    }
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count numbers
// with N digits which consists
// of odd number of 0's

// Function to count Numbers
// with N digits which consists
// of odd number of 0's
function countNumbers($N)
{
    return (pow(10, $N) -
            pow(8, $N)) / 2;
}

// Driver code
$n = 5;

echo countNumbers($n) ;

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
    // Javascript program to count numbers with N digits
    // which consists of odd number of 0's

    // Function to count Numbers with N digits
    // which consists of odd number of 0's
    function countNumbers(N)
    {
        return parseInt((Math.pow(10, N) - Math.pow(8, N)) / 2, 10);
    }

    let n = 5;
    document.write(countNumbers(n));

    // This code is contributed by divyeshrabadiya07.

</script>
```

**Output**

```
33616
```

**注**:答案可以很大，所以对于大于 9 的 N，使用[模幂](https://www.geeksforgeeks.org/modular-exponentiation-power-in-modular-arithmetic/)。

**时间复杂度:**O(log n)
T3】辅助空间: O(1)