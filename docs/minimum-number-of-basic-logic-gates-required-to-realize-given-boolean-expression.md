# 实现给定布尔表达式所需的最小基本逻辑门数

> 原文:[https://www . geesforgeks . org/最小基本逻辑门数-实现给定布尔表达式所需的数量/](https://www.geeksforgeeks.org/minimum-number-of-basic-logic-gates-required-to-realize-given-boolean-expression/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** ，表示[布尔表达式](https://www.geeksforgeeks.org/evaluate-a-boolean-expression-represented-as-string/)，任务是找到实现给定表达式所需的最小数量的 [AND，OR](https://www.geeksforgeeks.org/introduction-of-logic-gates/) ，以及 [NOT](https://www.geeksforgeeks.org/introduction-of-logic-gates/) 门。

**示例:**

> **输入:** S = "A+B.C"
> **输出:** 2
> **说明:**实现表达式需要 **1 个与门**用**' '表示**和 **1 或门**用**“+”表示。**
> 
> **输入:**S =(1–A)。B+C"
> **输出:** 3
> **说明:**实现表达式需要 **1 个以**' '为代表的 AND 门****和 **1 或门**用**“+”**表示， **1 非门**用**“-”表示。**

**方法:**按照以下步骤解决问题:

1.  [迭代字符串的字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)。
2.  初始化，门计数至 **0** 。
3.  如果当前字符是**'。**或**“+”**，或**“1”**，然后将门的**计数增加 **1****
4.  打印所需的门数。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the total
// number of gates required to
// realize the boolean expression S
void numberOfGates(string s)
{
    // Length of the string
    int N = s.size();

    // Stores the count
    // of total gates
    int ans = 0;

    // Traverse the string
    for (int i = 0; i < (int)s.size(); i++) {

        // AND, OR and NOT Gate
        if (s[i] == '.' || s[i] == '+'
            || s[i] == '1') {
            ans++;
        }
    }

    // Print the count
    // of gates required
    cout << ans;
}

// Driver Code
int main()
{
    // Input
    string S = "(1-A).B+C";

    // Function call to count the
    // total number of gates required
    numberOfGates(S);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
class GFG{

// Function to count the total
// number of gates required to
// realize the boolean expression S
static void numberOfGates(String s)
{

    // Length of the string
    int N = s.length();

    // Stores the count
    // of total gates
    int ans = 0;

    // Traverse the string
    for(int i = 0; i < (int)s.length(); i++)
    {

        // AND, OR and NOT Gate
        if (s.charAt(i) == '.' ||
            s.charAt(i) == '+' ||
            s.charAt(i) == '1')
        {
            ans++;
        }
    }

    // Print the count
    // of gates required
    System.out.println(ans);
}

// Driver Code
public static void main(String[] args)
{

    // Input
    String S = "(1-A).B+C";

    // Function call to count the
    // total number of gates required
    numberOfGates(S);
}
}

// This code is contributed by user_qa7r
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to count the total
# number of gates required to
# realize the boolean expression S
def numberOfGates(s):

    # Length of the string
    N = len(s)

    # Stores the count
    # of total gates
    ans = 0

    # Traverse the string
    for i in range(len(s)):

        # AND, OR and NOT Gate
        if (s[i] == '.' or s[i] == '+' or
            s[i] == '1'):
            ans += 1

    # Print the count
    # of gates required
    print(ans, end = "")

# Driver Code
if __name__ == "__main__":

    # Input
    S = "(1-A).B+C"

    # Function call to count the
    # total number of gates required
    numberOfGates(S)

# This code is contributed by AnkThon
```

## C#

```
// C# implementation of
// the above approach
using System;
public class GFG
{

// Function to count the total
// number of gates required to
// realize the boolean expression S
static void numberOfGates(string s)
{

    // Length of the string
    int N = s.Length;

    // Stores the count
    // of total gates
    int ans = 0;

    // Traverse the string
    for(int i = 0; i < s.Length; i++)
    {

        // AND, OR and NOT Gate
        if (s[i] == '.' ||
            s[i] == '+' ||
            s[i] == '1')
        {
            ans++;
        }
    }

    // Print the count
    // of gates required
    Console.WriteLine(ans);
}

// Driver Code
public static void Main(string[] args)
{

    // Input
    string S = "(1-A).B+C";

    // Function call to count the
    // total number of gates required
    numberOfGates(S);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to count the total
// number of gates required to
// realize the boolean expression S
function numberOfGates(s)
{

    // Length of the string
    let N = s.length;

    // Stores the count
    // of total gates
    let ans = 0;

    // Traverse the string
    for(let i = 0; i < s.length; i++)
    {

        // AND, OR and NOT Gate
        if (s[i] == '.' ||
            s[i] == '+' ||
            s[i] == '1')
        {
            ans++;
        }
    }

    // Print the count
    // of gates required
    document.write(ans);
}

// Driver Code

    // Input
    let S = "(1-A).B+C";

    // Function call to count the
    // total number of gates required
    numberOfGates(S);

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)