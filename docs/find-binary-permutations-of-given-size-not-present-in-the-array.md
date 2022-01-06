# 查找数组中不存在的给定大小的二进制排列

> 原文:[https://www . geesforgeks . org/find-给定大小的二进制排列-不在数组中/](https://www.geeksforgeeks.org/find-binary-permutations-of-given-size-not-present-in-the-array/)

给定一个正整数 **N** 和一个由[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)组成的大小为 **K** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，其中每个字符串的大小为 **N** ，任务是找出数组**arr【】**中不存在的所有大小为 **N** 的二进制字符串。

**示例:**

> **输入:** N = 3，arr[]= {“101”、“111”、“001”、“010”、“011”、“100”、“110”}
> **输出:** 000
> **说明:**给定数组中只缺少 000。
> 
> **输入:** N = 2，arr[]= {“00”，“01”}
> T3】输出: 10 11

**方法:**给定的问题可以通过[使用](https://www.geeksforgeeks.org/generate-all-the-binary-strings-of-n-bits/)[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)找到所有大小为**N**T5 的二进制字符串，然后打印数组中不存在的那些字符串 **arr[]** 来解决。按照以下步骤解决问题:

*   初始化一个由[字符串](https://www.geeksforgeeks.org/string-data-structure/)和**字符串**组成的无序集合，该集合将所有字符串存储在数组**arr【】**中。
*   初始化一个变量，说出**总计**，将其设置为**2<sup>N</sup>T7[功率](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)，其中 **N** 是字符串的[大小。](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)**
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，总计】**，并执行以下步骤:
    *   将空字符串变量 **num** 初始化为 **""** 。
    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【N–1，0】**，如果 **i** 和 **2 <sup>j</sup>** 的[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的值为**真**，则将字符 **1** 推入字符串 **num** 。否则，推字符 **0** 。
    *   如果集合 **S** 中不存在 **num** ，则打印字符串 **num** 作为结果字符串之一。
*   完成上述步骤后，如果数组中存在所有可能的二进制字符串，则打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find a Binary String of
// same length other than the Strings
// present in the array
void findMissingBinaryString(vector<string>& nums, int N)
{
    unordered_set<string> s;
    int counter = 0;

    // Map all the strings present in
    // the array
    for (string str : nums) {
        s.insert(str);
    }

    int total = (int)pow(2, N);
    string ans = "";

    // Find all the substring that
    // can be made
    for (int i = 0; i < total; i++) {
        string num = "";
        for (int j = N - 1; j >= 0; j--) {
            if (i & (1 << j)) {
                num += '1';
            }
            else {
                num += '0';
            }
        }

        // If num already exists then
        // increase counter
        if (s.find(num) != s.end()) {
            continue;
            counter++;
        }

        // If not found print
        else {
            cout << num << ", ";
        }
    }

    // If all the substrings are present
    // then print -1
    if (counter == total) {
        cout << "-1";
    }
}

// Driver Code
int main()
{
    int N = 3;
    vector<string> arr
        = { "101", "111", "001", "011", "100", "110" };

    findMissingBinaryString(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find a Binary String of
// same length other than the Strings
// present in the array
static void findMissingBinaryString(String[] nums, int N)
{
    HashSet<String> s = new HashSet<String>();
    int counter = 0;

    // Map all the Strings present in
    // the array
    for (String str : nums) {
        s.add(str);
    }

    int total = (int)Math.pow(2, N);
    String ans = "";

    // Find all the subString that
    // can be made
    for (int i = 0; i < total; i++) {
        String num = "";
        for (int j = N - 1; j >= 0; j--) {
            if ((i & (1 << j))>0) {
                num += '1';
            }
            else {
                num += '0';
            }
        }

        // If num already exists then
        // increase counter
        if (s.contains(num)) {

            counter++;
            continue;
        }

        // If not found print
        else {
            System.out.print(num+ ", ");
        }
    }

    // If all the subStrings are present
    // then print -1
    if (counter == total) {
        System.out.print("-1");
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;
    String []arr
        = { "101", "111", "001", "011", "100", "110" };

    findMissingBinaryString(arr, N);

}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 program for the above approach
from math import pow

# Function to find a Binary String of
# same length other than the Strings
# present in the array
def findMissingBinaryString(nums, N):
    s = set()
    counter = 0

    # Map all the strings present in
    # the array
    for x in nums:
        s.add(x)

    total = int(pow(2, N))
    ans = ""

    # Find all the substring that
    # can be made
    for i in range(total):
        num = ""
        j = N - 1
        while(j >= 0):
            if (i & (1 << j)):
                num += '1'
            else:
                num += '0'
            j -= 1

        # If num already exists then
        # increase counter
        if (num in s):
            continue
            counter += 1

        # If not found print
        else:
            print(num,end = ", ")

    # If all the substrings are present
    # then print -1
    if (counter == total):
        print("-1")

# Driver Code
if __name__ == '__main__':
    N = 3
    arr = ["101", "111", "001", "011", "100", "110"]

    findMissingBinaryString(arr, N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to find a Binary String of
    // same length other than the Strings
    // present in the array
    static void findMissingBinaryString(string[] nums,
                                        int N)
    {
        HashSet<string> s = new HashSet<string>();
        int counter = 0;

        // Map all the Strings present in
        // the array
        foreach(string str in nums) { s.Add(str); }

        int total = (int)Math.Pow(2, N);
        // string ans = "";

        // Find all the subString that
        // can be made
        for (int i = 0; i < total; i++) {
            string num = "";
            for (int j = N - 1; j >= 0; j--) {
                if ((i & (1 << j)) > 0) {
                    num += '1';
                }
                else {
                    num += '0';
                }
            }

            // If num already exists then
            // increase counter
            if (s.Contains(num)) {

                counter++;
                continue;
            }

            // If not found print
            else {
                Console.Write(num + ", ");
            }
        }

        // If all the subStrings are present
        // then print -1
        if (counter == total) {
            Console.Write("-1");
        }
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int N = 3;
        string[] arr
            = { "101", "111", "001", "011", "100", "110" };

        findMissingBinaryString(arr, N);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find a Binary String of
// same length other than the Strings
// present in the array
function findMissingBinaryString(nums, N) {
  let s = new Set();
  let counter = 0;

  // Map all the strings present in
  // the array
  for (let str of nums) {
    s.add(str);
  }

  let total = Math.pow(2, N);
  let ans = "";

  // Find all the substring that
  // can be made
  for (let i = 0; i < total; i++) {
    let num = "";
    for (let j = N - 1; j >= 0; j--) {
      if (i & (1 << j)) {
        num += "1";
      } else {
        num += "0";
      }
    }

    // If num already exists then
    // increase counter
    if (s.has(num)) {
      continue;
      counter++;
    }

    // If not found print
    else {
      document.write(num + ", ");
    }
  }

  // If all the substrings are present
  // then print -1
  if (counter == total) {
    document.write("-1");
  }
}

// Driver Code
let N = 3;
let arr = ["101", "111", "001", "011", "100", "110"];

findMissingBinaryString(arr, N);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
000, 010,
```

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(K)，其中 K 是数组的大小*