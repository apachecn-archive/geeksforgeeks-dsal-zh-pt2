# 计算将一个数字划分为递增数字序列的方法

> 原文:[https://www . geesforgeks . org/count-way-to-partition-a-number-in-递增数字序列/](https://www.geeksforgeeks.org/count-ways-to-partition-a-number-into-increasing-sequences-of-digits/)

给定一个数字[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找到将一个[字符串](https://www.geeksforgeeks.org/string-data-structure/)分割成由递增的数字组成的[子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)的方法数。

**示例:**

> **输入:**S = " 1345 "
> T3】输出:5
> T6】说明:可能的分区如下:
> 
> 1.  [1345]
> 2.  [13, 45], [1, 345]
> 3.  [1, 3, 45]
> 4.  [1, 3, 4, 5]
> 
> **输入:**S = " 12 "
> T3】输出: 2

**方法:**这个问题可以通过观察每个数字之间要么是前一个数字的一部分，要么是一个新的数字来解决，所以为了解决这个问题可以使用[递归](https://www.geeksforgeeks.org/recursion/)。按照以下步骤解决问题:

*   初始化一个整型变量，比如说**将**计数为 **0** ，以存储[将一个字符串](https://www.geeksforgeeks.org/string-partition-python/)划分为递增子集的方式数。
*   用**索引**(存储当前位置)、字符串 **S** (问题中给定的字符串)和字符串 **ans** (作为参数)声明函数 **print()** 。
*   现在，需要考虑以下两种情况:
    *   如果在前面的编号中插入了 **S【索引】**，则在 **ans** 的末尾追加 **S【索引】**，调用函数 **print()** ，参数为 **index + 1** 、 **S** 、 **ans** 。
    *   如果 **S【索引】**不是前一个数字的一部分，那么在 **ans** 的末尾追加**(空格)，然后插入 **S【索引】**并调用函数 **print()** ，参数为 **index + 1** 、 **S** 、 **ans** 。**
*   **如果**索引= S.length()** ，则检查形成的序列中的数字是否按递增顺序排列。如果形成的序列在增加，将**计数**增加 **1** 。**
*   **执行上述步骤后，打印**计**作为答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Stores the number of ways
// to partition a string
int count1 = 0;
vector<string> split(string str)
{
    vector<string> ans;
    string word = "";
    for(auto x : str)
    {
        if (x == ' ')
        {
            ans.push_back(word);
            word = "";
        }
        else
        {
            word = word + x;
        }
    }
    ans.push_back(word);
    return ans;
}

// Function to check if a sequence
// is strictly increasing or not
bool check(string m)
{

    // If there is only one number
    if (m.length() == 1)
    {
        return true;
    }

    // Split the string m when there is space
    vector<string> temp = split(m);
    int number[temp.size()];

    // Insert all the splits into the array
    for(int i = 0; i < temp.size(); ++i)
    {
        number[i] = stoi(temp[i]);
    }

    int first = number[0];
    for(int i = 1; i < temp.size(); ++i)
    {
        if (number[i] > first)
        {
            first = number[i];
        }
        else
        {

            // If number is not increasing
            return false;
        }
    }

    // If the sequence is increasing
    return true;
}

// Recursive function to partition
// a string in every possible substrings
void print1(string m, int index, string ans)
{

    // If index = m.length, check if ans
    // forms an increasing sequence or not
    if (index == m.length())
    {

        if (check(ans))
        {

            // Increment count by 1,
            // if sequence is increasing
            count1++;
        }
        return;
    }  

    // If S[index] is appended to previous number
    print1(m, index + 1, ans + m[index]);

    if (index != 0)

        // If S[index] is starting a new number
        print1(m, index + 1,
              ans + " " + m[index]);
}

// Driver Code
int main()
{

    // Given Input
    string k = "1345";

    // Function Call
    print1(k, 0, "");

    // Print the answer.
    cout << count1;
}

// This code is contributed by ipg2016107
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach

import java.io.*;
import java.util.*;
class GFG {

    // Stores the number of ways
    // to partition a string
    static int count = 0;

    // Function to check if a sequence
    // is strictly increasing or not
    static boolean check(String m)
    {
        // If there is only one number
        if (m.length() == 1) {
            return true;
        }

        // Split the string m when there is space
        String temp[] = m.split(" ");
        int number[] = new int[temp.length];

        // Insert all the splits into the array
        for (int i = 0; i < temp.length; ++i) {

            number[i] = Integer.parseInt(temp[i]);
        }

        int first = number[0];
        for (int i = 1; i < number.length; ++i) {

            if (number[i] > first) {
                first = number[i];
            }
            else {

                // If number is not increasing
                return false;
            }
        }

        // If the sequence is increasing
        return true;
    }

    // Recursive function to partition
    // a string in every possible substrings
    static void print(String m,
                      int index, String ans)
    {
        // If index = m.length, check if ans
        // forms an increasing sequence or not
        if (index == m.length()) {

            if (check(ans)) {

                // Increment count by 1,
                // if sequence is increasing
                ++count;
            }
            return;
        }

        // If S[index] is appended to previous number
        print(m, index + 1, ans + m.charAt(index));
        if (index != 0)
            // If S[index] is starting a new number
            print(m, index + 1,
                  ans + " " + m.charAt(index));
    }

    // DriverCode
    public static void main(String[] args)
    {
        // Given Input
        String k = Integer.toString(1345);

        // Function Call
        print(k, 0, "");

        // Print the answer.
        System.out.println(count);
    }
}
```

## **蟒蛇 3**

```
# Python3 program for the above approach
count = 0

# Function to check if a sequence
# is strictly increasing or not
def check(m):

    # If there is only one number
    if (len(m) == 1):
        return True

    # Split the string m when there is space
    temp = m.split(" ")
    number = [0]*(len(temp))

    # Insert all the splits into the array
    for i in range(len(temp)):
        number[i] = int(temp[i])

    first = number[0]
    for i in range(1, len(number)):
        if (number[i] > first):
            first = number[i]
        else:
            # If number is not increasing
            return False
    # If the sequence is increasing
    return True

# Recursive function to partition
# a string in every possible substrings
def Print(m, index, ans):
    global count

    # If index = m.length, check if ans
    # forms an increasing sequence or not
    if (index == len(m)):
        if (check(ans)):

            # Increment count by 1,
            # if sequence is increasing
            count+=1
        return

    # If S[index] is appended to previous number
    Print(m, index + 1, ans + m[index])
    if (index != 0):

        # If S[index] is starting a new number
        Print(m, index + 1, ans + " " + m[index])

# Given Input
k = "1345"

# Function Call
Print(k, 0, "")

# Print the answer.
print(count)

# This code is contributed by suresh07.
```

## **C#**

```
using System;

public class GFG {
    static int count = 0;

    // Function to check if a sequence
    // is strictly increasing or not
    static bool check(String m)
    {
        // If there is only one number
        if (m.Length == 1) {
            return true;
        }

        // Split the string m when there is space
        String[] temp = m.Split(" ");
        int[] number = new int[temp.Length];

        // Insert all the splits into the array
        for (int i = 0; i < temp.Length; ++i) {

            number[i] = int.Parse(temp[i]);
        }

        int first = number[0];
        for (int i = 1; i < number.Length; ++i) {

            if (number[i] > first) {
                first = number[i];
            }
            else {

                // If number is not increasing
                return false;
            }
        }

        // If the sequence is increasing
        return true;
    }

    // Recursive function to partition
    // a string in every possible substrings
    static void print(String m, int index, String ans)
    {
        // If index = m.length, check if ans
        // forms an increasing sequence or not
        if (index == m.Length) {

            if (check(ans)) {

                // Increment count by 1,
                // if sequence is increasing
                ++count;
            }
            return;
        }

        // If S[index] is appended to previous number
        print(m, index + 1, ans + m[index]);
        if (index != 0)
            // If S[index] is starting a new number
            print(m, index + 1, ans + " " + m[index]);
    }
    static public void Main()
    {

        String k = "1345";

        // Function Call
        print(k, 0, "");

        // Print the answer.
        Console.WriteLine(count);
    }
}

// This code is contributed by maddler.
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

// Stores the number of ways
// to partition a string
let count = 0;

// Function to check if a sequence
// is strictly increasing or not
function check(m)
{

    // If there is only one number
    if (m.length == 1)
    {
        return true;
    }

    // Split the string m when there is space
    let temp = m.split(" ");
    let number = new Array(temp.length);

    // Insert all the splits into the array
    for(let i = 0; i < temp.length; ++i)
    {
        number[i] = parseInt(temp[i]);
    }

    let first = number[0];
    for(let i = 1; i < number.length; ++i)
    {
        if (number[i] > first)
        {
            first = number[i];
        }
        else
        {

            // If number is not increasing
            return false;
        }
    }

    // If the sequence is increasing
    return true;
}

// Recursive function to partition
// a string in every possible substrings
function print(m, index, ans)
{

    // If index = m.length, check if ans
    // forms an increasing sequence or not
    if (index == m.length)
    {
        if (check(ans))
        {

            // Increment count by 1,
            // if sequence is increasing
            ++count;
        }
        return;
    }

    // If S[index] is appended to previous number
    print(m, index + 1, ans + m[index]);

    if (index != 0)

        // If S[index] is starting a new number
        print(m, index + 1,
              ans + " " + m[index]);
}

// Driver Code

// Given Input
let k = "1345";

// Function Call
print(k, 0, "");

// Print the answer.
document.write(count);

// This code is contributed by code_hunt

</script>
```

****Output:** 

```
5
```** 

*****时间复杂度:** O(N*2 <sup>N</sup> 其中 N 为*弦长 S
***辅助空间:** O(1)***