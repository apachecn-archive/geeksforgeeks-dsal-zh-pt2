# 找到一个数字 A 的字谜，当加到 A 上时会产生和 C

> 原文:[https://www . geeksforgeeks . org/find-a-a-a-a-number-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-](https://www.geeksforgeeks.org/find-an-anagram-of-a-number-a-that-generates-a-sum-c-when-added-to-a/)

给定两个正整数 **A** 和 **C** ，任务是检查数字 **B** 是否存在使得 **A + B = C** 和 **B** 是 **A** 的[字谜](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)。如果发现为真，则打印**“是”**。否则，打印**“否”**。

> **输入:** A = 123，C = 354
> **输出:** YES
> **说明:**
> 231 是 A 和 123 + 231 = 354
> 的字谜，所以需要的输出是“YES”。
> 
> **输入:** A = 123，C = 234
> T3】输出:否

**天真法:**解决问题最简单的方法是[生成**A**T5】的所有可能的数字排列，检查 **A** 和 **A** 的当前数字排列之和是否等于 **C** 。如果发现为真，则打印**“是”**。否则，如果没有找到这样的排列，打印**“否”**。](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)

***时间复杂度:** O(日志 <sub>10</sub> (N)！)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

> A+B = C
> B = C–A

按照以下步骤解决问题:

*   [检查**(C–A)**是否为 **A** 的字谜。如果发现是真的，则打印**“是”**。](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)
*   否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if an integer B exists
// such that A + B = C and B is an anagram of A
void CheckExistsABCAnagramOfA(int A, int C)
{

    int B = C - A;

    // Stores A in string format
    string a = to_string(A);

    // Stores B in string format
    string b = to_string(B);

    // Sort both the strings
    sort(a.begin(), a.end());
    sort(b.begin(), b.end());

    // Checks if both strings
    // are equal
    if (a == b) {
        cout << "YES\n";
    }
    else {
        cout << "NO\n";
    }
}

// Drivers Code
int main()
{
    int A = 123, C = 354;
    CheckExistsABCAnagramOfA(A, C);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to check if an integer B exists
// such that A + B = C and B is an anagram of A
static void CheckExistsABCAnagramOfA(int A, int C)
{
    int B = C - A;

    // Stores A in String format
    String a = String.valueOf(A);

    // Stores B in String format
    String b = String.valueOf(B);

    // Sort both the Strings
    a = sortString(a);
    b = sortString(b);

    // Checks if both Strings
    // are equal
    if (a.equals(b))
    {
        System.out.print("YES\n");
    }
    else
    {
        System.out.print("NO\n");
    }
}
static String sortString(String inputString)
{

    // convert input string to char array
    char tempArray[] = inputString.toCharArray();

    // sort tempArray
    Arrays.sort(tempArray);

    // return new sorted string
    return new String(tempArray);
}

// Drivers Code
public static void main(String[] args)
{
    int A = 123, C = 354;
    CheckExistsABCAnagramOfA(A, C);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program to implement the above
# approach

# Function to check if an integer B exists
# such that A + B = C and B is an anagram of A
def CheckExistsABCAnagramOfA(A, C):

    B = C - A

    # To convert number to list of integers
    a = [int(x) for x in str(A)]

    # To convert number to list of integers
    b = [int(x) for x in str(B)]

    # Sort both the strings
    a.sort()
    b.sort()

    # Checks if both strings
    # are equal
    if (a == b):
        print("YES")
    else:
        print("NO")

# Driver Code
A = 123
C = 354

CheckExistsABCAnagramOfA(A, C)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to check if an integer B
// exists such that A + B = C and B
// is an anagram of A
static void CheckExistsABCAnagramOfA(int A, int C)
{
    int B = C - A;

    // Stores A in String format
    String a = String.Join("", A);

    // Stores B in String format
    String b = String.Join("", B);

    // Sort both the Strings
    a = sortString(a);
    b = sortString(b);

    // Checks if both Strings
    // are equal
    if (a.Equals(b))
    {
        Console.Write("YES\n");
    }
    else
    {
        Console.Write("NO\n");
    }
}

static String sortString(String inputString)
{

    // Convert input string to char array
    char []tempArray = inputString.ToCharArray();

    // Sort tempArray
    Array.Sort(tempArray);

    // Return new sorted string
    return new String(tempArray);
}

// Driver Code
public static void Main(String[] args)
{
    int A = 123, C = 354;

    CheckExistsABCAnagramOfA(A, C);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to check if an integer B exists
// such that A + B = C and B is an anagram of A
function CheckExistsABCAnagramOfA(A, C)
{

    var B = C - A;

    // Stores A in string format
    var a = (A.toString());

    // Stores B in string format
    var b = (B.toString());

    // Sort both the strings
    a = a.split('').sort().join('');
    b = b.split('').sort().join('');

    // Checks if both strings
    // are equal
    if (a == b) {
        document.write( "YES");
    }
    else {
        document.write( "NO");
    }
}

// Drivers Code
var A = 123, C = 354;
CheckExistsABCAnagramOfA(A, C);

</script>
```

**Output:** 

```
YES
```

***时间复杂度:**O(log<sub>10</sub>(A)* log(log<sub>10</sub>(A)))*
***辅助空间:** O(log <sub>10</sub> (A))*