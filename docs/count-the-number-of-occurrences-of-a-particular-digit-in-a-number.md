# 计算一个数字中特定数字出现的次数

> 原文:[https://www . geeksforgeeks . org/count-数字中特定数字的出现次数/](https://www.geeksforgeeks.org/count-the-number-of-occurrences-of-a-particular-digit-in-a-number/)

给定一个数字 **N** 和一个数字 **D** ，任务是统计 N 中 **D 的出现次数。
**举例:**** 

```
Input: N = 25, D = 2
Output: 1

Input: N = 100, D = 0
Output: 2
```

**逼近:**在 N 中逐个取出数字，检查这个数字是否等于 d，如果等于，则计数递增 1。最后，打印计数。
以下是上述办法的实施情况:

## C++

```
// C++ program to count the number of occurrences
// of a particular digit in a number

#include <iostream>
using namespace std;

// Function to count the occurrences
// of the digit D in N
long long int countOccurrances(long long int n,
                               int d)
{
    long long int count = 0;

    // Loop to find the digits of N
    while (n > 0) {

        // check if the digit is D
        count = (n % 10 == d)
                    ? count + 1
                    : count;
        n = n / 10;
    }

    // return the count of the
    // occurrences of D in N
    return count;
}

// Driver code
int main()
{

    int d = 2;
    long long int n = 214215421;

    cout << countOccurrances(n, d)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number of occurrences
// of a particular digit in a number
import java.util.*;

class GFG
{

// Function to count the occurrences
// of the digit D in N
static int countOccurrances(int n,
                            int d)
{
    int count = 0;

    // Loop to find the digits of N
    while (n > 0)
    {

        // check if the digit is D
        count = (n % 10 == d) ?
                    count + 1 : count;
        n = n / 10;
    }

    // return the count of the
    // occurrences of D in N
    return count;
}

// Driver code
public static void main(String args[])
{
    int d = 2;
    int n = 214215421;

    System.out.println(countOccurrances(n, d));
}
}

// This code is contributed by Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 program to count the
# number of occurrences of a
# particular digit in a number

# Function to count the occurrences
# of the digit D in N
def countOccurrances(n, d):
    count = 0

    # Loop to find the digits of N
    while (n > 0):

        # check if the digit is D
        if(n % 10 == d):
            count = count + 1

        n = n // 10

    # return the count of the
    # occurrences of D in N
    return count

# Driver code
d = 2
n = 214215421
print(countOccurrances(n, d))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to count the number
// of occurrences of a particular
// digit in a number
using System;
class GFG
{

// Function to count the occurrences
// of the digit D in N
static int countOccurrances(int n,
                            int d)
{
    int count = 0;

    // Loop to find the digits of N
    while (n > 0)
    {

        // check if the digit is D
        count = (n % 10 == d) ?
                    count + 1 : count;
        n = n / 10;
    }

    // return the count of the
    // occurrences of D in N
    return count;
}

// Driver code
public static void Main()
{
    int d = 2;
    int n = 214215421;

    Console.WriteLine(countOccurrances(n, d));
}
}

// This code is contributed by Code_Mech.
```

## java 描述语言

```
<script>

// Javascript program to count
// the number of occurrences
// of a particular digit in a number

// Function to count the occurrences
// of the digit D in N
function countOccurrances(n, d)
{
    let count = 0;

    // Loop to find the digits of N
    while (n > 0) {

        // check if the digit is D
        count = (n % 10 == d)
                    ? count + 1
                    : count;
        n = parseInt(n / 10);
    }

    // return the count of the
    // occurrences of D in N
    return count;
}

// Driver code

    let d = 2;
    let n = 214215421;

    document.write(countOccurrances(n, d));

</script>
```

**Output:** 

```
3
```