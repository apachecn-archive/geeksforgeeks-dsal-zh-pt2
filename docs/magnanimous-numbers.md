# 大度的数字

> 原文:[https://www.geeksforgeeks.org/magnanimous-numbers/](https://www.geeksforgeeks.org/magnanimous-numbers/)

**大度数**是一个至少有 2 位数字的数，这样在它的任何位置的数字中间插入一个“+”所得到的和就是一个质数。

**例如:**

> 4001 是**大度数**，因为数字 4+001=5，40+01=41，400+1=401 都是质数。

### 检查 N 是否是一个大数字

给定一个数字 **N** ，任务是检查 **N** 是否是一个大度的数字。如果 N 是一个大数字，则打印“是”，否则打印“否”。

**示例:**

> **输入:** N = 4001
> **输出:**是
> **说明:**
> 4+001=5，40+01=41，400+1=401 都是质数。
> 
> **输入:**N = 18
> T3】输出:否

**进场:**

1.  将数字 N 转换为字符串
2.  遍历字符串，找到字符串的所有左部分和右部分。
3.  将字符串的左半部分和右半部分转换为整数，并检查左半部分和右半部分的总和是否不是素数，然后返回 false
4.  否则，最后还真

> 例如 N = 4001
> 左部+右部=质数
> 4+001=5 =质数
> 40+01=41 质数
> 400+1=401 质数

下面是上述方法的实现:

## C++

```
// C++ implementation to check
// if a number is Magnanimous

#include <bits/stdc++.h>
using namespace std;

// Function to check if n is prime
bool isPrime(int n)
{
    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for (int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to check if the number is
// Magnanimous or not
bool isMagnanimous(int N)
{
    // converting the number to string
    string s = to_string(N);

    // finding length of string
    int l = s.length();

    // number should not be of single digit
    if (l < 2)
        return false;

    // loop to find all left and right
    // part of the string
    for (int i = 0; i < l - 1; i++) {
        string left = s.substr(0, i + 1);
        string right = s.substr(i + 1);
        int x = stoi(left);
        int y = stoi(right);
        if (!isPrime(x + y))
            return false;
    }
    return true;
}

// Driver Code
int main()
{
    int N = 12;
    isMagnanimous(N) ? cout << "Yes"
                     : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check 
// if a number is Magnanimous
class GFG{

// Function to check if n is prime
static boolean isPrime(int n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to check if the number is
// Magnanimous or not
static boolean isMagnanimous(int N)
{

    // Converting the number to string
    String s = Integer.toString(N);

    // Finding length of string
    int l = s.length();

    // Number should not be of single digit
    if (l < 2)
        return false;

    // Loop to find all left and right
    // part of the string
    for(int i = 0; i < l - 1; i++)
    {
        String left = s.substring(0, i + 1);
        String right = s.substring(i + 1);
        int x = Integer. valueOf(left);
        int y = Integer. valueOf(right);

        if (!isPrime(x + y))
            return false;
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    int N = 12;

    if(isMagnanimous(N))
        System.out.print("Yes\n");
    else
        System.out.print("No\n");
}
}

// This code is contributed by shubham
```

## 蟒蛇 3

```
# Python3 implementation to check
# if a number is Magnanimous

# Function to check if n is prime
def isPrime(n):

    # Corner cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

    # This is checked so that we can skip
    # middle five numbers in below loop
    if (n % 2 == 0) or (n % 3 == 0):
        return False

    i = 5
    while (i * i <= n):
        if (n % i == 0 or n % (i + 2) == 0):
            return False

        i = i + 6

    return True

# Function to check if the number is
# Magnanimous or not
def isMagnanimous(N):

    # Converting the number to string
    s = str(N)

    # Finding length of string
    l = len(s)

    # Number should not be of single digit
    if (l < 2):
        return False

    # Loop to find all left and right
    # part of the string
    for i in range(l - 1):
        left = s[0 : i + 1]
        right = s[i + 1 : ]
        x = int(left)
        y = int(right)

        if (not isPrime(x + y)):
            return False

    return True

# Driver code
N = 12

if isMagnanimous(N):
    print("Yes")
else:
    print("No")

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation to check
// if a number is Magnanimous
using System;

class GFG{

// Function to check if n is prime
static bool isPrime(int n)
{

    // Corner cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // This is checked so that we can skip
    // middle five numbers in below loop
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    for(int i = 5; i * i <= n; i = i + 6)
        if (n % i == 0 || n % (i + 2) == 0)
            return false;

    return true;
}

// Function to check if the number is
// Magnanimous or not
static bool isMagnanimous(int N)
{

    // Converting the number to string
    String s = N.ToString();

    // Finding length of string
    int l = s.Length;

    // Number should not be of single digit
    if (l < 2)
        return false;

    // Loop to find all left and right
    // part of the string
    for(int i = 0; i < l - 1; i++)
    {
        String left = s.Substring(0, i + 1);
        String right = s.Substring(i + 1);

        int x = int.Parse(left);
        int y = int. Parse(right);

        if (!isPrime(x + y))
            return false;
    }
    return true;
}

// Driver code
public static void Main(String[] args)
{
    int N = 12;

    if(isMagnanimous(N))
        Console.Write("Yes\n");
    else
        Console.Write("No\n");
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
    // Javascript implementation to check
    // if a number is Magnanimous

    // Function to check if n is prime
    function isPrime(n)
    {

        // Corner cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // This is checked so that we can skip
        // middle five numbers in below loop
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        for(let i = 5; i * i <= n; i = i + 6)
            if (n % i == 0 || n % (i + 2) == 0)
                return false;

        return true;
    }

    // Function to check if the number is
    // Magnanimous or not
    function isMagnanimous(N)
    {

        // Converting the number to string
        let s = N.toString();

        // Finding length of string
        let l = s.length;

        // Number should not be of single digit
        if (l < 2)
            return false;

        // Loop to find all left and right
        // part of the string
        for(let i = 0; i < l - 1; i++)
        {
            let left = s.substring(0, i + 1);
            let right = s.substring(i + 1);
            let x = parseInt(left);
            let y = parseInt(right);

            if (!isPrime(x + y))
                return false;
        }
        return true;
    }

    let N = 12;

    if(isMagnanimous(N))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(n)*
T5】参考:[http://www.numbersaplenty.com/set/magnanimous_number/](http://www.numbersaplenty.com/set/magnanimous_number/)