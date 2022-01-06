# 找到房屋最大可能被盗价值

> 原文:[https://www . geesforgeks . org/find-最大可能被盗价值房屋/](https://www.geeksforgeeks.org/find-maximum-possible-stolen-value-houses/)

一条线上有 n 栋房子，每栋房子都有一定的价值。一个小偷要去偷这些房子的最大价值，但是他不能在相邻的两个房子里偷，因为被偷房子的主人会告诉他的左右两边的两个邻居。最大被盗价值是多少？
**例:**

```
Input: hval[] = {6, 7, 1, 3, 8, 2, 4}
Output: 19

Explanation: The thief will steal 6, 1, 8 and 4 from the house.

Input: hval[] = {5, 3, 4, 11, 2}
Output: 16

Explanation: Thief will steal 5 and 11
```

**<u>天真方法</u> :** 给定一个数组，解决方法是找到最大和子序列，其中没有两个选定的元素相邻。所以这个问题的解决方法是递归的。所以有两种情况。

1.  如果选择了一个元素，则不能选择下一个元素。
2.  如果一个元素没有被选中，那么下一个元素可以被选中。

所以递归解很容易设计出来。可以存储子问题，从而降低复杂性，并将递归解转换为动态规划问题。

**算法:**

1.  创建一个额外的空间 *dp* ，dp 数组来存储子问题。
2.  处理一些基本情况，如果数组的长度是 0，打印 0，如果数组的长度是 1，打印第一个元素，如果数组的长度是 2，打印最多两个元素。
3.  将*DP【0】*更新为*数组【0】*并将*DP【1】*更新为*数组【0】*和*数组【1】*的最大值
4.  遍历数组，从第二个元素(第二个索引)到数组的末尾。
5.  对于每个索引，将 *dp[i]* 更新为 *dp[i-2] +数组[i]* 和 *dp[i-1]* 的最大值，此步骤定义了两种情况，如果选择了一个元素，则不能选择上一个元素，如果没有选择元素，则可以选择上一个元素。
6.  打印数值 *dp[n-1]*

**执行:**

## C++

```
// CPP program to find the maximum stolen value
#include <iostream>
using namespace std;

// calculate the maximum stolen value
int maxLoot(int *hval, int n)
{
    if (n == 0)
        return 0;
    if (n == 1)
        return hval[0];
    if (n == 2)
        return max(hval[0], hval[1]);

    // dp[i] represent the maximum value stolen
    // so far after reaching house i.
    int dp[n];

    // Initialize the dp[0] and dp[1]
    dp[0] = hval[0];
    dp[1] = max(hval[0], hval[1]);

    // Fill remaining positions
    for (int i = 2; i<n; i++)
        dp[i] = max(hval[i]+dp[i-2], dp[i-1]);

    return dp[n-1];
}

// Driver to test above code
int main()
{
    int hval[] = {6, 7, 1, 3, 8, 2, 4};
    int n = sizeof(hval)/sizeof(hval[0]);
    cout << "Maximum loot possible : "
        << maxLoot(hval, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum stolen value
import java.io.*;

class GFG
{
    // Function to calculate the maximum stolen value
    static int maxLoot(int hval[], int n)
    {
        if (n == 0)
        return 0;
        if (n == 1)
            return hval[0];
        if (n == 2)
            return Math.max(hval[0], hval[1]);

        // dp[i] represent the maximum value stolen
        // so far after reaching house i.
        int[] dp = new int[n];

        // Initialize the dp[0] and dp[1]
        dp[0] = hval[0];
        dp[1] = Math.max(hval[0], hval[1]);

        // Fill remaining positions
        for (int i = 2; i<n; i++)
            dp[i] = Math.max(hval[i]+dp[i-2], dp[i-1]);

        return dp[n-1];
    }

    // Driver program
    public static void main (String[] args)
    {
        int hval[] = {6, 7, 1, 3, 8, 2, 4};
        int n = hval.length;
        System.out.println("Maximum loot value : " + maxLoot(hval, n));
    }
}

// Contributed by Pramod Kumar
```

## 计算机编程语言

```
# Python3 program to find the maximum stolen value

# calculate the maximum stolen value
def maximize_loot(hval, n):
    if n == 0:
        return 0
    if n == 1:
        return hval[0]
    if n == 2:
        return max(hval[0], hval[1])

    # dp[i] represent the maximum value stolen so
    # for after reaching house i.
    dp = [0]*n

    # Initialize the dp[0] and dp[1]
    dp[0] = hval[0]
    dp[1] = max(hval[0], hval[1])

    # Fill remaining positions
    for i in range(2, n):
        dp[i] = max(hval[i]+dp[i-2], dp[i-1])

    return dp[-1]

# Driver to test above code
def main():

    # Value of houses
    hval = [6, 7, 1, 3, 8, 2, 4]

    # number of houses
    n = len(hval)
    print("Maximum loot value : {}".
        format(maximize_loot(hval, n)))

if __name__ == '__main__':
    main()
```

## C#

```
// C# program to find the
// maximum stolen value
using System;

class GFG
{
   // Function to calculate the
   // maximum stolen value
    static int maxLoot(int []hval, int n)
    {
        if (n == 0)
        return 0;
        if (n == 1)
            return hval[0];
        if (n == 2)
            return Math.Max(hval[0], hval[1]);

        // dp[i] represent the maximum value stolen
        // so far after reaching house i.
        int[] dp = new int[n];

        // Initialize the dp[0] and dp[1]
        dp[0] = hval[0];
        dp[1] = Math.Max(hval[0], hval[1]);

        // Fill remaining positions
        for (int i = 2; i<n; i++)
            dp[i] = Math.Max(hval[i]+dp[i-2], dp[i-1]);

        return dp[n-1];
    }

    // Driver program
    public static void Main ()
    {
        int []hval = {6, 7, 1, 3, 8, 2, 4};
        int n = hval.Length;
        Console.WriteLine("Maximum loot value : " +
                                 maxLoot(hval, n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// the maximum stolen value

// calculate the maximum
// stolen value
function maxLoot($hval, $n)
{
    if ($n == 0)
        return 0;
    if ($n == 1)
        return $hval[0];
    if ($n == 2)
        return max($hval[0],
                   $hval[1]);

    // dp[i] represent the maximum
    // value stolen so far after
    // reaching house i.
    $dp = array();

    // Initialize the
    // dp[0] and dp[1]
    $dp[0] = $hval[0];
    $dp[1] = max($hval[0],
                 $hval[1]);

    // Fill remaining positions
    for ($i = 2; $i < $n; $i++)
        $dp[$i] = max($hval[$i] +
                      $dp[$i - 2],
                      $dp[$i - 1]);

    return $dp[$n - 1];
}

// Driver Code
$hval = array(6, 7, 1,
              3, 8, 2, 4);
$n = sizeof($hval);
echo "Maximum loot possible : ",
             maxLoot($hval, $n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

    // Javascript program to find
    // the maximum stolen value

    // Function to calculate the
       // maximum stolen value
    function maxLoot(hval, n)
    {
        if (n == 0)
            return 0;
        if (n == 1)
            return hval[0];
        if (n == 2)
            return Math.max(hval[0], hval[1]);

        // dp[i] represent the maximum value stolen
        // so far after reaching house i.
        let dp = new Array(n);

        // Initialize the dp[0] and dp[1]
        dp[0] = hval[0];
        dp[1] = Math.max(hval[0], hval[1]);

        // Fill remaining positions
        for (let i = 2; i<n; i++)
            dp[i] = Math.max(hval[i]+dp[i-2], dp[i-1]);

        return dp[n-1];
    }

    let hval = [6, 7, 1, 3, 8, 2, 4];
    let n = hval.length;
    document.write(
    "Maximum loot value : " + maxLoot(hval, n)
    );

</script>
```

**输出:**

```
Maximum loot value : 19
```

**复杂度分析:**

*   **时间复杂度:** ![O(n)     ](img/3f5dde030cf148810d5b451a02916dac.png "Rendered by QuickLaTeX.com")。
    只需要遍历一次原数组。所以时间复杂度是 O(n)
*   **空间复杂度:** ![O(n)     ](img/3f5dde030cf148810d5b451a02916dac.png "Rendered by QuickLaTeX.com")。
    需要一个大小为 n 的数组，所以空间复杂度为 O(n)。

**高效方法:**通过仔细观察 DP 数组，可以看出在计算一个指标的值时，前两个指标的值很重要。用两个变量替换整个数组。

**算法:**

1.  处理一些基本情况，如果数组的长度是 0，打印 0，如果数组的长度是 1，打印第一个元素，如果数组的长度是 2，打印最多两个元素。
2.  创建两个变量*值 1* 和*值 2* *值 1* 作为*数组【0】*和*值 2* 作为*数组【0】*和*数组【1】*的最大值，并创建一个变量 *max_val* 来存储答案
3.  遍历数组，从第二个元素(第二个索引)到数组的末尾。
4.  对于每个索引，将 *max_val* 更新为*值 1 +数组【I】*和*值 2* 的最大值，此步骤定义了两种情况，如果选择了一个元素，则不能选择上一个元素，如果没有选择元素，则可以选择上一个元素。
5.  对于每个指数，更新*值 1 =值 2* 和*值 2 =最大值*
6.  打印*最大 _ 值*的值

**执行:**

## C++

```
// C++ program to find the maximum stolen value
#include <iostream>
using namespace std;

// calculate the maximum stolen value
int maxLoot(int *hval, int n)
{
    if (n == 0)
        return 0;

    int value1 = hval[0];
    if (n == 1)
        return value1;

    int value2 = max(hval[0], hval[1]);
    if (n == 2)
        return value2;

    // contains maximum stolen value at the end
    int max_val;

    // Fill remaining positions
    for (int i=2; i<n; i++)
    {
        max_val = max(hval[i]+value1, value2);
        value1 = value2;
        value2 = max_val;
    }

    return max_val;
}

// Driver to test above code
int main()
{
    // Value of houses
    int hval[] = {6, 7, 1, 3, 8, 2, 4};
    int n = sizeof(hval)/sizeof(hval[0]);
    cout << "Maximum loot possible : "
        << maxLoot(hval, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum stolen value
import java.io.*;

class GFG
{
    // Function to calculate the maximum stolen value
    static int maxLoot(int hval[], int n)
    {
        if (n == 0)
        return 0;

        int value1 = hval[0];
        if (n == 1)
            return value1;

        int value2 = Math.max(hval[0], hval[1]);
        if (n == 2)
            return value2;

        // contains maximum stolen value at the end
        int max_val = 0;

        // Fill remaining positions
        for (int i=2; i<n; i++)
        {
            max_val = Math.max(hval[i]+value1, value2);
            value1 = value2;
            value2 = max_val;
        }

        return max_val;
    }

    // driver program
    public static void main (String[] args)
    {
        int hval[] = {6, 7, 1, 3, 8, 2, 4};
        int n = hval.length;
        System.out.println("Maximum loot value : " + maxLoot(hval, n));
    }
}

// Contributed by Pramod kumar
```

## 计算机编程语言

```
# Python3 program to find the maximum stolen value

# calculate the maximum stolen value
def maximize_loot(hval, n):
    if n == 0:
        return 0

    value1 = hval[0]
    if n == 1:
        return value1

    value2 = max(hval[0], hval[1])
    if n == 2:
        return value2

    # contains maximum stolen value at the end
    max_val = None

    # Fill remaining positions
    for i in range(2, n):
        max_val = max(hval[i]+value1, value2)
        value1 = value2
        value2 = max_val

    return max_val

# Driver to test above code
def main():

    # Value of houses
    hval = [6, 7, 1, 3, 8, 2, 4]

    # number of houses
    n = len(hval)
    print("Maximum loot value : {}".format(maximize_loot(hval, n)))

if __name__ == '__main__':
    main()
```

## C#

```
// C# program to find the
// maximum stolen value
using System;

public class GFG
{
    // Function to calculate the
    // maximum stolen value
    static int maxLoot(int []hval, int n)
    {
        if (n == 0)
        return 0;

        int value1 = hval[0];
        if (n == 1)
            return value1;

        int value2 = Math.Max(hval[0], hval[1]);
        if (n == 2)
            return value2;

        // contains maximum stolen value at the end
        int max_val = 0;

        // Fill remaining positions
        for (int i = 2; i < n; i++)
        {
            max_val = Math.Max(hval[i] + value1, value2);
            value1 = value2;
            value2 = max_val;
        }

        return max_val;
    }

    // Driver program
    public static void Main ()
    {
        int []hval = {6, 7, 1, 3, 8, 2, 4};
        int n = hval.Length;
        Console.WriteLine("Maximum loot value : " +
                                 maxLoot(hval, n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// the maximum stolen value

// calculate the
// maximum stolen value
function maxLoot($hval, $n)
{
    if ($n == 0)
        return 0;

    $value1 = $hval[0];
    if ($n == 1)
        return $value1;

    $value2 = max($hval[0],
                  $hval[1]);
    if ($n == 2)
        return $value2;

    // contains maximum
    // stolen value at the end
    $max_val;

    // Fill remaining positions
    for ($i = 2; $i < $n; $i++)
    {
        $max_val = max($hval[$i] +
                       $value1, $value2);
        $value1 = $value2;
        $value2 = $max_val;
    }

    return $max_val;
}

// Driver code
$hval = array(6, 7, 1, 3, 8, 2, 4);
$n = sizeof($hval);
echo "Maximum loot value : ",
          maxLoot($hval, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to find the
    // maximum stolen value

    // Function to calculate the
    // maximum stolen value
    function maxLoot(hval, n)
    {
        if (n == 0)
            return 0;

        let value1 = hval[0];
        if (n == 1)
            return value1;

        let value2 = Math.max(hval[0], hval[1]);
        if (n == 2)
            return value2;

        // contains maximum stolen value at the end
        let max_val = 0;

        // Fill remaining positions
        for (let i = 2; i < n; i++)
        {
            max_val = Math.max(hval[i] +
                               value1, value2);
            value1 = value2;
            value2 = max_val;
        }

        return max_val;
    }

    let hval = [6, 7, 1, 3, 8, 2, 4];
    let n = hval.length;
    document.write("Maximum loot value : "
    + maxLoot(hval, n));

</script>
```

**输出:**

```
Maximum loot value : 19
```

**复杂度分析:**

*   **时间复杂度:** ![O(n)     ](img/3f5dde030cf148810d5b451a02916dac.png "Rendered by QuickLaTeX.com")，只需要遍历一次原数组。所以时间复杂度是 O(n)。
*   **辅助空间:** ![O(1)     ](img/863866cdae429a7ac0da7a9c42279288.png "Rendered by QuickLaTeX.com")，不需要额外空间，所以空间复杂度不变。

本文由 [**阿图尔·库马尔**](https://www.linkedin.com/in/atul-kumar-733b32136/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。