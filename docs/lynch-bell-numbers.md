# 林奇-贝尔数字

> 原文:[https://www.geeksforgeeks.org/lynch-bell-numbers/](https://www.geeksforgeeks.org/lynch-bell-numbers/)

**林奇-贝尔数**是一个数字 **N** 如果它的数字都是不同的并且 **N** 可以被它的每个数字整除。

> 1、2、3、4、5、6、7、8、9、12、15、24……

给定一个数字 **N** ，任务是检查 **N** 是否是**林奇-贝尔数字**。如果 **N** 是林奇贝尔数，则打印**“是”**否则打印**“否”**。
**示例:**

> **输入:** N = 384
> **输出:**是
> **说明:**
> 384/3 = 128，384/8 = 48，384/4 = 96
> 和 384 都有不同的数字。
> **输入:** N = 1123
> **输出:**否
> **说明:**

**进近:** :

1.  其思想是遍历给定数字的每个数字，并将遍历的数字标记为已访问。因为数字的总数是 10，我们需要一个大小只有 10 的布尔数组来标记访问过的数字。
2.  我们想测试每个数字是否非零，并对数字进行除法运算。比如用 128，我们要测试 d！= 0 && 128 % d == 0 表示 d = 1，2，8。为此，我们需要迭代数字的每个数字。
3.  然后如果它的数字都是不同的并且 **N** 可以被它的每个数字整除，那么打印**“是”**否则打印**“否”**。

以下是上述方法的实现:

## C++

```
// C++ implementation for the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check the divisibility
// of the number by its digit.
bool checkDivisibility(int n, int digit)
{
    // If the digit divides the number
    // then return true else return false.
    return (digit != 0 && n % digit == 0);
}

// Function to check if all digits
// of n divide it or not
bool isAllDigitsDivide(int n)
{
    int temp = n;
    while (temp > 0) {

        // Taking the digit of the
        // number into digit var.
        int digit = temp % 10;
        if (!(checkDivisibility(n, digit)))
            return false;

        temp /= 10;
    }
    return true;
}

// Function to check if N
// has all distinct digits
bool isAllDigitsDistinct(int n)
{
    // Create an array of size 10 and initialize all
    // elements as false. This array is used to check
    // if a digit is already seen or not.
    bool arr[10];
    for (int i = 0; i < 10; i++)
        arr[i] = false;

    // Traverse through all digits of given number
    while (n > 0) {
        // Find the last digit
        int digit = n % 10;

        // If digit is already seen, return false
        if (arr[digit])
            return false;

        // Mark this digit as seen
        arr[digit] = true;

        // REmove the last digit from number
        n = n / 10;
    }
    return true;
}

// Function to check Lynch-Bell numbers
bool isLynchBell(int n)
{
    return isAllDigitsDivide(n) &&
           isAllDigitsDistinct(n);
}

// Driver Code
int main()
{
    // Given Number N
    int N = 12;

    // Function Call
    if (isLynchBell(N))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## C

```
// C implementation for the
// above approach
#include <stdio.h>

// Function to check the divisibility
// of the number by its digit.
int checkDivisibility(int n, int digit)
{

    // If the digit divides the number
    // then return true else return false.
    return (digit != 0 && n % digit == 0);
}

// Function to check if all digits
// of n divide it or not
int isAllDigitsDivide(int n)
{
    int temp = n;
    while (temp > 0)
    {

        // Taking the digit of the
        // number into digit var.
        int digit = temp % 10;
        if (!(checkDivisibility(n, digit)))
            return 0;

        temp /= 10;
    }
    return 1;
}

// Function to check if N
// has all distinct digits
int isAllDigitsDistinct(int n)
{

    // Create an array of size 10 and initialize all
    // elements as false. This array is used to check
    // if a digit is already seen or not.
    int arr[10],i,digit;

    for(i = 0; i < 10; i++)
        arr[i] = 0;

    // Traverse through all digits of given number
    while (n > 0)
    {

        // Find the last digit
        digit = n % 10;

        // If digit is already seen, return false
        if (arr[digit])
            return 0;

        // Mark this digit as seen
        arr[digit] = 1;

        // Remove the last digit from number
        n = n / 10;
    }
    return 1;
}

// Function to check Lynch-Bell numbers
int isLynchBell(int n)
{
    return isAllDigitsDivide(n) &&
           isAllDigitsDistinct(n);
}

// Driver Code
int main()
{

    // Given number N
    int N = 12;

    // Function call
    if (isLynchBell(N))
        printf("Yes");
    else
        printf("No");
    return 0;
}

// This code is contributed by adityakumar27200
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG{

// Function to check the divisibility
// of the number by its digit.
static boolean checkDivisibility(int n,
                                 int digit)
{
    // If the digit divides the number
    // then return true else return false.
    return (digit != 0 && n % digit == 0);
}

// Function to check if all digits
// of n divide it or not
static boolean isAllDigitsDivide(int n)
{
    int temp = n;
    while (temp > 0)
    {

        // Taking the digit of the
        // number into digit var.
        int digit = temp % 10;
        if (!(checkDivisibility(n, digit)))
            return false;

        temp /= 10;
    }
    return true;
}

// Function to check if N
// has all distinct digits
static boolean isAllDigitsDistinct(int n)
{
    // Create an array of size 10 and initialize all
    // elements as false. This array is used to check
    // if a digit is already seen or not.
    boolean arr[] = new boolean[10];

    // Traverse through all digits of given number
    while (n > 0)
    {
        // Find the last digit
        int digit = n % 10;

        // If digit is already seen, return false
        if (arr[digit])
            return false;

        // Mark this digit as seen
        arr[digit] = true;

        // REmove the last digit from number
        n = n / 10;
    }
    return true;
}

// Function to check Lynch-Bell numbers
static boolean isLynchBell(int n)
{
    return isAllDigitsDivide(n) &&
           isAllDigitsDistinct(n);
}

// Driver Code
public static void main(String[] args)
{
    // Given Number N
    int N = 12;

    // Function Call
    if (isLynchBell(N))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Shubham Prakash
```

## 蟒蛇 3

```
# Python3 implementation for the
# above approach
import math

# Function to check the divisibility
# of the number by its digit.
def checkDivisibility(n, digit):

    # If the digit divides the number
    # then return true else return false.
    return ((digit != 0) and ((n % digit) == 0))

# Function to check if all digits
# of n divide it or not
def isAllDigitsDivide(n):

    temp = n
    while (temp >= 1):

        # Taking the digit of the number
        # into digit var.
        digit = int(temp % 10)
        if (checkDivisibility(n, digit) == False):
            return 0

        temp = temp / 10

    return 1

# Function to check if N has all
# distinct digits
def isAllDigitsDistinct(n):

    # Create an array of size 10 and
    # initialize all elements as false.
    # This array is used to check if a
    # digit is already seen or not.
    arr = [0] * 10

    # Traverse through all digits
    # of given number
    while (n >= 1):

        # Find the last digit
        digit = int(n % 10)

        # If digit is already seen, return false
        if(arr[digit]):
            return 0

        # Mark this digit as seen
        arr[digit] = 1

        # Remove the last digit from number
        n = int(n / 10)

    return 1

# Function to check Lynch-Bell numbers
def isLynchBell(n):

    return (isAllDigitsDivide(n) and
            isAllDigitsDistinct(n))

# Driver Code
if __name__=='__main__':

    # Given number N
    N = 12

    # Function call
    if isLynchBell(N):
        print("Yes")
    else:
        print("No")

# This code is contributed by adityakumar27200
```

## C#

```
// C# program for above approach
using System;
class GFG{

// Function to check the divisibility
// of the number by its digit.
static bool checkDivisibility(int n,
                              int digit)
{
    // If the digit divides the number
    // then return true else return false.
    return (digit != 0 && n % digit == 0);
}

// Function to check if all digits
// of n divide it or not
static bool isAllDigitsDivide(int n)
{
    int temp = n;
    while (temp > 0)
    {

        // Taking the digit of the
        // number into digit var.
        int digit = temp % 10;
        if (!(checkDivisibility(n, digit)))
            return false;

        temp /= 10;
    }
    return true;
}

// Function to check if N
// has all distinct digits
static bool isAllDigitsDistinct(int n)
{
    // Create an array of size 10 and initialize all
    // elements as false. This array is used to check
    // if a digit is already seen or not.
    bool []arr = new bool[10];

    // Traverse through all digits of given number
    while (n > 0)
    {
        // Find the last digit
        int digit = n % 10;

        // If digit is already seen, return false
        if (arr[digit])
            return false;

        // Mark this digit as seen
        arr[digit] = true;

        // REmove the last digit from number
        n = n / 10;
    }
    return true;
}

// Function to check Lynch-Bell numbers
static bool isLynchBell(int n)
{
    return isAllDigitsDivide(n) &&
           isAllDigitsDistinct(n);
}

// Driver Code
public static void Main()
{
    // Given Number N
    int N = 12;

    // Function Call
    if (isLynchBell(N))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript program for above approach

    // Function to check the divisibility
    // of the number by its digit.
    function checkDivisibility( n, digit) {
        // If the digit divides the number
        // then return true else return false.
        return (digit != 0 && n % digit == 0);
    }

    // Function to check if all digits
    // of n divide it or not
    function isAllDigitsDivide( n) {
        let temp = n;
        while (temp > 0) {

            // Taking the digit of the
            // number into digit var.
            let digit = temp % 10;
            if (!(checkDivisibility(n, digit)))
                return false;

            temp = parseInt(temp/10);
        }
        return true;
    }

    // Function to check if N
    // has all distinct digits
    function isAllDigitsDistinct( n) {
        // Create an array of size 10 and initialize all
        // elements as false. This array is used to check
        // if a digit is already seen or not.
        let arr = Array(10).fill(0);

        // Traverse through all digits of given number
        while (n > 0) {
            // Find the last digit
            let digit = n % 10;

            // If digit is already seen, return false
            if (arr[digit])
                return false;

            // Mark this digit as seen
            arr[digit] = true;

            // REmove the last digit from number
            n = parseInt(n / 10);
        }
        return true;
    }

    // Function to check Lynch-Bell numbers
    function isLynchBell( n) {
        return isAllDigitsDivide(n) && isAllDigitsDistinct(n);
    }

    // Driver Code

        // Given Number N
        let N = 12;

        // Function Call
        if (isLynchBell(N))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:***O(n)*
T5】参考:[http://www.numbersaplenty.com/set/Lynch-Bell_number/](http://www.numbersaplenty.com/set/Lynch-Bell_number/)