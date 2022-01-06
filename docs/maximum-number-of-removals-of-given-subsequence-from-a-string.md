# 从字符串中删除给定子序列的最大次数

> 原文:[https://www . geeksforgeeks . org/从字符串中删除给定子序列的最大次数/](https://www.geeksforgeeks.org/maximum-number-of-removals-of-given-subsequence-from-a-string/)

给定字符串 **str** ，任务是计算在 **str** 上可以执行的最大可能操作数。一个操作包括从字符串中提取一个子序列**‘gks’**，并将其从字符串中移除。

**示例:**

```
Input: str = "ggkssk"
Output: 1
After 1st operation: str = "gsk"
No further operation can be performed.

Input: str = "kgs"
Output: 0
```

**进场:**

1.  取三个变量 **g** 、 **gk** 和 **gks** ，分别存储子序列**【g】**、**【GK】**和**【gks】**的出现。
2.  逐个字符遍历字符串:
    *   如果 **str[i] = 'g'** 则更新 **g = g + 1** 。
    *   如果 **str[i] = 'k'** 和 **g > 0** 则更新**g = g–1**和 **gk = gk + 1** ，因为先前发现的 **'g'** 现在与当前的 **'k'** 一起贡献给子序列 **'gk'** 。
    *   同样，如果 **str[i] = 's'** 和 **gk > 0** 则更新**GK = GK–1**和 **gks = gks + 1** 。
3.  最后打印 **gks** 的值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return max possible operation
// of the given type that can be performed on str
int maxOperations(string str)
{
    int i, g, gk, gks;
    i = g = gk = gks = 0;
    for (i = 0; i < str.length(); i++) {
        if (str[i] == 'g') {

            // Increment count of sub-sequence 'g'
            g++;
        }
        else if (str[i] == 'k') {

            // Increment count of sub-sequence 'gk'
            // if 'g' is available
            if (g > 0) {
                g--;
                gk++;
            }
        }
        else if (str[i] == 's') {

            // Increment count of sub-sequence 'gks'
            // if sub-sequence 'gk' appeared previously
            if (gk > 0) {
                gk--;
                gks++;
            }
        }
    }

    // Return the count of sub-sequence 'gks'
    return gks;
}

// Driver code
int main()
{
    string a = "ggkssk";
    cout << maxOperations(a);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{
// Function to return max possible
// operation of the given type that
// can be performed on str
static int maxOperations(String str)
{
    int i, g, gk, gks;
    i = g = gk = gks = 0;
    for (i = 0; i < str.length(); i++)
    {
        if (str.charAt(i) == 'g')
        {

            // Increment count of sub-sequence 'g'
            g++;
        }
        else if (str.charAt(i) == 'k')
        {

            // Increment count of sub-sequence 'gk'
            // if 'g' is available
            if (g > 0) {
                g--;
                gk++;
            }
        }
        else if (str.charAt(i) == 's')
        {

            // Increment count of sub-sequence 'gks'
            // if sub-sequence 'gk' appeared previously
            if (gk > 0)
            {
                gk--;
                gks++;
            }
        }
    }

    // Return the count of sub-sequence 'gks'
    return gks;
}

// Driver code
public static void main(String args[])
{
    String a = "ggkssk";
    System.out.print(maxOperations(a));
}
}

// This code is contributed
// by Akanksha Rai
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return max possible operation
# of the given type that can be performed
# on str
def maxOperations( str):

    i, g, gk, gks = 0, 0, 0, 0
    for i in range(len(str)) :
        if (str[i] == 'g') :

            # Increment count of sub-sequence 'g'
            g += 1

        elif (str[i] == 'k') :

            # Increment count of sub-sequence
            # 'gk', if 'g' is available
            if (g > 0) :
                g -= 1
                gk += 1

        elif (str[i] == 's') :

            # Increment count of sub-sequence 'gks'
            # if sub-sequence 'gk' appeared previously
            if (gk > 0) :
                gk -= 1
                gks += 1

    # Return the count of sub-sequence 'gks'
    return gks

# Driver code
if __name__ == "__main__":

    a = "ggkssk"
    print(maxOperations(a))

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the approach
using System ;

public class GFG{
    // Function to return max possible operation
    // of the given type that can be performed on str
    static int maxOperations(string str)
    {
        int i, g, gk, gks;
        i = g = gk = gks = 0;
        for (i = 0; i < str.Length; i++) {
            if (str[i] == 'g') {

                // Increment count of sub-sequence 'g'
                g++;
            }
            else if (str[i] == 'k') {

                // Increment count of sub-sequence 'gk'
                // if 'g' is available
                if (g > 0) {
                    g--;
                    gk++;
                }
            }
            else if (str[i] == 's') {

                // Increment count of sub-sequence 'gks'
                // if sub-sequence 'gk' appeared previously
                if (gk > 0) {
                    gk--;
                    gks++;
                }
            }
        }

        // Return the count of sub-sequence 'gks'
        return gks;
    }

    // Driver code
    public static void Main()
    {
        string a = "ggkssk";
        Console.WriteLine(maxOperations(a)) ;

    }

}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return max possible operation
// of the given type that can be performed on str
function maxOperations($str)
{
    $i = $g = $gk = $gks = 0;
    for ($i = 0; $i < strlen($str); $i++)
    {
        if ($str[$i] == 'g')
        {

            // Increment count of sub-sequence 'g'
            $g++;
        }
        else if ($str[$i] == 'k')
        {

            // Increment count of sub-sequence 'gk'
            // if 'g' is available
            if ($g > 0)
            {
                $g--;
                $gk++;
            }
        }
        else if ($str[$i] == 's')
        {

            // Increment count of sub-sequence 'gks'
            // if sub-sequence 'gk' appeared previously
            if ($gk > 0)
            {
                $gk--;
                $gks++;
            }
        }
    }

    // Return the count of sub-sequence 'gks'
    return $gks;
}

// Driver code
$a = "ggkssk";
echo maxOperations($a);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return max possible
// operation of the given type that
// can be performed on str
function maxOperations(str)
{
    let i, g, gk, gks;
    i = g = gk = gks = 0;
    for (i = 0; i < str.length; i++)
    {
        if (str[i] == 'g')
        {

            // Increment count of sub-sequence 'g'
            g++;
        }
        else if (str[i] == 'k')
        {

            // Increment count of sub-sequence 'gk'
            // if 'g' is available
            if (g > 0) {
                g--;
                gk++;
            }
        }
        else if (str[i] == 's')
        {

            // Increment count of sub-sequence 'gks'
            // if sub-sequence 'gk' appeared previously
            if (gk > 0)
            {
                gk--;
                gks++;
            }
        }
    }

    // Return the count of sub-sequence 'gks'
    return gks;
}

// Driver code
let a = "ggkssk";
document.write(maxOperations(a));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
1
```