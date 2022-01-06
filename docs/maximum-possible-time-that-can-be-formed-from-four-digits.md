# 可由四位数字构成的最大可能时间

> 原文:[https://www . geeksforgeeks . org/最大可能四位数形成时间/](https://www.geeksforgeeks.org/maximum-possible-time-that-can-be-formed-from-four-digits/)

给定一个数组 **arr[]** ，该数组只有 **4** 个整数位。任务是返回最大 **24 小时时间**，该时间可以使用数组中的数字形成。
**注意**24 小时格式的最短时间为 **00:00** ，最长时间为 **23:59** 。如果无法形成有效时间，则返回 **-1** 。
**举例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 23:41
> **输入:** arr[] = {5，5，6，6}
> **输出:** -1

**方法:**创建一个 HashMap，并在地图中存储每个数字的频率，这可以用来知道有多少这样的数字可用。
现在，为了生成有效时间，必须满足以下条件:

*   **小时的第一位数字**必须在**【0，2】**的范围内。按照递减顺序开始检查，以便最大化时间，即从 **2** 到 **0** 。一旦选择了数字，通过 **1** 减少其在地图中的出现。
*   **小时的第二位数字**必须在**【0，3】**范围内，如果第一位数字被选择为 **2** 否则**【0，9】**。选择数字后，相应地更新哈希表。
*   **分钟的第一位数字**必须来自范围**【0，5】**和**分钟的第二位数字**必须来自范围**【0，9】**。

如果上述任一条件失败，即在任何时候都不能选择数字，则打印 **-1** 否则打印时间。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the updated frequency map
// for the array passed as argument
map<int, int> getFrequencyMap(int arr[], int n)
{
    map<int, int> hashMap;
    for (int i = 0; i < n; i++) {

        hashMap[arr[i]]++;
    }
    return hashMap;
}

// Function that returns true if the passed digit is present
// in the map after decrementing it's frequency by 1
bool hasDigit(map<int, int>* hashMap, int digit)
{

    // If map contains the digit
    if ((*hashMap)[digit]) {

        // Decrement the frequency of the digit by 1
        (*hashMap)[digit]--;

        // True here indicates that the digit was found in the map
        return true;
    }

    // Digit not found
    return false;
}

// Function to return the maximum possible time_value in 24-Hours format
string getMaxtime_value(int arr[], int n)
{
    map<int, int> hashMap = getFrequencyMap(arr, n);
    int i;
    bool flag;
    string time_value = "";

    flag = false;

    // First digit of hours can be from the range [0, 2]
    for (i = 2; i >= 0; i--) {
        if (hasDigit(&hashMap, i)) {
            flag = true;
            time_value += (char)i + 48;
            break;
        }
    }

    // If no valid digit found
    if (!flag)
        return "-1";

    flag = false;

    // If first digit of hours was chosen as 2 then
    // the second digit of hours can be
    // from the range [0, 3]
    if (time_value[0] == '2') {
        for (i = 3; i >= 0; i--) {
            if (hasDigit(&hashMap, i)) {
                flag = true;
                time_value += (char)i + 48;
                break;
            }
        }
    }

    // Else it can be from the range [0, 9]
    else {
        for (i = 9; i >= 0; i--) {
            if (hasDigit(&hashMap, i)) {
                flag = true;
                time_value += (char)i + 48;
                break;
            }
        }
    }
    if (!flag)
        return "-1";

    // Hours and minutes separator
    time_value += ":";

    flag = false;

    // First digit of minutes can be from the range [0, 5]
    for (i = 5; i >= 0; i--) {
        if (hasDigit(&hashMap, i)) {
            flag = true;
            time_value += (char)i + 48;
            break;
        }
    }
    if (!flag)
        return "-1";

    flag = false;

    // Second digit of minutes can be from the range [0, 9]
    for (i = 9; i >= 0; i--) {
        if (hasDigit(&hashMap, i)) {
            flag = true;
            time_value += (char)i + 48;
            break;
        }
    }
    if (!flag)
        return "-1";

    // Return the maximum possible time_value
    return time_value;
}

// Driver code
int main()
{
    int arr[] = { 0, 0, 0, 9 };
    int n = sizeof(arr) / sizeof(int);
    cout << (getMaxtime_value(arr, n));
    return 0;
}
// contributed by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.util.*;

public class GFG {

    // Function to return the updated frequency map
    // for the array passed as argument
    static HashMap<Integer, Integer> getFrequencyMap(int arr[])
    {
        HashMap<Integer, Integer> hashMap = new HashMap<>();
        for (int i = 0; i < arr.length; i++) {
            if (hashMap.containsKey(arr[i])) {
                hashMap.put(arr[i], hashMap.get(arr[i]) + 1);
            }
            else {
                hashMap.put(arr[i], 1);
            }
        }
        return hashMap;
    }

    // Function that returns true if the passed digit is present
    // in the map after decrementing it's frequency by 1
    static boolean hasDigit(HashMap<Integer, Integer> hashMap, int digit)
    {

        // If map contains the digit
        if (hashMap.containsKey(digit) && hashMap.get(digit) > 0) {

            // Decrement the frequency of the digit by 1
            hashMap.put(digit, hashMap.get(digit) - 1);

            // True here indicates that the digit was found in the map
            return true;
        }

        // Digit not found
        return false;
    }

    // Function to return the maximum possible time in 24-Hours format
    static String getMaxTime(int arr[])
    {
        HashMap<Integer, Integer> hashMap = getFrequencyMap(arr);
        int i;
        boolean flag;
        String time = "";

        flag = false;

        // First digit of hours can be from the range [0, 2]
        for (i = 2; i >= 0; i--) {
            if (hasDigit(hashMap, i)) {
                flag = true;
                time += i;
                break;
            }
        }

        // If no valid digit found
        if (!flag) {
            return "-1";
        }

        flag = false;

        // If first digit of hours was chosen as 2 then
        // the second digit of hours can be
        // from the range [0, 3]
        if (time.charAt(0) == '2') {
            for (i = 3; i >= 0; i--) {
                if (hasDigit(hashMap, i)) {
                    flag = true;
                    time += i;
                    break;
                }
            }
        }

        // Else it can be from the range [0, 9]
        else {
            for (i = 9; i >= 0; i--) {
                if (hasDigit(hashMap, i)) {
                    flag = true;
                    time += i;
                    break;
                }
            }
        }
        if (!flag) {
            return "-1";
        }

        // Hours and minutes separator
        time += ":";

        flag = false;

        // First digit of minutes can be from the range [0, 5]
        for (i = 5; i >= 0; i--) {
            if (hasDigit(hashMap, i)) {
                flag = true;
                time += i;
                break;
            }
        }
        if (!flag) {
            return "-1";
        }

        flag = false;

        // Second digit of minutes can be from the range [0, 9]
        for (i = 9; i >= 0; i--) {
            if (hasDigit(hashMap, i)) {
                flag = true;
                time += i;
                break;
            }
        }
        if (!flag) {
            return "-1";
        }

        // Return the maximum possible time
        return time;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 0, 0, 0, 9 };
        System.out.println(getMaxTime(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import defaultdict

# Function to return the updated frequency
# map for the array passed as argument
def getFrequencyMap(arr, n):

    hashMap = defaultdict(lambda:0)
    for i in range(n):
        hashMap[arr[i]] += 1

    return hashMap

# Function that returns true if the passed
# digit is present in the map after
# decrementing it's frequency by 1
def hasDigit(hashMap, digit):

    # If map contains the digit
    if hashMap[digit] > 0:

        # Decrement the frequency of
        # the digit by 1
        hashMap[digit] -= 1

        # True here indicates that the
        # digit was found in the map
        return True

    # Digit not found
    return False

# Function to return the maximum possible
# time_value in 24-Hours format
def getMaxtime_value(arr, n):

    hashMap = getFrequencyMap(arr, n)
    flag = False
    time_value = ""

    # First digit of hours can be
    # from the range [0, 2]
    for i in range(2, -1, -1):
        if hasDigit(hashMap, i) == True:
            flag = True
            time_value += str(i)
            break

    # If no valid digit found
    if not flag:
        return "-1"

    flag = False

    # If first digit of hours was chosen as 2 then
    # the second digit of hours can be
    # from the range [0, 3]
    if(time_value[0] == '2'):
        for i in range(3, -1, -1):
            if hasDigit(hashMap, i) == True:
                flag = True
                time_value += str(i)
                break

    # Else it can be from the range [0, 9]
    else:
        for i in range(9, -1, -1):
            if hasDigit(hashMap, i) == True:
                flag = True
                time_value += str(i)
                break

    if not flag:
        return "-1"

    # Hours and minutes separator
    time_value += ":"

    flag = False

    # First digit of minutes can be
    # from the range [0, 5]
    for i in range(5, -1, -1):
        if hasDigit(hashMap, i) == True:
            flag = True
            time_value += str(i)
            break

    if not flag:
        return "-1"

    flag = False

    # Second digit of minutes can be
    # from the range [0, 9]
    for i in range(9, -1, -1):
        if hasDigit(hashMap, i) == True:
            flag = True
            time_value += str(i)
            break

    if not flag:
        return "-1"

    # Return the maximum possible
    # time_value
    return time_value

# Driver code
if __name__ == "__main__":

    arr = [0, 0, 0, 9]
    n = len(arr)
    print(getMaxtime_value(arr, n))

# This code is contributed by
# Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return the updated frequency map
    // for the array passed as argument
    static Dictionary<int, int> getFrequencyMap(int []arr)
    {
        Dictionary<int, int> hashMap = new Dictionary<int, int>();
        for (int i = 0; i < arr.Length; i++)
        {
            if (hashMap.ContainsKey(arr[i]))
            {
                hashMap[arr[i]] = hashMap[arr[i]] + 1;
            }
            else
            {
                hashMap.Add(arr[i], 1);
            }
        }
        return hashMap;
    }

    // Function that returns true if the passed digit is present
    // in the map after decrementing it's frequency by 1
    static bool hasDigit(Dictionary<int, int> hashMap, int digit)
    {

        // If map contains the digit
        if (hashMap.ContainsKey(digit) && hashMap[digit] > 0)
        {

            // Decrement the frequency of the digit by 1
            hashMap[digit] = hashMap[digit] - 1;

            // True here indicates that the
            // digit was found in the map
            return true;
        }

        // Digit not found
        return false;
    }

    // Function to return the maximum
    // possible time in 24-Hours format
    static String getMaxTime(int []arr)
    {
        Dictionary<int, int> hashMap = getFrequencyMap(arr);
        int i;
        bool flag;
        String time = "";

        flag = false;

        // First digit of hours can be from the range [0, 2]
        for (i = 2; i >= 0; i--)
        {
            if (hasDigit(hashMap, i))
            {
                flag = true;
                time += i;
                break;
            }
        }

        // If no valid digit found
        if (!flag)
        {
            return "-1";
        }

        flag = false;

        // If first digit of hours was chosen as 2 then
        // the second digit of hours can be
        // from the range [0, 3]
        if (time[0] == '2')
        {
            for (i = 3; i >= 0; i--)
            {
                if (hasDigit(hashMap, i))
                {
                    flag = true;
                    time += i;
                    break;
                }
            }
        }

        // Else it can be from the range [0, 9]
        else
        {
            for (i = 9; i >= 0; i--)
            {
                if (hasDigit(hashMap, i))
                {
                    flag = true;
                    time += i;
                    break;
                }
            }
        }
        if (!flag)
        {
            return "-1";
        }

        // Hours and minutes separator
        time += ":";

        flag = false;

        // First digit of minutes can be from the range [0, 5]
        for (i = 5; i >= 0; i--)
        {
            if (hasDigit(hashMap, i))
            {
                flag = true;
                time += i;
                break;
            }
        }
        if (!flag)
        {
            return "-1";
        }

        flag = false;

        // Second digit of minutes can be from the range [0, 9]
        for (i = 9; i >= 0; i--)
        {
            if (hasDigit(hashMap, i))
            {
                flag = true;
                time += i;
                break;
            }
        }
        if (!flag)
        {
            return "-1";
        }

        // Return the maximum possible time
        return time;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 0, 0, 0, 9 };
        Console.WriteLine(getMaxTime(arr));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

      // JavaScript implementation of the approach

      // Function to return the updated frequency map
      // for the array passed as argument
      function getFrequencyMap(arr) {
        var hashMap = {};
        for (var i = 0; i < arr.length; i++) {
          if (hashMap.hasOwnProperty(arr[i])) {
            hashMap[arr[i]] = hashMap[arr[i]] + 1;
          } else {
            hashMap[arr[i]] = 1;
          }
        }
        return hashMap;
      }

      // Function that returns true if the passed digit is present
      // in the map after decrementing it's frequency by 1
      function hasDigit(hashMap, digit) {
        // If map contains the digit
        if (hashMap.hasOwnProperty(digit) && hashMap[digit] > 0) {
          // Decrement the frequency of the digit by 1
          hashMap[digit] = hashMap[digit] - 1;

          // True here indicates that the
          // digit was found in the map
          return true;
        }

        // Digit not found
        return false;
      }

      // Function to return the maximum
      // possible time in 24-Hours format
      function getMaxTime(arr) {
        var hashMap = getFrequencyMap(arr);
        var i;
        var flag;
        var time = "";

        flag = false;

        // First digit of hours can be from the range [0, 2]
        for (i = 2; i >= 0; i--) {
          if (hasDigit(hashMap, i)) {
            flag = true;
            time += i;
            break;
          }
        }

        // If no valid digit found
        if (!flag) {
          return "-1";
        }

        flag = false;

        // If first digit of hours was chosen as 2 then
        // the second digit of hours can be
        // from the range [0, 3]
        if (time[0] === "2") {
          for (i = 3; i >= 0; i--) {
            if (hasDigit(hashMap, i)) {
              flag = true;
              time += i;
              break;
            }
          }
        }

        // Else it can be from the range [0, 9]
        else {
          for (i = 9; i >= 0; i--) {
            if (hasDigit(hashMap, i)) {
              flag = true;
              time += i;
              break;
            }
          }
        }
        if (!flag) {
          return "-1";
        }

        // Hours and minutes separator
        time += ":";

        flag = false;

        // First digit of minutes can be from the range [0, 5]
        for (i = 5; i >= 0; i--) {
          if (hasDigit(hashMap, i)) {
            flag = true;
            time += i;
            break;
          }
        }
        if (!flag) {
          return "-1";
        }

        flag = false;

        // Second digit of minutes can be from the range [0, 9]
        for (i = 9; i >= 0; i--) {
          if (hasDigit(hashMap, i)) {
            flag = true;
            time += i;
            break;
          }
        }
        if (!flag) {
          return "-1";
        }

        // Return the maximum possible time
        return time;
      }

      // Driver code
      var arr = [0, 0, 0, 9];
      document.write(getMaxTime(arr));

 </script>
```

**Output:** 

```
09:00
```

**时间复杂度:** O(n)

**辅助空间:** O(n)