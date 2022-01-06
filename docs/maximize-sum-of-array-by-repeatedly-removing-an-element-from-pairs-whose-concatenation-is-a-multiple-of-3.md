# 通过从串联倍数为 3 的对中重复移除一个元素来最大化数组的和

> 原文:[https://www . geeksforgeeks . org/通过重复从其串联是 3 的倍数的对中移除元素来最大化数组的和/](https://www.geeksforgeeks.org/maximize-sum-of-array-by-repeatedly-removing-an-element-from-pairs-whose-concatenation-is-a-multiple-of-3/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是在重复删除串联[是 **3**](https://www.geeksforgeeks.org/write-an-efficient-method-to-check-if-a-number-is-multiple-of-3/) 倍数的两个元素后，找到剩余数组元素的最大可能和。

**示例:**

> **输入:** arr[] = {23，12，43，3，56}
> **输出:** 91
> **解释:**
> 最初数组为{23，12，43，3，56}。执行以下阵列元素移除:
> 
> *   **对{23，43}:** 串联= 2343，可被 3 整除。现在，移除 43 会将数组修改为{23，12，3，56}。
> *   **对{12，3}:** 串联= 123，可被 3 整除。现在，删除 3 会将数组修改为{23，12，56}。
> 
> 经过以上运算，数组元素的和= 12 + 56 + 23 = 91。
> 
> **输入:** arr[] = {324，32，53，67，330 }
> T3】输出: 415

**方法:**利用一个数的余数被 **3** 除时，等于其位数之和被 **3** 除时的余数，可以解决给定的问题。按照以下步骤解决问题:

*   初始化三个变量，比如 **maxRem0** 、 **maxRem1** 和 **maxRem2** ，将有余数的元素分别存储为 **0** 、 **1** 和 **2** 。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   初始化一个变量， **digitSum** 存储数字和。
    *   如果 **digitSum % 3 == 0** ，则将 **maxRem0** 的值更新为 **max(maxRem0，arr[i])** 。
    *   否则，如果余数为 **1** 或 **2** ，则
*   完成上述步骤后，打印 **maxRem0** 之和以及 **maxRem1** 和 **maxRem2** 的最大值作为结果。

下面是上述方法的实现:

## C++

```
// C++ approach for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate sum
// of digits of an integer
int getSum(int n)
{
    int ans = 0;

    // char[] arr = (String.valueOf(n)).toCharArray();
    string arr = to_string(n);
    for(int i = 0; i < arr.length(); i++)
    {
        ans += int(arr[i]);
    }
    return ans;
}

// Function to calculate maximum sum
// of array after removing pairs whose
// concatenation is divisible by 3
void getMax(int arr[], int n)
{

    // Stores the sum of
    // digits of array element
    int maxRem0 = 0;

    int rem1 = 0;
    int rem2 = 0;

    for(int i = 0; i < n; i++)
    {

        // Find the sum of digits
        int digitSum = getSum(arr[i]);

        // If i is divisible by 3
        if (digitSum % 3 == 0)
            maxRem0 = max(maxRem0, arr[i]);

        // Otherwise, if i modulo 3 is 1
        else if (digitSum % 3 == 1)
            rem1 += arr[i];

        // Otherwise, if i modulo 3 is 2
        else
            rem2 += arr[i];
    }

    // Return the resultant
    // sum of array elements
    cout << (maxRem0 + max(rem1, rem2));
}

// Driver Code
int main()
{
    int arr[] = { 23, 12, 43, 3, 56 };
    int n = sizeof(arr) / sizeof(arr[0]);

    getMax(arr, n);
}

// This code is contributed by ukasp
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java approach for the above approach
class GFG{

// Function to calculate sum
// of digits of an integer
static int getSum(int n)
{
    int ans = 0;
    char[] arr = (String.valueOf(n)).toCharArray();

    for(char ch : arr)
    {
        ans += Character.getNumericValue(ch);
    }
    return ans;
}

// Function to calculate maximum sum
// of array after removing pairs whose
// concatenation is divisible by 3
static void getMax(int[] arr)
{

    // Stores the sum of
    // digits of array element
    int maxRem0 = 0;

    int rem1 = 0;
    int rem2 = 0;

    for(int i:arr)
    {

        // Find the sum of digits
        int digitSum = getSum(i);

        // If i is divisible by 3
        if (digitSum % 3 == 0)
            maxRem0 = Math.max(maxRem0, i);

        // Otherwise, if i modulo 3 is 1
        else if (digitSum % 3 == 1)
            rem1 += i;

        // Otherwise, if i modulo 3 is 2
        else
            rem2 += i;
    }

    // Return the resultant
    // sum of array elements
    System.out.print(maxRem0 +
                     Math.max(rem1, rem2));
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 23, 12, 43, 3, 56 };
    getMax(arr);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate sum
# of digits of an integer
def getSum(n):
  ans = 0
  for i in str(n):
    ans += int(i)

  return ans

# Function to calculate maximum sum
# of array after removing pairs whose
# concatenation is divisible by 3
def getMax(arr):

    # Stores the sum of
    # digits of array element
    maxRem0 = 0

    rem1 = 0
    rem2 = 0

    for i in arr:

        # Find the sum of digits
        digitSum = getSum(i)

        # If i is divisible by 3
        if digitSum % 3 == 0:
            maxRem0 = max(maxRem0, i)

        # Otherwise, if i modulo 3 is 1
        elif digitSum % 3 == 1:
            rem1 += i

        # Otherwise, if i modulo 3 is 2
        else:
            rem2 += i

    # Return the resultant
    # sum of array elements
    print( maxRem0 + max(rem1, rem2))

# Driver Code

# Given array
arr = [ 23, 12, 43, 3, 56 ]
getMax(arr)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate sum
// of digits of an integer
static int getSum(int n)
{
    int ans = 0;
    string str = n.ToString();
    Char[] arr = str.ToCharArray();

    foreach(Char ch in arr)
    {
        ans += (int)Char.GetNumericValue(ch);
    }
    return ans;
}

// Function to calculate maximum sum
// of array after removing pairs whose
// concatenation is divisible by 3
static void getMax(int[] arr)
{

    // Stores the sum of
    // digits of array element
    int maxRem0 = 0;

    int rem1 = 0;
    int rem2 = 0;

    foreach(int i in arr)
    {

        // Find the sum of digits
        int digitSum = getSum(i);

        // If i is divisible by 3
        if (digitSum % 3 == 0)
            maxRem0 = Math.Max(maxRem0, i);

        // Otherwise, if i modulo 3 is 1
        else if (digitSum % 3 == 1)
            rem1 += i;

        // Otherwise, if i modulo 3 is 2
        else
            rem2 += i;
    }

    // Return the resultant
    // sum of array elements
    Console.WriteLine(maxRem0 +
                     Math.Max(rem1, rem2));
}

// Driver Code
static void Main()
{
    int[] arr = { 23, 12, 43, 3, 56 };
    getMax(arr);
}
}

// This code is contributed by souravghosh0416.
```

## java 描述语言

```
<script>

        // Javascript program for the
        // above approach

        // Function to calculate sum
        // of digits of an integer
        function getSum(n) {
            let ans = 0;

            let arr = n.toString();
            for (let i = 0; i < arr.length; i++)
            {
                ans += arr[i];
            }
            return ans;
        }

        // Function to calculate maximum sum
        // of array after removing pairs whose
        // concatenation is divisible by 3
        function getMax(arr, n) {

            // Stores the sum of
            // digits of array element
            let maxRem0 = 0;

            let rem1 = 0;
            let rem2 = 0;

            for (let i = 0; i < n; i++) {

                // Find the sum of digits
                let digitSum = getSum(arr[i]);

                // If i is divisible by 3
                if (digitSum % 3 == 0)
                    maxRem0 = Math.max(maxRem0, arr[i]);

                // Otherwise, if i modulo 3 is 1
                else if (digitSum % 3 == 1)
                    rem1 += arr[i];

                // Otherwise, if i modulo 3 is 2
                else
                    rem2 += arr[i];
            }

            // Return the resultant
            // sum of array elements
            document.write(maxRem0 + Math.max(rem1, rem2))
        }

        // Driver Code
        let arr = [23, 12, 43, 3, 56];
        let n = arr.length;

        getMax(arr, n);

        // This code is contributed by Hritik

    </script>
```

**Output:** 

```
91
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)