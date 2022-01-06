# 原始索引处无数字的字典最小排列

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最小原始索引无数字排列/](https://www.geeksforgeeks.org/lexicographically-smallest-permutation-with-no-digits-at-original-index/)

给定一个整数 N，任务是找到形式为: **12345…N** 的整数的字典最小排列，这样索引处就不会出现与原数字相同的数字，即如果**P<sup>1</sup>P<sup>2</sup>P<sup>3</sup>…P<sup>N</sup>T11】是我们的排列，那么 P <sup>i</sup> 一定不等于 i.
**注
**例**:****

```
Input : N = 5
Output : 21435

Input : N = 2
Output : 21
```

对于最小的排列，较小的数字应该放在起始位置。所以，有两种情况来处理这个问题。

1.  **N 为偶数**，即位数为偶数。在这种情况下，如果所有奇数被放置到下一个偶数索引，所有偶数被放置到它们前面的索引，我们将有满足上述条件的最小排列。
2.  **N 为奇数**，即位数为奇数。在这种情况下，所有都类似于上述情况，唯一的变化是最后三个数字以这样一种方式混洗，使得它们的排列最小。例如，如果我们有 123 作为最后三个数字，那么 231 是最小可能的排列。

**算法**:

```
If N is even:place all even digits (upto N) in increasing order at odd index.place all odd digits in increasing order at even index.elseplace all even digits (upto N-3) in increasing order at odd index.place all odd digits (upto N-4) in increasing order at even index.Place N at (N-1)th place, N-1 at (N-2)th and N-2 at Nth place.
```

下面是上述方法的实现:

## C++

```
// C++ program to find the smallest permutation

#include <bits/stdc++.h>
using namespace std;

// Function to print the smallest permutation
string smallestPermute(int n)
{
    char res[n + 1];

    // when n is even
    if (n % 2 == 0) {
        for (int i = 0; i < n; i++) {
            if (i % 2 == 0)
                res[i] = 48 + i + 2;
            else
                res[i] = 48 + i;
        }
    }

    // when n is odd
    else {
        for (int i = 0; i < n - 2; i++) {
            if (i % 2 == 0)
                res[i] = 48 + i + 2;
            else
                res[i] = 48 + i;
        }
        // handling last 3 digit
        res[n - 1] = 48 + n - 2;
        res[n - 2] = 48 + n;
        res[n - 3] = 48 + n - 1;
    }

    // add EOL and print result
    res[n] = '\0';

    return res;
}

// Driver Code
int main()
{
    int n = 7;

    cout << smallestPermute(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest permutation
class GFG
{

// Function to print the smallest permutation
static void smallestPermute(int n)
{
    char res[] = new char[n + 1];

    // when n is even
    if (n % 2 == 0) {
        for (int i = 0; i < n; i++)
        {
            if (i % 2 == 0)
                res[i] = (char)(48 + i + 2);
            else
                res[i] = (char)(48 + i);
        }
    }

    // when n is odd
    else
    {
        for (int i = 0; i < n - 2; i++)
        {
            if (i % 2 == 0)
                res[i] = (char)(48 + i + 2);
            else
                res[i] = (char)(48 + i);
        }
        // handling last 3 digit
        res[n - 1] = (char)(48 + n - 2);
        res[n - 2] = (char)(48 + n);
        res[n - 3] = (char)(48 + n - 1);
    }

    // add EOL and print result
    res[n] = '\0';

    for (int i = 0; i < n ; i++)
    {
        System.out.print(res[i]);
    }
}

// Driver Code
public static void main(String []args)
{
    int n = 7;

    smallestPermute(n);
}
}

// This code is contributed by ANKITRAI1
```

## 蟒蛇 3

```
# Python 3 program to find the
# smallest permutation

# Function to print the smallest
# permutation
def smallestPermute( n):

    res = [""] * (n + 1)

    # when n is even
    if (n % 2 == 0) :
        for i in range(n):
            if (i % 2 == 0):
                res[i] = chr(48 + i + 2)
            else:
                res[i] = chr(48 + i)

    # when n is odd
    else :
        for i in range(n - 2 ):
            if (i % 2 == 0):
                res[i] = chr(48 + i + 2)
            else:
                res[i] = chr(48 + i)

        # handling last 3 digit
        res[n - 1] = chr(48 + n - 2)
        res[n - 2] = chr(48 + n)
        res[n - 3] = chr(48 + n - 1)

    # add EOL and print result
    res = ''.join(res)
    return res

# Driver Code
if __name__ == "__main__":

    n = 7
    print(smallestPermute(n))

# This code is contributed by ita_c
```

## C#

```
// C# program to find the smallest
// permutation
using System;
class GFG
{

// Function to print the smallest
// permutation
static void smallestPermute(int n)
{
    char[] res = new char[n + 1];

    // when n is even
    if (n % 2 == 0)
    {
        for (int i = 0; i < n; i++)
        {
            if (i % 2 == 0)
                res[i] = (char)(48 + i + 2);
            else
                res[i] = (char)(48 + i);
        }
    }

    // when n is odd
    else
    {
        for (int i = 0; i < n - 2; i++)
        {
            if (i % 2 == 0)
                res[i] = (char)(48 + i + 2);
            else
                res[i] = (char)(48 + i);
        }
        // handling last 3 digit
        res[n - 1] = (char)(48 + n - 2);
        res[n - 2] = (char)(48 + n);
        res[n - 3] = (char)(48 + n - 1);
    }

    // add EOL and print result
    res[n] = '\0';

    for (int i = 0; i < n ; i++)
    {
        Console.Write(res[i]);
    }
}

// Driver Code
public static void Main()
{
    int n = 7;

    smallestPermute(n);
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the smallest permutation

// Function to print the smallest permutation
function smallestPermute($n)
{
    $res = array_fill(0, $n + 1, "");

    // when n is even
    if ($n % 2 == 0)
    {
        for ($i = 0; $i < $n; $i++)
        {
            if ($i % 2 == 0)
                $res[$i] = chr(48 + $i + 2);
            else
                $res[$i] = chr(48 + $i);
        }
    }

    // when n is odd
    else
    {
        for ($i = 0; $i < $n - 2; $i++)
        {
            if ($i % 2 == 0)
                $res[$i] = chr(48 + $i + 2);
            else
                $res[$i] = chr(48 + $i);
        }

        // handling last 3 digit
        $res[$n - 1] = chr(48 + $n - 2);
        $res[$n - 2] = chr(48 + $n);
        $res[$n - 3] = chr(48 + $n - 1);
    }

    // add EOL and print result
    $res[$n] = '\0';

    for ($i = 0; $i < $n ; $i++)
    {
        echo $res[$i];
    }
}

// Driver Code
$n = 7;

smallestPermute($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find the smallest permutation

// Function to print the smallest permutation
function smallestPermute(n)
{
    var res = Array(n+1).fill(0);

    // when n is even
    if (n % 2 == 0) {
        for (var i = 0; i < n; i++) {
            if (i % 2 == 0)
                res[i] = 48 + i + 2;
            else
                res[i] = 48 + i;
        }
    }

    // when n is odd
    else {
        for (var i = 0; i < n - 2; i++) {
            if (i % 2 == 0)
                res[i] = 48 + i + 2;
            else
                res[i] = 48 + i;
        }
        // handling last 3 digit
        res[n - 1] = 48 + n - 2;
        res[n - 2] = 48 + n;
        res[n - 3] = 48 + n - 1;
    }

    for(var i =0; i<res.length; i++)
    {
      res[i] = String.fromCharCode(res[i]);
    }

    return res.join("");
}

// Driver Code
var n = 7;
document.write( smallestPermute(n));

</script>
```

**Output:** 

```
2143675
```