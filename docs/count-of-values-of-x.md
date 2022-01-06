# x<值的计数= n，其中(n 异或 x)=(n–x)

> 原文:[https://www.geeksforgeeks.org/count-of-values-of-x/](https://www.geeksforgeeks.org/count-of-values-of-x/)

给定一个整数 **n** ，任务是找出满足**n XOR x = n–x**的 **0 ≤ x ≤ n** 的可能值的个数。

**示例:**

> **输入:** n = 5
> **输出:** 4
> 下列 x 值满足等式
> 5 异或 0 = 5–0 = 5
> 5 异或 1 = 5–1 = 4
> 5 异或 4 = 5–4 = 1
> 5 异或 5 = 5–5 = 0
> 
> **输入:**n = 2
> T3】输出: 2

**天真方法:**简单的方法是检查从 0 到 n(包括 0 和 n)的所有值，并找出它们是否满足等式。下面的代码实现了这种方法:

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the count of
// valid values of x
static int countX(int n)
{
    int count = 0;

    for (int i = 0; i <= n; i++)
    {

        // If n - x = n XOR x
        if (n - i == (n ^ i))
                count++;
    }

        // Return the required count;
        return count;
}

// Driver code
int main()
{
    int n = 5;
    int answer = countX(n);
    cout << answer;
}

// This code is contributed by
// Shivi_Aggarwal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Function to return the count of
    // valid values of x
    static int countX(int n)
    {
        int count = 0;

        for (int i = 0; i <= n; i++) {

            // If n - x = n XOR x
            if (n - i == (n ^ i))
                count++;
        }

        // Return the required count;
        return count;
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 5;
        int answer = countX(n);
        System.out.println(answer);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math as mt

# Function to return the count of
# valid values of x
def countX(n):
    count = 0

    for i in range(n + 1):

        if n - i == (n ^ i):
            count += 1

    return count

# Driver Code
if __name__ == '__main__':
    n = 5
    answer = countX(n)
    print(answer)

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the count of
    // valid values of x
    static int countX(int n)
    {
        int count = 0;

        for (int i = 0; i <= n; i++)
        {

            // If n - x = n XOR x
            if (n - i == (n ^ i))
                count++;
        }

        // Return the required count;
        return count;
    }

    // Driver code
    public static void Main()
    {
        int n = 5;
        int answer = countX(n);
        Console.WriteLine(answer);
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of
// valid values of x
function countX($n)
{
    $count = 0;

    for ($i = 0; $i <= $n; $i++)
    {

        // If n - x = n XOR x
        if ($n - $i == ($n ^ $i))
            $count++;
    }

    // Return the required count;
    return $count;
}

// Driver code
$n = 5;
$answer = countX($n);
echo($answer);

// This code is Contributed
// by Mukul Singh.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of
// valid values of x
function countX(n)
{
    let count = 0;

    for (let i = 0; i <= n; i++)
    {

        // If n - x = n XOR x
        if (n - i == (n ^ i))
                count++;
    }

        // Return the required count;
        return count;
}

// Driver code
    let n = 5;
    let answer = countX(n);
    document.write(answer);

</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N)

**有效方法:**将 **n** 转换为其二进制表示。现在，对于二进制串中的每一个 **1** ，无论我们从中减去 **1** 还是 **0** ，都相当于 1 与 0 或 1 的异或，即
**(1–1)=(1 XOR 1)= 0**
**(1–0)=(1 XOR 0)= 1**
，但 **0** 并不满足这个条件。所以，我们只需要考虑 **n** 二进制表示中的所有 1。现在，对于每一个 **1** 都有两种可能，**不是 0 就是 1** 。因此，如果我们在 **n** 中有 **m 个 1 的**，那么我们的解决方案将是 **2 <sup>m</sup>** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the count of
// valid values of x
int countX(int n)
{
    // Convert n into binary String
    string binary = bitset<8>(n).to_string();

    // To store the count of 1s
    int count = 0;
    for (int i = 0; i < binary.length(); i++)
    {
        // If current bit is 1
        if (binary.at(i) == '1')
            count++;
    }

    // Calculating answer
    int answer = (int)pow(2, count);
    return answer;
}

// Driver code
int main()
{
    int n = 5;
    int answer = countX(n);
    cout << (answer);
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Function to return the count of
    // valid values of x
    static int countX(int n)
    {
        // Convert n into binary String
        String binary = Integer.toBinaryString(n);

        // To store the count of 1s
        int count = 0;

        for (int i = 0; i < binary.length(); i++) {

            // If current bit is 1
            if (binary.charAt(i) == '1')
                count++;
        }

        // Calculating answer
        int answer = (int)Math.pow(2, count);
        return answer;
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 5;
        int answer = countX(n);
        System.out.println(answer);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# valid values of x
def countX(n):

    # Convert n into binary String
    binary = "{0:b}".format(n)

    # To store the count of 1s
    count = 0

    for i in range(len(binary)):

        # If current bit is 1
        if (binary[i] == '1'):
            count += 1

    # Calculating answer
    answer = int(pow(2, count))
    return answer

# Driver code
if __name__ == "__main__":

    n = 5
    answer = countX(n)
    print(answer)

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of
// valid values of x
static int countX(int n)
{
    // Convert n into binary String
    string binary = Convert.ToString(n, 2);

    // To store the count of 1s
    int count = 0;

    for (int i = 0; i < binary.Length; i++)
    {

        // If current bit is 1
        if (binary[i] == '1')
            count++;
    }

    // Calculating answer
    int answer = (int)Math.Pow(2, count);
    return answer;
}

// Driver code
public static void Main()
{
    int n = 5;
    int answer = countX(n);
    Console.WriteLine(answer);
}
}

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of
// valid values of x
function countX(n)
{

    // Convert n into binary String
    let binary = (n >>> 0).toString(2);

    // To store the count of 1s
    let count = 0;

    for(let i = 0; i < binary.length; i++)
    {

        // If current bit is 1
        if (binary[i] == '1')
            count++;
    }

    // Calculating answer
    let answer = Math.floor(Math.pow(2, count));
    return answer;
}

// Driver code
let n = 5;
let answer = countX(n);

document.write(answer);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
4
```

**时间复杂度:** ![$O(\log{}n)$      ](img/1dd1ee1288aebc278040e4bbaaa0981a.png "Rendered by QuickLaTeX.com")