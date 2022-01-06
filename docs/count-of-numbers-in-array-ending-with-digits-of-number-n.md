# 以数字 N 的数字结束的数组中数字的计数

> 原文:[https://www . geeksforgeeks . org/以 n 位数结尾的数组中的数字计数/](https://www.geeksforgeeks.org/count-of-numbers-in-array-ending-with-digits-of-number-n/)

给定一个数字 **N** 和一个由 **K** 个数字组成的数组**arr【】**，任务是找出数组中以数字 N 中任何一个数字结尾的数字的个数

**示例:**

> **输入:** N = 1731 arr[] = {57，6786}
> **输出:** 1
> **说明:**
> 对于 57，最后一位数字是 7，既然 7 存在就是 N，那么计数就是 1。
> 对于 6786，最后一位数字是 6，由于 N 中不存在 6，因此计数保持为 1。
> **输入:** N = 1324，arr[] = {23，25，12，121}
> **输出:** 3

**天真方法:**这个问题的天真方法是，对于数组**arr【】**中的每个数字，检查它的最后一个数字是否等于 n 中的任何一个数字。增加每个这样的数字的计数，并在末尾打印出来。
**时间复杂度:** *O(N * K)* ，其中 N 为数字，K 为数组 arr[]中的元素个数。
**有效方法:**解决这个问题的有效方法是执行预处理。

*   最初，创建一个大小为 10 的数组 A[]。
*   这个数组充当一个[散列](https://www.geeksforgeeks.org/hashing-set-1-introduction/)，它存储出现在数字 N 中的所有数字
*   之后，对于 arr[]数组中的每个数字，提取最后一个数字，并检查该最后一个数字是否出现在数组中。
*   增加每个数字的计数，并在最后打印出来。

以下是上述方法的实现:

## C++

```
// C++ program to find the count
// of numbers in Array ending
// with digits of number N

#include <bits/stdc++.h>
using namespace std;

// Array to keep the
// track of digits occurred
// Initially all are 0(false)
int digit[10] = { 0 };

// Function to initialize true
// if the digit is present
void digitsPresent(int n)
{
    // Variable to store the last digit
    int lastDigit;

    // Loop to iterate through every
    // digit of the number N
    while (n != 0) {
        lastDigit = n % 10;

        // Updating the array according
        // to the presence of the
        // digit in n at the array index
        digit[lastDigit] = true;
        n /= 10;
    }
}

// Function to check if the
// numbers in the array
// end with the digits of
// the number N
int checkLastDigit(int num)
{

    // Variable to store the count
    int count = 0;

    // Variable to store the last digit
    int lastDigit;
    lastDigit = num % 10;

    // Checking the presence of
    // the last digit in N
    if (digit[lastDigit] == true)
        count++;

    return count;
}

// Function to find
// the required count
void findCount(int N, int K, int arr[])
{

    int count = 0;

    for (int i = 0; i < K; i++) {

        count = checkLastDigit(arr[i]) == 1
                    ? count + 1
                    : count;
    }
    cout << count << endl;
}

// Driver code
int main()
{
    int N = 1731;

    // Preprocessing
    digitsPresent(N);

    int K = 5;
    int arr[] = { 57, 6786,
                  1111, 3, 9812 };

    findCount(N, K, arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count
// of numbers in Array ending
// with digits of number N
class GFG{

// Array to keep the
// track of digits occurred
// Initially all are 0(false)
public static int[] digit = new int[10];

// Function to initialize 1(true)
// if the digit is present
public static void digitsPresent(int n)
{

    // Variable to store the last digit
    int lastDigit;

    // Loop to iterate through every
    // digit of the number N
    while (n != 0)
    {
        lastDigit = n % 10;

        // Updating the array according
        // to the presence of the
        // digit in n at the array index
        digit[lastDigit] = 1;
        n /= 10;
    }
}

// Function to check if the
// numbers in the array
// end with the digits of
// the number N
public static int checkLastDigit(int num)
{

    // Variable to store the count
    int count = 0;

    // Variable to store the last digit
    int lastDigit;
    lastDigit = num % 10;

    // Checking the presence of
    // the last digit in N
    if (digit[lastDigit] == 1)
        count++;

    return count;
}

// Function to find
// the required count
public static void findCount(int N, int K,
                             int arr[])
{
    int count = 0;

    for(int i = 0; i < K; i++)
    {
       count = checkLastDigit(arr[i]) == 1 ?
               count + 1 : count;
    }
    System.out.println(count);
}

// Driver code
public static void main(String[] args)
{
    int N = 1731;

    // Preprocessing
    digitsPresent(N);

    int K = 5;
    int arr[] = { 57, 6786, 1111, 3, 9812 };

    findCount(N, K, arr);
}
}

// This code is contributed by Sayantan Pal
```

## 蟒蛇 3

```
# Python3 program to find the count
# of numbers in Array ending
# with digits of number N

# Array to keep the
# track of digits occurred
# Initially all are 0(false)
digit = [0] * 10

# Function to initialize true
# if the digit is present
def digitsPresent(n):

    # Variable to store the last digit
    lastDigit = 0;

    # Loop to iterate through every
    # digit of the number N
    while (n != 0):
        lastDigit = n % 10;

        # Updating the array according
        # to the presence of the
        # digit in n at the array index
        digit[int(lastDigit)] = 1;
        n /= 10;

# Function to check if the numbers
# in the array end with the digits
# of the number N
def checkLastDigit(num):

    # Variable to store the count
    count = 0;

    # Variable to store the last digit
    lastDigit = 0;
    lastDigit = num % 10;

    # Checking the presence of
    # the last digit in N
    if (digit[int(lastDigit)] == 1):
        count += 1

    return count;

# Function to find the required count
def findCount(N, K, arr):

    count = 0;
    for i in range(K):
        if checkLastDigit(arr[i]) == 1:
            count += 1
        else:
            count

    print(count)

# Driver code
N = 1731;

# Preprocessing
digitsPresent(N);

K = 5;
arr = [ 57, 6786, 1111, 3, 9812 ];

findCount(N, K, arr);

# This code is contributed by grand_master
```

## C#

```
// C# program to find the count
// of numbers in Array ending
// with digits of number N
using System;

class GFG{

// Array to keep the track of digits occurred
// Initially all are 0(false)
public static int []digit = new int[10];

// Function to initialize 1(true)
// if the digit is present
public static void digitsPresent(int n)
{

    // Variable to store the last digit
    int lastDigit;

    // Loop to iterate through every
    // digit of the number N
    while (n != 0)
    {
        lastDigit = n % 10;

        // Updating the array according to the
        // presence of the digit in n at the
        // array index
        digit[lastDigit] = 1;
        n /= 10;
    }
}

// Function to check if the numbers in the
// array end with the digits of the number N
public static int checkLastDigit(int num)
{

    // Variable to store the count
    int count = 0;

    // Variable to store the last digit
    int lastDigit;
    lastDigit = num % 10;

    // Checking the presence of
    // the last digit in N
    if (digit[lastDigit] == 1)
        count++;

    return count;
}

// Function to find the required count
public static void findCount(int N, int K,
                             int []arr)
{
    int count = 0;

    for(int i = 0; i < K; i++)
    {
        count = checkLastDigit(arr[i]) == 1 ?
                count + 1 : count;
    }
    Console.WriteLine(count);
}

// Driver code
static public void Main()
{
    int N = 1731;

    // Preprocessing
    digitsPresent(N);

    int K = 5;
    int []arr = { 57, 6786, 1111, 3, 9812 };

    findCount(N, K, arr);
}
}

// This code is contributed by piyush3010
```

## java 描述语言

```
<script>

// Javascript program to find the count
// of numbers in Array ending
// with digits of number N

// Array to keep the
// track of digits occurred
// Initially all are 0(false)
let digit = new Uint8Array(10);

// Function to initialize true
// if the digit is present
function digitsPresent(n)
{
    // Variable to store the last digit
    let lastDigit;

    // Loop to iterate through every
    // digit of the number N
    while (n != 0) {
        lastDigit = n % 10;

        // Updating the array according
        // to the presence of the
        // digit in n at the array index
        digit[lastDigit] = true;
        n = Math.floor(n/10);
    }
}

// Function to check if the
// numbers in the array
// end with the digits of
// the number N
function checkLastDigit(num)
{

    // Variable to store the count
    let count = 0;

    // Variable to store the last digit
    let lastDigit;
    lastDigit = num % 10;

    // Checking the presence of
    // the last digit in N
    if (digit[lastDigit] == true)
        count++;

    return count;
}

// Function to find
// the required count
function findCount(N, K, arr)
{
    let count = 0;

    for (let i = 0; i < K; i++) {

        count = checkLastDigit(arr[i]) == 1
                    ? count + 1
                    : count;
    }
    document.write(count + "<br>");
}

// Driver code

    let N = 1731;

    // Preprocessing
    digitsPresent(N);

    let K = 5;
    let arr = [ 57, 6786,
                1111, 3, 9812 ];

    findCount(N, K, arr);

//This code is contributed by Mayank Tyagi
</script>
```

**Output:** 

```
3
```

**时间复杂度:**

*   *O(N)，*其中 N 是预处理的给定数。
*   *O(K)，*其中 K 是为查询找到答案的查询数。