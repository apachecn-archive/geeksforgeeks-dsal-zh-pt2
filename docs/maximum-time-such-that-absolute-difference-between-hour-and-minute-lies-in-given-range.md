# 小时和分钟的绝对差值在给定范围内的最大时间

> 原文:[https://www . geesforgeks . org/最大时间-小时与分钟之间的绝对差值在给定范围内/](https://www.geeksforgeeks.org/maximum-time-such-that-absolute-difference-between-hour-and-minute-lies-in-given-range/)

给定一个 **24 小时的时间**值，其中一些数字上有问号('？')，以及两个整数 **L** 和 **R** 。问号可以用任何数字代替。任务是找到最大时间，使得小时值和分钟值之间的绝对差值位于区间[ **L，R** ]内。如果不存在可能的时间值，则打印 **-1** 。

**示例:**

> **输入:**时间=“2？:03 "，L = 5，R = 18
> **输出:** 21:03
> **说明:**因为，差值为 21–3 = 18，时间值 21:03 是差值在[5，18]范围内的最大可能值
> 
> **输入:**时间=？？:??"，L = 60，R = 69
> **输出:** -1
> **解释:**因为小时值和分钟值之间最大可能的差值是 59。所以，没有时间价值是可能的。

**方法:**
我们将运行两个嵌套循环，一个表示从 23 到 0 的“小时”值，另一个表示从 59 到 0 的“分钟”值。我们不断减少“小时”和“分钟”的值，直到我们得到所需的时间值。

1.  由于需要最大时间值，因此我们将“小时”值从 23 减少到 0，类似地将“分钟”值从 59 减少到 0。
2.  在减少“小时”和“分钟”值后，我们需要检查“小时”和“分钟”值是否有效。
3.  “小时”和“分钟”值的更改只允许在那些包含“？”的位置进行。其他位置的更改将使时间值无效。为了确保这一点，我们将调用函数 isValid()。
4.  继续减少“小时”和“分钟”值，直到找到一个有效时间，其差值在[ **L，R** 范围内。
5.  如果没有找到有效时间，则打印“-1”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function checks whether
// given time is correct
bool isValid(char a1, char a2,
             string str, int flag)
{

    char v1, v2;
    // To check minute value of time
    if (flag == 0) {
        v1 = str[4];
        v2 = str[3];
    }
    else {
        // To check hour value of time
        v1 = str[1];
        v2 = str[0];
    }

    // Changes in value is not allowed
    // at position where '?' is not
    // present
    if (v1 != a1 && v1 != '?')
        return false;
    if (v2 != a2 && v2 != '?')
        return false;

    return true;
}

// Function checks whether
// the absolute difference
// between hour and minute
// value is within [L, R]
bool inRange(int hh,
             int mm, int L, int R)
{
    int a = abs(hh - mm);

    // Checks if the difference is outside
    // the give range
    if (a < L || a > R)
        return false;

    return true;
}

// Displays time in proper
// 24-hour format
void displayTime(int hh, int mm)
{
    if (hh > 10)
        cout << hh << ":";
    else if (hh < 10)
        cout << "0" << hh << ":";

    if (mm > 10)
        cout << mm << endl;
    else if (mm < 10)
        cout << "0" << mm << endl;
}

// Function find the desired
// value of time whose difference
// lies in the range [L, R]
void maximumTimeWithDifferenceInRange(
    string str,
    int L, int R)
{
    int i, j;
    int h1, h2, m1, m2;

    // Decrease hour value from 23 to 0
    for (i = 23; i >= 0; i--) {
        h1 = i % 10;
        h2 = i / 10;

        // Check if the hour value is valid
        // if not valid then no need to change
        // minute value, since time will still
        // remain in valid, to check hour value
        // flag is set to 1.
        if (!isValid(h1 + '0', h2 + '0', str, 1)) {
            continue;
        }

        // Decrease minute value from 59 to 0
        for (j = 59; j >= 0; j--) {
            m1 = j % 10;
            m2 = j / 10;

            // Check if the minute value is valid,
            // if not valid then skip the current
            // iteration, to check 'minute' value
            // flag is set to 0.
            if (!isValid(m1 + '0', m2 + '0', str, 0)) {
                continue;
            }

            if (inRange(i, j, L, R)) {
                displayTime(i, j);
                return;
            }
        }
    }
    if (inRange(i, j, L, R))
        displayTime(i, j);
    else
        cout << "-1" << endl;
}

// Driver code
int main()
{
    // Input time
    string timeValue = "??:??";

    // Difference range
    int L = 20, R = 39;
    maximumTimeWithDifferenceInRange(
        timeValue,
        L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for
// the above approach
import java.util.*;
class GFG {

// Function checks whether
// given time is correct
static boolean isValid(char a1, char a2,
                       String str, int flag)
{
  char v1, v2;

  // To check minute value of time
  if (flag == 0)
  {
    v1 = str.charAt(4);
    v2 = str.charAt(3);
  }
  else
  {
    // To check hour value of time
    v1 = str.charAt(1);
    v2 = str.charAt(0);
  }

  // Changes in value is not allowed
  // at position where '?' is not
  // present
  if (v1 != a1 && v1 != '?')
    return false;
  if (v2 != a2 && v2 != '?')
    return false;

  return true;
}

// Function checks whether
// the absolute difference
// between hour and minute
// value is within [L, R]
static boolean inRange(int hh, int mm,
                       int L, int R)
{
  int a = Math.abs(hh - mm);

  // Checks if the difference
  // is outside the give range
  if (a < L || a > R)
    return false;

  return true;
}

// Displays time in proper
// 24-hour format
static void displayTime(int hh, int mm)
{
  if (hh > 10)
    System.out.print(hh + ":");
  else if (hh < 10)
    System.out.print("0" + hh + ":");

  if (mm > 10)
    System.out.println(mm);
  else if (mm < 10)
    System.out.println("0" + mm);
}

// Function find the desired
// value of time whose difference
// lies in the range [L, R]
static void maximumTimeWithDifferenceInRange(String str,
                                             int L,
                                             int R)
{
  int i = 0, j = 0;
  int h1, h2, m1, m2;

  // Decrease hour value
  // from 23 to 0
  for (i = 23; i >= 0; i--)
  {
    h1 = i % 10;
    h2 = i / 10;

    // Check if the hour value
    // is valid if not valid
    // then no need to change
    // minute value, since time
    // will still remain in valid,
    // to check hour value
    // flag is set to 1.
    if (!isValid((char)h1,
                 (char)h2, str, 1))
    {
      continue;
    }

    // Decrease minute value
    // from 59 to 0
    for (j = 59; j >= 0; j--)
    {
      m1 = j % 10;
      m2 = j / 10;

      // Check if the minute value
      // is valid, if not valid
      // then skip the current
      // iteration, to check
      // 'minute' value
      // flag is set to 0.
      if (!isValid((char)m1,
                   (char)m2, str, 0))
      {
        continue;
      }

      if (inRange(i, j, L, R))
      {
        displayTime(i, j);
        return;
      }
    }
  }
  if (inRange(i, j, L, R))
    displayTime(i, j);
  else
    System.out.println("-1");
}

// Driver code
public static void main(String[] args)
{
  // Input time
  String timeValue = "??:??";

  // Difference range
  int L = 20, R = 39;
  maximumTimeWithDifferenceInRange(timeValue, L, R);
}
}

// This code is contributed by Chitranayal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function checks whether
# given time is correct
def isValid(a1, a2, strr, flag):

    v1, v2 = 0, 0

    # To check minute value of time
    if (flag == 0):
        v1 = strr[4]
        v2 = strr[3]
    else:

        # To check hour value of time
        v1 = strr[1]
        v2 = strr[0]

    # Changes in value is not allowed
    # at position where '?' is not
    # present
    if (v1 != a1 and v1 != '?'):
        return False
    if (v2 != a2 and v2 != '?'):
        return False

    return True

# Function checks whether
# the absolute difference
# between hour and minute
# value is within [L, R]
def inRange(hh, mm, L, R):
    a = abs(hh - mm)

    # Checks if the difference is
    # outside the give range
    if (a < L or a > R):
        return False

    return True

# Displays time in proper
# 24-hour format
def displayTime(hh, mm):

    if (hh > 10):
        print(hh, end = ":")
    elif (hh < 10):
        print("0", hh, end = ":")

    if (mm > 10):
        print(mm)
    elif (mm < 10):
        print("0", mm)

# Function find the desired
# value of time whose difference
# lies in the range [L, R]
def maximumTimeWithDifferenceInRange(strr, L, R):

    i, j = 0, 0
    h1, h2, m1, m2 = 0, 0, 0, 0

    # Decrease hour value from 23 to 0
    for i in range(23, -1, -1):
        h1 = i % 10
        h2 = i // 10

        # Check if the hour value is valid
        # if not valid then no need to change
        # minute value, since time will still
        # remain in valid, to check hour value
        # flag is set to 1.
        if (not isValid(chr(h1), chr(h2), strr, 1)):
            continue

        # Decrease minute value from 59 to 0
        for j in range(59, -1, -1):
            m1 = j % 10
            m2 = j // 10

            # Check if the minute value is valid,
            # if not valid then skip the current
            # iteration, to check 'minute' value
            # flag is set to 0.
            if (not isValid(chr(m1), chr(m2),
                            strr, 0)):
                continue

            if (inRange(i, j, L, R)):
                displayTime(i, j)
                return

    if (inRange(i, j, L, R)):
        displayTime(i, j)
    else:
        print(-1)

# Driver code

# Input time
timeValue = "??:??"

# Difference range
L = 20
R = 39

maximumTimeWithDifferenceInRange(timeValue, L, R)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function checks whether
// given time is correct
static bool isValid(char a1, char a2,
                    string str, int flag)
{
    char v1, v2;

    // To check minute value of time
    if (flag == 0)
    {
        v1 = str[4];
        v2 = str[3];
    }
    else
    {

        // To check hour value of time
        v1 = str[1];
        v2 = str[0];
    }

    // Changes in value is not allowed
    // at position where '?' is not
    // present
    if (v1 != a1 && v1 != '?')
    {
        return false;
    }
    if (v2 != a2 && v2 != '?')
    {
        return false;
    }
    return true;
}

// Function checks whether
// the absolute difference
// between hour and minute
// value is within [L, R]
static bool inRange(int hh, int mm,
                    int L, int R)
{
    int a = Math.Abs(hh - mm);

    // Checks if the difference
    // is outside the give range
    if (a < L || a > R)
    {
        return false;
    }
    return true;
}

// Displays time in proper
// 24-hour format
static void displayTime(int hh, int mm)
{
    if (hh > 10)
    {
        Console.Write(hh + ":");
    }
    else if (hh < 10)
    {
        Console.Write("0" + hh + ":");
    }
    if (mm > 10)
    {
        Console.Write(mm);
    }
    else if (mm < 10)
    {
        Console.Write("0" + mm);
    }
}

// Function find the desired
// value of time whose difference
// lies in the range [L, R]
static void maximumTimeWithDifferenceInRange(
    string str, int L, int R)
{
    int i = 0, j = 0;
    int h1, h2, m1, m2;

    // Decrease hour value
    // from 23 to 0
    for(i = 23; i >= 0; i--)
    {
        h1 = i % 10;
        h2 = i / 10;

        // Check if the hour value
        // is valid if not valid
        // then no need to change
        // minute value, since time
        // will still remain in valid,
        // to check hour value
        // flag is set to 1.   
        if (!isValid((char)h1, (char)h2, str, 1))
        {
            continue;
        }

        // Decrease minute value
        // from 59 to 0
        for(j = 59; j >= 0; j--)
        {
            m1 = j % 10;
            m2 = j / 10;

            // Check if the minute value
            // is valid, if not valid
            // then skip the current
            // iteration, to check
            // 'minute' value
            // flag is set to 0.
            if (!isValid((char)m1, (char)m2, str, 0))
            {
                continue;
            }
            if (inRange(i, j, L, R))
            {
                displayTime(i, j);
                return;
            }
        }
    }
    if (inRange(i, j, L, R))
    {
        displayTime(i, j);
    }
    else
    {
        Console.WriteLine("-1");
    }
}

// Driver code
static public void Main()
{

    // Input time
    string timeValue = "??:??";

    // Difference range
    int L = 20, R = 39;

    maximumTimeWithDifferenceInRange(timeValue, L, R);
}
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// Javascript program for
// the above approach

// Function checks whether
// given time is correct
function isValid(a1, a2, str, flag)
{
    let v1, v2;

  // To check minute value of time
  if (flag == 0)
  {
    v1 = str[4];
    v2 = str[3];
  }
  else
  {
    // To check hour value of time
    v1 = str[1];
    v2 = str[0];
  }

  // Changes in value is not allowed
  // at position where '?' is not
  // present
  if (v1 != a1 && v1 != '?')
    return false;
  if (v2 != a2 && v2 != '?')
    return false;

  return true;
}

// Function checks whether
// the absolute difference
// between hour and minute
// value is within [L, R]
function inRange(hh,mm,L,R)
{
    let a = Math.abs(hh - mm);

  // Checks if the difference
  // is outside the give range
  if (a < L || a > R)
    return false;

  return true;
}

// Displays time in proper
// 24-hour format
function displayTime(hh,mm)
{
    if (hh > 10)
    document.write(hh + ":");
  else if (hh < 10)
    document.write("0" + hh + ":");

  if (mm > 10)
    document.write(mm+"<br>");
  else if (mm < 10)
    document.write("0" + mm+"<br>");
}

// Function find the desired
// value of time whose difference
// lies in the range [L, R]   
function maximumTimeWithDifferenceInRange(str,L,R)
{
    let i = 0, j = 0;
  let h1, h2, m1, m2;

  // Decrease hour value
  // from 23 to 0
  for (i = 23; i >= 0; i--)
  {
    h1 = i % 10;
    h2 = Math.floor(i / 10);

    // Check if the hour value
    // is valid if not valid
    // then no need to change
    // minute value, since time
    // will still remain in valid,
    // to check hour value
    // flag is set to 1.
    if (!isValid(String.fromCharCode(h1),String.fromCharCode(h2), str, 1))
    {
      continue;
    }

    // Decrease minute value
    // from 59 to 0
    for (j = 59; j >= 0; j--)
    {
      m1 = j % 10;
      m2 = Math.floor(j / 10);

      // Check if the minute value
      // is valid, if not valid
      // then skip the current
      // iteration, to check
      // 'minute' value
      // flag is set to 0.
      if (!isValid(String.fromCharCode(m1),
                   String.fromCharCode(m2), str, 0))
      {
        continue;
      }

      if (inRange(i, j, L, R))
      {
        displayTime(i, j);
        return;
      }
    }
  }
  if (inRange(i, j, L, R))
    displayTime(i, j);
  else
    document.write("-1<br>");
}

// Driver code
// Input time
  let timeValue = "??:??";

  // Difference range
  let L = 20, R = 39;
  maximumTimeWithDifferenceInRange(timeValue, L, R);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
23:59
```

**时间复杂度:***O(1)*
T5】辅助空间: *O(1)*