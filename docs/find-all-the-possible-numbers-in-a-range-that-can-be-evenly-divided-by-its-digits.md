# 找出一个范围内所有可能的数字，这个范围可以被它的数字均匀划分

> 原文:[https://www . geeksforgeeks . org/find-所有可能的数字-在一个范围内-可以被其数字平均划分的数字/](https://www.geeksforgeeks.org/find-all-the-possible-numbers-in-a-range-that-can-be-evenly-divided-by-its-digits/)

给定两个整数 n 和 m，它们分别代表一个范围，其中 n 是下界，m 是上界。任务是找出所有可能的数字，这些数字位于 n 和 m 之间，可以用它们的位数平均分配。

**示例:**

> **输入:** n = 1，m = 15
> **输出:**【1，2，3，4，5，6，7，8，9，11，12，15】
> **说明:**
> 数组中的数字除了
> 2 数字 10 和 13 之外，都可以用它们的位数平均划分，数字 10 和 13 位于 1 和 15 之间。
> 10 可以分解成 1 和 0 两个数字。
> 10 % 1 == 0 但 10 % 0！= 0.
> 13 可以分解成数字 1 和 3。
> 13 % 1 == 0 但 13 % 3！= 0.
> 
> **输入:** n = 21，m = 25
> **输出:**【22，24】
> **说明:**
> 数组中的数字除了
> 有 3 个数字之外，都可以用数字等分；21、23 和 25 位于 21 和 25 之间。
> 21 可以分解成数字 2 和 1。
> 21 % 2！= 0 和 21 % 1！= 0
> 23 可以分解成数字 2 和 3。
> 23 % 2！= 0 和 23 % 3！= 0.
> 25 可以分解成数字 2 和 5。
> 25 % 2！= 0 但 25 % 5 == 0。

**方法:**
主要思想是从左到右迭代每个数字。对于每个数字，将其转换为后跟字符数组的字符串，并检查它是否包含 0。如果它包含 0，则忽略它。否则，对于每个数字，检查该数字是否被其数字平均划分。如果数字被其位数平均分割，那么将其添加到列表中，否则将其丢弃。最后，返回列表。

下面是上述方法的实现:

## C++

```
// C++ program to find all the
// possible numbers that can be
// evenly divided by its digits
#include<bits/stdc++.h>
#include<sstream>
#include<string>
using namespace std;

// Function to check whether the
// number is evenly divisible by
// its digits or not.
bool isDivisible(int num)
{
  // Iterate each number convert
  // number into string and then
  // to character array.

  // declaring output string stream
  ostringstream str1;

  // Sending a number as a stream
  // into output string
  str1 << num;

  // the str() converts number into
  // string
  string str2 = str1.str();

  for (char c : str2 )
  {
    if (c == '0' ||
        num % (c - '0') > 0)
    {
      return false;
    }
  }
  return true;
}

// Function to check each and every
// number from left to right. If the
// number is divisible by its digits
// then the number is added into the list
vector<int> selfDividingNumber(int left,
                               int right)
{
  vector<int>list ;

  for (int i = left; i <= right; i++)
  {
    if (isDivisible(i))
    {
      list.push_back(i);
    }
  }
  return list;
}

// Driver Code
int main()
{
  // initialise range
  int n1 = 1, m1 = 15;

  vector<int> ans =
  (selfDividingNumber(n1, m1));

  for(auto i = ans.begin();
           i != ans.end(); i++)
    cout << (*i) << " ";
}

// This code is contributed by Chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all the possible numbers
// that can be evenly divided by its digits

import java.util.*;
class GFG {

    // Function to check each and every number
    // from left to right. If the number is
    // divisible by its digits
    // then the number is added into the list
    static List<Integer> selfDividingNumber(int left,
                                            int right)
    {

        List<Integer> list = new ArrayList<Integer>();
        for (int i = left; i <= right; i++) {
            if (isDivisible(i)) {
                list.add(i);
            }
        }
        return list;
    }

    // Function to check whether the number
    // is evenly divisible by its digits or not.
    static boolean isDivisible(int num)
    {

        // Iterate each number convert number
        // into string and then to character array.
        for (char c : String.valueOf(num).toCharArray()) {
            if (c == '0' || num % (c - '0') > 0) {
                return false;
            }
        }
        return true;
    }

    // Driver Code
    public static void main(String args[])
    {

        // initialise range
        int n1 = 1, m1 = 15;

        System.out.print(selfDividingNumber(n1, m1));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find all the possible numbers
# that can be evenly divided by its digits

# Function to check each and every number
# from left to right. If the number is
# divisible by its digits
# then the number is added into the list
def selfDividingNumber(left, right) :
    array_list = [];

    for i in range(left, right + 1) :
        if (isDivisible(i)) :
            array_list.append(i);

    return array_list;

# Function to check whether the number
# is evenly divisible by its digits or not.
def isDivisible(num) :

    # Iterate each number convert number
    # into string and then to character array.
    for c in list(str(num)) :
        if (c == '0' or num % (ord(c) - ord('0')) > 0):
            return False;

    return True;

# Driver Code
if __name__ == "__main__" :

    # Initialise range
    n1 = 1; m1 = 15;
    print(selfDividingNumber(n1, m1));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find all the
// possible numbers that can
// be evenly divided by its digits
using System;
using System.Collections.Generic;

public class GFG {

// Function to check each and every number
// from left to right. If the number is
// divisible by its digits then the number
// is added into the list
static List<int> selfDividingNumber(int left,
                                    int right)
{
    List<int> list = new List<int>();
    for(int i = left; i <= right; i++)
    {
       if (isDivisible(i))
       {
           list.Add(i);
       }
    }
    return list;
}

// Function to check whether the number
// is evenly divisible by its digits or not.
static bool isDivisible(int num)
{

    // Iterate each number convert number
    // into string and then to character array.
    foreach(char c in String.Join("", num).ToCharArray())
    {
        if (c == '0' || num % (c - '0') > 0)
        {
            return false;
        }
    }
    return true;
}

// Driver Code
public static void Main(String []args)
{

    // Initialise range
    int n1 = 1, m1 = 15;
    List<int> t = selfDividingNumber(n1, m1);

    foreach(int val in t)
        Console.Write(val + ", ");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to find all the possible numbers
// that can be evenly divided by its digits

   // Function to check each and every number
    // from left to right. If the number is
    // divisible by its digits
    // then the number is added into the list
    function selfDividingNumber(left, right)
    {

        let list = [];
        for (let i = left; i <= right; i++) {
            if (isDivisible(i)) {
                list.push(i);
            }
        }
        return list;
    }

    // Function to check whether the number
    // is evenly divisible by its digits or not.
    function isDivisible(numm)
    {
         let num = numm.toString();
        // Iterate each number convert number
        // into string and then to character array.
        for (let c in num.split('')) {
            if (num == '0' || num % (num  - '0') > 0) {
                return false;
            }
        }
        return true;
    }

// Driver Code

    // initialise range
    let n1 = 1, m1 = 15;

    document.write(selfDividingNumber(n1, m1));

</script>
```

**Output:** 

```
[1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 15]
```

**时间复杂度:** O(N)，其中 N 为从左到右的整数个数。

**辅助空间:** O(N)