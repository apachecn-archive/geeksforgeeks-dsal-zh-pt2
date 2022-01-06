# 计算三元组(a，b，c)，使得 a + b，b + c 和 a + c 都可以被 K 整除

> 原文:[https://www . geesforgeks . org/count-triples-a-B- c-so-ab-BC-and-AC-都可以被 k 整除/](https://www.geeksforgeeks.org/count-triplets-a-b-c-such-that-ab-bc-and-ac-are-all-divisible-by-k/)

给定两个整数‘N’和‘K’，任务是计算不大于‘N’的正整数的三元组(a，b，c)的数量，使得‘a+b’、‘b+ c’和‘c+a’都是‘K’的倍数。请注意,“a”、“b”和“c”在三元组中可以相同，也可以不同。
**例:**

> **输入:** N = 2，K = 2
> **输出:** 1
> 所有可能的三元组为
> (1，1，1)和(2，2，2)
> **输入:** N = 3，K = 2
> **输出:** 9

**方法:**从‘1’到‘N’运行三个嵌套循环，检查 i+j、j+l 和 l+i 是否都可以被‘K’整除。如果条件为真，则增加计数。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include<iostream>
using namespace std;
class gfg
{
    // Function returns the
    // count of the triplets
    public:
    long count_triples(int n, int k);
};

    long gfg :: count_triples(int n, int k)
    {
        int i = 0, j = 0, l = 0;
        int count = 0;

        // iterate for all
        // triples pairs (i, j, l)
        for (i = 1; i <= n; i++)
        {
            for (j = 1; j <= n; j++)
            {
                for (l = 1; l <= n; l++)
                {

                    // if the condition
                    // is satisfied
                    if ((i + j) % k == 0
                        && (i + l) % k == 0
                        && (j + l) % k == 0)
                        count++;
                }
            }
        }
        return count;
    }

    // Driver code
    int main()
    {
        gfg g;
        int n = 3;
        int k = 2;
        long ans = g.count_triples(n, k);
        cout << ans;
    }
//This code is contributed by Soumik
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function returns the
    // count of the triplets
    static long count_triples(int n, int k)
    {
        int i = 0, j = 0, l = 0;
        int count = 0;

        // iterate for all
        // triples pairs (i, j, l)
        for (i = 1; i <= n; i++) {
            for (j = 1; j <= n; j++) {
                for (l = 1; l <= n; l++) {

                    // if the condition
                    // is satisfied
                    if ((i + j) % k == 0
                        && (i + l) % k == 0
                        && (j + l) % k == 0)
                        count++;
                }
            }
        }
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 3;
        int k = 2;
        long ans = count_triples(n, k);
        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach
def count_triples(n, k):

    count, i, j, l = 0, 0, 0, 0

    # Iterate for all triples
    # pairs (i, j, l)
    for i in range(1, n + 1):
        for j in range(1, n + 1):
            for l in range(1, n + 1):

                # If the condition
                # is satisfied
                if ((i + j) % k == 0 and
                    (i + l) % k == 0 and
                    (j + l) % k == 0):
                    count += 1

    return count

# Driver code
if __name__ == "__main__":

    n, k = 3, 2
    ans = count_triples(n, k)
    print(ans)

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of the approach

using System;

class GFG {

    // Function returns the
    // count of the triplets
    static long count_triples(int n, int k)
    {
        int i = 0, j = 0, l = 0;
        int count = 0;

        // iterate for all
        // triples pairs (i, j, l)
        for (i = 1; i <= n; i++) {
            for (j = 1; j <= n; j++) {
                for (l = 1; l <= n; l++) {

                    // if the condition
                    // is satisfied
                    if ((i + j) % k == 0
                        && (i + l) % k == 0
                        && (j + l) % k == 0)
                        count++;
                }
            }
        }
        return count;
    }

    // Driver code
    public static void Main()
    {
        int n = 3;
        int k = 2;
        long ans = count_triples(n, k);
        Console.WriteLine(ans);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP implementation of the approach
// Function returns the
// count of the triplets
function count_triples($n, $k)
    {
         $i = 0; $j = 0; $l = 0;
        $count = 0;

        // iterate for all
        // triples pairs (i, j, l)
        for ($i = 1; $i <= $n; $i++) {
            for ($j = 1; $j <= $n; $j++) {
                for ($l = 1; $l <= $n; $l++) {

                    // if the condition
                    // is satisfied
                    if (($i + $j) % $k == 0
                        && ($i + $l) % $k == 0
                        && ($j + $l) % $k == 0)
                        $count++;
                }
            }
        }
        return $count;
    }

    // Driver code
        $n = 3;
        $k = 2;
        $ans = count_triples($n, $k);
        echo ($ans);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the quadratic
// equation whose roots are a and b
function count_triples(n, k)
{
    var i = 0, j = 0, l = 0;
    var count = 0;

    // iterate for all
    // triples pairs (i, j, l)
    for(i = 1; i <= n; i++)
    {
        for(j = 1; j <= n; j++)
        {
            for(l = 1; l <= n; l++)
            {

                // if the condition
                // is satisfied
                if ((i + j) % k == 0
                    && (i + l) % k == 0
                    && (j + l) % k == 0)
                    count++;
            }
        }
    }
    return count;
}
// Driver Code
var n = 3;
var k = 2;
var ans = count_triples(n, k);

document.write(ans);

// This code is contributed by Khushboogoyal499

</script>
```

**Output:** 

```
9
```