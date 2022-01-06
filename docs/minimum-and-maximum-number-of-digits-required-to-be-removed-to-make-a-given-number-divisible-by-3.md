# 要使给定的数字能被 3 整除，需要去除的最小和最大位数

> 原文:[https://www . geeksforgeeks . org/最小和最大位数-需要移除才能使给定数字被 3 整除/](https://www.geeksforgeeks.org/minimum-and-maximum-number-of-digits-required-to-be-removed-to-make-a-given-number-divisible-by-3/)

给定一个数字串 **S** ，任务是找出必须从 **S** 中删除的最小和最大位数，使其能够被**3**T7】整除。如果无法做到，则打印**-1”**。

**示例:**

> **输入:** S = "12345"
> **输出:**
> 最小值:0
> 最大值:4
> **说明:**给定数字 12345 可被 3 整除。因此，要使它能被 3 整除，需要去掉的最小位数是 0。去掉数字 1、2、4、5 后，只剩下 3，可被 3 整除。因此，需要删除的最大位数是 4。
> 
> **输入:**S = " 44 "
> T3】输出:T5】最小值:-1
> 最大值:-1

**方法:**这个问题可以基于这样的观察来解决:对于任何要被 3 整除的[数](https://www.geeksforgeeks.org/check-large-number-divisible-3-not/)，位数之和也必须能被 3 整除。按照以下步骤解决此问题:

*   将给定字符串的每个数字插入一个数组，比如 **arr[]** ，作为**(S[I]–‘0’)% 3**。
*   在数组**arr【】**中找到 **0** s、 **1** s、 **2** s 的计数。
*   然后，计算数字的和，即**(arr[0]% 3)+(arr[1]% 3)+(arr[2]% 3)…。**。更新**总和=总和% 3** 。
*   根据**和**的值，会出现以下三种情况:
    *   **如果总和= 0:** 需要删除的最小位数为 **0** 。
    *   **如果总和= 1:** 这些数字应被移除，其总和在除以 **3** 时给出余数 **1** 。因此，需要考虑以下情况:
        *   如果 **1** s 的计数大于或等于 **1** ，则需要删除的最小位数为 1。
        *   如果 **2** s 的计数大于或等于 **2** ，那么需要删除的最小位数将是 **2【自(2+2)% 3 = 1】**。
    *   **如果总和= 3:** 这些数字应被移除，其总和在除以 **3** 时给出余数 **2** 。因此，会出现以下情况:
        *   如果 **2** s 的计数大于或等于 **1** ，则需要删除的最小位数为 **1** 。
        *   否则，如果 **1** s 的计数大于或等于 **2** ，则需要删除的最小位数为 **2 [(1 + 1) % 3 = 2]** 。
*   为了找到要删除的最大位数，需要考虑以下三种情况:
    *   如果 **0** s 的计数大于或等于 **1** ，则需要删除的最大位数为**(位数–1)**。
    *   如果 **1** s 和 **2** s 的计数都大于或等于 **1** ，则需要删除的最大位数为**(位数–2)[(1+2)% 3 = 0]**。
    *   如果 **1** s 或 **2** s 的计数大于或等于 **3** ，则需要删除的最大位数为**(位数–3)[(1+1+1)% 3 = 0，(2+2+2) % 3 = 0]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum and
// minimum number of digits to be
// removed to make str divisible by 3
void minMaxDigits(string str, int N)
{
    // Convert the string into
    // array of digits
    int arr[N];
    for (int i = 0; i < N; i++)
        arr[i] = (str[i] - '0') % 3;

    // Count of 0s, 1s, and 2s
    int zero = 0, one = 0, two = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        if (arr[i] == 0)
            zero++;
        if (arr[i] == 1)
            one++;
        if (arr[i] == 2)
            two++;
    }

    // Find the sum of digits % 3
    int sum = 0;

    for (int i = 0; i < N; i++) {
        sum = (sum + arr[i]) % 3;
    }

    // Cases to find minimum number
    // of digits to be removed
    if (sum == 0) {
        cout << 0 << ' ';
    }
    if (sum == 1) {
        if (one && N > 1)
            cout << 1 << ' ';
        else if (two > 1 && N > 2)
            cout << 2 << ' ';
        else
            cout << -1 << ' ';
    }
    if (sum == 2) {
        if (two && N > 1)
            cout << 1 << ' ';
        else if (one > 1 && N > 2)
            cout << 2 << ' ';
        else
            cout << -1 << ' ';
    }

    // Cases to find maximum number
    // of digits to be removed
    if (zero > 0)
        cout << N - 1 << ' ';
    else if (one > 0 && two > 0)
        cout << N - 2 << ' ';
    else if (one > 2 || two > 2)
        cout << N - 3 << ' ';
    else
        cout << -1 << ' ';
}

// Driver Code
int main()
{
    string str = "12345";
    int N = str.length();

    // Function Call
    minMaxDigits(str, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the maximum and
// minimum number of digits to be
// removed to make str divisible by 3
static void minMaxDigits(String str, int N)
{

    // Convert the string into
    // array of digits
    int arr[] = new int[N];
    for(int i = 0; i < N; i++)
        arr[i] = (str.charAt(i) - '0') % 3;

    // Count of 0s, 1s, and 2s
    int zero = 0, one = 0, two = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {
        if (arr[i] == 0)
            zero++;
        if (arr[i] == 1)
            one++;
        if (arr[i] == 2)
            two++;
    }

    // Find the sum of digits % 3
    int sum = 0;

    for(int i = 0; i < N; i++)
    {
        sum = (sum + arr[i]) % 3;
    }

    // Cases to find minimum number
    // of digits to be removed
    if (sum == 0)
    {
        System.out.print(0 + " ");
    }
    if (sum == 1)
    {
        if ((one != 0) && (N > 1))
            System.out.print(1 + " ");
        else if (two > 1 && N > 2)
            System.out.print(2 + " ");
        else
            System.out.print(-1 + " ");
    }
    if (sum == 2)
    {
        if (two != 0 && N > 1)
            System.out.print(1 + " ");
        else if (one > 1 && N > 2)
            System.out.print(2 + " ");
        else
            System.out.print(-1 + " ");
    }

    // Cases to find maximum number
    // of digits to be removed
    if (zero > 0)
        System.out.print(N - 1 + " ");
    else if (one > 0 && two > 0)
        System.out.print(N - 2 + " ");
    else if (one > 2 || two > 2)
        System.out.print(N - 3 + " ");
    else
        System.out.print(-1 + " ");
}

// Driver code
public static void main(String[] args)
{
    String str = "12345";
    int N = str.length();

    // Function Call
    minMaxDigits(str, N);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum and
# minimum number of digits to be
# removed to make str divisible by 3
def minMaxDigits(str, N):

    # Convert the string into
    # array of digits
    arr = [0]* N

    for i in range(N):
        arr[i] = (ord(str[i]) -
                  ord('0')) % 3

    # Count of 0s, 1s, and 2s
    zero = 0
    one = 0
    two = 0

    # Traverse the array
    for i in range(N):
        if (arr[i] == 0):
            zero += 1
        if (arr[i] == 1):
            one += 1
        if (arr[i] == 2):
            two += 1

    # Find the sum of digits % 3
    sum = 0

    for i in range(N):
        sum = (sum + arr[i]) % 3

    # Cases to find minimum number
    # of digits to be removed
    if (sum == 0):
        print("0", end = " ")

    if (sum == 1):
        if (one and N > 1):
            print("1", end = " ")
        elif (two > 1 and N > 2):
            print("2", end = " ")
        else:
            print("-1", end = " ")

    if (sum == 2):
        if (two and N > 1):
            print("1", end = " ")
        elif (one > 1 and N > 2):
            print("2", end = " ")
        else:
            print("-1", end = " ")

    # Cases to find maximum number
    # of digits to be removed
    if (zero > 0):
        print(N - 1, end = " ")
    elif (one > 0 and two > 0):
        print(N - 2, end = " ")
    elif (one > 2 or two > 2):
        print(N - 3, end = " ")
    else :
        print("-1", end = " ")

# Driver Code
str = "12345"
N = len(str)

# Function Call
minMaxDigits(str, N)

# This code is contributed by susmitakundugoaldanga
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum and
// minimum number of digits to be
// removed to make str divisible by 3
static void minMaxDigits(string str, int N)
{

    // Convert the string into
    // array of digits
    int[] arr = new int[N];
    for(int i = 0; i < N; i++)
        arr[i] = (str[i] - '0') % 3;

    // Count of 0s, 1s, and 2s
    int zero = 0, one = 0, two = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {
        if (arr[i] == 0)
            zero++;
        if (arr[i] == 1)
            one++;
        if (arr[i] == 2)
            two++;
    }

    // Find the sum of digits % 3
    int sum = 0;

    for(int i = 0; i < N; i++)
    {
        sum = (sum + arr[i]) % 3;
    }

    // Cases to find minimum number
    // of digits to be removed
    if (sum == 0)
    {
        Console.Write(0 + " ");
    }
    if (sum == 1)
    {
        if ((one != 0) && (N > 1))
            Console.Write(1 + " ");
        else if (two > 1 && N > 2)
            Console.Write(2 + " ");
        else
            Console.Write(-1 + " ");
    }
    if (sum == 2)
    {
        if (two != 0 && N > 1)
            Console.Write(1 + " ");
        else if (one > 1 && N > 2)
            Console.Write(2 + " ");
        else
            Console.Write(-1 + " ");
    }

    // Cases to find maximum number
    // of digits to be removed
    if (zero > 0)
        Console.Write(N - 1 + " ");
    else if (one > 0 && two > 0)
        Console.Write(N - 2 + " ");
    else if (one > 2 || two > 2)
        Console.Write(N - 3 + " ");
    else
        Console.Write(-1 + " ");
}

// Driver code
public static void Main()
{
    string str = "12345";
    int N = str.Length;

    // Function Call
    minMaxDigits(str, N);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the maximum and
// minimum number of digits to be
// removed to make str divisible by 3
function minMaxDigits(str, N)
{

    // Convert the string into
    // array of digits
    let arr = [];
    for(let i = 0; i < N; i++)
        arr[i] = (str[i] - '0') % 3;

    // Count of 0s, 1s, and 2s
    let zero = 0, one = 0, two = 0;

    // Traverse the array
    for(let i = 0; i < N; i++)
    {
        if (arr[i] == 0)
            zero++;
        if (arr[i] == 1)
            one++;
        if (arr[i] == 2)
            two++;
    }

    // Find the sum of digits % 3
    let sum = 0;

    for(let i = 0; i < N; i++)
    {
        sum = (sum + arr[i]) % 3;
    }

    // Cases to find minimum number
    // of digits to be removed
    if (sum == 0)
    {
       document.write(0 + " ");
    }
    if (sum == 1)
    {
        if ((one != 0) && (N > 1))
            document.write(1 + " ");
        else if (two > 1 && N > 2)
            document.write(2 + " ");
        else
            document.write(-1 + " ");
    }
    if (sum == 2)
    {
        if (two != 0 && N > 1)
           document.write(1 + " ");
        else if (one > 1 && N > 2)
            document.write(2 + " ");
        else
            document.write(-1 + " ");
    }

    // Cases to find maximum number
    // of digits to be removed
    if (zero > 0)
        document.write(N - 1 + " ");
    else if (one > 0 && two > 0)
       document.write(N - 2 + " ");
    else if (one > 2 || two > 2)
        document.write(N - 3 + " ");
    else
        document.write(-1 + " ");
}

// Driver code
let str = "12345";
let N = str.length;

// Function Call
minMaxDigits(str, N);

// This code is contributed by avijitmondal1998

</script>
```

**Output:** 

```
0 4
```

***时间复杂度:**O(log<sub>10</sub>N)*
***辅助空间:** O(log <sub>10</sub> N)*