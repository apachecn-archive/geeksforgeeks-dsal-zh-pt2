# 对于给定的附加字符成本，字典上最大的可能字符串

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最大可能字符串附加字符成本/](https://www.geeksforgeeks.org/lexicographically-largest-string-possible-for-a-given-cost-of-appending-characters/)

给定一个整数 **W** 和一个大小为 26 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**a【】**，其中 a <sub>i</sub> 表示使用 i <sup>th</sup> 字母表的成本，任务是从字典顺序上找到可以为成本生成的最大字符串 **W** 。

**示例:**

> **输入:** W = 236，a[] = {1，1，2，33，4，6，9，7，36，32，58，32，28，904，22，255，47，69，558，544，21，36，48，85，48，58}
> **输出:**zzzzze
> **解释:**
> 4 *(z 的成本)
> 
> **输入:** W = 6674，a[] = {252，288，578，746，295，884，198，655，503，868，942，506，718，498，727，338，43，768，783，312，369，712，230，106，102，554 }
> T3

**方法:**思路是[迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)**a【】**从字符“ **z** 到“ **a** 的字母表。现在，在**a【】**中找到一个和等于 **W** 的组合。相同的重复次数可以从**a【】**中无限次选择。然后，使用[递归](https://www.geeksforgeeks.org/recursion/)和[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)解决问题。按照以下步骤解决问题:

*   **对于任意时刻的子问题 sum = 0，**打印作为存储在数组中的字符的成本获得的字符串，到目前为止总计为 **W** ，并且由于该字符串是通过附加从“ **z** ”开始的字符而生成的，因此这样形成的字符串是**字典上最大的字符串**。
*   否则，如果总和为负或指数为 T2 0，则这些子问题返回假。
*   否则，通过在结果字符串中包含和排除当前字符，在字典中找到可能的最大字符串。
*   按字典顺序打印通过完成上述步骤获得的最大字符串。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// lexicographically largest
// String possible
bool lexi_largest_String(int a[], int i,
                         int sum, vector<int> &v)
{
  // If sum is less than 0
  if (sum < 0)
    return false;

  // If sum is equal to 0
  if (sum == 0)
    return true;

  // If sum is less than 0
  if (i < 0)
    return false;

  // Add current character
  v.push_back(i);

  // Check if selecting current
  // character generates
  // lexicographically largest String
  if (lexi_largest_String(a, i,
                          sum - a[i], v))
    return true;

  // Backtrack if solution
  // not found
  auto it = v.end();
  it--;
  v.erase(it);

  // Find the lexicographically
  // largest String excluding
  // the current character
  return lexi_largest_String(a, i - 1,
                             sum, v);
}

// Function to print the
// lexicographically largest
// String generated
void generateString(int a[], int sum)
{
  vector<int> v;

  // Function call
  lexi_largest_String(a, 25,
                      sum, v);

  // Stores the String
  string s = "";

  for (int j = 0; j < v.size(); j++)
    s += (char)(v[j] + 'a');

  // Print the lexicographically
  // largest String formed
  cout << s << endl;
}

// Driver code
int main()
{
  // Cost of adding each
  // alphabet
  int a[] = {1, 1, 2, 33, 4, 6, 9,
             7, 36, 32, 58, 32, 28,
             904, 22, 255, 47, 69,
             558, 544, 21, 36, 48,
             85, 48, 58};

  // Cost of generating
  // the String
  int sum = 236;

  generateString(a, sum); 
  return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find the
// lexicographically largest
// String possible
static boolean lexi_largest_String(int a[], int i,
                                   int sum,
                                   Vector<Integer> v)
{
  // If sum is less than 0
  if (sum < 0)
    return false;

  // If sum is equal to 0
  if (sum == 0)
    return true;

  // If sum is less than 0
  if (i < 0)
    return false;

  // Add current character
  v.add(i);

  // Check if selecting current
  // character generates
  // lexicographically largest String
  if (lexi_largest_String(a, i, sum -
                          a[i], v))
    return true;

  // Backtrack if solution
  // not found
  v.remove(v.size() - 1);

  // Find the lexicographically
  // largest String excluding
  // the current character
  return lexi_largest_String(a, i - 1,
                             sum, v);
}

// Function to print the
// lexicographically largest
// String generated
static void generateString(int a[],
                           int sum)
{
  Vector<Integer> v = new Vector<Integer>();

  // Function call
  lexi_largest_String(a, 25, sum, v);

  // Stores the String
  String s = "";

  for (int j = 0; j < v.size(); j++)
    s += (char)(v.get(j) + 'a');

  // Print the lexicographically
  // largest String formed
  System.out.print(s + "\n");
}

// Driver code
public static void main(String[] args)
{
  // Cost of adding each alphabet
  int a[] = {1, 1, 2, 33, 4, 6, 9,
             7, 36, 32, 58, 32, 28,
             904, 22, 255, 47, 69,
             558, 544, 21, 36, 48,
             85, 48, 58};

  // Cost of generating
  // the String
  int sum = 236;

  generateString(a, sum);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the lexicographically
# largest string possible
def lexi_largest_string(a, i, sum, v):

    # If sum is less than 0
    if (sum < 0):
        return False

    # If sum is equal to 0
    if (sum == 0):
        return True

    # If sum is less than 0
    if (i < 0):
        return False

    # Add current character
    v.append(i)

    # Check if selecting current character
    # generates lexicographically
    # largest string
    if(lexi_largest_string(a, i,
                           sum - a[i], v)):
        return True

    # Backtrack if solution not found
    v.pop(-1)

    # Find the lexicographically
    # largest string excluding
    # the current character
    return lexi_largest_string(a, i - 1,
                               sum, v)

# Function to print the lexicographically
# largest string generated
def generateString(a, sum):

    v = []

    # Function call
    lexi_largest_string(a, 25, sum , v)

    # Stores the string
    s = ""

    for j in range(len(v)):
        s += chr(v[j] + ord('a'))

    # Print the lexicographically
    # largest string formed
    print(s)

# Driver code
if __name__ == '__main__':

    a = [ 1, 1, 2, 33, 4, 6, 9,
          7, 36, 32, 58, 32, 28,
          904, 22, 255, 47, 69,
          558, 544, 21, 36, 48,
          85, 48, 58 ]

    # Cost of generating
    # the string
    sum = 236

    generateString(a, sum)

# This code is contributed by Shivam Singh
```

## C#

```
// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to find the
// lexicographically largest
// String possible
static bool lexi_largest_String(int []a, int i,
                                int sum, List<int> v)
{
  // If sum is less than 0
  if (sum < 0)
    return false;

  // If sum is equal to 0
  if (sum == 0)
    return true;

  // If sum is less than 0
  if (i < 0)
    return false;

  // Add current character
  v.Add(i);

  // Check if selecting current
  // character generates
  // lexicographically largest String
  if (lexi_largest_String(a, i, sum -
                          a[i], v))
    return true;

  // Backtrack if solution
  // not found
  v.RemoveAt(v.Count - 1);

  // Find the lexicographically
  // largest String excluding
  // the current character
  return lexi_largest_String(a, i - 1,
                             sum, v);
}

// Function to print the
// lexicographically largest
// String generated
static void generateString(int []a,
                           int sum)
{
  List<int> v = new List<int>();

  // Function call
  lexi_largest_String(a, 25, sum, v);

  // Stores the String
  String s = "";

  for (int j = 0; j < v.Count; j++)
    s += (char)(v[j] + 'a');

  // Print the lexicographically
  // largest String formed
  Console.Write(s + "\n");
}

// Driver code
public static void Main(String[] args)
{
  // Cost of adding each alphabet
  int []a = {1, 1, 2, 33, 4, 6, 9,
             7, 36, 32, 58, 32, 28,
             904, 22, 255, 47, 69,
             558, 544, 21, 36, 48,
             85, 48, 58};

  // Cost of generating
  // the String
  int sum = 236;

  generateString(a, sum);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // Javascript Program to implement the above approach

    // Function to find the
    // lexicographically largest
    // String possible
    function lexi_largest_String(a, i, sum, v)
    {
      // If sum is less than 0
      if (sum < 0)
        return false;

      // If sum is equal to 0
      if (sum == 0)
        return true;

      // If sum is less than 0
      if (i < 0)
        return false;

      // Add current character
      v.push(i);

      // Check if selecting current
      // character generates
      // lexicographically largest String
      if (lexi_largest_String(a, i, sum - a[i], v))
        return true;

      // Backtrack if solution
      // not found
      v.pop();

      // Find the lexicographically
      // largest String excluding
      // the current character
      return lexi_largest_String(a, i - 1, sum, v);
    }

    // Function to print the
    // lexicographically largest
    // String generated
    function generateString(a, sum)
    {
      let v = [];

      // Function call
      lexi_largest_String(a, 25, sum, v);

      // Stores the String
      let s = "";

      for (let j = 0; j < v.length; j++)
        s += String.fromCharCode(v[j] + 'a'.charCodeAt());

      // Print the lexicographically
      // largest String formed
      document.write(s + "</br>");
    }

    // Cost of adding each alphabet
    let a = [1, 1, 2, 33, 4, 6, 9,
             7, 36, 32, 58, 32, 28,
             904, 22, 255, 47, 69,
             558, 544, 21, 36, 48,
             85, 48, 58];

    // Cost of generating
    // the String
    let sum = 236;

    generateString(a, sum);

</script>
```

**Output**

```
zzzze
```

***时间复杂度:**O(2<sup>26)</sup>T5
T7**辅助空间:** O(N)*