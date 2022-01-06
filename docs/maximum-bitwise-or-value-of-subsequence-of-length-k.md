# 长度为 K 的子序列的最大位或值

> 原文:[https://www . geeksforgeeks . org/长度为 k 的子序列的最大位或值/](https://www.geeksforgeeks.org/maximum-bitwise-or-value-of-subsequence-of-length-k/)

给定一个正整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个数 **K** ，任务是找到大小为 K 的子序列的按位或的最大值

**示例:**

> **输入:** arr[] = {2，5，3，6，11，13}，k = 3
> **输出:** 15
> **解释:**
> 子序列 wil 最大 OR 值为 2，11，13。
> 
> **输入:** arr[] = {5，9，7，19}，k = 3
> **输出:** 31
> **解释:**
> 大小为 k = 3 的子序列的按位 OR 的最大值为 31。

**天真方法:**天真方法是[生成长度为 K](https://www.geeksforgeeks.org/print-all-sequences-of-given-length/) 的所有子序列，并找到所有子序列的[按位 OR](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 值。其中最大的将是答案。

**时间复杂度:***O(N<sup>2</sup>)*
**辅助空间:** *O(K)*

**高效方法:**为了优化上述方法，尝试执行**贪婪方法**。以下是步骤:

1.  初始化大小为 32 的整数数组*位[]* ，所有值等于 0。
2.  现在从 31 到 0 迭代位[]数组的每个索引，并检查位数组的第 i <sup>个</sup>值是否为 0，然后在给定数组中迭代，并在取值后找到对我们的位数组贡献最大 1 的元素。
3.  取该元素并相应地改变位数组，如果 k > 0，每次也将 k 减少 1。否则就脱离循环。
4.  现在把 bit[]数组转换成十进制数，得到最终答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to convert bit array to
// decimal number
int build_num(int bit[])
{
    int ans = 0;

    for (int i = 0; i < 32; i++)
        if (bit[i])
            ans += (1 << i);

    // Return the final result
    return ans;
}

// Function to find the maximum Bitwise
// OR value of subsequence of length K
int maximumOR(int arr[], int n, int k)
{
    // Initialize bit array of
    // size 32 with all value as 0
    int bit[32] = { 0 };

    // Iterate for each index of bit[]
    // array from 31 to 0, and check if
    // the ith value of bit array is 0
    for (int i = 31; i >= 0; i--) {

        if (bit[i] == 0 && k > 0) {
            int temp = build_num(bit);
            int temp1 = temp;
            int val = -1;

            for (int j = 0; j < n; j++) {

                // Check for maximum
                // contributing element
                if (temp1 < (temp | arr[j])) {
                    temp1 = temp | arr[j];
                    val = arr[j];
                }
            }

            // Update the bit array
            // if max_contributing
            // element is found
            if (val != -1) {

                // Decrement the value of K
                k--;
                for (int j = 0; j < 32; j++) {
                    if (val & (1 << j))
                        bit[j]++;
                }
            }
        }
    }

    // Return the result
    return build_num(bit);
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 5, 9, 7, 19 };

    // Length of subsequence
    int k = 3;
    int n = sizeof arr / sizeof arr[0];

    // Function Call
    cout << maximumOR(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to convert bit array to
// decimal number
static int build_num(int []bit)
{
    int ans = 0;

    for(int i = 0; i < 32; i++)
       if (bit[i] == 1)
           ans += (1 << i);
           ans += 32;

    // Return the final result
    return ans;
}

// Function to find the maximum Bitwise
// OR value of subsequence of length K
static int maximumOR(int []arr, int n, int k)
{

    // Initialize bit array of
    // size 32 with all value as 0
    int bit[] = new int[32];

    // Iterate for each index of bit[]
    // array from 31 to 0, and check if
    // the ith value of bit array is 0
    for(int i = 31; i >= 0; i--)
    {
       if (bit[i] == 0 && k > 0)
       {
           int temp = build_num(bit);
           int temp1 = temp;
           int val = -1;

           for(int j = 0; j < n; j++)
           {

              // Check for maximum
              // contributing element
              if (temp1 < (temp | arr[j]))
              {
                  temp1 = temp | arr[j];
                  val = arr[j];
              }
           }

           // Update the bit array
           // if max_contributing
           // element is found
           if (val != -1)
           {

               // Decrement the value of K
               k--;
               for(int j = 0; j < 32; j++)
               {
                  bit[j]++;
               }
           }
       }
    }

    // Return the result
    return build_num(bit);
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 5, 9, 7, 19 };

    // Length of subsequence
    int k = 3;
    int n = arr.length;

    // Function call
    System.out.println(maximumOR(arr, n, k));
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program to implement
# above approach

# Function to convert bit array to
# decimal number
def build_num(bit):

    ans = 0
    for i in range(0, 32):
        if (bit[i]):
            ans += (1 << i)

    # Return the final result
    return ans;

# Function to find the maximum Bitwise
# OR value of subsequence of length K
def maximumOR(arr, n, k):

    # Initialize bit array of
    # size 32 with all value as 0
    bit = [0] * 32

    # Iterate for each index of bit[]
    # array from 31 to 0, and check if
    # the ith value of bit array is 0
    for i in range(31, -1, -1):
        if (bit[i] == 0 and k > 0):
            temp = build_num(bit)
            temp1 = temp
            val = -1

            for j in range(0, n):

                # Check for maximum
                # contributing element
                if (temp1 < (temp | arr[j])):
                    temp1 = temp | arr[j]
                    val = arr[j]

            # Update the bit array
            # if max_contributing
            # element is found
            if (val != -1):

                # Decrement the value of K
                k -= 1
                for j in range(0, 32):
                    if (val & (1 << j)):
                        bit[j] += 1

    # Return the result
    return build_num(bit)

# Driver Code

# Given array arr[]
arr = [ 5, 9, 7, 19 ]

# Length of subsequence
k = 3;
n = len(arr)

# Function call
print(maximumOR(arr, n, k))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to convert bit array to
// decimal number
static int build_num(int []bit)
{
    int ans = 0;

    for(int i = 0; i < 32; i++)
       if (bit[i] == 1)
           ans += (1 << i);
           ans += 32;

    // Return the final result
    return ans;
}

// Function to find the maximum Bitwise
// OR value of subsequence of length K
static int maximumOR(int []arr, int n, int k)
{

    // Initialize bit array of
    // size 32 with all value as 0
    int []bit = new int[32];

    // Iterate for each index of bit[]
    // array from 31 to 0, and check if
    // the ith value of bit array is 0
    for(int i = 31; i >= 0; i--)
    {
       if (bit[i] == 0 && k > 0)
       {
           int temp = build_num(bit);
           int temp1 = temp;
           int val = -1;

           for(int j = 0; j < n; j++)
           {

              // Check for maximum
              // contributing element
              if (temp1 < (temp | arr[j]))
              {
                  temp1 = temp | arr[j];
                  val = arr[j];
              }
           }

           // Update the bit array
           // if max_contributing
           // element is found
           if (val != -1)
           {

               // Decrement the value of K
               k--;
               for(int j = 0; j < 32; j++)
               {
                  bit[j]++;
               }
           }
       }
    }

    // Return the result
    return build_num(bit);
}

// Driver Code
public static void Main()
{

    // Given array arr[]
    int []arr = { 5, 9, 7, 19 };

    // Length of subsequence
    int k = 3;
    int n = arr.Length;

    // Function call
    Console.Write(maximumOR(arr, n, k));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to convert bit array to
// decimal number
function build_num(bit)
{
    let ans = 0;

    for(let i = 0; i < 32; i++)
        if (bit[i] > 0)
            ans += (1 << i);

    // Return the final result
    return ans;
}

// Function to find the maximum Bitwise
// OR value of subsequence of length K
function maximumOR(arr, n, k)
{

    // Initialize bit array of
    // size 32 with all value as 0
    let bit = new Array(32);
    bit.fill(0);

    // Iterate for each index of bit[]
    // array from 31 to 0, and check if
    // the ith value of bit array is 0
    for(let i = 31; i >= 0; i--)
    {
        if (bit[i] == 0 && k > 0)
        {
            let temp = build_num(bit);
            let temp1 = temp;
            let val = -1;

            for(let j = 0; j < n; j++)
            {

                // Check for maximum
                // contributing element
                if (temp1 < (temp | arr[j]))
                {
                    temp1 = temp | arr[j];
                    val = arr[j];
                }
            }

            // Update the bit array
            // if max_contributing
            // element is found
            if (val != -1)
            {

                // Decrement the value of K
                k--;
                for(let j = 0; j < 32; j++)
                {
                    if ((val & (1 << j)) > 0)
                        bit[j]++;
                }
            }
        }
    }

    // Return the result
    return build_num(bit);
}

// Driver code

// Given array arr[]
let arr = [ 5, 9, 7, 19 ];

// Length of subsequence
let k = 3;
let n = arr.length;

// Function Call
document.write(maximumOR(arr, n, k));

// This code is contributed by divyeshrabadiya07   

</script>
```

**Output:** 

```
31
```

**时间复杂度:***O(N * log N)*
T5】辅助空间: *O(1)*
**类似文章:** [长度为 K 的子序列的最大按位 AND 值](https://www.geeksforgeeks.org/maximum-bitwise-and-value-of-subsequence-of-length-k/)