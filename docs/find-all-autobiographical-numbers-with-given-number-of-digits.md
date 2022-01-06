# 查找给定位数的所有自传号

> 原文:[https://www . geesforgeks . org/find-all-自传数字-带给定位数/](https://www.geeksforgeeks.org/find-all-autobiographical-numbers-with-given-number-of-digits/)

给定 **N** 作为位数，任务是找到所有长度等于 N
的**自传号**

> [**自传体数字**](https://www.geeksforgeeks.org/self-descriptive-number/) 是这样一个数字，它的第一个数字计算其中有多少个 0，第二个数字计算其中有多少个 1，以此类推。
> **比如** 1210 有 1 个零，2 个一，1 个二，0 个三。

**例:**

> **输入:** N = 4
> **输出:** 1210，2020
> **输入:** N = 5
> **输出:** 21200

**方式:**任意 N 位数字都在**【10<sup>(N-1)</sup>、10<sup>N</sup>-1】**范围内。因此，这个范围内的每个数字都被迭代，并检查它是否是自传体数字。

1.  将数字转换为字符串
2.  遍历每个数字并将其存储在变量中。
3.  然后运行一个内部循环，将外部循环的迭代器与内部循环的每个数字进行比较，如果它们相等，则增加该数字的出现次数。
4.  然后检查出现次数和存储每个数字的变量是否相等，这样我们就可以知道当前数字是否是自传性的。

**以下是上述方法的实施:**

## C++

```
// C++ implementation to find
// Autobiographical numbers with length N

#include <bits/stdc++.h>
using namespace std;

// Function to return if the
// number is autobiographical or not
bool isAutoBio(int num)
{

    string autoStr;

    int index, number, i, j, cnt;

    // Converting the integer
    // number to string
    autoStr = to_string(num);

    for (int i = 0;
         i < autoStr.size();
         i++) {

        // Extracting each character
        // from each index one by one
        // and converting into an integer
        index = autoStr.at(i) - '0';

        // Initialise count as 0
        cnt = 0;

        for (j = 0; j < autoStr.size(); j++) {

            number = autoStr.at(j) - '0';

            // Check if it is equal to the
            // index i if true then
            // increment the count
            if (number == i)

                // It is an
                // Autobiographical
                // number
                cnt++;
        }

        // Return false if the count and
        // the index number are not equal
        if (index != cnt)

            return false;
    }

    return true;
}

// Function to print autobiographical number
// with given number of digits
void findAutoBios(int n)
{

    int high, low, i, flag = 0;

    // Left boundary of interval
    low = pow(10, n - 1);

    // Right boundary of interval
    high = pow(10, n) - 1;

    for (i = low; i <= high; i++) {
        if (isAutoBio(i)) {
            flag = 1;
            cout << i << ", ";
        }
    }

    // Flag = 0 implies that the number
    // is not an autobiographical no.
    if (!flag)
        cout << "There is no "
             << "Autobiographical number"
             << " with " << n
             << " digits\n";
}

// Driver Code
int main()
{

    int N = 0;
    findAutoBios(N);

    N = 4;
    findAutoBios(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// Autobiographical numbers with length N

import java.util.*;
import java.lang.Math;

public class autobio {
    public static boolean isAutoBio(int num)
    {
        String autoStr;

        int index, number, i, j, cnt;

        // Converting the integer
        // number to string
        autoStr = Integer.toString(num);

        for (i = 0; i < autoStr.length(); i++) {

            // Extracting each character
            // from each index one by one
            // and converting into an integer
            index = Integer.parseInt(autoStr.charAt(i) + "");

            // initialize count as 0
            cnt = 0;

            for (j = 0; j < autoStr.length(); j++) {
                number = Integer.parseInt(autoStr.charAt(j) + "");

                // Check if it is equal to the
                // index i if true then
                // increment the count
                if (number == i)

                    // It is an
                    // Autobiographical
                    // number
                    cnt++;
            }

            // Return false if the count and
            // the index number are not equal
            if (cnt != index)

                return false;
        }

        return true;
    }

    // Function to print autobiographical number
    // with given number of digits
    public static void findAutoBios(double n)
    {
        // both the boundaries are taken double, so as
        // to satisfy Math.pow() function's signature
        double high, low;

        int i, flag = 0;

        // Left boundary of interval
        low = Math.pow(10.0, n - 1);

        // Right boundary of interval
        high = Math.pow(10.0, n) - 1.0;

        for (i = (int)low; i <= (int)high; i++)

            if (isAutoBio(i)) {
                flag = 1;
                System.out.print(i + ", ");
            }

        // Flag = 0 implies that the number
        // is not an autobiographical no.
        if (flag == 0)

            System.out.println("There is no Autobiographical Number"
                               + "with " + (int)n + " digits");
    }

    // Driver Code
    public static void main(String[] args)
    {
        double N = 0;
        findAutoBios(N);

        N = 4;
        findAutoBios(N);
    }
}
```

## 蟒蛇 3

```
# Python implementation to find
# Autobiographical numbers with length N

from math import pow

# Function to return if the
# number is autobiographical or not
def isAutoBio(num):

    # Converting the integer
    # number to string
    autoStr = str(num)

    for i in range(0, len(autoStr)):

        # Extracting each character
        # from each index one by one
        # and converting into an integer
        index = int(autoStr[i])

        # Initialize count as 0
        cnt = 0

        for j in range(0, len(autoStr)):

            number = int(autoStr[j])

            # Check if it is equal to the
            # index i if true then
            # increment the count
            if number == i:

                # It is an
                # Autobiographical
                # number
                cnt += 1

        # Return false if the count and
        # the index number are not equal
        if cnt != index:

            return False

    return True

# Function to print autobiographical number
# with given number of digits
def findAutoBios(n):

    # Left boundary of interval
    low = int(pow(10, n-1))

    # Right boundary of interval
    high = int(pow(10, n) - 1)

    flag = 0

    for i in range(low, high + 1):
        if isAutoBio(i):
            flag = 1
            print(i, end =', ')

    # Flag = 0 implies that the number
    # is not an autobiographical no.
    if flag == 0:
        print("There is no Autobiographical Number with "+ str(n) + " digits")

# Driver Code
if __name__ == "__main__":

    N = 0
    findAutoBios(N)

    N = 4
    findAutoBios(N)
```

## C#

```
// C# implementation to find
// Autobiographical numbers with length N
using System;

class autobio {
    public static bool isAutoBio(int num)
    {
        String autoStr;

        int index, number, i, j, cnt;

        // Converting the integer
        // number to string
        autoStr = num.ToString();

        for (i = 0; i < autoStr.Length; i++) {

            // Extracting each character
            // from each index one by one
            // and converting into an integer
            index = Int32.Parse(autoStr[i] + "");

            // initialize count as 0
            cnt = 0;

            for (j = 0; j < autoStr.Length; j++) {
                number = Int32.Parse(autoStr[j] + "");

                // Check if it is equal to the
                // index i if true then
                // increment the count
                if (number == i)

                    // It is an
                    // Autobiographical
                    // number
                    cnt++;
            }

            // Return false if the count and
            // the index number are not equal
            if (cnt != index)

                return false;
        }

        return true;
    }

    // Function to print autobiographical number
    // with given number of digits
    public static void findAutoBios(double n)
    {
        // both the boundaries are taken double, so as
        // to satisfy Math.Pow() function's signature
        double high, low;

        int i, flag = 0;

        // Left boundary of interval
        low = Math.Pow(10.0, n - 1);

        // Right boundary of interval
        high = Math.Pow(10.0, n) - 1.0;

        for (i = (int)low; i <= (int)high; i++)

            if (isAutoBio(i)) {
                flag = 1;
                Console.Write(i + ", ");
            }

        // Flag = 0 implies that the number
        // is not an autobiographical no.
        if (flag == 0)

            Console.WriteLine("There is no Autobiographical Number"
                               + "with " + (int)n + " digits");
    }

    // Driver Code
    public static void Main(String[] args)
    {
        double N = 0;
        findAutoBios(N);

        N = 4;
        findAutoBios(N);
    }
}

// This code is contributed by sapnasingh4991
```

**Output:** 

```
There is no Autobiographical number with 0 digits
1210, 2020
```

时间复杂度:O(10<sup>n</sup>–10<sup>n-1</sup>

辅助空间:0(1)