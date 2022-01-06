# 最小翻转数，使左边的全 1 和右边的全 0 |设置 1(使用位掩码)

> 原文:[https://www . geesforgeks . org/minimum-flips-make-1s-left-0s-right-set-1-using-bit mask/](https://www.geeksforgeeks.org/minimum-flips-make-1s-left-0s-right-set-1-using-bitmask/)

给定一个二进制数组，我们可以将所有的 1 翻转到左边，将所有的 0 翻转到右边。计算左全 1 和右全 0 所需的最小翻转次数。

**示例:**

```
Input: 1011000  
Output: 1
1 flip is required to make it 1111000.

Input : 00001 
Output : 2
2 flips required to make it 10000.
```

为了解决这个问题，我们使用位屏蔽。首先，我们把这个数组转换成一个字符串，然后我们找到这个二进制字符串的等价十进制数。我们尝试了所有面具，左边 1，右边 0 的所有可能性。我们迭代一个循环，直到十进制数为零。每次我们将对带有掩码的数字进行按位异或运算，异或值中的 1 数将是所需的翻转数。我们将 n 减 1 并更新掩码。
1-以二进制数组为输入
2-将数组转换为字符串，然后转换为等效的十进制数(num)
3-取初始掩码值并迭代直到 num<= 0
4-使用(num XOR 掩码)
5-查找最小翻转并减少 num 并更新掩码
6-返回最小计数

## C++

```
// C++ program to find
// of flips till that
// all 1s in left
#include <bits/stdc++.h>
using namespace std;

int countones(long n);

// Function to count minimum
// number of flips
int findMiniFlip(int nums[], int n)
{
  string s = "";
  for (int i = 0; i < n; i++)
    s += nums[i];

  char *end;
  char tmp[s.length()];
  strcpy(tmp, s.c_str());

  // This is converting string
  // s into integer of base 2
  // (if s = '100' then num = 4)
  long num = strtol(tmp, &end, 2);

  // Initialize minXor
  // with n that can be
  // maximum number of flips
  int minXor = n;

  // right shift 1 by (n-1) bits
  long mask = (1 << (n - 1));
  while (n - 1 > 0)
  {
    // Calculate bitwise
    // XOR of num and mask
    long temp = (num ^ mask);

    // Math.min(a, b) returns
    // minimum of a and b
    // return minimum number
    // of flips till that digit
    minXor = min(minXor, countones(temp));
    n--;
    mask = (mask | (1 << (n - 1)));
  }
  return minXor;
}

// Function to count number of 1s
int countones(long n)
{
  int c = 0;
  while (n > 0)
  {
    n = n & (n - 1);
    c++;
  }
  return c;
}

// Driver code
int main()
{
  int nums[] = {1, 0, 1,
                1, 0, 0, 0};
  int size = sizeof(nums) /
             sizeof(nums[0]);
  int n = findMiniFlip(nums, size);
  cout << n;
}

// This code is contributed by Rutvik_56
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum flips to make
// all 1s in left
import java.io.*;

class GFG {

    // function to count minimum number of flips
    public static int findMiniFlip(int[] nums)
    {
        int n = nums.length;
        String s = "";
        for (int i = 0; i < n; i++)
            s += nums[i];

        // This is converting string s into integer
        // of base 2 (if s = '100' then num = 4)
        long num = Integer.parseInt(s, 2);

        // initialize minXor with n that can be maximum
        // number of flips
        int minXor = n;

        // right shift 1 by (n-1) bits
        long mask = (1 << (n-1));
        while (n-1 > 0) {

            // calculate bitwise XOR of num and mask
            long temp = (num ^ mask);

            // Math.min(a, b) returns minimum of a and b
            // return minimum number of flips till that
            // digit
            minXor = Math.min(minXor, countones(temp));
            n--;

            mask = (mask | (1 << n -1));
        }
        return minXor;
    }

    // function to count number of 1s
    public static int countones(long n)
    {
        int c = 0;
        while (n > 0) {
            n = n & (n-1);
            c++;
        }
        return c;
    }

    public static void main(String[] args)
    {
        int[] nums = { 1, 0, 1, 1, 0, 0, 0 };
        int n = findMiniFlip(nums);
        System.out.println(n);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find minimum flips to make
# all 1s in left

# Function to count minimum number of flips
def findMiniFlip(nums):

    n = len(nums)
    s = ''

    for i in range(n):
        s += str(nums[i])

    # This is converting string s into integer
    # of base 2 (if s='100' then num=4)
    num = int(s, 2)

    # Initialize minXor with n that can be maximum
    # number of flips
    minXor = n;

    # Right shift 1 by(n-1) bits
    mask = (1 << (n - 1))
    while (n - 1 > 0):

        # Calculate bitwise XOR of num and mask
        temp = (num ^ mask)

        # Math.min(a, b) returns minimum of a and b
        # return minimum number of flips till that
        # digit
        minXor = min(minXor, countones(temp))
        n -= 1
        mask = (mask | (1 << n - 1))

    return minXor

# Function to count number of 1s
def countones(n):

    c = 0
    while (n > 0):
        n = n & (n - 1)
        c += 1

    return c

# Driver code
if __name__ == "__main__":

    nums = [ 1, 0, 1, 1, 0, 0, 0 ]
    n = findMiniFlip(nums)

    print(n)

# This code is contributed by chitranayal
```

## C#

```
// C# program to find
// minimum flips to make
// all 1s in left
using System;
class GFG{

// Function to count minimum
// number of flips
public static int findMiniFlip(int[] nums)
{
  int n = nums.Length;
  String s = "";
  for (int i = 0; i < n; i++)
    s += nums[i];

  // This is converting string
  // s into integer of base 2
  // (if s = '100' then num = 4)
  long num = Convert.ToInt32(s, 2);

  // initialize minXor with n
  // that can be maximum
  // number of flips
  int minXor = n;

  // right shift 1 by (n-1) bits
  long mask = (1 << (n - 1));
  while (n - 1 > 0)
  {
    // calculate bitwise XOR
    // of num and mask
    long temp = (num ^ mask);

    // Math.Min(a, b) returns
    // minimum of a and b
    // return minimum number
    // of flips till that
    // digit
    minXor = Math.Min(minXor,
                      countones(temp));
    n--;
    mask = (mask | (1 << n - 1));
  }
  return minXor;
}

// Function to count number of 1s
public static int countones(long n)
{
  int c = 0;
  while (n > 0)
  {
    n = n & (n - 1);
    c++;
  }
  return c;
}

// Driver code
public static void Main(String[] args)
{
  int[] nums = {1, 0, 1, 1,
                0, 0, 0};
  int n = findMiniFlip(nums);
  Console.WriteLine(n);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program to find minimum
// flips to make all 1s in left

// Function to count minimum number of flips
function findMiniFlip(nums)
{
    let n = nums.length;
    let s = "";
    for(let i = 0; i < n; i++)
        s += nums[i];

    // This is converting string s into integer
    // of base 2 (if s = '100' then num = 4)
    let num = parseInt(s, 2);

    // Initialize minXor with n that
    // can be maximum number of flips
    let minXor = n;

    // Right shift 1 by (n-1) bits
    let mask = (1 << (n - 1));
    while (n - 1 > 0)
    {

        // Calculate bitwise XOR of num and mask
        let temp = (num ^ mask);

        // Math.min(a, b) returns minimum of a and b
        // return minimum number of flips till that
        // digit
        minXor = Math.min(minXor, countones(temp));
        n--;

        mask = (mask | (1 << n -1));
    }
    return minXor;
}

// Function to count number of 1s
function countones(n)
{
    let c = 0;
    while (n > 0)
    {
        n = n & (n - 1);
        c++;
    }
    return c;
}

// Driver Code
let nums = [ 1, 0, 1, 1, 0, 0, 0 ];
let n = findMiniFlip(nums);

document.write(n);

// This code is contributed by code_hunt

</script>
```

**输出:**

```
1
```