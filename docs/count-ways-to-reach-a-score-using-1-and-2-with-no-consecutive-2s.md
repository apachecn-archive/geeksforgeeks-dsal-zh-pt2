# 用 1 和 2 计算得分的方式，不连续 2 秒

> 原文:[https://www . geesforgeks . org/count-way-to-reach-a-score-in-1-2-with-no-continuous-2s/](https://www.geeksforgeeks.org/count-ways-to-reach-a-score-using-1-and-2-with-no-consecutive-2s/)

板球运动员必须得 N 分，条件是他只能得 1 分或 2 分，连续得分不得超过 2 分。找到所有可能的组合。
**例:**

```
Input : N = 4 
Output : 4
1+1+1+1, 1+2+1, 2+1+1, 1+1+2

Input : N = 5
Output : 6
```

来源:[甲骨文校园访谈](https://www.geeksforgeeks.org/oracle-interview-experience-on-campus-2/)

这个问题是[在一个游戏](https://www.geeksforgeeks.org/count-number-ways-reach-given-score-game/)中计算达到给定分数的途径数的一个变种，可以在 O(n)时间和不变的辅助空间中求解。

第一次得分可能是:

a) 1。现在玩家必须得 N-1 分。

b)或 2。因为 2 不能连续跑，下一次跑得分必须是 1。之后，玩家必须得 N-(2+1)分。
下面是上述问题的递归解。

递归关系将是:

计数路(N) =计数路(N-1) +计数路(N-2)

遵循递归解需要指数时间和空间(类似于斐波那契数)。

## C++

```
// A simple recursive implementation for
// counting ways to reach a score using 1 and 2 with
// consecutive 2 allowed
#include <iostream>
using namespace std;

int CountWays(int n)
{
    // base cases
    if (n == 0) {
        return 1;
    }
    if (n == 1) {
        return 1;
    }
    if (n == 2) {
        return 1 + 1;
    }

    // For cases n > 2
    return CountWays(n - 1) + CountWays(n - 3);
}

// Driver code
int main()
{
    int n = 10;
    cout << CountWays(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple recursive implementation for
// counting ways to reach a score using 1 and 2 with
// consecutive 2 allowed

import java.io.*;

class GFG {
    static int CountWays(int n)
    {
        // base cases
        if (n == 0) {
            return 1;
        }
        if (n == 1) {
            return 1;
        }
        if (n == 2) {
            return 1 + 1;
        }

        // For cases n > 2
        return CountWays(n - 1) + CountWays(n - 3);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 5;
        System.out.println(CountWays(n));
    }
}
```

## 蟒蛇 3

```
# A simple recursive implementation for
# counting ways to reach a score using 1 and 2 with
# consecutive 2 allowed

def CountWays(n):

    # base case
    if n == 0:
        return 1
    if n == 1:
        return 1
    if n == 2:
        return 1 + 1

    # For cases n > 2
    return CountWays(n - 1) + CountWays(n - 3)

# Driver code
if __name__ == '__main__':
    n = 5
    print(CountWays(n))
```

## C#

```
// A simple recursive implementation
// for counting ways to reach a score
// using 1 and 2 with consecutive 2 allowed
using System;

class GFG {
    static int CountWays(int n)
    {
        // base cases
        if (n == 0) {
            return 1;
        }
        if (n == 1) {
            return 1;
        }
        if (n == 2) {
            return 1 + 1;
        }

        // For cases n > 2
        return CountWays(n - 1) + CountWays(n - 3);
    }

    // Driver Code
    static public void Main()
    {
        int n = 5;
        Console.WriteLine(CountWays(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple recursive implementation
// for counting ways to reach a score
// using 1 and 2 with consecutive 2 allowed

function CountWays($n)
{
    // base cases
    if ($n == 0) {
        return 1;
    }
    if ($n == 1) {
        return 1;
    }
    if ($n == 2) {
        return 1 + 1;
    }

    // For cases n > 2
    return CountWays($n - 1) + CountWays($n - 3);
}

// Driver Code
$n = 5;
echo CountWays($n);
?>
```

## java 描述语言

```
<script>

// A simple recursive implementation for
// counting ways to reach a score using 1 and 2 with
// consecutive 2 allowed

function CountWays(n, flag)
{
    // base cases
    if (n == 0) {
        return 1;
    }
    if (n == 1) {
        return 1;
    }
    if (n == 2) {
        return 1 + 1;
    }

    // For cases n > 2
    return CountWays(n - 1) + CountWays(n - 3);
}

// Driver code

let n = 5;
document.write(CountWays(n, false));

</script>
```

**Output:** 

```
6
```

我们可以存储中间值，并在 O(n)时间和 O(n)空间中求解。

## C++

```
// Bottom up approach for
// counting ways to reach a score using 1 and 2 with
// consecutive 2 allowed
#include <iostream>
using namespace std;

int CountWays(int n)
{
    // noOfWays[i] will store count for value i.
    // 3 extra values are to take care of corner case n = 0
    int noOfWays[n + 3];

    noOfWays[0] = 1;
    noOfWays[1] = 1;
    noOfWays[2] = 1 + 1;

    // Loop till "n+1" to compute value for "n"
    for (int i=3; i<n+1; i++) {
      noOfWays[i] =
        // number of ways if first run is 1
        noOfWays[i-1]
        // number of ways if first run is 2
        // and second run is 1
        + noOfWays[i-3];
    }
    return noOfWays[n];
}

int main()
{
    int n = 0;
    cout << CountWays(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

// Bottom up approach for
// counting ways to reach a score using
// 1 and 2 with consecutive 2 allowed
class GfG {
    static int CountWays(int n)
    {
        // noOfWays[i] will store count for value i.
        // 3 extra values are to take care of cornser case n
        // = 0
        int noOfWays[] = new int[n + 3];

        noOfWays[0] = 1;
        noOfWays[1] = 1;
        noOfWays[2] = 1 + 1;

        // Loop till "n+1" to compute value for "n"
        for (int i = 3; i < n + 1; i++) {
            noOfWays[i] =
                // number of ways if first run is 1
                noOfWays[i - 1]
                // number of ways if first run is 2
                // and second run is 1
                + noOfWays[i - 3];
        }
        return noOfWays[n];
    }

    public static void main(String[] args)
    {
        int n = 5;
        System.out.println(CountWays(n));
    }
}
```

## 蟒蛇 3

```
# Bottom up approach for
# counting ways to reach a score using
# 1 and 2 with consecutive 2 allowed

def CountWays(n):

    # noOfWays[i] will store count for value i.
    # 3 extra values are to take care of corner case n = 0
    noOfWays = [0] * (n + 3)

    noOfWays[0] = 1
    noOfWays[1] = 1
    noOfWays[2] = 1 + 1

    # Loop till "n+1" to compute value for "n"
    for i in range(3, n+1):
        # number of ways if first run is 1
        # +
        # number of ways if first run is 2
        # and second run is 1
        noOfWays[i] = noOfWays[i-1] + noOfWays[i-3]
    return noOfWays[n]

# Driver Code
if __name__ == '__main__':
    n = 5
    print(CountWays(n))
```

## C#

```
// Bottom up approach for
// counting ways to reach a score using
// 1 and 2 with consecutive 2 allowed
using System;

class GfG
{

    static int CountWays(int n)
    {
        // if this state is already visited return
        // its value
        if (dp[n, flag] != -1)
        {
            return dp[n, flag];
        }

        // base case
        if (n == 0)
        {
            return 1;
        }

        // 2 is not scored last time so we can
        // score either 2 or 1
        int sum = 0;
        if (flag == 0 && n > 1)
        {
            sum = sum + CountWays(n - 1, 0) +
                    CountWays(n - 2, 1);
        }

        // 2 is scored last time so we can only score 1
        else
        {
            sum = sum + CountWays(n - 1, 0);
        }

        return dp[n,flag] = sum;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 5;
        for (int i = 0; i <dp.GetLength(0); i++)
            for (int j = 0; j < dp.GetLength(1); j++)
                dp[i,j]=-1;
    Console.WriteLine(CountWays(n, 0));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Bottom up approach for
// counting ways to reach a score using
// 1 and 2 with consecutive 2 allowed
    function CountWays(n)
    {

        // noOfWays[i] will store count for value i.
        // 3 extra values are to take care of cornser case n
        // = 0
        var noOfWays = Array(n + 3).fill(0);

        noOfWays[0] = 1;
        noOfWays[1] = 1;
        noOfWays[2] = 1 + 1;

        // Loop till "n+1" to compute value for "n"
        for (var i = 3; i < n + 1; i++) {

        // number of ways if first run is 1
        // number of ways if first run is 2
        // and second run is 1
            noOfWays[i] = noOfWays[i - 1] + noOfWays[i - 3];
        }
        return noOfWays[n];
    }

    // Driver code
        var n = 5;
        document.write(CountWays(n));

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
6
```

通过仅存储最后 3 个值，这可以进一步提高到 O(n)时间和恒定空间。

## C++

```
// Bottom up approach for
// counting ways to reach a score using 1 and 2 with
// consecutive 2 allowed
#include <iostream>
using namespace std;

int CountWays(int n)
{
    // noOfWays[i] will store count
    // for last 3 values before i.
    int noOfWays[3];

    noOfWays[0] = 1;
    noOfWays[1] = 1;
    noOfWays[2] = 1 + 1;

    // Loop till "n+1" to compute value for "n"
    for (int i=3; i<n+1; i++) {
      noOfWays[i] =
        // number of ways if first run is 1
        noOfWays[3-1]
        // number of ways if first run is 2
        // and second run is 1
        + noOfWays[3-3];

      // Remember last 3 values
      noOfWays[0] = noOfWays[1];
      noOfWays[1] = noOfWays[2];
      noOfWays[2] = noOfWays[i];
    }
    return noOfWays[n];
}

int main()
{
    int n = 5;
    cout << CountWays(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Bottom up approach for
// counting ways to reach a score using 1 and 2 with
// consecutive 2 allowed
import java.io.*;
class GFG
{

static int CountWays(int n)
{

    // noOfWays[i] will store count
    // for last 3 values before i.
    int noOfWays[] = new int[n + 3];

    noOfWays[0] = 1;
    noOfWays[1] = 1;
    noOfWays[2] = 1 + 1;

    // Loop till "n+1" to compute value for "n"
    for (int i=3; i<n+1; i++) {
      noOfWays[i] =
        // number of ways if first run is 1
        noOfWays[3-1]
        // number of ways if first run is 2
        // and second run is 1
        + noOfWays[3-3];

      // Remember last 3 values
      noOfWays[0] = noOfWays[1];
      noOfWays[1] = noOfWays[2];
      noOfWays[2] = noOfWays[i];
    }
    return noOfWays[n];
}

  // Driver code
public static void main (String[] args) {
    int n = 5;
    System.out.println(CountWays(n));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Bottom up approach for
# counting ways to reach a score using 1 and 2 with
# consecutive 2 allowed
def CountWays(n):

    # noOfWays[i] will store count
    # for last 3 values before i.
    noOfWays = [0] * (n+1)

    noOfWays[0] = 1
    noOfWays[1] = 1
    noOfWays[2] = 1 + 1

    # Loop till "n+1" to compute value for "n"
    for i in range(3, n+1):

        # number of ways if first run is 1
        # number of ways if first run is 2
        # and second run is 1
        noOfWays[i] = noOfWays[3-1] + noOfWays[3-3]

        # Remember last 3 values
        noOfWays[0] = noOfWays[1]
        noOfWays[1] = noOfWays[2]
        noOfWays[2] = noOfWays[i]

    return noOfWays[n]

if __name__ == '__main__':
    n = 5
    print(CountWays(n))

# this code is contributed by shivanisingh2110
```

## C#

```
// Bottom up approach for
// counting ways to reach a score using 1 and 2 with
// consecutive 2 allowed
using System;
using System.Collections.Generic;
public class GFG {

    static int CountWays(int n) {

        // noOfWays[i] will store count
        // for last 3 values before i.
        int []noOfWays = new int[n + 3];

        noOfWays[0] = 1;
        noOfWays[1] = 1;
        noOfWays[2] = 1 + 1;

        // Loop till "n+1" to compute value for "n"
        for (int i = 3; i < n + 1; i++) {
            noOfWays[i] =
                    // number of ways if first run is 1
                    noOfWays[3 - 1]
                            // number of ways if first run is 2
                            // and second run is 1
                            + noOfWays[3 - 3];

            // Remember last 3 values
            noOfWays[0] = noOfWays[1];
            noOfWays[1] = noOfWays[2];
            noOfWays[2] = noOfWays[i];
        }
        return noOfWays[n];
    }

    // Driver code
    public static void Main(String[] args) {
        int n = 5;
        Console.WriteLine(CountWays(n));
    }
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>
// Bottom up approach for
// counting ways to reach a score using 1 and 2 with
// consecutive 2 allowed
function CountWays(n)
{

    // noOfWays[i] will store count
    // for last 3 values before i.
    var noOfWays = Array(3).fill(0);

    noOfWays[0] = 1;
    noOfWays[1] = 1;
    noOfWays[2] = 1 + 1;

    // Loop till "n+1" to compute value for "n"
    for (var i = 3; i < n + 1; i++) {
      noOfWays[i] =
        // number of ways if first run is 1
        noOfWays[3-1]
        // number of ways if first run is 2
        // and second run is 1
        + noOfWays[3-3];

      // Remember last 3 values
      noOfWays[0] = noOfWays[1];
      noOfWays[1] = noOfWays[2];
      noOfWays[2] = noOfWays[i];
    }
    return noOfWays[n];
}

var n = 5;
document.write(CountWays(n));

// This code is contributed by shivanisinghss2110
</script>
```

**Output**

```
6
```