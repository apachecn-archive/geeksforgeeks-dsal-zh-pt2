# 实现柯拉茨猜想的程序

> 原文:[https://www . geeksforgeeks . org/c-program-implement-collaz-猜想/](https://www.geeksforgeeks.org/c-program-implement-collatz-conjecture/)

给定一个正整数 n，任务是在执行以下两个操作后，找出这个数是否达到 1:-

1.  如果 n 是偶数，那么 n = n/2。
2.  如果 n 是奇数，那么 n = 3*n + 1。
3.  重复以上步骤，直到变成 1。

例如，对于 n = 12，我们得到序列 12，6，3，10，5，16，8，4，2，1。
**例:**

```
Input : n = 4
Output : Yes

Input : n = 5
Output : Yes
```

其思想是简单地遵循给定的规则，递归地调用具有缩减值的函数，直到它达到 1。如果在递归过程中再次看到一个值，那么就有一个循环，我们不能达到 1。在这种情况下，我们返回 false。

## C++

```
// C++ program to implement Collatz Conjecture
#include<bits/stdc++.h>
using namespace std;

// Function to find if n reaches to 1 or not.
bool isToOneRec(int n, unordered_set<int> &s)
{
    if (n == 1)
        return true;

    // If there is a cycle formed, we can't r
    // reach 1.
    if (s.find(n) != s.end())
        return false;
     s.insert(n);//inserting elements to thee s

    // If n is odd then pass n = 3n+1 else n = n/2
    return (n % 2)? isToOneRec(3*n + 1, s) :
                    isToOneRec(n/2, s);
}

// Wrapper over isToOneRec()
bool isToOne(int n)
{
   // To store numbers visited using recursive calls.
   unordered_set<int> s;

   return isToOneRec(n, s);
}

// Drivers code
int main()
{
    int n = 5;
    isToOne(n) ? cout << "Yes" : cout <<"No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement Collatz Conjecture
import java.util.*;

class GFG
{

    // Function to find if n reaches to 1 or not.
    static boolean isToOneRec(int n, HashSet<Integer> s)
    {
        if (n == 1)
        {
            return true;
        }

        // If there is a cycle formed, we can't r
        // reach 1.
        if (s.contains(n))
        {
            return false;
        }

        // If n is odd then pass n = 3n+1 else n = n/2
        return (n % 2 == 1) ? isToOneRec(3 * n + 1, s)
                : isToOneRec(n / 2, s);
    }

    // Wrapper over isToOneRec()
    static boolean isToOne(int n)
    {
        // To store numbers visited using recursive calls.
        HashSet<Integer> s = new HashSet<Integer>();

        return isToOneRec(n, s);
    }

    // Drivers code
    public static void main(String[] args)
    {
        int n = 5;
        if (isToOne(n))
        {
            System.out.print("Yes");
        }
        else
        {
            System.out.print("No");
        }
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to implement Collatz Conjecture

# Function to find if n reaches to 1 or not.
def isToOneRec(n: int, s: set) -> bool:
    if n == 1:
        return True

    # If there is a cycle formed,
    # we can't reach 1.
    if n in s:
        return False

    # If n is odd then pass n = 3n+1 else n = n/2
    if n % 2:
        return isToOneRec(3 * n + 1, s)
    else:
        return isToOneRec(n // 2, s)

# Wrapper over isToOneRec()
def isToOne(n: int) -> bool:

    # To store numbers visited
    # using recursive calls.
    s = set()

    return isToOneRec(n, s)

# Driver Code
if __name__ == "__main__":
    n = 5
    if isToOne(n):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to implement
// Collatz Conjecture
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find if n reaches to 1 or not.
    static Boolean isToOneRec(int n, HashSet<int> s)
    {
        if (n == 1)
        {
            return true;
        }

        // If there is a cycle formed,
        // we can't reach 1.
        if (s.Contains(n))
        {
            return false;
        }

        // If n is odd then pass n = 3n+1 else n = n/2
        return (n % 2 == 1) ? isToOneRec(3 * n + 1, s)
                            : isToOneRec(n / 2, s);
    }

    // Wrapper over isToOneRec()
    static Boolean isToOne(int n)
    {
        // To store numbers visited using
        // recursive calls.
        HashSet<int> s = new HashSet<int>();

        return isToOneRec(n, s);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 5;
        if (isToOne(n))
        {
            Console.Write("Yes");
        }
        else
        {
            Console.Write("No");
        }
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to implement Collatz Conjecture

    // Function to find if n reaches to 1 or not.
    function isToOneRec(n, s)
    {
        if (n == 1)
        {
            return true;
        }

        // If there is a cycle formed,
        // we can't reach 1.
        if (s.has(n))
        {
            return false;
        }

        // If n is odd then pass n = 3n+1 else n = n/2
        return (n % 2 == 1) ? isToOneRec(3 * n + 1, s)
                            : isToOneRec(n / 2, s);
    }

    // Wrapper over isToOneRec()
    function isToOne(n)
    {
        // To store numbers visited using
        // recursive calls.
        let s = new Set();

        return isToOneRec(n, s);
    }

    let n = 5;
    if (isToOne(n))
    {
      document.write("Yes");
    }
    else
    {
      document.write("No");
    }

    // This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
Yes
```

上述程序效率低下。想法是用[整理猜想](https://www.geeksforgeeks.org/collatz-sequence/)。它指出，如果 n 是正数，那么在一定时间后，它会以某种方式达到 1。因此，通过使用这个事实，它可以在 O(1)中完成，即只需检查 n 是否为正整数。
注意，负数的答案是假的。对于负数，上述操作将保持负数，并且它永远不会达到 1。

## C++

```
// C++ program to implement Collatz Conjecture
#include<bits/stdc++.h>
using namespace std;

// Function to find if n reaches to 1 or not.
bool isToOne(int n)
{
    // Return true if n is positive
    return (n > 0);
}

// Drivers code
int main()
{
    int n = 5;
    isToOne(n) ? cout << "Yes" : cout <<"No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement Collatz
// Conjecture
class GFG {

    // Function to find if n reaches
    // to 1 or not.
    static boolean isToOne(int n)
    {

        // Return true if n is positive
        return (n > 0);
    }

    // Drivers code
    public static void main(String[] args)
    {
        int n = 5;

        if(isToOne(n) == true)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Smitha.
```

## 蟒蛇 3

```
# Python 3 program to implement
# Collatz Conjecture

# Function to find if n
# reaches to 1 or not.
def isToOne(n):

    # Return true if n
    # is positive
    return (n > 0)

# Drivers code
n = 5

if isToOne(n) == True:
    print("Yes")
else:
    print("No")

# This code is contributed
# by Smitha.
```

## C#

```
// C# program to implement
// Collatz Conjecture
using System;

class GFG {

    // Function to find if n
    // reaches to 1 or not.
    static bool isToOne(int n)
    {

        // Return true if n
        // is positive
        return (n > 0);
    }

    // Drivers code
    public static void Main()
    {
        int n = 5;

        if(isToOne(n) == true)
            Console.Write("Yes") ;
        else
            Console.Write("No");
    }
}

// This code is contributed
// by Smitha.
```

## java 描述语言

```
<script>
    // Javascript program to implement Collatz Conjecture

    // Function to find if n
    // reaches to 1 or not.
    function isToOne(n)
    {

        // Return true if n
        // is positive
        return (n > 0);
    }

    let n = 5;

    if(isToOne(n) == true)
      document.write("Yes") ;
    else
      document.write("No");

    // This code is contributed by mukesh07.
</script>
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement Collatz Conjecture

// Function to find if n reaches
// to 1 or not.
function isToOne($n)
{
    // Return true if n is positive
    if($n > 0)
        return true;
    return false;
}

// Driver code
$n = 5;
isToOne($n)? print("Yes") : print("No");

// This code is contributed by princiraj1992
?>
```

**输出:**

```
Yes
```

我们强烈建议参考以下问题作为练习:
[**最大排序长度**](https://practice.geeksforgeeks.org/problems/maximum-collatz-sequence-length5849/1)
本文由[**Sahil Chhabra(akku)**](https://auth.geeksforgeeks.org/?to=https://auth.geeksforgeeks.org/profile.php)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。