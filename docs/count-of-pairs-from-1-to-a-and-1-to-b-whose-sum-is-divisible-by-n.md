# 从 1 到 a 和 1 到 b 的配对数，其和可被 N 整除

> 原文:[https://www . geesforgeks . org/从 1 到 a 和从 1 到 b 的配对计数，其总和可被 n 整除/](https://www.geeksforgeeks.org/count-of-pairs-from-1-to-a-and-1-to-b-whose-sum-is-divisible-by-n/)

给定三个整数 **a** 、 **b** 和 **N** 。求从 **1 到 a** 中选择一个整数，从 **1 到 b** 中选择另一个整数可以形成的不同对的总数，这样它们的和可以被 n 整除

**示例:**

```
Input : a = 4, b = 4, N = 4
Output : 4

Input : a = 5, b = 13, N = 3
Output : 22
```

**基本方法:**对于一个可以被 **N** 整除的对，它必须包含一个范围从 1 到 a 的数和一个范围从 1 到 b 的数。
因此，对于这个从 1 到 a 的整数的迭代，对于每个整数(I)，b/N 个数都存在，它们与 I 的和可以被 N 整除。此外，如果(i%N + b%N) > = N，那么还存在 1 个其和可以被 N 整除的对

例如取 a = 7，b = 6 和 N = 4:

```
Let's check for i = 3:
```

*   b/N = 6/4 = 1 = >有一个从 1 到 b 的整数，
    与 3 的和可被 4 整除，即(3，1)。
*   同样，i%N + b%N = 3%4 + 6%4 = 3+2 = 5 > 4，
    表示从 1 到 b 还有一个整数
    ，其与 3 的和可被 4 整除(即 3，5)。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the distinct pairs from
// 1-a & 1-b such that their sum is divisible by n.
int findCountOfPairs(int a, int b, int n)
{
    int ans = 0;

    // Iterate over 1 to a to find distinct pairs
    for (int i = 1; i <= a; i++) {
        // For each integer from 1 to a
        // b/n integers exists such that pair
        // sum is divisible by n
        ans += b / n;

        // If (i%n +b%n ) >= n one more pair is possible
        ans += (i % n + b % n) >= n ? 1 : 0;
    }

    // Return answer
    return ans;
}

// Driver code
int main()
{
    int a = 5, b = 13, n = 3;
    cout << findCountOfPairs(a, b, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

// Function to find the distinct pairs from
// 1-a & 1-b such that their sum is divisible by n.
static int findCountOfPairs(int a, int b, int n)
{
    int ans = 0;

    // Iterate over 1 to a to find distinct pairs
    for (int i = 1; i <= a; i++)
    {
        // For each integer from 1 to a
        // b/n integers exists such that pair
        // sum is divisible by n
        ans += b / n;

        // If (i%n +b%n ) >= n one more pair is possible
        ans += (i % n + b % n) >= n ? 1 : 0;
    }

    // Return answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int a = 5, b = 13, n = 3;
    System.out.println(findCountOfPairs(a, b, n));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation of above approach

# Function to find the distinct pairs from
# 1-a & 1-b such that their sum is divisible by n.
def findCountOfPairs(a, b, n):
    ans = 0
    for i in range(1, a + 1):

        # For each integer from 1 to a
        # b/n integers exists such that pair
        # / sum is divisible by n
        ans += b//n

        # If (i%n +b%n ) >= n one more pair is possible
        ans += 1 if (i % n + b % n) >= n else 0

    return ans

# Driver code
a = 5; b = 13; n = 3
print(findCountOfPairs(a, b, n))

# This code is contributed by Shrikant13
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

// Function to find the distinct pairs from
// 1-a & 1-b such that their sum is divisible by n.
static int findCountOfPairs(int a, int b, int n)
{
    int ans = 0;

    // Iterate over 1 to a to find distinct pairs
    for (int i = 1; i <= a; i++)
    {
        // For each integer from 1 to a
        // b/n integers exists such that pair
        // sum is divisible by n
        ans += b / n;

        // If (i%n +b%n ) >= n one more pair is possible
        ans += (i % n + b % n) >= n ? 1 : 0;
    }

    // Return answer
    return ans;
}

// Driver code
static public void Main ()
{
    int a = 5, b = 13, n = 3;
    Console.WriteLine(findCountOfPairs(a, b, n));
}
}

// This code has been contributed by ajit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to find the distinct pairs from
// 1-a & 1-b such that their sum is divisible by n.
function findCountOfPairs($a, $b, $n)
{
    $ans = 0;

    // Iterate over 1 to a to find
    // distinct pairs
    for ($i = 1; $i <= $a; $i++)
    {

        // For each integer from 1 to a
        // b/n integers exists such that pair
        // sum is divisible by n
        $ans += (int)($b / $n);

        // If (i%n +b%n ) >= n one more
        // pair is possible
        $ans += (($i % $n ) +
                 ($b % $n)) >= $n ? 1 : 0;
    }

    // Return answer
    return $ans;
}

// Driver code
$a = 5;
$b = 13;
$n = 3;
echo findCountOfPairs($a, $b, $n);

// This code is contributed by akt_mit.
?>
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Function to find the distinct pairs from
    // 1-a & 1-b such that their sum is divisible by n.
    function findCountOfPairs(a, b, n)
    {
        let ans = 0;

        // Iterate over 1 to a to find distinct pairs
        for (let i = 1; i <= a; i++)
        {

            // For each integer from 1 to a
            // b/n integers exists such that pair
            // sum is divisible by n
            ans += parseInt(b / n, 10);

            // If (i%n +b%n ) >= n one more pair is possible
            ans += (i % n + b % n) >= n ? 1 : 0;
        }

        // Return answer
        return ans;
    }

    let a = 5, b = 13, n = 3;
    document.write(findCountOfPairs(a, b, n));

    // This code is contributed by mukesh07.

</script>
```

**Output:** 

```
22
```

**时间复杂度** : O(N)

**第二种方法:-** 这种方法有点棘手。这里我们找到 n 的倍数是多少对

**先:-** 守(甲<乙)，若不守则使用互换。

**秒:-** 从 N 的最低倍数开始一个 for 循环，并遍历该倍数。

*   现在最小元素(a)大于或等于当前倍数，然后我们将((Current _ Multiple)–1)对添加到 ans。
*   现在 a 变小了，但是 b 大于或等于我们给 ans 加上 a 的当前倍数。
*   现在，如果 a 和 b 都小于，我们计算剩下的一对，加 a –( current _ multiple–b)+1。
*   打破循环。

下面是上述逻辑的实现。

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the distinct pairs from
// 1-a & 1-b such that their sum is divisible by n.
int findCountOfPairs(int a, int b, int n)
{
    if (a > b)
    {
        // if first element is bigger then swap
        swap(a, b);
    }
    int temp = 1, count = 0;
    // count is store the number of pair.
    for (int i = n; temp > 0; i += n)
    {
        // we use temp for breaking a loop.
        if (a >= i)
        {
            // count when a is greater.
            temp = i - 1;
        }
        else if (b >= i)
        {
            // Count when a is smaller but
            // b is greater
            temp = a;
        }
        else if (i > b)
        {
            // Count when a and b both are smaller
            temp = a - (i - b) + 1;
        }
        if (temp > 0) //breaking condition
        {
            // For storing The pair in count.
            count += temp;
        }
    }
    // return the number of pairs.
    return count;
}

// Driver code
int main()
{
    int a = 5, b = 13, n = 3;
    cout << findCountOfPairs(a, b, n);

    return 0;
}
// contribute by Vivek Javiya
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
class GFG{

// Function to find the
// distinct pairs from
// 1-a & 1-b such that
// their sum is divisible by n.
public static int findCountOfPairs(int a,
                                   int b,
                                   int n)
{
  if (a > b)
  {
    // if first element is
    // bigger then swap
    int temp = a;
    a = b;
    b = temp;
  }

  int temp = 1, count = 0;

  // count is store the
  // number of pair.
  for (int i = n; temp > 0; i += n)
  {
    // we use temp for
    // breaking a loop.
    if (a >= i)
    {
      // count when a
      // is greater.
      temp = i - 1;
    }
    else if (b >= i)
    {
      // Count when a is
      // smaller but
      // b is greater
      temp = a;
    }
    else if (i > b)
    {
      // Count when a and b
      // both are smaller
      temp = a - (i - b) + 1;
    }

    //breaking condition
    if (temp > 0)
    {
      // For storing The
      // pair in count.
      count += temp;
    }
  }

  // return the number
  // of pairs.
  return count;
}

// Driver code
public static void main(String[] args)
{
  int a = 5, b = 13, n = 3;
  System.out.print(findCountOfPairs(a,
                                    b, n));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python implementation of above approach

# Function to find the distinct pairs from
# 1-a & 1-b such that their sum is divisible by n.
def findCountOfPairs(a, b, n):
    if(a > b):

        # if first element is bigger then swap
        a, b = b, a

    temp = 1
    count = 0

    # count is store the number of pair.
    i = n
    while(temp > 0):

        # we use temp for breaking a loop.
        if(a >= i):

            # count when a is greater.
            temp = i - 1
        elif(b >= i):

            # Count when a is smaller but
            # b is greater
            temp = a
        elif(i > b):

            # Count when a and b both are smaller
            temp = a - (i - b) + 1

        if(temp > 0):

          # breaking condition
            # For storing The pair in count.
            count += temp
        i += n

    # return the number of pairs.
    return count

# Driver code
a = 5
b = 13
n = 3

print(findCountOfPairs(a, b, n))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# implementation of
// the above approach
using System;

class GFG
{

    // Function to find the
    // distinct pairs from
    // 1-a & 1-b such that
    // their sum is divisible by n.
    static int findCountOfPairs(int a, int b, int n)
    {
      if (a > b)
      {

        // if first element is
        // bigger then swap
        int temp1 = a;
        a = b;
        b = temp1;
      }

      int temp = 1, count = 0;

      // count is store the
      // number of pair.
      for (int i = n; temp > 0; i += n)
      {

        // we use temp for
        // breaking a loop.
        if (a >= i)
        {

          // count when a
          // is greater.
          temp = i - 1;
        }
        else if (b >= i)
        {

          // Count when a is
          // smaller but
          // b is greater
          temp = a;
        }
        else if (i > b)
        {

          // Count when a and b
          // both are smaller
          temp = a - (i - b) + 1;
        }

        // breaking condition
        if (temp > 0)
        {

          // For storing The
          // pair in count.
          count += temp;
        }
      }

      // return the number
      // of pairs.
      return count;
    }

  // Driver code
  static void Main()
  {
      int a = 5, b = 13, n = 3;
      Console.WriteLine(findCountOfPairs(a, b, n));
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

    // Javascript implementation of
    // the above approach

    // Function to find the
    // distinct pairs from
    // 1-a & 1-b such that
    // their sum is divisible by n.
    function findCountOfPairs(a, b, n)
    {
      if (a > b)
      {

        // if first element is
        // bigger then swap
        let temp1 = a;
        a = b;
        b = temp1;
      }

      let temp = 1, count = 0;

      // count is store the
      // number of pair.
      for (let i = n; temp > 0; i += n)
      {

        // we use temp for
        // breaking a loop.
        if (a >= i)
        {

          // count when a
          // is greater.
          temp = i - 1;
        }
        else if (b >= i)
        {

          // Count when a is
          // smaller but
          // b is greater
          temp = a;
        }
        else if (i > b)
        {

          // Count when a and b
          // both are smaller
          temp = a - (i - b) + 1;
        }

        // breaking condition
        if (temp > 0)
        {

          // For storing The
          // pair in count.
          count += temp;
        }
      }

      // return the number
      // of pairs.
      return count;
    }

    let a = 5, b = 13, n = 3;
      document.write(findCountOfPairs(a, b, n));

</script>
```

**输出:**

```
22
```

**高效方法:**为了高效地解决问题，将问题分解为四部分，求解如下:

*   从 1 到 N*(a/N)范围内的每个整数将正好具有从 1 到 N*(b/N)的 b/N 个整数，其和可被 N 整除
*   存在范围从 1 到 N*(a/N)的 a/N 个整数，它们可以与范围从 N*(b/N)到 b 的 b%N 个整数形成对
*   存在从 N*(a/N)到 a 的%N 个整数，它们可以与从 1 到 N*(b/N)的 b/N 个整数形成对。
*   存在从 N*(a/N)到 a 和从 N*(b/N)到 b 的(a%N + b%N)/N 个整数，它们可以形成和可被 N 整除的对

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the distinct pairs from
// 1-a & 1-b such that their sum is divisible by n.
int findCountOfPairs(int a, int b, int n)
{
    int ans = 0;

    // pairs from 1 to n*(a/n) and 1 to n*(b/n)
    ans += n * (a / n) * (b / n);

    // pairs from 1 to n*(a/n) and n*(b/n) to b
    ans += (a / n) * (b % n);

    // pairs from n*(a/n) to a and 1 to n*(b/n)
    ans += (a % n) * (b / n);

    // pairs from n*(a/n) to a and  n*(b/n) to b
    ans += ((a % n) + (b % n)) / n;

    // Return answer
    return ans;
}

// Driver code
int main()
{
    int a = 5, b = 13, n = 3;
    cout << findCountOfPairs(a, b, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.io.*;

class GFG
{

// Function to find the distinct pairs from
// 1-a & 1-b such that their sum is divisible by n.
static int findCountOfPairs(int a, int b, int n)
{
    int ans = 0;

    // pairs from 1 to n*(a/n) and 1 to n*(b/n)
    ans += n * (a / n) * (b / n);

    // pairs from 1 to n*(a/n) and n*(b/n) to b
    ans += (a / n) * (b % n);

    // pairs from n*(a/n) to a and 1 to n*(b/n)
    ans += (a % n) * (b / n);

    // pairs from n*(a/n) to a and n*(b/n) to b
    ans += ((a % n) + (b % n)) / n;

    // Return answer
    return ans;
}

// Driver code
public static void main (String[] args)
{
    int a = 5, b = 13, n = 3;
    System.out.println (findCountOfPairs(a, b, n));
}
}

// This code is contributed by ajit..
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function to find the distinct pairs from
# 1-a & 1-b such that their sum is divisible by n.
def findCountOfPairs(a, b, n):
    ans = 0

    # pairs from 1 to n*(a/n) and 1 to n*(b/n)
    ans += n * int(a / n) * int(b / n)

    # pairs from 1 to n*(a/n) and n*(b/n) to b
    ans += int(a / n) * (b % n)

    # pairs from n*(a/n) to a and 1 to n*(b/n)
    ans += (a % n) * int(b / n)

    # pairs from n*(a/n) to a and n*(b/n) to b
    ans += int(((a % n) + (b % n)) / n);

    # Return answer
    return ans

# Driver code
if __name__ == '__main__':
    a = 5
    b = 13
    n = 3
    print(findCountOfPairs(a, b, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to find the distinct pairs from
// 1-a & 1-b such that their sum is divisible by n.

static int findCountOfPairs(int a, int b, int n)
{
    int ans = 0;

    // pairs from 1 to n*(a/n) and 1 to n*(b/n)
    ans += n * (a / n) * (b / n);

    // pairs from 1 to n*(a/n) and n*(b/n) to b
    ans += (a / n) * (b % n);

    // pairs from n*(a/n) to a and 1 to n*(b/n)
    ans += (a % n) * (b / n);

    // pairs from n*(a/n) to a and n*(b/n) to b
    ans += ((a % n) + (b % n)) / n;

    // Return answer
    return ans;
}

// Driver code
    static public void Main (){
    int a = 5, b = 13, n = 3;
    Console.WriteLine(findCountOfPairs(a, b, n));
}
}

// This code is contributed by @Tushil
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to find the distinct pairs from
// 1-a & 1-b such that their sum is divisible by n.
function findCountOfPairs($a, $b, $n)
{
    $ans = 0;

    // pairs from 1 to n*(a/n) and 1 to n*(b/n)
    $ans += $n * (int)($a / $n) * (int)($b / $n);

    // pairs from 1 to n*(a/n) and n*(b/n) to b
    $ans += (int)($a / $n) * ($b % $n);

    // pairs from n*(a/n) to a and 1 to n*(b/n)
    $ans += ($a % $n) * (int)($b / $n);

    // pairs from n*(a/n) to a and n*(b/n) to b
    $ans += (($a % $n) + (int)($b % $n)) / $n;

    // Return answer
    return $ans;
}

// Driver code
$a = 5;
$b = 13;
$n = 3;
echo findCountOfPairs($a, $b, $n);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    // Function to find the distinct pairs from
    // 1-a & 1-b such that their sum is divisible by n.
    function findCountOfPairs(a, b, n)
    {
        let ans = 0;

        // pairs from 1 to n*(a/n) and 1 to n*(b/n)
        ans += n * parseInt(a / n, 10) * parseInt(b / n, 10)

        // pairs from 1 to n*(a/n) and n*(b/n) to b
        ans += parseInt(a / n, 10) * parseInt(b % n, 10);

        // pairs from n*(a/n) to a and 1 to n*(b/n)
        ans += parseInt(a % n, 10) * parseInt(b / n, 10);

        // pairs from n*(a/n) to a and  n*(b/n) to b
        ans += parseInt(((a % n) + (b % n)) / n, 10);

        // Return answer
        return ans;
    }

    let a = 5, b = 13, n = 3;
    document.write(findCountOfPairs(a, b, n));

</script>
```

**Output:** 

```
22
```

**时间复杂度:** O(1)