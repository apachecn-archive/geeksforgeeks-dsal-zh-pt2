# 用 1/n 的小数值求周期长度

> 原文:[https://www . geesforgeks . org/find-length-period-decimal-value-1n/](https://www.geeksforgeeks.org/find-length-period-decimal-value-1n/)

给定一个正整数 n，求 1/n 的十进制值中的周期。十进制值中的周期是不断重复的位数(小数点后某处)。
**例:**

```
Input:  n = 3
Output: 1
The value of 1/3 is 0.333333...

Input: n = 7
Output: 6
The value of 1/7 is 0.142857142857142857.....

Input: n = 210
Output: 6
The value of 1/210 is 0.0047619047619048.....
```

我们先来讨论一个比较简单的 1/n 值找个别数字的问题
**1/n 值怎么找个别数字？**
让我们举个例子来了解一下这个过程。例如 n = 7。第一个数字可以通过做 10/7 得到。第二个数字可以用 30/7 来表示(3 是上一次除法的余数)。第三个数字可以用 20/7 来表示(2 是上一次除法的余数)。所以想法是得到第一个数字，然后继续取值(余数* 10)/n 作为下一个数字，并继续更新余数为(余数* 10) % 10。完整的程序在这里[讨论](http://geeksquiz.com/print-first-k-digits-1n-n-positive-integer/)。
**如何找到期间？**
1/n 的周期等于上述过程中使用的余数序列中的周期。这很容易从数字直接来源于余数这一事实中得到证明。
关于余数序列的一个有趣的事实是，在这个余数序列的周期中，所有的模式都是不同的。原因很简单，如果余数重复，那就是新周期的开始。
以下是上述思路的实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find length of period of 1/n
#include <iostream>
#include <map>
using namespace std;

// Function to find length of period in 1/n
int getPeriod(int n)
{
   // Create a map to store mapping from remainder
   // its position
   map<int, int> mymap;
   map<int, int>::iterator it;

   // Initialize remainder and position of remainder
   int rem = 1, i = 1;

   // Keep finding remainders till a repeating remainder
   // is found
   while (true)
   {
        // Find next remainder
        rem = (10*rem) % n;

        // If remainder exists in mymap, then the difference
        // between current and previous position is length of
        // period
        it = mymap.find(rem);
        if (it != mymap.end())
            return (i - it->second);

        // If doesn't exist, then add 'i' to mymap
        mymap[rem] = i;
        i++;
   }

   // This code should never be reached
   return INT_MAX;
}

// Driver program to test above function
int main()
{
    cout <<  getPeriod(3) << endl;
    cout <<  getPeriod(7) << endl;
    return 0;
}
```

输出:

```
1
6
```

我们可以使用以下事实来避免使用 map 或 hash。对于一个数 n，最多可以有 n 个不同的余数。此外，周期可能不会从第一个余数开始，因为一些初始余数可能是非重复的(不是任何周期的一部分)。因此，为了确保从一个周期中挑选余数，从第(n+1)个余数开始，并继续寻找下一个余数。第(n+1)个余数与其下一个余数之间的距离是周期的长度。

## C++

```
// C++ program to find length of period of 1/n without
// using map or hash
#include <iostream>
using namespace std;

// Function to find length of period in 1/n
int getPeriod(int n)
{
   // Find the (n+1)th remainder after decimal point
   // in value of 1/n
   int rem = 1; // Initialize remainder
   for (int i = 1; i <= n+1; i++)
         rem = (10*rem) % n;

   // Store (n+1)th remainder
   int d = rem;

   // Count the number of remainders before next
   // occurrence of (n+1)'th remainder 'd'
   int count = 0;
   do {
      rem = (10*rem) % n;
      count++;
   } while(rem != d);

   return count;
}

// Driver program to test above function
int main()
{
    cout <<  getPeriod(3) << endl;
    cout <<  getPeriod(7) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length
// of period of 1/n without using
// map or hash

class GFG {

// Function to find length of period in 1/n
static int getPeriod(int n)
{
    // Find the (n+1)th remainder after
    // decimal point in value of 1/n

    int rem = 1; // Initialize remainder
    for (int i = 1; i <= n + 1; i++)
            rem = (10 * rem) % n;

    // Store (n+1)th remainder
    int d = rem;

    // Count the number of remainders before next
    // occurrence of (n+1)'th remainder 'd'
    int count = 0;
    do {
        rem = (10 * rem) % n;
        count++;
    } while(rem != d);

    return count;
}

// Driver code
public static void main(String[] args)
{
    System.out.println(getPeriod(3) );
    System.out.println(getPeriod(7));
}
}

// This code is contributed by Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python3 program to find length of
# period of 1/n without using map or hash

# Function to find length
# of period in 1/n
def getPeriod( n) :

    # Find the (n+1)th remainder after
    # decimal point in value of 1/n
    rem = 1 # Initialize remainder
    for i in range(1, n + 2):
        rem = (10 * rem) % n

    # Store (n+1)th remainder
    d = rem

    # Count the number of remainders
    # before next occurrence of
    # (n+1)'th remainder 'd'
    count = 0
    rem = (10 * rem) % n
    count += 1
    while rem != d :
        rem = (10 * rem) % n
        count += 1

    return count

# Driver Code
if __name__ == "__main__":

    print (getPeriod(3))
    print (getPeriod(7))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find length of
// period of 1/n without using
// map or hash
using System;

class GFG {

// Function to find length of period in 1/n
static int getPeriod(int n)
{
    // Find the (n+1)th remainder after
    // decimal point in value of 1/n

    int rem = 1; // Initialize remainder
    for (int i = 1; i <= n + 1; i++)
            rem = (10 * rem) % n;

    // Store (n+1)th remainder
    int d = rem;

    // Count the number of remainders before next
    // occurrence of (n+1)'th remainder 'd'
    int count = 0;
    do {
        rem = (10 * rem) % n;
        count++;
    } while(rem != d);

    return count;
}

// Driver code
public static void Main()
{
    Console.Write(getPeriod(3) + "\n");
    Console.Write(getPeriod(7));
}
}

// This code is contributed by Smitha Dinesh Semwal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find length
// of period of 1/n without
// using map or hash

// Function to find length
// of period in 1/n
function getPeriod($n)
{
    // Find the (n+1)th remainder
    // after decimal point
    // in value of 1/n

    // Initialize remainder
    $rem = 1;
    for ($i = 1; $i <= $n + 1; $i++)
        $rem = (10 * $rem) % $n;

    // Store (n+1)th
    // remainder
    $d = $rem;

    // Count the number of
    // remainders before next
    // occurrence of (n+1)'th
    // remainder 'd'
    $count = 0;
    do
    {
        $rem = (10 * $rem) % $n;
        $count++;
    } while($rem != $d);

    return $count;
}

    // Driver Code
    echo getPeriod(3), "\n";
    echo getPeriod(7), "\n";

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find length
// of period of 1/n without using
// map or hash

    // Function to find length of period in 1/n
    function getPeriod(n)
    {
        // Find the (n+1)th remainder after
        // decimal point in value of 1/n

        let rem = 1; // Initialize remainder
        for (let i = 1; i <= n + 1; i++)
            rem = (10 * rem) % n;

        // Store (n+1)th remainder
        let d = rem;

        // Count the number of remainders before next
        // occurrence of (n+1)'th remainder 'd'
        let count = 0;
        do {
            rem = (10 * rem) % n;
            count++;
        } while(rem != d);

        return count;
    }

    // Driver code
    document.write(getPeriod(3)+"<br>")
    document.write(getPeriod(7)+"<br>")

    // This code is contributed by rag2127

</script>
```

**输出:**

```
1
6
```

**参考:**
[算法与编程:问题与解决方案](http://www.flipkart.com/algorithms-programming-problems-solutions-english-first/p/itmdwjdzydjcdmmp?pid=9780817638474&affid=sandeepgfg)
本文由**沙钦**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。