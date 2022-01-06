# 字母和数字字符数量相等的最长子数组

> 原文:[https://www . geesforgeks . org/字母和数字字符数相等的最长子数组/](https://www.geeksforgeeks.org/longest-sub-array-with-equal-number-of-alphabets-and-numeric-characters/)

给定一组字母数字字符。任务是找到字母(字母)和数字(数字)数量相等的最长连续子数组。打印该子数组的开始和结束索引。如果有多个结果，输出起始索引最低的结果。
**例:**

> **输入:** arr[] = {'A '，' B '，' X '，' 4 '，' 6 '，' X '，' a'}
> **输出:** 1 4
> 所需子数组为{'B '，' X '，' 4 '，' 6'}。
> {'X '，' 4 '，' 6 '，' X'}也是最大
> 长度的有效子数组，但其起始索引不是最小的。
> **输入:** arr[] = {'1 '，' 2 '，' a '，' b '，' c '，' 1 '，' n '，' c '，' 1 '，' 2'}
> **输出:** 0 9

**处理方法:**我们要考虑到所有的数字都可以一样处理(也就是说 0 和 5 可以一样处理，但是 0 和‘a’不能一样处理)，同样所有的字母也可以用类似的方法一样处理。所以我们遍历数组，用“0”替换每个字母，用“1”替换每个数字。
这个问题就简化为。
为了符合这个问题，修改了上面算法的代码后，我们想出了下面的代码来解决这个问题。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the starting and the
// ending index of the sub-array with equal
// number of alphabets and numeric digits
void findSubArray(int arr[], int n)
{
    int sum = 0;
    int maxsize = -1, startindex;
    for (int i = 0; i < n; i++) {

        // If its an alphabet
        if (isalpha(arr[i])) {
            arr[i] = 0;
        }

        // Else its a number
        else {
            arr[i] = 1;
        }
    }

    // Pick a starting point as i
    for (int i = 0; i < n - 1; i++) {
        sum = (arr[i] == 0) ? -1 : 1;

        // Consider all sub-arrays starting from i
        for (int j = i + 1; j < n; j++) {
            (arr[j] == 0) ? (sum += -1) : (sum += 1);

            // If this is a 0 sum sub-array then
            // compare it with maximum size sub-array
            // calculated so far
            if (sum == 0 && maxsize < j - i + 1) {
                maxsize = j - i + 1;
                startindex = i;
            }
        }
    }

    // If no valid sub-array found
    if (maxsize == -1)
        cout << maxsize;
    else
        cout << startindex << " " << (startindex + maxsize - 1);
}

// Driver code
int main()
{
    int arr[] = { 'A', 'B', 'X', 4, 6, 'X', 'a' };
    int size = sizeof(arr) / sizeof(arr[0]);

    findSubArray(arr, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    static boolean isalpha(int input_char)
    {
        if ((input_char >= 65 && input_char <= 90)
            || (input_char >= 97 && input_char <= 122))
            return true;

        return false;
    }

    // Function to find the starting and the
    // ending index of the sub-array with equal
    // number of alphabets and numeric digits
    static void findSubArray(int arr[], int n)
    {
        int sum = 0;
        int maxsize = -1, startindex = 0;
        for (int i = 0; i < n; i++)
        {

            // If its an alphabet
            if (isalpha(arr[i]))
            {
                arr[i] = 0;
            }

            // Else its a number
            else
            {
                arr[i] = 1;
            }
        }

        // Pick a starting point as i
        for (int i = 0; i < n - 1; i++)
        {
            sum = (arr[i] == 0) ? -1 : 1;

            // Consider all sub-arrays starting from i
            for (int j = i + 1; j < n; j++)
            {
                if(arr[j] == 0)
                    sum += -1;
                else
                    sum += 1;

                // If this is a 0 sum sub-array then
                // compare it with maximum size sub-array
                // calculated so far
                if (sum == 0 && maxsize < j - i + 1)
                {
                    maxsize = j - i + 1;
                    startindex = i;
                }
            }
        }

        // If no valid sub-array found
        if (maxsize == -1)
            System.out.println(maxsize);
        else
            System.out.println(startindex + " " + (startindex + maxsize - 1));
    }

    // Driver code
    public static void main (String[] args)
    {

        int arr[] = { 'A', 'B', 'X', 4, 6, 'X', 'a' };
        int size = arr.length;

        findSubArray(arr, size);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the starting and the
# ending index of the sub-array with equal
# number of alphabets and numeric digits
def findSubArray(arr, n):
    sum = 0
    maxsize = -1
    startindex=0
    for i in range(n):

        # If its an alphabet
        if (arr[i].isalpha()):
            arr[i] = 0

        # Else its a number
        else :
            arr[i] = 1

    # Pick a starting poas i
    for i in range(n-1):
        if arr[i]=='1':
            sum=1
        else:
            sum=-1   

        # Consider all sub-arrays starting from i
        for j in range(i+1,n):
            if arr[j]==0:
                sum-=1
            else:
                sum+=1   

            # If this is a 0 sum sub-array then
            # compare it with maximum size sub-array
            # calculated so far
            if (sum == 0 and maxsize < j - i + 1) :
                maxsize = j - i + 1
                startindex = i

    # If no valid sub-array found
    if (maxsize == -1):
        print(maxsize,end=" ")
    else:
        print(startindex,(startindex + maxsize - 1))

# Driver code
arr=['A', 'B', 'X', '4', '6', 'X', 'a']
size =len(arr)

findSubArray(arr, size)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

    static bool isalpha(int input_char)
    {
        if ((input_char >= 65 && input_char <= 90)
            || (input_char >= 97 && input_char <= 122))
            return true;

        return false;
    }

    // Function to find the starting and the
    // ending index of the sub-array with equal
    // number of alphabets and numeric digits
    static void findSubArray(int []arr, int n)
    {
        int sum = 0;
        int maxsize = -1, startindex = 0;
        for (int i = 0; i < n; i++)
        {

            // If its an alphabet
            if (isalpha(arr[i]))
            {
                arr[i] = 0;
            }

            // Else its a number
            else
            {
                arr[i] = 1;
            }
        }

        // Pick a starting point as i
        for (int i = 0; i < n - 1; i++)
        {
            sum = (arr[i] == 0) ? -1 : 1;

            // Consider all sub-arrays starting from i
            for (int j = i + 1; j < n; j++)
            {
                if(arr[j] == 0)
                    sum += -1;
                else
                    sum += 1;

                // If this is a 0 sum sub-array then
                // compare it with maximum size sub-array
                // calculated so far
                if (sum == 0 && maxsize < j - i + 1)
                {
                    maxsize = j - i + 1;
                    startindex = i;
                }
            }
        }

        // If no valid sub-array found
        if (maxsize == -1)
            Console.WriteLine(maxsize);
        else
        Console.WriteLine(startindex + " " + (startindex + maxsize - 1));
    }

    // Driver code
    public static void Main()
    {

        int []arr = { 'A', 'B', 'X', 4, 6, 'X', 'a' };
        int size = arr.Length;

        findSubArray(arr, size);
    }
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    function isalpha(input_char)
    {
        if ((input_char >= 65 && input_char <= 90)
            || (input_char >= 97 && input_char <= 122))
            return true;

        return false;
    }

    // Function to find the starting and the
    // ending index of the sub-array with equal
    // number of alphabets and numeric digits
    function findSubArray(arr, n)
    {
        let sum = 0;
        let maxsize = -1, startindex = 0;
        for (let i = 0; i < n; i++)
        {

            // If its an alphabet
            if (isalpha(arr[i].charCodeAt()))
            {
                arr[i] = 0;
            }

            // Else its a number
            else
            {
                arr[i] = 1;
            }
        }

        // Pick a starting point as i
        for (let i = 0; i < n - 1; i++)
        {
            sum = (arr[i] == 0) ? -1 : 1;

            // Consider all sub-arrays starting from i
            for (let j = i + 1; j < n; j++)
            {
                if(arr[j] == 0)
                    sum += -1;
                else
                    sum += 1;

                // If this is a 0 sum sub-array then
                // compare it with maximum size sub-array
                // calculated so far
                if (sum == 0 && maxsize < j - i + 1)
                {
                    maxsize = j - i + 1;
                    startindex = i;
                }
            }
        }

        // If no valid sub-array found
        if (maxsize == -1)
            document.write(maxsize + "</br>");
        else
            document.write(startindex + " " + (startindex + maxsize - 1) + "</br>");
    }

    let arr = [ 'A', 'B', 'X', '4', '6', 'X', 'a' ];
    let size = arr.length;

    findSubArray(arr, size);

</script>
```

**Output:** 

```
1 4
```