# 通过向左移动数字最小次数

来最大化素数和非素数数组元素之和的差

> 原文:[https://www . geeksforgeeks . org/最大化素数和非素数数组元素之间的差值按位数左移最小次数/](https://www.geeksforgeeks.org/maximize-difference-between-sum-of-prime-and-non-prime-array-elements-by-left-shifting-of-digits-minimum-number-of-times/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是通过将数组元素的位数左移 1 个最小次数，找到[素数之和](https://www.geeksforgeeks.org/prime-numbers/)与数组中非素数之和之间的最大差值。

**示例:**

> **输入:** arr[] **=** {541，763，321，716，143}
> **输出:**差值= 631，操作数= 6
> **说明:**
> 操作 1:将 arr[1]的位数左移(= 763)。因此，arr[1]变为 637。
> 操作 2:左移 arr[1] (= 637)的位数。因此，arr[1]变为 376。
> 操作 3:左移 arr[2] (= 321)的位数。因此，arr[2]变为 213。
> 操作 4:左移 arr[2] (= 213)的位数。因此，arr[2]变为 132。
> 操作 5:左移 arr[3] (= 716)的位数。因此，arr[3]变为 167。
> 操作 6:左移 arr[4] (= 143)的位数。因此，arr[4]变为 431。
> 因此，素数组元素之和= 541 + 167 + 431 = 1139。
> 因此，非素数组元素之和= 376 + 132 = 508。
> 因此，差值= 1139–508 = 631。
> 
> **输入:** {396，361，359，496，780}
> **输出:**差值= 236，运算数= 4
> **说明:**
> 运算 1:将 arr[1]的位数左移(= 361)。因此，arr[1]变为 613。
> 操作 2:将 arr[2] (= 359)的数字左移。因此，arr[2]变为 593。
> 操作 3:左移 arr[4] (= 780)的位数。因此，arr[4]变为 807。
> 操作 4:将 arr[4] (= 807)的数字左移。因此，arr[4]变为 078。
> 因此，要求差= 613+593–496–78–396 = 236。

**进场:**给定的问题可以解决[贪婪的](https://www.geeksforgeeks.org/greedy-algorithms/)。如果可以将一个元素转换成一个或多个[质数](https://www.geeksforgeeks.org/prime-numbers/)，则取其中的最大值。否则，尝试使用所有可能的旋转来最小化元素。
按照以下步骤解决问题:

*   初始化两个变量，比如 **ans** 和 **cost，**分别存储所需的最大差值和最小运算次数。
*   使用变量 **i** 遍历数组 **arr[]** ，并执行以下步骤:
    *   将变量 **maxPrime** 和 **minRotation** 初始化为 **-1** ，以存储从**arr【I】**通过左旋转可以获得的最大素数和最小数。
    *   [生成所有左旋转的数字](https://www.geeksforgeeks.org/generate-all-rotations-of-a-number/)**arr【I】**。
        *   [如果**arr【I】**是一个超过 **maxPrime** 的素数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)，那么更新 **maxPrime** 为**arr【I】**，相应的**费用**。
    *   如果 **maxPrime** 的值保持不变，则通过类似地生成所有左旋转来找到 **minRotation** 的值。
    *   将**arr【I】**的值加到 **ans** 上。
*   完成以上步骤后，打印 **ans** 和 **cost** 的值作为结果。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a
// number is prime or not
bool isPrime(int n)
{

    // Base cases
    if (n <= 1)
        return false;
    if (n <= 3)
        return true;

    // Check if the number is
    // a multiple of 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
        return false;

    int i = 5;

    // Iterate until square root of n
    while (i * i <= n) {

        // If n is divisible by both i and i + 2
        if (n % i == 0 || n % (i + 2) == 0)
            return false;
        i = i + 6;
    }
    return true;
}

// Function to left shift a number
// to maximize its contribution
pair<int, int> rotateElement(int n)
{

    // Convert the number to string
    string strN = to_string(n);

    // Stores the maximum prime number
    // that can be obtained from n
    int maxPrime = -1;

    // Store the required
    // number of operations
    int cost = 0;

    string temp = strN;

    // Check for all the left
    // rotations of the number
    for (int i = 0; i < strN.size(); i++) {

        // If the number is prime, then
        // take the maximum among them
        if (isPrime(stoi(temp)) && stoi(temp) > maxPrime) {
            maxPrime = stoi(temp);
            cost = i;
        }

        // Left rotation
        temp = temp.substr(1) + temp[0];
    }

    int optEle = maxPrime;

    // If no prime number can be obtained
    if (optEle == -1) {
        optEle = INT_MAX;
        temp = strN;

        // Check all the left
        // rotations of the number
        for (int i = 0; i < strN.size(); i++) {

            // Take the minimum element
            if (stoi(temp) < optEle) {
                optEle = stoi(temp);
                cost = i;
            }

            // Left rotation
            temp = temp.substr(1) + temp[0];
        }
        optEle *= (-1);
    }

    return { optEle, cost };
}

// Function to find the maximum sum
// obtained using the given operations
void getMaxSum(int arr[], int N)
{

    // Store the maximum sum and
    // the number of operations
    int maxSum = 0, cost = 0;

    // Traverse array elements
    for (int i = 0; i < N; i++) {
        int x = arr[i];

        // Get the optimal element and the
        // number of operations to obtain it
        pair<int, int> ret = rotateElement(x);

        int optEle = ret.first, optCost = ret.second;

        // Increment the maximum difference
        // and number of operations required
        maxSum += optEle;
        cost += optCost;
    }

    // Print the result
    cout << "Difference = " << maxSum << " , "
         << "Count of operations = " << cost;
}

// Driven Program
int main()
{
    // Given array arr[]
    int arr[] = { 541, 763, 321, 716, 143 };

    // Store the size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    getMaxSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

    // Function to check if a
    // number is prime or not
    static boolean isPrime(int n)
    {

        // Base cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // Check if the number is
        // a multiple of 2 or 3
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        int i = 5;

        // Iterate until square root of n
        while (i * i <= n) {

            // If n is divisible by both i and i + 2
            if (n % i == 0 || n % (i + 2) == 0)
                return false;
            i = i + 6;
        }
        return true;
    }

    // Function to left shift a number
    // to maximize its contribution
    static int[] rotateElement(int n)
    {

        // Convert the number to string
        String strN = Integer.toString(n);

        // Stores the maximum prime number
        // that can be obtained from n
        int maxPrime = -1;

        // Store the required
        // number of operations
        int cost = 0;

        String temp = strN;

        // Check for all the left
        // rotations of the number
        for (int i = 0; i < strN.length(); i++) {

            // If the number is prime, then
            // take the maximum among them
            if (isPrime(Integer.parseInt(temp))
                && Integer.parseInt(temp) > maxPrime) {
                maxPrime = Integer.parseInt(temp);
                cost = i;
            }

            // Left rotation
            temp = temp.substring(1) + temp.charAt(0);
        }

        int optEle = maxPrime;

        // If no prime number can be obtained
        if (optEle == -1) {
            optEle = Integer.MAX_VALUE;
            temp = strN;

            // Check all the left
            // rotations of the number
            for (int i = 0; i < strN.length(); i++) {

                // Take the minimum element
                if (Integer.parseInt(temp) < optEle) {
                    optEle = Integer.parseInt(temp);
                    cost = i;
                }

                // Left rotation
                temp = temp.substring(1) + temp.charAt(0);
            }
            optEle *= (-1);
        }
        return new int[] { optEle, cost };
    }

    // Function to find the maximum sum
    // obtained using the given operations
    static void getMaxSum(int arr[])
    {

        // Store the maximum sum and
        // the number of operations
        int maxSum = 0, cost = 0;

        // Traverse array elements
        for (int x : arr) {

            // Get the optimal element and the
            // number of operations to obtain it
            int ret[] = rotateElement(x);

            int optEle = ret[0], optCost = ret[1];

            // Increment the maximum difference
            // and number of operations required
            maxSum += optEle;
            cost += optCost;
        }

        // Print the result
        System.out.println("Difference = " + maxSum + " , "
                           + "Count of operations = "
                           + cost);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given array arr[]
        int arr[] = { 541, 763, 321, 716, 143 };

        // Function call
        getMaxSum(arr);
    }
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check if a
# number is prime or not
def isPrime(n):

    # Base cases
    if (n <= 1):
        return False
    if (n <= 3):
        return True

    # Check if the number is
    # a multiple of 2 or 3
    if (n % 2 == 0 or n % 3 == 0):
        return False

    i = 5

    # Iterate until square root of n
    while(i * i <= n):

        # If n is divisible by both i and i + 2
        if (n % i == 0 or n % (i + 2) == 0):
            return False
        i = i + 6

    return True

# Function to left shift a number
# to maximize its contribution
def rotateElement(n):

        # Convert the number to string
    strN = str(n)

    # Stores the maximum prime number
    # that can be obtained from n
    maxPrime = -1

    # Store the required
    # number of operations
    cost = 0

    temp = str(strN)

    # Check for all the left
    # rotations of the number
    for i in range(len(strN)):

        # If the number is prime, then
        # take the maximum among them
        if isPrime(int(temp)) and int(temp) > maxPrime:
            maxPrime = int(temp)
            cost = i

        # Left rotation
        temp = temp[1:]+temp[:1]

    optEle = maxPrime

    # If no prime number can be obtained
    if optEle == -1:
        optEle = float('inf')
        temp = str(strN)

        # Check all the left
        # rotations of the number
        for i in range(len(strN)):

            # Take the minimum element
            if int(temp) < optEle:
                optEle = int(temp)
                cost = i

            # Left rotation
            temp = temp[1:]+temp[:1]
        optEle *= (-1)

    return (optEle, cost)

# Function to find the maximum sum
# obtained using the given operations
def getMaxSum(arr):

    # Store the maximum sum and
    # the number of operations
    maxSum, cost = 0, 0

    # Traverse array elements
    for x in arr:

        # Get the optimal element and the
        # number of operations to obtain it
        optEle, optCost = rotateElement(x)

        # Increment the maximum difference
        # and number of operations required
        maxSum += optEle
        cost += optCost

    # Print the result
    print('Difference =', maxSum, ',',
          'Count of operations =', cost)

# Driver Code

arr = [541, 763, 321, 716, 143]
getMaxSum(arr)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;                   

class GFG {

  // Function to check if a
  // number is prime or not
  static bool isPrime(int n)
  {

    // Base cases
    if (n <= 1)
      return false;
    if (n <= 3)
      return true;

    // Check if the number is
    // a multiple of 2 or 3
    if (n % 2 == 0 || n % 3 == 0)
      return false;

    int i = 5;

    // Iterate until square root of n
    while (i * i <= n) {

      // If n is divisible by both i and i + 2
      if (n % i == 0 || n % (i + 2) == 0)
        return false;
      i = i + 6;
    }
    return true;
  }

  // Function to left shift a number
  // to maximize its contribution
  static int[] rotateElement(int n)
  {

    // Convert the number to string
    string strN = n.ToString();

    // Stores the maximum prime number
    // that can be obtained from n
    int maxPrime = -1;

    // Store the required
    // number of operations
    int cost = 0;

    string temp = strN;

    // Check for all the left
    // rotations of the number
    for (int i = 0; i < strN.Length; i++) {

      // If the number is prime, then
      // take the maximum among them
      if (isPrime(Int32.Parse(temp))
          &&  Int32.Parse(temp) > maxPrime) {
        maxPrime =  Int32.Parse(temp);
        cost = i;
      }

      // Left rotation
      temp = temp.Substring(1) + temp[0];
    }

    int optEle = maxPrime;

    // If no prime number can be obtained
    if (optEle == -1) {
      optEle = 2147483647;
      temp = strN;

      // Check all the left
      // rotations of the number
      for (int i = 0; i < strN.Length; i++) {

        // Take the minimum element
        if (Int32.Parse(temp) < optEle) {
          optEle = Int32.Parse(temp);
          cost = i;
        }

        // Left rotation
        temp = temp.Substring(1) + temp[0];
      }
      optEle *= (-1);
    }
    return new int[] { optEle, cost };
  }

  // Function to find the maximum sum
  // obtained using the given operations
  static void getMaxSum(int []arr)
  {

    // Store the maximum sum and
    // the number of operations
    int maxSum = 0, cost = 0;

    // Traverse array elements
    foreach (int x in arr) {

      // Get the optimal element and the
      // number of operations to obtain it
      int[] ret = rotateElement(x);

      int optEle = ret[0], optCost = ret[1];

      // Increment the maximum difference
      // and number of operations required
      maxSum += optEle;
      cost += optCost;
    }

    // Print the result
    Console.Write("Difference = " + maxSum + " , "+ "Count of operations = "
                  + cost);
  }

  // Driver Code
  public static void Main()
  {

    // Given array arr[]
    int []arr = { 541, 763, 321, 716, 143 };

    // Function call
    getMaxSum(arr);
  }
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

    // JavaScript program for the above approach

    // Function to check if a
    // number is prime or not
    function isPrime(n)
    {

        // Base cases
        if (n <= 1)
            return false;
        if (n <= 3)
            return true;

        // Check if the number is
        // a multiple of 2 or 3
        if (n % 2 == 0 || n % 3 == 0)
            return false;

        let i = 5;

        // Iterate until square root of n
        while (i * i <= n) {

            // If n is divisible by both i and i + 2
            if (n % i == 0 || n % (i + 2) == 0)
                return false;
            i = i + 6;
        }
        return true;
    }

    // Function to left shift a number
    // to maximize its contribution
    function rotateElement(n)
    {

        // Convert the number to string
        let strN = n.toString();

        // Stores the maximum prime number
        // that can be obtained from n
        let maxPrime = -1;

        // Store the required
        // number of operations
        let cost = 0;

        let temp = strN;

        // Check for all the left
        // rotations of the number
        for (let i = 0; i < strN.length; i++) {

            // If the number is prime, then
            // take the maximum among them
            if (isPrime(parseInt(temp)) && parseInt(temp) > maxPrime)
            {
                maxPrime = parseInt(temp);
                cost = i;
            }

            // Left rotation
            temp = temp.substr(1) + temp[0];
        }

        let optEle = maxPrime;

        // If no prime number can be obtained
        if (optEle == -1) {
            optEle = Number.MAX_VALUE;
            temp = strN;

            // Check all the left
            // rotations of the number
            for (let i = 0; i < strN.length; i++) {

                // Take the minimum element
                if (parseInt(temp) < optEle) {
                    optEle = parseInt(temp);
                    cost = i;
                }

                // Left rotation
                temp = temp.substr(1) + temp[0];
            }
            optEle *= (-1);
        }

        return [ optEle, cost ];
    }

    // Function to find the maximum sum
    // obtained using the given operations
    function getMaxSum(arr,N)
    {

        // Store the maximum sum and
        // the number of operations
        let maxSum = 0, cost = 0;

        // Traverse array elements
        for (let i = 0; i < N; i++) {
            let x = arr[i];

            // Get the optimal element and the
            // number of operations to obtain it
            let ret = rotateElement(x);

            let optEle = ret[0], optCost = ret[1];

            // Increment the maximum difference
            // and number of operations required
            maxSum += optEle;
            cost += optCost;
        }

        // Print the result
         document.write("Difference = " + maxSum + " , "
            + "Count of operations = " + cost);
    }

    // Driven Program

    // Given array arr[]
    let arr = [ 541, 763, 321, 716, 143 ];

    // Store the size of the array
    let N = arr.length

    // Function call
    getMaxSum(arr, N);

</script>
```

**Output:** 

```
Difference = 631 , Count of operations = 6
```

***时间复杂度:** O(N*√X*log(X))，其中 **X** 是数组中最大的* [*元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)
***辅助空间:** O(1)*