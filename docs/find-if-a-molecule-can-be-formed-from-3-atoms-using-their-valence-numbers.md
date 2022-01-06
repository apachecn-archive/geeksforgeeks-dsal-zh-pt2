# 用化合价数

找出一个分子是否可以由 3 个原子组成

> 原文:[https://www . geeksforgeeks . org/find-if-a-如果一个分子可以由 3 个原子利用它们的化合价数字形成/](https://www.geeksforgeeks.org/find-if-a-molecule-can-be-formed-from-3-atoms-using-their-valence-numbers/)

原子的化合价定义为该原子必须与其他原子形成的键的确切数目。给定 3 个原子的化合价，任务是确定它们是否能一起形成一个分子。原子可以彼此形成多重键。

**示例:**

```
Input: 2 4 2
Output: YES
The bonds are between the following atoms:
1 - 2
1 - 2
2 - 3
2 - 3

Input: 1 2 3
Output: NO 
```

**逼近:**设化合价为 a、b、c，设 c 最大。我们有两种情况不能形成分子:

*   **a+b+c 为奇数:**由于每个键将 2 个原子的化合价减少 1，所以化合价的总和应该是偶数。
*   **a+b < c:** 在这种情况下，即使每一个键都与 c 形成，c 也不会被满足。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible
void printPossible(int a, int b, int c)
{
    if ((a + b + c) % 2 != 0 || a + b < c)
        cout << "NO";
    else
        cout << "YES";
}

// Driver code
int main()
{
    int a = 2, b = 4, c = 2;
    printPossible(a, b, c);

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.io.*;

class GFG {
    // Function to check if it is possible
static void printPossible(int a, int b, int c)
{
    if ((a + b + c) % 2 != 0 || a + b < c)
        System.out.println("NO");
    else
        System.out.println("YES");
}

// Driver code
    public static void main (String[] args) {

    int a = 2, b = 4, c = 2;
    printPossible(a, b, c);
    }
}

// This code is contributed by akt_mit
```

## 蟒蛇 3

```
# Python 3 implementation of the
# above approach

# Function to check if it is possible
def printPossible( a, b, c):

    if ((a + b + c) % 2 != 0 or a + b < c):
        print ("NO")
    else:
        print ("YES")

# Driver code
if __name__ == "__main__":

    a = 2
    b = 4
    c = 2
    printPossible(a, b, c)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to check if it is possible
static void printPossible(int a, int b, int c)
{
    if ((a + b + c) % 2 != 0 || a + b < c)
        Console.Write("NO");
    else
        Console.Write("YES");
}

// Driver code
public static void Main()
{
    int a = 2, b = 4, c = 2;
    printPossible(a, b, c);
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to check if it is possible
function printPossible($a, $b, $c)
{
    if (($a + $b + $c) % 2 != 0 ||
         $a + $b < $c)
        echo ("NO");
    else
        echo ("YES");
}

// Driver code
$a = 2;
$b = 4;
$c = 2;
printPossible($a, $b, $c);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    // Function to check if it is possible
    function printPossible(a, b, c)
    {
        if ((a + b + c) % 2 != 0 || a + b < c)
            document.write("No");
        else
            document.write("Yes");
    }

    let a = 2, b = 4, c = 2;
    printPossible(a, b, c);

</script>
```

**输出:**

```
Yes
```

**时间复杂度:** O(1)