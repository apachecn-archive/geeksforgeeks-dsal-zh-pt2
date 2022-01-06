# 通过替换“？”来计算可能的排列二进制字符串中的字符

> 原文:[https://www . geeksforgeeks . org/count-置换-通过替换二进制字符串中的可能字符/](https://www.geeksforgeeks.org/count-permutations-possible-by-replacing-characters-in-a-binary-string/)

给定一个由字符 **0** 、 **1** 和**组成的[字符串](https://www.geeksforgeeks.org/python-strings/)T2**，任务是统计通过替换**“？”形成的[二进制串](https://www.geeksforgeeks.org/tag/binary-string/)的所有可能组合**由 **0** 或 **1** 组成。

**示例:**

> **输入:**S =“0100？110“
> **输出:** 2
> **说明:**替换各“？”如果使用“1”和“0”，则此类字符串的数目将等于“01001110”和“01000110”。因此，这样形成的字符串总数是 2。
> 
> **输入:**S =“00？0?111”
> T3】输出: 4

**方法:**给定的问题可以基于以下观察来解决:

*   自从每一个**“？”**可以用**‘0’**或**‘1’**代替，每一个**’？”**性格。
*   现在，任务简化为寻找**“？”** s，说**数**。
*   因此，可以形成的不同字符串的总数为 **2 <sup>计数</sup>** 。

按照以下步骤解决问题:

*   统计**“？”的[出现次数](https://www.geeksforgeeks.org/python-count-occurrences-of-a-character-in-string/)**T3，说**数**
*   打印 **2 <sup>的值，将</sup>** 算作形成的字符串的合成组合。

下面是上述方法的实现:

## C++14

```
#include <bits/stdc++.h>

using namespace std;

//Function to count all possible
//permutations of the string s
void countPermutations(string s){

    //Stores frequency of the
    //character '?'
    int count = 0;

    //Traverse the string
    for (char i:s){
        if (i == '?')
            count += 1;
      }

    //Print the answer
    cout<<pow(2,count);
}

//Driver Code
int main()
{
  //Given string S
  string s = "0100?110";

  //Function call to count
  //the number of permutations
  countPermutations(s);

  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to count all possible
// permutations of the string s
static void countPermutations(String s)
{

    // Stores frequency of the
    // character '?'
    int count = 0;

    // Traverse the string
    for (char i : s.toCharArray())
    {
        if (i == '?')
            count += 1;
      }

    // Print the answer
    System.out.print((int)Math.pow(2,count));
}

// Driver Code
public static void main(String[] args)
{

    // Given string S
  String s = "0100?110";

  // Function call to count
  // the number of permutations
  countPermutations(s);
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count all possible
# permutations of the string s
def countPermutations(s):

    # Stores frequency of the
    # character '?'
    count = 0

    # Traverse the string
    for i in s:
        if i == '?':

            # Increment count
            count += 1

    # Print the answer
    print(2**count)

# Driver Code

# Given string S
s = "0100?110"

# Function call to count
# the number of permutations
countPermutations(s)

# This code is contribute by mohit kumar 29.
```

## C#

```
// C# program for above approach
using System;

public class GFG
{

// Function to count all possible
// permutations of the string s
static void countPermutations(string s)
{

    // Stores frequency of the
    // character '?'
    int count = 0;

    // Traverse the string
    foreach (char i in s)
    {
        if (i == '?')
            count += 1;
      }

    // Print the answer
    Console.WriteLine(Math.Pow(2,count));
}

// Driver code
public static void Main(String[] args)
{

    // Given string S
  string s = "0100?110";

  // Function call to count
  // the number of permutations
  countPermutations(s);
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

//Function to count all possible
//permutations of the string s
function countPermutations(s){

    //Stores frequency of the
    //character '?'
    var count = 0;

    //Traverse the string
    for(var i =0; i< s.length; i++)
    {
        if (s[i] == '?')
            count += 1;
    }

    //Print the answer
    document.write( Math.pow(2,count));
}

//Driver Code

//Given string S
var s = "0100?110";

//Function call to count
//the number of permutations
countPermutations(s);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)