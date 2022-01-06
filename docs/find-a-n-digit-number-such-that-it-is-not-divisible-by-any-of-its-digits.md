# 找到一个 N 位数，这样它就不能被它的任何一个数字整除

> 原文:[https://www . geesforgeks . org/find-a-n-digit-number-so-它不能被它的任何一个数字整除/](https://www.geeksforgeeks.org/find-a-n-digit-number-such-that-it-is-not-divisible-by-any-of-its-digits/)

给定一个整数 **N** ，任务是找到任何 N 位数的正数(除了零)，这样它就不能被它的任何位数整除。如果找不到这样的号码，则打印 **-1** 。
**注:**同一个 N 位数字可以有多个这样的数字。
**示例:**

```
Input: N = 2  
Output: 23
23 is not divisible by 2 or 3

Input: N = 3
Output: 239
```

**方法:**
这个问题最简单的解决方法可以借助数字‘4’和‘5’来想到。

1.  因为，为了让一个数能被 5 整除，这个数必须以 0 或 5 结尾；为了能被 4 整除，如果数字必须能被 4 整除，最后两位数字。
2.  因此，可以应用一种快捷方法来防止 4 和 5 的可除性标准，如下所示:
    *   为了防止一个数被 5 整除，除了最后一个数字，这个数可以每隔一个数字包含 5。

```
Therefore for N digit number,
(N - 1) digits must be 5 = 5555...(N-1 times)d
where d is the Nth digit
```

*   为了防止一个数被 4 整除，这个数可以在倒数第二位包含 5，在最后一位包含 4。

```
Therefore for N digit number,
Last digit must be 4 = 5555...(N-1 times)4
```

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to find N digit number such
// that it is not divisible by any of its digits

#include <bits/stdc++.h>
using namespace std;

// Function that print the answer
void findTheNumber(int n)
{
    // if n == 1 then it is
    // not possible
    if (n == 1) {
        cout << "Impossible" << endl;
        return;
    }

    // loop to n-1 times
    for (int i = 0; i < n - 1; i++) {
        cout << "5";
    }

    // print 4 as last digit of
    // the number
    cout << "4";
}

// Driver code
int main()
{
    int n = 12;

    // Function call
    findTheNumber(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find N digit number such
// that it is not divisible by any of its digits
class GFG{

// Function that print the answer
static void findTheNumber(int n)
{
    // if n == 1 then it is
    // not possible
    if (n == 1) {
        System.out.print("Impossible" +"\n");
        return;
    }

    // loop to n-1 times
    for (int i = 0; i < n - 1; i++) {
        System.out.print("5");
    }

    // print 4 as last digit of
    // the number
    System.out.print("4");
}

// Driver code
public static void main(String[] args)
{
    int n = 12;

    // Function call
    findTheNumber(n);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find N digit number such
# that it is not divisible by any of its digits

# Function that print answer
def findTheNumber(n):
    # if n == 1 then it is
    # not possible
    if (n == 1):
        print("Impossible")
        return

    # loop to n-1 times
    for i in range(n-1):
        print("5",end="")

    # print as last digit of
    # the number
    print("4")

# Driver code
if __name__ == '__main__':
    n = 12

    #Function call
    findTheNumber(n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find N digit number such
// that it is not divisible by any of its digits
using System;

class GFG{

// Function that print the answer
static void findTheNumber(int n)
{
    // if n == 1 then it is
    // not possible
    if (n == 1) {
        Console.Write("Impossible" +"\n");
        return;
    }

    // loop to n-1 times
    for (int i = 0; i < n - 1; i++) {
        Console.Write("5");
    }

    // print 4 as last digit of
    // the number
    Console.Write("4");
}

// Driver code
public static void Main(String[] args)
{
    int n = 12;

    // Function call
    findTheNumber(n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find N digit number such
// that it is not divisible by any of its digits

// Function that print the answer
function findTheNumber(n)
{
    // if n == 1 then it is
    // not possible
    if (n == 1) {
        document.write( "Impossible" );
        return;
    }

    // loop to n-1 times
    for (var i = 0; i < n - 1; i++) {
        document.write( "5");
    }

    // print 4 as last digit of
    // the number
    document.write( "4");
}

// Driver code
var n = 12;
// Function call
findTheNumber(n);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
555555555554
```

**时间复杂度:** **0(N)**