# 对(I，j)进行计数，使得((n % i) % j) % n 最大化

> 原文:[https://www . geesforgeks . org/I-j-so-n-I-j-n-is-maximized/](https://www.geeksforgeeks.org/count-of-pairs-of-i-j-such-that-n-i-j-n-is-maximized/)

给定一个整数 **n** ，任务是计算对的数量 **(i，j)** ，使得 **((n % i) % j) % n** 最大化，其中 **1 ≤ i，j ≤ n**
**示例:**

> **输入:** n = 5
> **输出:** 3
> (3，3)、(3，4)和(3，5)是唯一有效的对。
> **输入:** n = 55
> **输出:** 28

**天真法:**要获得最大余数值， **n** 必须除以 **(n / 2) + 1** 。存储**最大值= n % ((n / 2) + 1)** ，现在检查 **i** 和 **j** 的所有可能值。如果 **((n % i) % j) % n =最大值**，则更新**计数=计数+ 1** 。最后打印**计数**。

## C++

```
// CPP implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the count of required pairs
int countPairs(int n)
{
    // Number which will give the max value
    // for ((n % i) % j) % n
    int num = ((n / 2) + 1);

    // To store the maximum possible value of
    // ((n % i) % j) % n
    int max = n % num;

    // To store the count of possible pairs
    int count = 0;

    // Check all possible pairs
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= n; j++)
        {

            // Calculating the value of ((n % i) % j) % n
            int val = ((n % i) % j) % n;

            // If value is equal to maximum
            if (val == max)
                count++;
        }
    }

    // Return the number of possible pairs
    return count;
}

// Driver code
int main()
{
    int n = 5;
    cout << (countPairs(n));
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the count of required pairs
    public static int countPairs(int n)
    {
        // Number which will give the max value
        // for ((n % i) % j) % n
        int num = ((n / 2) + 1);

        // To store the maximum possible value of
        // ((n % i) % j) % n
        int max = n % num;

        // To store the count of possible pairs
        int count = 0;

        // Check all possible pairs
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= n; j++) {

                // Calculating the value of ((n % i) % j) % n
                int val = ((n % i) % j) % n;

                // If value is equal to maximum
                if (val == max)
                    count++;
            }
        }

        // Return the number of possible pairs
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 5;
        System.out.println(countPairs(n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# required pairs
def countPairs(n):

    # Number which will give the Max
    # value for ((n % i) % j) % n
    num = ((n // 2) + 1)

    # To store the Maximum possible value
    # of ((n % i) % j) % n
    Max = n % num

    # To store the count of possible pairs
    count = 0

    # Check all possible pairs
    for i in range(1, n + 1):

        for j in range(1, n + 1):

            # Calculating the value of
            # ((n % i) % j) % n
            val = ((n % i) % j) % n

            # If value is equal to Maximum
            if (val == Max):
                count += 1

    # Return the number of possible pairs
    return count

# Driver code
n = 5
print(countPairs(n))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to return the count of required pairs
static int countPairs(int n)
{
    // Number which will give the max
    // value for ((n % i) % j) % n
    int num = ((n / 2) + 1) ;

    // To store the maximum possible value
    // of ((n % i) % j) % n
    int max = n % num;

    // To store the count of possible pairs
    int count = 0;

    // Check all possible pairs
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= n; j++)
        {

            // Calculating the value of
            // ((n % i) % j) % n
            int val = ((n % i) % j) % n;

            // If value is equal to maximum
            if (val == max)
                count++;
        }
    }

    // Return the number of possible pairs
    return count;
}

// Driver code
public static void Main()
{
    int n = 5;
    Console.WriteLine(countPairs(n));
}
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the
// approach Function to return
// the count of required pairs

function countPairs($n)
{
    // Number which will give the max
    // value for ((n % i) % j) % n
    $num = (($n / 2) + 1);

    // To store the maximum possible
    // value of ((n % i) % j) % n
    $max = $n % $num;

    // To store the count of possible pairs
    $count = 0;

    // Check all possible pairs
    for ($i = 1; $i <= $n; $i++)
    {
        for ($j = 1; $j <= $n; $j++)
        {

            // Calculating the value
            // of ((n % i) % j) % n
            $val = (($n % $i) % $j) % $n;

            // If value is equal to maximum
            if ($val == $max)
                $count++;
        }
    }

    // Return the number of possible pairs
    return $count;
}

// Driver code
    $n = 5;
    echo (countPairs($n));

// This code is contributed by ajit..
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of the above approach

    // Function to return the count of required pairs
    function countPairs(n)
    {
        // Number which will give the max
        // value for ((n % i) % j) % n
        let num = (parseInt(n / 2, 10) + 1) ;

        // To store the maximum possible value
        // of ((n % i) % j) % n
        let max = n % num;

        // To store the count of possible pairs
        let count = 0;

        // Check all possible pairs
        for (let i = 1; i <= n; i++)
        {
            for (let j = 1; j <= n; j++)
            {

                // Calculating the value of
                // ((n % i) % j) % n
                let val = ((n % i) % j) % n;

                // If value is equal to maximum
                if (val == max)
                    count++;
            }
        }

        // Return the number of possible pairs
        return count;
    }

    let n = 5;
    document.write(countPairs(n));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(n <sup>2</sup> )
**有效途径:**求余数最大值即 **max = n % num** 其中 **num = ((n / 2) + 1)** 。现在 **i** 必须选择为 **num** 才能获得最大值， **j** 可以选择为**【max，n】**范围内的任意值，因为我们不需要减少计算出的最大值，选择 **j > max** 不会影响之前获得的值。因此总对数将为**n–max**。
这种方法对 **n = 2** 无效。这是因为，对于 **n = 2** ，最大余数将为 **0** ，**n–max**将给出 **2** 但我们知道答案是 **4** 。这种情况下所有可能的配对都是 **(1，1)** 、 **(1，2)** 、 **(2，1)** 和 **(2，2)** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the count of
// required pairs
int countPairs(int n)
{

    // Special case
    if (n == 2)
        return 4;

    // Number which will give the max value
    // for ((n % i) % j) % n
    int num = ((n / 2) + 1);

    // To store the maximum possible value
    // of ((n % i) % j) % n
    int max = n % num;

    // Count of possible pairs
    int count = n - max;

    return count;
}

// Driver code
int main()
{
    int n = 5;
    cout << countPairs(n);
}

// This code is contributed by Code_Mech.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the count of required pairs
    public static int countPairs(int n)
    {

        // Special case
        if (n == 2)
            return 4;

        // Number which will give the max value
        // for ((n % i) % j) % n
        int num = ((n / 2) + 1);

        // To store the maximum possible value of
        // ((n % i) % j) % n
        int max = n % num;

        // Count of possible pairs
        int count = n - max;

        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 5;
        System.out.println(countPairs(n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of required pairs
def countPairs(n):

    # Special case
    if (n == 2):
        return 4

    # Number which will give the max value
    # for ((n % i) % j) % n
    num = ((n // 2) + 1);

    # To store the maximum possible value
    # of ((n % i) % j) % n
    max = n % num;

    # Count of possible pairs
    count = n - max;

    return count

# Driver code
if __name__ =="__main__" :

    n = 5;
print(countPairs(n));

# This code is contributed by Code_Mech
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

    // Function to return the count of required pairs
    static int countPairs(int n)
    {

        // Special case
        if (n == 2)
            return 4;

        // Number which will give the max value
        // for ((n % i) % j) % n
        int num = ((n / 2) + 1);

        // To store the maximum possible value of
        // ((n % i) % j) % n
        int max = n % num;

        // Count of possible pairs
        int count = n - max;

        return count;
    }

    // Driver code
    static public void Main ()
    {
            int n = 5;
        Console.WriteLine(countPairs(n));
    }
}

// This code is contributed by Tushil..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count
// of required pairs
function countPairs($n)
{

    // Special case
    if ($n == 2)
        return 4;

    // Number which will give the max
    // value. for ((n % i) % j) % n
    $num = ((int)($n / 2) + 1);

    // To store the maximum possible
    // value of((n % i) % j) % n
    $max = $n % $num;

    // Count of possible pairs
    $count = ($n - $max);

    return $count;
}

// Driver code
$n = 5;
echo (countPairs($n));

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the count of
    // required pairs
    function countPairs(n)
    {

        // Special case
        if (n == 2)
            return 4;

        // Number which will give the max value
        // for ((n % i) % j) % n
        let num = (parseInt(n / 2, 10) + 1);

        // To store the maximum possible value
        // of ((n % i) % j) % n
        let max = n % num;

        // Count of possible pairs
        let count = n - max;

        return count;
    }

    let n = 5;
    document.write(countPairs(n));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(1)