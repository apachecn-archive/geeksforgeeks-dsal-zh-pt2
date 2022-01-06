# 使用交换、插入或删除操作将一个给定字符串转换为另一个给定字符串的最小成本

> 原文:[https://www . geeksforgeeks . org/使用交换插入或删除操作将一个给定字符串转换为另一个给定字符串的最小成本/](https://www.geeksforgeeks.org/minimum-cost-to-convert-one-given-string-to-another-using-swap-insert-or-delete-operations/)

给定两个长度分别为 **N** 和 **M** 的字符串 **A** 和 **B** ，任务是使用以下操作找到将字符串 **A** 转换为 **B** 的最小成本:

*   字符串**的一个字符可以与同一字符串的另一个字符交换。成本= **0** 。**
*   一个字符可以从字符串 **B** 中删除，也可以插入到字符串 **A** 中。成本= **1** 。

**示例:**

> **输入:**A =“1aB+-”，B =“CC”
> **输出:** 7
> **说明:**去掉字符串 A 中所有 5 个字符，插入字符 C 两次。因此，总成本= 5 + 2 = 7。
> 
> **输入:** A = "aBcD "，B = "DBac"
> **输出:** 0
> **说明:**将字符串 A 转换为字符串 B 需要进行以下操作:
> 
> 1.  用“D”替换“a”。因此，A =“DBca”。
> 2.  用“c”替换“a”。因此，A =“DBAc”。<
> 
> 因此，总成本= 0。

**方法:**想法是执行一次交换操作的最大次数，以降低总成本。注意字符串 **A** 和 **B** 之间常见的字符可以在 **A** 中交换任意多次，使字符串等于 **B** 。所有出现在字符串 **A** 中但不出现在字符串 **B** 中的字符必须从 **A** 中删除，所有出现在 **B** 中但不出现在 **A** 中的字符必须插入到 **A** 中，以使两个字符串相等。按照以下步骤解决问题:

1.  初始化长度为 **256** 到[的两个](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**分别存储字符串 **A** 和 **B** 中每个字符的频率。
2.  初始化一个变量，比如**最小成本**，来存储最小成本。
3.  使用变量 **i** 遍历范围**【0，255】**，在每次迭代中，将**最小成本**增加**绝对值(a[I]–b[I])**。
4.  完成上述步骤后，打印**最小成本**的值，作为将字符串 **A** 转换为 **B** 所需的最小成本。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost
// to convert string a to b
void minimumCost(string a, string b)
{
    // Stores the frequency of string
    // a and b respectively
    vector<int> fre1(256), fre2(256);

    // Store the frequencies of
    // characters in a
    for (char c : a)
        fre1[(int)(c)]++;

    // Store the frequencies of
    // characters in b
    for (char c : b)
        fre2[(int)(c)]++;

    // Minimum cost to convert A to B
    int mincost = 0;

    // Find the minimum cost
    for (int i = 0; i < 256; i++) {
        mincost += abs(fre1[i]
                       - fre2[i]);
    }

    // Print the minimum cost
    cout << mincost << endl;
}

// Driver Code
int main()
{
    string A = "1AB+-", B = "cc";

    // Function Call
    minimumCost(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the minimum cost
// to convert string a to b
public static void minimumCost(String a, String b)
{

    // Stores the frequency of string
    // a and b respectively
    int fre1[] = new int[256];
    int fre2[] = new int[256];

    // Store the frequencies of
    // characters in a
    for(char c : a.toCharArray())
        fre1[(int)(c)]++;

    // Store the frequencies of
    // characters in b
    for(char c : b.toCharArray())
        fre2[(int)(c)]++;

    // Minimum cost to convert A to B
    int mincost = 0;

    // Find the minimum cost
    for(int i = 0; i < 256; i++)
    {
        mincost += Math.abs(fre1[i] -
                            fre2[i]);
    }

    // Print the minimum cost
    System.out.println(mincost);
}

// Driver Code
public static void main(String[] args)
{
    String A = "1AB+-", B = "cc";

    // Function Call
    minimumCost(A, B);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum cost
# to convert a to b
def minimumCost(a, b):

    # Stores the frequency of string
    # a and b respectively
    fre1 = [0]*(256)
    fre2 = [0]*(256)

    # Store the frequencies of
    # characters in a
    for c in a:
        fre1[ord(c)] += 1

    # Store the frequencies of
    # characters in b
    for c in b:
        fre2[ord(c)] += 1

    # Minimum cost to convert A to B
    mincost = 0

    # Find the minimum cost
    for i in range(256):
        mincost += abs(fre1[i] - fre2[i])

    # Print the minimum cost
    print(mincost)

# Driver Code
if __name__ == '__main__':
    A = "1AB+-"
    B = "cc"

    # Function Call
    minimumCost(A, B)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum cost
// to convert string a to b
public static void minimumCost(string a,
                               string b)
{

    // Stores the frequency of string
    // a and b respectively
    int[] fre1 = new int[256];
    int[] fre2 = new int[256];

    // Store the frequencies of
    // characters in a
    foreach(char c in a.ToCharArray())
        fre1[(int)(c)]++;

    // Store the frequencies of
    // characters in b
    foreach(char c in b.ToCharArray())
        fre2[(int)(c)]++;

    // Minimum cost to convert A to B
    int mincost = 0;

    // Find the minimum cost
    for(int i = 0; i < 256; i++)
    {
        mincost += Math.Abs(fre1[i] -
                            fre2[i]);
    }

    // Print the minimum cost
    Console.Write(mincost);
}

// Driver code
public static void Main()
{
    string A = "1AB+-", B = "cc";

    // Function Call
    minimumCost(A, B);
}   
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum cost
// to convert string a to b
function minimumCost(a, b)
{
    // Stores the frequency of string
    // a and b respectively
    var fre1 = Array(256).fill(0), fre2= Array(256).fill(0);

    // Store the frequencies of
    // characters in a
    a.split('').forEach(c => {
        fre1[c.charCodeAt(0)]++;
    });

    // Store the frequencies of
    // characters in b
    b.split('').forEach(c => {
        fre2[c.charCodeAt(0)]++;
    });

    // Minimum cost to convert A to B
    var mincost = 0;

    // Find the minimum cost
    for (var i = 0; i < 256; i++) {
        mincost += Math.abs(fre1[i]
                       - fre2[i]);
    }

    // Print the minimum cost
    document.write( mincost );
}

// Driver Code
var A = "1AB+-", B = "cc";

// Function Call
minimumCost(A, B);

// This code is contributed by importantly.
</script>   
```

**Output:** 

```
7
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(N + M)*