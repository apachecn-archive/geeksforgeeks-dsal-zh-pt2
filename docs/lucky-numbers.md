# 幸运数字

> 原文:[https://www.geeksforgeeks.org/lucky-numbers/](https://www.geeksforgeeks.org/lucky-numbers/)

幸运数字是整数的子集。不多讲理论，让我们看看得出幸运数字的过程，
取整数集
1，2，3，4，5，6，7，8，9，10，11，12，13，14，15，16，17，18，19，…
首先，删除每一秒钟的数字，我们得到以下约简集。
1，3，5，7，9，11，13，15，17，19，…………
现在，删除第三个数字，我们得到
1，3，7，9，13，15，19，…。….
无限期地继续这个过程……
任何没有因上述过程而被删除的数字都被称为“幸运”。
因此，幸运数字集是 1，3，7，13，…………
现在，给定一个整数‘n’，编写一个函数来表示这个数字是否幸运。

```
    bool isLucky(int n)
```

**算法:**
在每次迭代之前，如果我们计算给定数字的位置，那么在给定的迭代中，我们可以确定该数字是否会被删除。假设在某次迭代之前，给定数的计算位置是 P，在这次迭代中，每个 Ith 数都将被移除，I

f P < I 那么输入的数字就是幸运的，

如果 P 是这样的，P%I == 0 (I 是 P 的除数)，那么输入 no 就不算幸运。

**如何计算数字的下一个位置:**

我们知道，最初数的位置是 n 本身。现在，任何下一个位置将等于前一个位置减去移除的元素(或者说项目)的数量。

也就是说，**next _ position = current _ position–移除的数字计数**

以 **n=13** 为例。

我们有:初始位置:n，即。13 本身。

1,2,3,4,5,6,7,8,9,10,11,12,13

现在，在删除每一秒元素之后，我们实际上删除了 n/2 个元素。所以现在 13 的位置将是: **n-n/2=13-6=7 (n=13)，i=2**

1,3,5,7,9,11,13.

之后，我们移除 n/3 个项目。注意，n 现在是 n=7。所以 13 的位置: **n-n/3 = 7-7/3 = 7-2 = 5 (n=7)，i=3**

1,3,7,9,13

所以接下来会是: **n-n/4 = 5-5/4 = 4 (n=5)，i=4**

1,3,7,13

所以现在我=5，但是因为 13 的位置只有 4，所以它将被保存。因此是一个幸运数字！ **n=4，i=5**

**递归方式:**

## C++

```
// C++ program for Lucky Numbers
#include <bits/stdc++.h>
using namespace std;
#define bool int

/* Returns 1 if n is a lucky no.
otherwise returns 0*/
bool isLucky(int n)
{
    static int counter = 2;

    if(counter > n)
        return 1;
    if(n % counter == 0)
        return 0;

    /*calculate next position of input no.
      Variable "next_position" is just for
    readability of the program we can
    remove it and update in "n" only */
    int next_position = n - (n/counter);

    counter++;
    return isLucky(next_position);
}

// Driver Code
int main()
{
    int x = 5;
    if( isLucky(x) )
        cout << x << " is a lucky no.";
    else
        cout << x << " is not a lucky no.";
}

// This code is contributed
// by rathbhupendra
```

## C

```
#include <stdio.h>
#define bool int

/* Returns 1 if n is a lucky no. otherwise returns 0*/
bool isLucky(int n)
{
    static int counter = 2;

    if(counter > n)
        return 1;
    if(n%counter == 0)
        return 0;    

    /*calculate next position of input no.
      Variable "next_position" is just for
    readability of the program we can
    remove it and update in "n" only */
    int next_position = n - (n/counter);

    counter++;
    return isLucky(next_position);
}

/*Driver function to test above function*/
int main()
{
    int x = 5;
    if( isLucky(x) )
        printf("%d is a lucky no.", x);
    else
        printf("%d is not a lucky no.", x);
    getchar();
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check Lucky Number
import java.io.*;

class GFG
{
    public static int counter = 2;   

    // Returns 1 if n is a lucky no.
    // otherwise returns 0
    static boolean isLucky(int n)
    {
        if(counter > n)
            return true;
        if(n%counter == 0)
            return false;     

        /*calculate next position of input no.
        Variable "next_position" is just for
        readability of the program we can
        remove it and update in "n" only */
        int next_position = n - (n/counter);

        counter++;
        return isLucky(next_position);
    }

    // driver program
    public static void main (String[] args)
    {
        int x = 5;
        if( isLucky(x) )
            System.out.println(x+" is a lucky no.");
        else
            System.out.println(x+" is not a lucky no.");
    }
}

// Contributed by Pramod Kumar
```

## 计算机编程语言

```
# Python program to check for lucky number

# Returns 1 if n is a lucky number
# otherwise returns 0
def isLucky(n):

    # Function attribute will act
    # as static variable  

    if isLucky.counter > n:
        return 1
    if n % isLucky.counter == 0:
        return 0

    #calculate next position of input no.
      #Variable "next_position" is just for
    #readability of the program we can
    #remove it and update in "n" only
    next_position = n - (n/isLucky.counter)

    isLucky.counter = isLucky.counter + 1

    return isLucky(next_position)

# Driver Code

isLucky.counter = 2 # Acts as static variable
x = 5
if isLucky(x):
    print x,"is a Lucky number"
else:
    print x,"is not a Lucky number"

# Contributed by Harshit Agrawal
```

## C#

```
// C# program to check Lucky Number
using System;

class GFG {

    public static int counter = 2;

    // Returns 1 if n is a lucky no.
    // otherwise returns 0
    static bool isLucky(int n)
    {       
        if(counter > n)
            return true;
        if(n % counter == 0)
            return false;    

       /*calculate next position of input no.
        Variable "next_position" is just for
        readability of the program we can
        remove it and update in "n" only */
        int next_position = n - (n/counter);

        counter++;

        return isLucky(next_position);
    }

    // driver program
    public static void Main ()
    {
        int x = 5;

        if( isLucky(x) )
            Console.Write(x + " is a "
                         + "lucky no.");
        else
            Console.Write(x + " is not"
                      + " a lucky no.");
    }
}

// This code is contributed by
// nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for Lucky Numbers

/* Returns 1 if n is a lucky
   no. otherwise returns 0 */
function isLucky($n)
{
    $counter = 2;

    if($counter > $n)
        return 1;
    if($n % $counter == 0)
        return 0;

    /*calculate next position of input no.
      Variable "next_position" is just for
    readability of the program we can
    remove it and update in "n" only */
    $next_position = $n - ($n / $counter);

    $counter++;
    return isLucky($next_position);
}

    // Driver Code
    $x = 5;
    if(isLucky($x) )
        echo $x ," is a lucky no.";
    else
        echo $x ," is not a lucky no.";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// C++ program for Lucky Numbers

/* Returns 1 if n is a lucky no.
otherwise returns 0*/
function isLucky(n)
{
    let counter = 2;

    if(counter > n)
        return 1;
    if(n % counter == 0)
        return 0;

   /*calculate next position of input no.
      Variable "next_position" is just for
    readability of the program we can
    remove it and update in "n" only */
    let next_position = n - Math.floor(n/counter);

    counter++;
    return isLucky(next_position);
}

// Driver Code

    let x = 5;
    if( isLucky(x) )
        document.write(x + " is a lucky no.");
    else
        document.write(x + " is not a lucky no.");

// This code is contributed by Mayank Tyagi

</script>
```

**Output**

```
5 is not a lucky no.
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*

**例:**
我们举一个 19
1，2，3，4，5，6，7，8，9，10，11，12，13，14，15，15，17，18，19，20，21，…
1，3，5，7，9，11，13，15，17，19，…..
1，3，7，9，13，15，19，…。
1，3，7，13，15，19、……
1，3，7，13，19、……
下一步每隔 6 个 no。按顺序将被删除。此步骤后不会删除 19，因为 19 的位置在此步骤后第 5 位。因此，19 岁是幸运的。让我们看看上面的 C 代码是如何发现的:

**Current function call** **Position after this call** **Counter for next call** **Next Call** isLucky(19 ) 10 3 isLucky(10) isLucky(10) 7 4 isLucky(7) isLucky(7) 6 5 isLucky(6) isLucky(6) 5 6 isLucky(5)  

当调用 isLucky(6)时，它返回 1(因为 counter > n)。
如果发现给定程序中有 bug 或其他解决同样问题的方法，请写评论。