# 使两根弦相同的最小成本

> 原文:[https://www . geeksforgeeks . org/制作两个字符串的最低成本-相同/](https://www.geeksforgeeks.org/minimum-cost-to-make-two-strings-same/)

给定四个整数 **a** 、 **b** 、 **c** 、 **d** 和两个等长的字符串 **S1** 和 **S2** ，它们只由字符**‘2’**、**‘1’**和【T16’‘0’组成。

1.  将**‘1’**转换为**‘2’**或反之亦然需要**一个**。
2.  将 **'2'** 转换为 **'3'** 或反之亦然需要 **b** 。
3.  将 **'3'** 转换为 **'1'** 或反之亦然需要 **c** 。
4.  从**中删除**I<sup>th</sup>T3【字符】两个**字符串都要花费 **d** 。**

任务是找到使两个字符串在配置上相等的最小成本。
**例:**

> **输入:**S1 =“121”，S2 =“223”，a = 2，b = 3，c = 4，d = 10
> **输出:** 6
> 将第一个字符从‘1’改为‘2’，费用为 2。
> 将第三个字符从‘3’改为‘1’，费用为 4。
> **输入:** s1 = '222 '，s2 = '111 '，a = 20，b = 30，c = 40，d = 1
> **输出:** 3
> 删除所有花费 3 的字符，这是最小的可能。

**进场:**

*   迭代字符串，如果 **s1[i] = s2[i]** ，则不执行任何操作。
*   如果 **s1[i] = '1'** 和 **s2[i] = '2'** ，则执行以下最小成本操作:
    1.  删除花费 **d** 的**S1【I】**和**S2【I】**。
    2.  将**‘1’**改为**‘2’**，这需要**一个**
    3.  将 **'1'** 改为 **'3'** ，然后将 **'3'** 改为 **'2'** ，费用为 **b + c** 。
*   如果 **s1[i] = '2'** 和 **s2[i] = '3'** ，则从以下进行最小成本操作:
    1.  删除花费 **d** 的**S1【I】**和**S2【I】**。
    2.  将**‘2’**改为**‘3’**，费用为 **b** 。
    3.  将**‘2’**改为**‘1’**，然后将**‘1’**改为**‘3’**，费用为 **a + c** 。
*   如果 **s1[i] = '3'** 和 **s2[i] = '1'** ，则从以下进行最小成本操作:
    1.  删除花费 **d** 的**S1【I】**和**S2【I】**。
    2.  将**‘3’**改为**‘1’**，费用为 **c** 。
    3.  将**‘3’**改为**‘2’**，然后将**‘2’**改为**‘1’**，费用为 **b + a** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum cost to make the
// configuration of both the strings same
int findCost(string s1, string s2,
             int a, int b, int c, int d, int n)
{
    int cost = 0;

    // Iterate and find the cost
    for (int i = 0; i < n; i++) {
        if (s1[i] == s2[i])
            continue;
        else {

            // Find the minimum cost
            if ((s1[i] == '1' && s2[i] == '2')
                || (s2[i] == '1' && s1[i] == '2'))
                cost += min(d, min(a, b + c));
            else if ((s1[i] == '2' && s2[i] == '3')
                     || (s2[i] == '2' && s1[i] == '3'))
                cost += min(d, min(b, a + c));
            else if ((s1[i] == '1' && s2[i] == '3')
                     || (s2[i] == '1' && s1[i] == '3'))
                cost += min(d, min(c, a + b));
        }
    }
    return cost;
}

// Driver Code
int main()
{
    string s1 = "121";
    string s2 = "223";
    int a = 2, b = 3, c = 4, d = 10;
    int n = s1.size();
    cout << findCost(s1, s2, a, b, c, d, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the minimum cost to make the
// configuration of both the strings same
static int findCost(String s1, String s2,
                    int a, int b, int c,
                    int d, int n)
{
    int cost = 0;

    // Iterate and find the cost
    for (int i = 0; i < n; i++)
    {
        if (s1.charAt(i) == s2.charAt(i))
            continue;
        else
        {

            // Find the minimum cost
            if ((s1.charAt(i) == '1' && s2.charAt(i) == '2') ||
                (s2.charAt(i) == '1' && s1.charAt(i) == '2'))
                cost += Math.min(d, Math.min(a, b + c));
            else if ((s1.charAt(i) == '2' && s2.charAt(i) == '3') ||
                     (s2.charAt(i) == '2' && s1.charAt(i) == '3'))
                cost += Math.min(d, Math.min(b, a + c));
            else if ((s1.charAt(i) == '1' && s2.charAt(i) == '3') ||
                     (s2.charAt(i) == '1' && s1.charAt(i) == '3'))
                cost += Math.min(d, Math.min(c, a + b));
        }
    }
    return cost;
}

// Driver Code
public static void main(String[] args)
{
    String s1 = "121";
    String s2 = "223";
    int a = 2, b = 3, c = 4, d = 10;
    int n = s1.length();
    System.out.println(findCost(s1, s2, a, b, c, d, n));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the minimum cost to make
# the configuration of both the strings same
def findCost(s1, s2, a, b, c, d, n):
    cost = 0

    # Iterate and find the cost
    for i in range(n):
        if (s1[i] == s2[i]):
            continue
        else:

            # Find the minimum cost
            if ((s1[i] == '1' and s2[i] == '2') or
                (s2[i] == '1' and s1[i] == '2')):
                cost += min(d, min(a, b + c))
            elif ((s1[i] == '2' and s2[i] == '3') or
                  (s2[i] == '2' and s1[i] == '3')):
                cost += min(d, min(b, a + c))
            elif ((s1[i] == '1' and s2[i] == '3') or
                  (s2[i] == '1' and s1[i] == '3')):
                cost += min(d, min(c, a + b))
    return cost

# Driver Code
if __name__ == '__main__':
    s1 = "121"
    s2 = "223"
    a = 2
    b = 3
    c = 4
    d = 10
    n = len(s1)
    print(findCost(s1, s2, a, b, c, d, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum cost to make the
// configuration of both the strings same
static int findCost(string s1, string s2,
            int a, int b, int c, int d, int n)
{
    int cost = 0;

    // Iterate and find the cost
    for (int i = 0; i < n; i++)
    {
        if (s1[i] == s2[i])
            continue;
        else
        {

            // Find the minimum cost
            if ((s1[i] == '1' && s2[i] == '2')
                || (s2[i] == '1' && s1[i] == '2'))
                cost +=Math.Min(d,Math.Min(a, b + c));
            else if ((s1[i] == '2' && s2[i] == '3')
                    || (s2[i] == '2' && s1[i] == '3'))
                cost +=Math.Min(d,Math.Min(b, a + c));
            else if ((s1[i] == '1' && s2[i] == '3')
                    || (s2[i] == '1' && s1[i] == '3'))
                cost +=Math.Min(d,Math.Min(c, a + b));
        }
    }
    return cost;
}

// Driver Code
public static void Main()
{
    string s1 = "121";
    string s2 = "223";
    int a = 2, b = 3, c = 4, d = 10;
    int n = s1.Length;
    Console.WriteLine(findCost(s1, s2, a, b, c, d, n));
}
}

// This Code is Contributed by Code_Mech.
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function to return the minimum cost to make the
// configuration of both the strings same
function findCost( s1,  s2 ,a,  b,  c,  d,  n)
{
    var cost = 0;

    // Iterate and find the cost
    for (var i = 0; i < n; i++)
    {
        if (s1[i] == s2[i])
            continue;
        else
        {

            // Find the minimum cost
            if ((s1[i] == '1' && s2[i] == '2')
                || (s2[i] == '1' && s1[i] == '2'))
                cost +=Math.min(d,Math.min(a, b + c));
            else if ((s1[i] == '2' && s2[i] == '3')
                    || (s2[i] == '2' && s1[i] == '3'))
                cost +=Math.min(d,Math.min(b, a + c));
            else if ((s1[i] == '1' && s2[i] == '3')
                    || (s2[i] == '1' && s1[i] == '3'))
                cost +=Math.min(d,Math.min(c, a + b));
        }
    }
    return cost;
}

// Driver Code

    var s1 = "121";
    var s2 = "223";
    var a = 2, b = 3, c = 4, d = 10;
    var n = s1.length;
    document.write(findCost(s1, s2, a, b, c, d, n));

 // This code is contributed by bunnyram19.
</script>
```

**Output:** 

```
6
```