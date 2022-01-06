# 获得给定总和所需的最小位数

> 原文:[https://www . geesforgeks . org/最小位数-需要获得给定金额/](https://www.geeksforgeeks.org/minimum-count-of-digits-required-to-obtain-given-sum/)

给定一个整数 **N** ，任务是找到生成一个位数总和等于 **N** 的数字所需的最小位数。

**示例:**

> **输入:** N = 18
> **输出:** 2
> **说明:**
> 位数之和等于 18 的最小数为 99。
> 
> **输入:** N = 28
> **输出:** 4
> **说明:**
> 8884、6877 等 4 位数字长度最小，位数之和等于 28。

**方法:**通过以下观察可以解决问题:

1.  将**计数**增加 **9** 。因此，现在计数等于最短数中 9 的个数。将 **N** 降低至 **N % 9**
2.  现在，如果 **N** 超过 0，将**计数**增加 **1** 。
3.  最后打印**把**算作答案。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// minimum count of digits
void mindigits(int n)
{
    // IF N is divisible by 9
    if (n % 9 == 0) {

        // Count of 9's is the answer
        cout << n / 9 << endl;
    }
    else {

        // If remainder is non-zero
        cout << (n / 9) + 1 << endl;
    }
}

// Driver Code
int main()
{
    int n1 = 24;
    int n2 = 14;
    mindigits(n1);
    mindigits(n2);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
// required to make the given sum
import java.util.*;

class Main {

    // Function to print the minimum
    // count of digits
    static void mindigits(int n)
    {

        // IF N is divisible by 9
        if (n % 9 == 0) {

            // Count of 9's is the answer
            System.out.println(n / 9);
        }
        else {

            // If remainder is non-zero
            System.out.println((n / 9) + 1);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n1 = 24;
        int n2 = 18;
        mindigits(n1);
        mindigits(n2);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to print the minimum
# count of digits
def mindigits(n):

    # IF N is divisible by 9
    if (n % 9 == 0):

        # Count of 9's is the answer
        print(n // 9);
    else:

        # If remainder is non-zero
        print((n // 9) + 1);

# Driver Code
if __name__ == '__main__':

    n1 = 24;
    n2 = 18;

    mindigits(n1);
    mindigits(n2);

# This code is contributed by amal kumar choubey
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to print the minimum
// count of digits
static void mindigits(int n)
{

    // IF N is divisible by 9
    if (n % 9 == 0)
    {

        // Count of 9's is the answer
        Console.WriteLine(n / 9);
    }
    else
    {

        // If remainder is non-zero
        Console.WriteLine((n / 9) + 1);
    }
}

// Driver Code
public static void Main(String[] args)
{
    int n1 = 24;
    int n2 = 18;

    mindigits(n1);
    mindigits(n2);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach
// required to make the given sum

    // Function to print the minimum
    // count of digits
    function mindigits(n)
    {

        // IF N is divisible by 9
        if (n % 9 == 0) {

            // Count of 9's is the answer
            document.write(Math.floor(n / 9) + "<br/>");
        }
        else {

            // If remainder is non-zero
            document.write(Math.floor(n / 9) + 1 + "<br/>");
        }
    }

// Driver Code

        let n1 = 24;
        let n2 = 18;
        mindigits(n1);
        mindigits(n2);

</script>
```

**Output:** 

```
3
2
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)