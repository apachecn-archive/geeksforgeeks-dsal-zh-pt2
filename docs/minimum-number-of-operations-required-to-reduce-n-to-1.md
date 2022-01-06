# 将 N 减少到 1 所需的最小操作次数

> 原文:[https://www . geesforgeks . org/最小操作数-需要将 n 减少到 1/](https://www.geeksforgeeks.org/minimum-number-of-operations-required-to-reduce-n-to-1/)

给定一个整数元素“N”，任务是找到使“N”等于 1 所需执行的最小操作数。
允许执行的操作有:

1.  N 减 1。
2.  将 N 增加 1。
3.  如果 N 是 3 的倍数，你可以用 3 除 N。

**示例:**

> **输入:** N = 4
> **输出:**2
> 4–1 = 3
> 3/3 = 1
> 所需的最小操作次数为 2。
> 
> **输入:** N = 8
> **输出:**3
> 8+1 = 9
> 9/3 = 3
> 3/3 = 1
> 所需的最小操作次数为 3。

**进场:**

*   如果这个数是 3 的倍数，就除以 3。
*   如果数模 3 是 1，则减 1。
*   如果模 3 的数字是 2，则增加 1。
*   当数字等于 2 时有一个例外，在这种情况下，数字应该减 1。
*   重复以上步骤，直到数字大于 1，并打印最后执行的操作计数。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include<bits/stdc++.h>
using namespace std;

// Function that returns the minimum
// number of operations to be performed
// to reduce the number to 1
int count_minimum_operations(long long n)
{

    // To stores the total number of
    // operations to be performed
    int count = 0;
    while (n > 1) {

        // if n is divisible by 3
        // then reduce it to n / 3
        if (n % 3 == 0)
            n /= 3;

        // if n modulo 3 is 1
        // decrement it by 1
        else if (n % 3 == 1)
            n--;
        else {
            if (n == 2)
                n--;

            // if n modulo 3 is 2
            // then increment it by 1
            else
                n++;
        }

        // update the counter
        count++;
    }
    return count;
}

// Driver code
int main()
{

    long long n = 4;
    long long ans = count_minimum_operations(n);
    cout<<ans<<endl;
    return 0;
}

// This code is contributed by mits
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

class GFG {

    // Function that returns the minimum
    // number of operations to be performed
    // to reduce the number to 1
    static int count_minimum_operations(long n)
    {

        // To stores the total number of
        // operations to be performed
        int count = 0;
        while (n > 1) {

            // if n is divisible by 3
            // then reduce it to n / 3
            if (n % 3 == 0)
                n /= 3;

            // if n modulo 3 is 1
            // decrement it by 1
            else if (n % 3 == 1)
                n--;
            else {
                if (n == 2)
                    n--;

                // if n modulo 3 is 2
                // then increment it by 1
                else
                    n++;
            }

            // update the counter
            count++;
        }
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {

        long n = 4;
        long ans = count_minimum_operations(n);
        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function that returns the minimum
# number of operations to be performed
# to reduce the number to 1
def count_minimum_operations(n):

    # To stores the total number of
    # operations to be performed
    count = 0
    while (n > 1) :

        # if n is divisible by 3
        # then reduce it to n / 3
        if (n % 3 == 0):
            n //= 3

        # if n modulo 3 is 1
        # decrement it by 1
        elif (n % 3 == 1):
            n -= 1
        else :
            if (n == 2):
                n -= 1

            # if n modulo 3 is 2
            # then increment it by 1
            else:
                n += 1

        # update the counter
        count += 1

    return count

# Driver code
if __name__ =="__main__":
    n = 4
    ans = count_minimum_operations(n)
    print (ans)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of above approach
using System;

public class GFG{

        // Function that returns the minimum
    // number of operations to be performed
    // to reduce the number to 1
    static int count_minimum_operations(long n)
    {

        // To stores the total number of
        // operations to be performed
        int count = 0;
        while (n > 1) {

            // if n is divisible by 3
            // then reduce it to n / 3
            if (n % 3 == 0)
                n /= 3;

            // if n modulo 3 is 1
            // decrement it by 1
            else if (n % 3 == 1)
                n--;
            else {
                if (n == 2)
                    n--;

                // if n modulo 3 is 2
                // then increment it by 1
                else
                    n++;
            }

            // update the counter
            count++;
        }
        return count;
    }

    // Driver code
    static public void Main (){

        long n = 4;
        long ans = count_minimum_operations(n);
        Console.WriteLine(ans);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function that returns the minimum
// number of operations to be performed
// to reduce the number to 1
function count_minimum_operations($n)
{

    // To stores the total number of
    // operations to be performed
    $count = 0;
    while ($n > 1)
    {

        // if n is divisible by 3
        // then reduce it to n / 3
        if ($n % 3 == 0)
            $n /= 3;

        // if n modulo 3 is 1
        // decrement it by 1
        else if ($n % 3 == 1)
            $n--;
        else
        {
            if ($n == 2)
                $n--;

            // if n modulo 3 is 2
            // then increment it by 1
            else
                $n++;
        }

        // update the counter
        $count++;
    }
    return $count;
}

// Driver code
$n = 4;

$ans = count_minimum_operations($n);
echo $ans, "\n";

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>

    // Javascript implementation of above approach

    // Function that returns the minimum
    // number of operations to be performed
    // to reduce the number to 1
    function count_minimum_operations(n)
    {

        // To stores the total number of
        // operations to be performed
        let count = 0;
        while (n > 1) {

            // if n is divisible by 3
            // then reduce it to n / 3
            if (n % 3 == 0)
                n /= 3;

            // if n modulo 3 is 1
            // decrement it by 1
            else if (n % 3 == 1)
                n--;
            else {
                if (n == 2)
                    n--;

                // if n modulo 3 is 2
                // then increment it by 1
                else
                    n++;
            }

            // update the counter
            count++;
        }
        return count;
    }

    let n = 4;
    let ans = count_minimum_operations(n);
    document.write(ans);

</script>
```

**Output**

```
2
```

**递归方法:**递归方法类似于上面使用的方法。

下面是实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns the minimum
// number of operations to be performed
// to reduce the number to 1
int count_minimum_operations(long long n)
{

    // Base cases
    if (n == 2) {
        return 1;
    }
    else if (n == 1) {
        return 0;
    }
    if (n % 3 == 0) {
        return 1 + count_minimum_operations(n / 3);
    }
    else if (n % 3 == 1) {
        return 1 + count_minimum_operations(n - 1);
    }
    else {
        return 1 + count_minimum_operations(n + 1);
    }
}

// Driver code
int main()
{

    long long n = 4;
    long long ans = count_minimum_operations(n);
    cout << ans << endl;
    return 0;
}

// This code is contributed by koulick_sadhu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class GFG{

// Function that returns the minimum
// number of operations to be performed
// to reduce the number to 1
public static int count_minimum_operations(int n)
{

    // Base cases
    if (n == 2)
    {
        return 1;
    }
    else if (n == 1)
    {
        return 0;
    }
    if (n % 3 == 0)
    {
        return 1 + count_minimum_operations(n / 3);
    }
    else if (n % 3 == 1)
    {
        return 1 + count_minimum_operations(n - 1);
    }
    else
    {
        return 1 + count_minimum_operations(n + 1);
    }
}

// Driver code
public static void main(String []args)
{
    int n = 4;
    int ans = count_minimum_operations(n);

    System.out.println(ans);
}
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function that returns the minimum
# number of operations to be performed
# to reduce the number to 1
def count_minimum_operations(n):

    # Base cases
    if (n == 2):
        return 1
    elif (n == 1):
        return 0
    if (n % 3 == 0):
        return 1 + count_minimum_operations(n / 3)
    elif (n % 3 == 1):
        return 1 + count_minimum_operations(n - 1)
    else:
        return 1 + count_minimum_operations(n + 1)

# Driver Code
n = 4
ans = count_minimum_operations(n)

print(ans)

# This code is contributed by divyesh072019
```

## C#

```
// C# implementation of above approach
using System;
class GFG {

    // Function that returns the minimum
    // number of operations to be performed
    // to reduce the number to 1
    static int count_minimum_operations(int n)
    {

        // Base cases
        if (n == 2) {
            return 1;
        }
        else if (n == 1) {
            return 0;
        }
        if (n % 3 == 0) {
            return 1 + count_minimum_operations(n / 3);
        }
        else if (n % 3 == 1) {
            return 1 + count_minimum_operations(n - 1);
        }
        else {
            return 1 + count_minimum_operations(n + 1);
        }
    }

  // Driver code
  static void Main() {
    int n = 4;
    int ans = count_minimum_operations(n);
    Console.WriteLine(ans);
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    // Function that returns the minimum
    // number of operations to be performed
    // to reduce the number to 1
    function count_minimum_operations(n)
    {

        // Base cases
        if (n == 2) {
            return 1;
        }
        else if (n == 1) {
            return 0;
        }
        if (n % 3 == 0) {
            return 1 + count_minimum_operations(n / 3);
        }
        else if (n % 3 == 1) {
            return 1 + count_minimum_operations(n - 1);
        }
        else {
            return 1 + count_minimum_operations(n + 1);
        }
    }

    let n = 4;
    let ans = count_minimum_operations(n);
    document.write(ans);

    // This code is contributed by suresh07.
</script>
```

**Output**

```
2
```

**另一种方法** ***(高效)*** **:**

**采用记忆化的差压(自上而下的方法)**

通过存储到目前为止计算出的操作，我们可以避免重复的工作。我们只需要将所有的值存储在一个数组中。

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

int static dp[1001];

// Function that returns the minimum
// number of operations to be performed
// to reduce the number to 1
int count_minimum_operations(long long n)
{
    // Base cases
    if (n == 2) {
        return 1;
    }
    if (n == 1) {
        return 0;
    }
    if(dp[n] != -1)
    {
        return dp[n];
    }
    if (n % 3 == 0) {
        dp[n] = 1 + count_minimum_operations(n / 3);
    }
    else if (n % 3 == 1) {
        dp[n] = 1 + count_minimum_operations(n - 1);
    }
    else {
        dp[n] = 1 + count_minimum_operations(n + 1);
    }
    return dp[n];
}

// Driver code
int main()
{
    long long n = 4;
      memset(dp, -1, sizeof(dp));
    long long ans = count_minimum_operations(n);
    cout << ans << endl;
    return 0;
}

// This code is contributed by Samim Hossain Mondal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
public class GFG
{

static int []dp = new int[1001];

// Function that returns the minimum
// number of operations to be performed
// to reduce the number to 1
public static int count_minimum_operations(int n)
{

    // Base cases
    if (n == 2)
    {
        return 1;
    }
    else if (n == 1)
    {
        return 0;
    }
    if(dp[n] != -1)
    {
        return dp[n];
    }
    if (n % 3 == 0) {
        dp[n] = 1 + count_minimum_operations(n / 3);
    }
    else if (n % 3 == 1) {
        dp[n] = 1 + count_minimum_operations(n - 1);
    }
    else {
        dp[n] = 1 + count_minimum_operations(n + 1);
    }
    return dp[n];
}

// Driver code
public static void main(String []args)
{
    int n = 4;

    for(int i = 0; i < 1001; i++) {
        dp[i] = -1;
    }

    int ans = count_minimum_operations(n);
    System.out.println(ans);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 计算机编程语言

```
# Python3 implementation of above approach

# Function that returns the minimum
# number of operations to be performed
# to reduce the number to 1
dp = [-1 for i in range(1001)]

def count_minimum_operations(n):

    # Base cases
    if (n == 2):
        return 1
    elif (n == 1):
        return 0
    if(dp[n] != -1):
        return dp[n]

    elif (n % 3 == 0):
        dp[n] = 1 + count_minimum_operations(n / 3)

    elif (n % 3 == 1):
        dp[n] = 1 + count_minimum_operations(n - 1)

    else:
        dp[n] = 1 + count_minimum_operations(n + 1)

    return dp[n]

# Driver Code
n = 4
ans = count_minimum_operations(n)

print(ans)

# This code is contributed by Samim Hossain Mondal
```

## C#

```
// C# implementation of above approach
using System;
class GFG
{

  static int []dp = new int[1001];

  // Function that returns the minimum
  // number of operations to be performed
  // to reduce the number to 1
  public static int count_minimum_operations(int n)
  {

    // Base cases
    if (n == 2)
    {
      return 1;
    }
    else if (n == 1)
    {
      return 0;
    }
    if(dp[n] != -1)
    {
      return dp[n];
    }
    if (n % 3 == 0) {
      dp[n] = 1 + count_minimum_operations(n / 3);
    }
    else if (n % 3 == 1) {
      dp[n] = 1 + count_minimum_operations(n - 1);
    }
    else {
      dp[n] = 1 + count_minimum_operations(n + 1);
    }
    return dp[n];
  }

  // Driver code
  public static void Main()
  {
    int n = 4;

    for(int i = 0; i < 1001; i++) {
      dp[i] = -1;
    }

    int ans = count_minimum_operations(n);
    Console.Write(ans);
  }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

let dp = [];

// Function that returns the minimum
// number of operations to be performed
// to reduce the number to 1
function count_minimum_operations(n)
{
    // Base cases
    if (n == 2) {
        return 1;
    }
    if (n == 1) {
        return 0;
    }
    if(dp[n] != -1)
    {
        return dp[n];
    }
    if (n % 3 == 0) {
        dp[n] = 1 + count_minimum_operations(n / 3);
    }
    else if (n % 3 == 1) {
        dp[n] = 1 + count_minimum_operations(n - 1);
    }
    else {
        dp[n] = 1 + count_minimum_operations(n + 1);
    }
    return dp[n];
}

// Driver Code
// Input Nth term
let n = 4;

for(let i = 0; i < 1001; i++) {
    dp[i] = -1;
}

let ans = count_minimum_operations(n);
document.write(ans);

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
2
```

**时间复杂度:** O(n)

**辅助空间:** O(n)