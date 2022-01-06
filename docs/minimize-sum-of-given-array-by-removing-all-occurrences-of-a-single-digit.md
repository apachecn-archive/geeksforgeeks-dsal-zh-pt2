# 通过移除所有出现的单个数字来最小化给定数组的和

> 原文:[https://www . geeksforgeeks . org/通过移除所有出现的一位数来最小化给定数组的总和/](https://www.geeksforgeeks.org/minimize-sum-of-given-array-by-removing-all-occurrences-of-a-single-digit/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过移除单个数字的所有出现来最小化总和。

**示例:**

> **输入:** arr[] = {34，23，85，93}
> **输出:** 100
> **解释:**从数组的每个元素中删除数字 3 的出现将 arr[]修改为{4，2，85，9}。因此，数组的最小和= 4 + 2 + 85 + 9 = 100。
> 
> **输入:** arr[] = {434，863，342，121 }
> T3】输出: 293

**方法:**思路是将每个可能数字(**【0，9】**)的所有出现逐一去除，并计算去除每个数字后的数组的[和。最后，求这些和的最小值。按照以下步骤解决问题:](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

*   初始化一个变量，比如说 **minSum** ，存储最小和， **curSum** 存储去掉一个数字的所有出现后得到的和。
*   迭代范围**【0，9】**中的数字，并执行以下操作:
    *   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并通过移除每个数字来检查最小和。
    *   从字符串中删除数字后，将字符串转换回整数，并将其添加到**光标**中。
    *   每次迭代后更新 **minSum** 的值。
*   打印 **minSum** 的值作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for super ugly number
#include<bits/stdc++.h>
using namespace std;

// Function to remove each digit
// from the given integer
int remove(int N, int digit)
{

    // Convert into string
    string strN = to_string(N);

    // Stores final string
    string ans = "";

    // Traverse the string
    for (char i:strN)
    {
        if ((i - '0') == digit)
        {
            continue;
        }

        // Append it to the
        // final string
        ans += i;
      }

    // Return integer value
    return stoi(ans);
}

// Function to find the minimum sum by
// removing occurences of each digit
void getMin(vector<int> arr)
{
    int minSum = INT_MAX;

    // Iterate in range [0, 9]
    for (int i = 0; i < 10; i++)
    {
        int curSum = 0;

        // Traverse the array
        for (int num :arr)
            curSum += remove(num, i);

        // Update the minimum sum
        minSum = min(minSum, curSum);
      }

    // Print the minimized sum
    cout << minSum;
}

/* Driver program to test above functions */
int main()
{
  vector<int> arr = {34, 23, 85, 93};
  getMin(arr);
  return 0;
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to remove each digit
// from the given integer
static int remove(int N, int digit)
{

    // Convert into string
    String strN = String.valueOf(N);

    // Stores final string
    String ans = "";

    // Traverse the string
    for (char i:strN.toCharArray())
    {
        if ((i - '0') == digit)
        {
            continue;
        }

        // Append it to the
        // final string
        ans += i;
      }

    // Return integer value
    return Integer.parseInt(ans);
}

// Function to find the minimum sum by
// removing occurences of each digit
static void getMin(int[] arr)
{
    int minSum = Integer.MAX_VALUE;

    // Iterate in range [0, 9]
    for (int i = 0; i < 10; i++)
    {
        int curSum = 0;

        // Traverse the array
        for (int num :arr)
            curSum += remove(num, i);

        // Update the minimum sum
        minSum = Math.min(minSum, curSum);
      }

    // Print the minimized sum
    System.out.print(minSum);
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = {34, 23, 85, 93};
    getMin(arr);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to remove each digit
# from the given integer
def remove(N, digit):

    # Convert into string
    strN = str(N)

    # Stores final string
    ans = ''

    # Traverse the string
    for i in strN:
        if int(i) == digit:
            continue

        # Append it to the
        # final string
        ans += i

    # Return integer value
    return int(ans)

# Function to find the minimum sum by
# removing occurences of each digit
def getMin(arr):
    minSum = float('inf')

    # Iterate in range [0, 9]
    for i in range(10):
        curSum = 0

        # Traverse the array
        for num in arr:
            curSum += remove(num, i)

        # Update the minimum sum
        minSum = min(minSum, curSum)

    # Print the minimized sum
    print(minSum)

# Given array
arr = [34, 23, 85, 93]
getMin(arr)
```

## C#

```
using System;
public class GFG
{

  // Function to remove each digit
  // from the given integer
  static int remove(int N, int digit)
  {

    // Convert into string
    String strN = N.ToString();

    // Stores final string
    String ans = "";

    // Traverse the string
    foreach(char i in strN.ToCharArray())
    {
      if ((i - '0') == digit)
      {
        continue;
      }

      // Append it to the
      // final string
      ans += i;
    }

    // Return integer value
    return Int32.Parse(ans);
  }

  // Function to find the minimum sum by
  // removing occurences of each digit
  static void getMin(int[] arr)
  {
    int minSum = Int32.MaxValue;

    // Iterate in range [0, 9]
    for (int i = 0; i < 10; i++)
    {
      int curSum = 0;

      // Traverse the array
      foreach(int num in arr)
        curSum += remove(num, i);

      // Update the minimum sum
      minSum = Math.Min(minSum, curSum);
    }

    // Print the minimized sum
    Console.WriteLine(minSum);
  }

  // Driver Code
  static public void Main (){

    int[] arr = {34, 23, 85, 93};
    getMin(arr);
  }
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

// Javascript program for super ugly number

// Function to remove each digit
// from the given integer
function remove(N, digit)
{

    // Convert into string
    var strN = N.toString();

    // Stores final string
    var ans = "";

    var i;
    // Traverse the string
    for(i=0;i<strN.length;i++){
        if ((strN.charCodeAt(i) - 48) == digit)
        {
            continue;
        }

        // Append it to the
        // final string
        ans += strN[i];
    }

    // Return integer value
    return parseInt(ans);
}

// Function to find the minimum sum by
// removing occurences of each digit
function getMin(arr)
{
    var minSum = 1000000000;

    var i,j;
    // Iterate in range [0, 9]
    for (i = 0; i < 10; i++)
    {
        var curSum = 0;

        // Traverse the array
        for(j=0;j<arr.length;j++){
           curSum += remove(arr[j], i);
        }

        // Update the minimum sum
        minSum = Math.min(minSum, curSum);
      }

    // Print the minimized sum
    document.write(minSum);
}

/* Driver program to test above functions */

  var arr = [34, 23, 85, 93];
  getMin(arr);

</script>
```

**Output:** 

```
100
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)