# 可被 K 整除的子串数

> 原文:[https://www . geesforgeks . org/可被 k 整除的子字符串计数/](https://www.geeksforgeeks.org/count-of-sub-strings-that-are-divisible-by-k/)

给定一个整数 **K** 和一个数字字符串 **str** (所有字符均来自 **['0 '，' 9']** )。任务是统计**串**中可被 **K** 整除的子串数量。

**示例:**

> **输入:** str = "33445 "，K = 11
> **输出:** 3
> 可被 11 整除的子串为“33”、“44”和“3344”
> 
> **输入:** str = "334455 "，K = 11
> **输出:** 6

**方法:**初始化**计数= 0** 。取**串**的所有子串，检查是否能被 **K** 整除。如果**是**，则更新**计数=计数+ 1** 。最后打印**计数**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of sub-strings
// of str that are divisible by k
int countSubStr(string str, int len, int k)
{
    int count = 0;

    for (int i = 0; i < len; i++)
    {
        int n = 0;

        // Take all sub-strings starting from i
        for (int j = i; j < len; j++)
        {
            n = n * 10 + (str[j] - '0');

            // If current sub-string is divisible by k
            if (n % k == 0)
                count++;
        }
    }

    // Return the required count
    return count;
}

// Driver code
int main()
{
    string str = "33445";
    int len = str.length();
    int k = 11;
    cout << countSubStr(str, len, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

    // Function to return the count of sub-strings
    // of str that are divisible by k
    static int countSubStr(String str, int len, int k)
    {
        int count = 0;

        for (int i = 0; i < len; i++)
        {
            int n = 0;

            // Take all sub-strings starting from i
            for (int j = i; j < len; j++)
            {
                n = n * 10 + (str.charAt(j) - '0');

                // If current sub-string is divisible by k
                if (n % k == 0)
                    count++;
            }
        }

        // Return the required count
        return count;
    }

    // Driver code
    public static void main(String []args)
    {
        String str = "33445";
        int len = str.length();
        int k = 11;
        System.out.println(countSubStr(str, len, k));
    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the count of sub-strings
# of str that are divisible by k
def countSubStr(str, l, k):
    count = 0

    for i in range(l):
        n = 0

        # Take all sub-strings starting from i
        for j in range(i, l, 1):
            n = n * 10 + (ord(str[j]) - ord('0'))

            # If current sub-string is divisible by k
            if (n % k == 0):
                count += 1

    # Return the required count
    return count

# Driver code
if __name__ == '__main__':
    str = "33445"
    l = len(str)
    k = 11
    print(countSubStr(str, l, k))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

    // Function to return the count of sub-strings
    // of str that are divisible by k
    static int countSubStr(String str, int len, int k)
    {
        int count = 0;

        for (int i = 0; i < len; i++)
        {
            int n = 0;

            // Take all sub-strings starting from i
            for (int j = i; j < len; j++)
            {
                n = n * 10 + (str[j] - '0');

                // If current sub-string is divisible by k
                if (n % k == 0)
                    count++;
            }
        }

        // Return the required count
        return count;
    }

    // Driver code
    public static void Main()
    {
        String str = "33445";
        int len = str.Length;
        int k = 11;
        Console.WriteLine(countSubStr(str, len, k));
    }
}

// This code is contributed by Code_Mech
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of sub-strings
// of str that are divisible by k
function countSubStr($str, $len, $k)
{
    $count = 0;

    for ($i = 0; $i < $len; $i++)
    {
        $n = 0;

        // Take all sub-strings starting from i
        for ($j = $i; $j < $len; $j++)
        {
            $n = $n * 10 + ($str[$j] - '0');

            // If current sub-string is
            // divisible by k
            if ($n % $k == 0)
                $count++;
        }
    }

    // Return the required count
    return $count;
}

// Driver code
$str = "33445";
$len = strlen($str);
$k = 11;
echo countSubStr($str, $len, $k);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to return the count of sub-strings
// of str that are divisible by k
function countSubStr(str, len, k)
{
    let count = 0;

    for(let i = 0; i < len; i++)
    {
        let n = 0;

        // Take all sub-strings starting from i
        for(let j = i; j < len; j++)
        {
            n = n * 10 + (str[j].charCodeAt() -
                             '0'.charCodeAt());

            // If current sub-string is
            // divisible by k
            if (n % k == 0)
                count++;
        }
    }

    // Return the required count
    return count;
}

// Driver code
let str = "33445";
let len = str.length;
let k = 11;

document.write(countSubStr(str, len, k));

// This code is contributed by mukesh07

</script>
```

**Output**

```
3
```

**高效方法:**

其思想是使用一个 hashmap 来存储字符串中每个后缀的余数，这样如果任何后缀已经存在于 hashMap 中，那么它们之间的子字符串可以被 k 整除。

下面是上述方法的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above approach
import java.util.*;
public class Main
{

  // Program to count number of substrings
  public static int Divisible(String s,
                                    int k)
  {

    // To count substrings
    int num_of_substrings = 0;

    // To store the remainders
    int rem[] = new int[k];

    rem[0] = 1;
    StringBuffer curr = new StringBuffer();

    // Iterate from s.length() - 1 to 0
    for (int i = s.length() - 1; i >= 0; i--)
    {

      // to Calculate suffix string
      curr.insert(0, s.charAt(i));

      // convert to number
      long num = Long.parseLong(curr.
                                toString());
      num_of_substrings += rem[(int)num % k];

      // Keep track of visited remainders
      rem[(int)num % k]++;
    }

    // Return number of substrings
    return num_of_substrings;
  }

  // Driver Code
  public static void main(String args[])
  {
    String s = "111111";
    int k = 11;

    // Function Call
    System.out.println("Number of sub strings : "
                       + Divisible(s, k));
  }
}
```

**Output**

```
Number of sub strings : 9
```