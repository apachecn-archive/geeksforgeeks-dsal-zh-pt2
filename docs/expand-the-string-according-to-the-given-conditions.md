# 根据给定条件

展开管柱

> 原文:[https://www . geesforgeks . org/根据给定条件展开字符串/](https://www.geeksforgeeks.org/expand-the-string-according-to-the-given-conditions/)

给定类型为**“3(ab)4(CD)”**的字符串 **str** ，任务是将其扩展为“abababcdcdcdcd”，其中整数来自范围**【1，9】**。
这个问题在 2018 年 10 月举行的[thinkworks 访谈](https://www.geeksforgeeks.org/thoughtworks-interview-experience-on-campus-2/)中被问到。

**示例:**

> **输入:**str =“3(ab)4(CD)”
> **输出:** abababcdcdcdcd
> **输入:**str =“2(KL)3(AP)”
> **输出:**klklklapapp

**方法:**我们遍历字符串，等待一个数值， **num** 在位置 **i** 出现。它一到，我们就检查 **i + 1** 是否有**(“**)。如果存在，那么程序进入一个循环，提取**(“**”和**)“**中的任何内容，并将其连接成一个空字符串， **temp** 。稍后，另一个循环打印生成的字符串**编号**的次数。重复这些步骤，直到字符串结束。

以下是该方法的实施情况:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to expand and print the given string
void expandString(string strin)
{
    string temp = "";
    int j;

    for (int i = 0; i < strin.length(); i++)
    {
        if (strin[i] >= 0)
        {

            // Subtract '0' to convert char to int
            int num = strin[i] - '0';
            if (strin[i + 1] == '(')
            {

                // Characters within brackets
                for (j = i + 1; strin[j] != ')'; j++)
                {
                    if ((strin[j] >= 'a' && strin[j] <= 'z') ||
                        (strin[j] >= 'A' && strin[j] <= 'Z'))
                    {
                        temp += strin[j];
                    }
                }

                // Expanding
                for (int k = 1; k <= num; k++)
                {
                    cout << (temp);
                }

                // Reset the variables
                num = 0;
                temp = "";

                if (j < strin.length())
                {
                    i = j;
                }
            }
        }
    }
}

// Driver code
int main()
{
    string strin = "3(ab)4(cd)";
    expandString(strin);
}

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
public class GFG {

    // Function to expand and print the given string
    static void expandString(String strin)
    {
        String temp = "";
        int j;

        for (int i = 0; i < strin.length(); i++) {
            if (strin.charAt(i) >= 0) {

                // Subtract '0' to convert char to int
                int num = strin.charAt(i) - '0';
                if (strin.charAt(i + 1) == '(') {

                    // Characters within brackets
                    for (j = i + 1; strin.charAt(j) != ')'; j++) {
                        if ((strin.charAt(j) >= 'a'
                             && strin.charAt(j) <= 'z')
                            || (strin.charAt(j) >= 'A'
                                && strin.charAt(j) <= 'Z')) {
                            temp += strin.charAt(j);
                        }
                    }

                    // Expanding
                    for (int k = 1; k <= num; k++) {
                        System.out.print(temp);
                    }

                    // Reset the variables
                    num = 0;
                    temp = "";

                    if (j < strin.length()) {
                        i = j;
                    }
                }
            }
        }
    }

    // Driver code
    public static void main(String args[])
    {
        String strin = "3(ab)4(cd)";
        expandString(strin);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to expand and print the given string
def expandString(strin):

    temp = ""
    j = 0
    i = 0
    while(i < len(strin)):
        if (strin[i] >= "0"):

            # Subtract '0' to convert char to int
            num = ord(strin[i])-ord("0")
            if (strin[i + 1] == '('):

                # Characters within brackets
                j = i + 1
                while(strin[j] != ')'):
                    if ((strin[j] >= 'a' and strin[j] <= 'z') or \
                        (strin[j] >= 'A' and strin[j] <= 'Z')):
                        temp += strin[j]
                    j += 1

                # Expanding
                for k in range(1, num + 1):
                    print(temp,end="")

                # Reset the variables
                num = 0
                temp = ""
                if (j < len(strin)):
                    i = j
        i += 1

# Driver code
strin = "3(ab)4(cd)"
expandString(strin)

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation of
// the above approach
using System;
class GFG{

// Function to expand and
// print the given string
static void expandString(string strin)
{
  string temp = "";
  int j;

  for (int i = 0;
           i < strin.Length; i++)
  {
    if (strin[i] >= 0)
    {
      // Subtract '0' to
      // convert char to int
      int num = strin[i] - '0';
      if (strin[i + 1] == '(')
      {
        // Characters within brackets
        for (j = i + 1;
             strin[j] != ')'; j++)
        {
          if ((strin[j] >= 'a' &&
               strin[j] <= 'z') ||
              (strin[j] >= 'A' &&
               strin[j] <= 'Z'))
          {
            temp += strin[j];
          }
        }

        // Expanding
        for (int k = 1; k <= num; k++)
        {
          Console.Write(temp);
        }

        // Reset the variables
        num = 0;
        temp = "";

        if (j < strin.Length)
        {
          i = j;
        }
      }
    }
  }
}

// Driver code
public static void Main(String [] args)
{
  string strin = "3(ab)4(cd)";
  expandString(strin);
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

    // Function to expand and print the given string
    function expandString(strin)
    {
        let temp = "";
        let j;

        for (let i = 0; i < strin.length; i++) {
            if (strin[i].charCodeAt(0) >= 0) {

                // Subtract '0' to convert char to int
                let num = strin[i].charCodeAt(0) - '0'.charCodeAt(0);
                if (strin[i+1] == '(') {

                    // Characters within brackets
                    for (j = i + 1; strin[j] != ')'; j++) {
                        if ((strin[j] >= 'a'
                             && strin[j] <= 'z')
                            || (strin[j] >= 'A'
                                && strin[j] <= 'Z')) {
                            temp += strin[j];
                        }
                    }

                    // Expanding
                    for (let k = 1; k <= num; k++) {
                        document.write(temp);
                    }

                    // Reset the variables
                    num = 0;
                    temp = "";

                    if (j < strin.length) {
                        i = j;
                    }
                }
            }
        }
    }

    // Driver code
    let strin = "3(ab)4(cd)";
    expandString(strin);

// This code is contributed by rag2127
</script>
```

**Output:** 

```
abababcdcdcdcd
```

**时间复杂度:**O(N * N)
T3】辅助空间: O(1)