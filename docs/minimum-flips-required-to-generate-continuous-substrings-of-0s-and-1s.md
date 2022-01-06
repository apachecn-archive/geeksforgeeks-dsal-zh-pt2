# 生成 0 和 1 的连续子串所需的最小翻转次数

> 原文:[https://www . geesforgeks . org/minimum-flips-required-to-generate-continuous-substrings-of-0s-and-1s/](https://www.geeksforgeeks.org/minimum-flips-required-to-generate-continuous-substrings-of-0s-and-1s/)

给定长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找到转换给定字符串所需的最小位翻转数，使其仅包含 0 和 1 的连续子字符串，从而使最终字符串的形式为 **000..000** 、 **111..111** 、 **111…000** 或 **000…111** 。

**示例:**

> **输入:** S = 000100101，N = 9
> **输出:** 2
> **解释:**
> 000**1**00**1**01->000**0**00**0**01
> 
> **输入:** S = 01100，N = 5
> **输出:** 1
> **解释:**
> **0**1100->**1**1100

**方法:**
在两次线性遍历中可以有效地计算出翻转的最小次数。
在第一次遍历中，我们将计算最坏情况下所需的最小翻转次数，因为它可以等于*最初的 0 总数*。
在第二次遍历中，在每一步，所需的翻转总数将是该点之前的 1 和该点之后的 0 的总和。我们将对每一步计算的所有值取最小值。

因此，要解决该问题，请遵循以下步骤:

*   初始化变量**计数 0** = 0、**计数 1** = 0 和 **res** = 0。其中，count0 存储计数 0，count1 存储计数 1，res 存储所需的位翻转。
*   遍历输入字符串，计算 0 并将其存储在 res 变量中。
*   遍历输入字符串，如果找到字符 0，则减去 0 的计数，并将字符 1 的计数存储在变量 count1 中，并将 res 更新为 **min(res，count0+count1)** 。

下面是上述方法的实现。

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

int minChanges(string str, int N)
{
    int res;
    int count0 = 0, count1 = 0;

    // Traverse input string
    // and store the count of 0
    for (char x : str) {
        count0 += (x == '0');
    }
    res = count0;

    // Traverse the input string again
    // to find minimum number of flips
    for (char x : str) {
        count0 -= (x == '0');
        count1 += (x == '1');
        res = min(res, count1 + count0);
    }

    return res;
}

// Driver code
int main()
{
    int N = 9;
    string str = "000101001";

    cout << minChanges(str, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG{

static int minChanges(String str, int N)
{
    int res;
    int count0 = 0, count1 = 0;

    // Traverse input string
    // and store the count of 0
    for(char x : str.toCharArray())
    {
       if (x == '0')
           count0++;
    }
    res = count0;

    // Traverse the input string again
    // to find minimum number of flips
    for(char x : str.toCharArray())
    {
       if (x == '0')
           count0--;
       if (x == '1')
           count1++;

       res = Math.min(res, count1 + count0);
    }
    return res;
}

// Driver code
public static void main(String[] args)
{
    int N = 9;
    String str = "000101001";

    System.out.println(minChanges(str, N));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
def minChanges(str, N):

    count0 = 0
    count1 = 0

    # Traverse input string
    # and store the count of 0
    for x in str:
        count0 += (x == '0')

    res = count0

    # Traverse the input string again
    # to find minimum number of flips
    for x in str:
        count0 -= (x == '0')
        count1 += (x == '1')
        res = min(res, count1 + count0)

    return res

# Driver code
N = 9
str = "000101001"

print(minChanges(str, N))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation of the above approach
using System;

class GFG{

static int minChanges(String str, int N)
{
    int res;
    int count0 = 0, count1 = 0;

    // Traverse input string
    // and store the count of 0
    for(int i = 0; i < str.Length; i++)
    {
        if (str[i] == '0')
            count0++;
    }
    res = count0;

    // Traverse the input string again
    // to find minimum number of flips
    for(int i = 0; i< str.Length; i++)
    {
        if (str[i] == '0')
            count0--;
        if (str[i] == '1')
            count1++;

        res = Math.Min(res, count1 + count0);
    }
    return res;
}

// Driver code
public static void Main()
{
    int N = 9;
    String str = "000101001";

    Console.Write(minChanges(str, N));
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

function minChanges(str, N)
{
    var res;
    var count0 = 0, count1 = 0;

    // Traverse input string
    // and store the count of 0
    str.split('').forEach(x => {

        count0 += (x == '0');
    });
    res = count0;

    // Traverse the input string again
    // to find minimum number of flips
    str.split('').forEach(x => {

        count0 -= (x == '0');
        count1 += (x == '1');
        res = Math.min(res, count1 + count0);
    });

    return res;
}

// Driver code
var N = 9;
var str = "000101001";
document.write( minChanges(str, N));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** *O(k)* ，其中，k 是二进制字符串的长度。
**空间复杂度:** *O(1)*