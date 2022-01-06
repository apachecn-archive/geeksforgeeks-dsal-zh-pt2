# 带有*和+

的表达式的最小值和最大值

> 原文:[https://www . geesforgeks . org/minimum-maximum-values-expression/](https://www.geeksforgeeks.org/minimum-maximum-values-expression/)

给定一个包含数字和两个运算符“+”和“*”的表达式，我们需要找到最大值和最小值，这可以通过用不同的圆括号来计算这个表达式来获得。
示例:

```
Input  : expr = “1+2*3+4*5” 
Output : Minimum Value = 27, Maximum Value = 105 
Explanation:
Minimum evaluated value = 1 + (2*3) + (4*5) = 27
Maximum evaluated value = (1 + 2)*(3 + 4)*5 = 105
```

我们可以用动态规划的方法来解决这个问题，我们可以看到这个问题类似于[矩阵链乘法](//www.geeksforgeeks.org/dynamic-programming-set-8-matrix-chain-multiplication/)，这里我们尝试不同的圆括号来最大化和最小化表达式值，而不是矩阵乘法的个数。
在下面的代码中，我们首先将运算符和数字从给定的表达式中分离出来，然后使用两个 2D 数组来存储中间结果，中间结果的更新类似于矩阵链乘法，并根据它们之间出现的运算符在数字之间尝试不同的括号。最后，第一行的最后一个单元格将在两个 2D 数组中存储最终结果。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to get maximum and minimum
// values of an expression
#include <bits/stdc++.h>
using namespace std;

// Utility method to check whether a character
// is operator or not
bool isOperator(char op)
{
    return (op == '+' || op == '*');
}

// method prints minimum and maximum value
// obtainable from an expression
void printMinAndMaxValueOfExp(string exp)
{
    vector<int> num;
    vector<char> opr;
    string tmp = "";

    //  store operator and numbers in different vectors
    for (int i = 0; i < exp.length(); i++)
    {
        if (isOperator(exp[i]))
        {
            opr.push_back(exp[i]);
            num.push_back(atoi(tmp.c_str()));
            tmp = "";
        }
        else
        {
            tmp += exp[i];
        }
    }
    //  storing last number in vector
    num.push_back(atoi(tmp.c_str()));

    int len = num.size();
    int minVal[len][len];
    int maxVal[len][len];

    //  initializing minval and maxval 2D array
    for (int i = 0; i < len; i++)
    {
        for (int j = 0; j < len; j++)
        {
            minVal[i][j] = INT_MAX;
            maxVal[i][j] = 0;

            //  initializing main diagonal by num values
            if (i == j)
                minVal[i][j] = maxVal[i][j] = num[i];
        }
    }

    // looping similar to matrix chain multiplication
    // and updating both 2D arrays
    for (int L = 2; L <= len; L++)
    {
        for (int i = 0; i < len - L + 1; i++)
        {
            int j = i + L - 1;
            for (int k = i; k < j; k++)
            {
                int minTmp = 0, maxTmp = 0;

                // if current operator is '+', updating tmp
                // variable by addition
                if(opr[k] == '+')
                {
                    minTmp = minVal[i][k] + minVal[k + 1][j];
                    maxTmp = maxVal[i][k] + maxVal[k + 1][j];
                }

                // if current operator is '*', updating tmp
                // variable by multiplication
                else if(opr[k] == '*')
                {
                    minTmp = minVal[i][k] * minVal[k + 1][j];
                    maxTmp = maxVal[i][k] * maxVal[k + 1][j];
                }

                //  updating array values by tmp variables
                if (minTmp < minVal[i][j])
                    minVal[i][j] = minTmp;
                if (maxTmp > maxVal[i][j])
                    maxVal[i][j] = maxTmp;
            }
        }
    }

    //  last element of first row will store the result
    cout << "Minimum value : " << minVal[0][len - 1]
         << ", Maximum value : " << maxVal[0][len - 1];
}

//  Driver code to test above methods
int main()
{
    string expression = "1+2*3+4*5";
    printMinAndMaxValueOfExp(expression);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to get maximum and minimum
// values of an expression
import java.io.*;
import java.util.*;
class GFG
{

  // Utility method to check whether a character
  // is operator or not
  static boolean isOperator(char op)
  {
    return (op == '+' || op == '*');
  }

  // method prints minimum and maximum value
  // obtainable from an expression
  static void printMinAndMaxValueOfExp(String exp)
  {
    Vector<Integer> num = new Vector<Integer>();
    Vector<Character> opr = new Vector<Character>();
    String tmp = "";

    //  store operator and numbers in different vectors
    for (int i = 0; i < exp.length(); i++)
    {
      if (isOperator(exp.charAt(i)))
      {
        opr.add(exp.charAt(i));
        num.add(Integer.parseInt(tmp));
        tmp = "";
      }
      else
      {
        tmp += exp.charAt(i);
      }
    }

    //  storing last number in vector
    num.add(Integer.parseInt(tmp));

    int len = num.size();
    int[][] minVal = new int[len][len];
    int[][] maxVal = new int[len][len];

    //  initializing minval and maxval 2D array
    for (int i = 0; i < len; i++)
    {
      for (int j = 0; j < len; j++)
      {
        minVal[i][j] = Integer.MAX_VALUE;
        maxVal[i][j] = 0;

        //  initializing main diagonal by num values
        if (i == j)
          minVal[i][j] = maxVal[i][j]
          = num.get(i);
      }
    }

    // looping similar to matrix chain multiplication
    // and updating both 2D arrays
    for (int L = 2; L <= len; L++)
    {
      for (int i = 0; i < len - L + 1; i++)
      {
        int j = i + L - 1;
        for (int k = i; k < j; k++)
        {
          int minTmp = 0, maxTmp = 0;

          // if current operator is '+', updating
          // tmp variable by addition
          if (opr.get(k) == '+')
          {
            minTmp = minVal[i][k]
              + minVal[k + 1][j];
            maxTmp = maxVal[i][k]
              + maxVal[k + 1][j];
          }

          // if current operator is '*', updating
          // tmp variable by multiplication
          else if (opr.get(k) == '*')
          {
            minTmp = minVal[i][k]
              * minVal[k + 1][j];
            maxTmp = maxVal[i][k]
              * maxVal[k + 1][j];
          }

          //  updating array values by tmp
          //  variables
          if (minTmp < minVal[i][j])
            minVal[i][j] = minTmp;
          if (maxTmp > maxVal[i][j])
            maxVal[i][j] = maxTmp;
        }
      }
    }

    //  last element of first row will store the result
    System.out.print(
      "Minimum value : " + minVal[0][len - 1]
      + ", Maximum value : " + maxVal[0][len - 1]);
  }

  //  Driver code to test above methods
  public static void main(String[] args)
  {
    String expression = "1+2*3+4*5";
    printMinAndMaxValueOfExp(expression);
  }
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program to get maximum and minimum
# values of an expression

# Utility method to check whether a character
# is operator or not
def isOperator(op):
    return (op == '+' or op == '*')

# method prints minimum and maximum value
# obtainable from an expression
def printMinAndMaxValueOfExp(exp):
    num = []
    opr = []
    tmp = ""

    # store operator and numbers in different vectors
    for i in range(len(exp)):
        if (isOperator(exp[i])):
            opr.append(exp[i])
            num.append(int(tmp))
            tmp = ""
        else:
            tmp += exp[i]

    # storing last number in vector
    num.append(int(tmp))

    llen = len(num)
    minVal = [[ 0 for i in range(llen)] for i in range(llen)]
    maxVal = [[ 0 for i in range(llen)] for i in range(llen)]

    # initializing minval and maxval 2D array
    for i in range(llen):
        for j in range(llen):
            minVal[i][j] = 10**9
            maxVal[i][j] = 0

            # initializing main diagonal by num values
            if (i == j):
                minVal[i][j] = maxVal[i][j] = num[i]

    # looping similar to matrix chain multiplication
    # and updating both 2D arrays
    for L in range(2, llen + 1):
        for i in range(llen - L + 1):
            j = i + L - 1
            for k in range(i, j):

                minTmp = 0
                maxTmp = 0

                # if current operator is '+', updating tmp
                # variable by addition
                if(opr[k] == '+'):

                    minTmp = minVal[i][k] + minVal[k + 1][j]
                    maxTmp = maxVal[i][k] + maxVal[k + 1][j]

                # if current operator is '*', updating tmp
                # variable by multiplication
                elif(opr[k] == '*'):

                    minTmp = minVal[i][k] * minVal[k + 1][j]
                    maxTmp = maxVal[i][k] * maxVal[k + 1][j]

                # updating array values by tmp variables
                if (minTmp < minVal[i][j]):
                    minVal[i][j] = minTmp
                if (maxTmp > maxVal[i][j]):
                    maxVal[i][j] = maxTmp

    # last element of first row will store the result
    print("Minimum value : ",minVal[0][llen - 1],", \
            Maximum value : ",maxVal[0][llen - 1])

# Driver code
expression = "1+2*3+4*5"
printMinAndMaxValueOfExp(expression)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to get maximum and minimum
// values of an expression
using System;
using System.Collections.Generic;

public class GFG
{

  // Utility method to check whether a character
  // is operator or not
  static bool isOperator(char op)
  {
    return (op == '+' || op == '*');
  }

  // method prints minimum and maximum value
  // obtainable from an expression
  static void printMinAndMaxValueOfExp(string exp)
  {
    List<int> num = new List<int>();
    List<char> opr = new List<char>();

    string tmp = "";

    //  store operator and numbers in different vectors
    for (int i = 0; i < exp.Length; i++)
    {
      if (isOperator(exp[i]))
      {
        opr.Add(exp[i]);
        num.Add(int.Parse(tmp));
        tmp = "";
      }
      else
      {
        tmp += exp[i];
      }
    }

    //  storing last number in vector
    num.Add(int.Parse(tmp));      
    int len = num.Count;
    int[,] minVal = new int[len,len];
    int[,] maxVal = new int[len,len];

    //  initializing minval and maxval 2D array
    for (int i = 0; i < len; i++)
    {
      for (int j = 0; j < len; j++)
      {
        minVal[i, j] = Int32.MaxValue;
        maxVal[i, j] = 0;

        //  initializing main diagonal by num values
        if (i == j)
        {
          minVal[i, j] = maxVal[i, j] = num[i];
        }
      }
    }

    // looping similar to matrix chain multiplication
    // and updating both 2D arrays
    for (int L = 2; L <= len; L++)
    {
      for (int i = 0; i < len - L + 1; i++)
      {
        int j = i + L - 1;
        for (int k = i; k < j; k++)
        {
          int minTmp = 0, maxTmp = 0;

          // if current operator is '+', updating
          // tmp variable by addition
          if (opr[k] == '+')
          {
            minTmp = minVal[i, k] + minVal[k + 1, j];
            maxTmp = maxVal[i, k] + maxVal[k + 1, j];
          }

          // if current operator is '*', updating
          // tmp variable by multiplication
          else if (opr[k] == '*')
          {
            minTmp = minVal[i, k] * minVal[k + 1, j];
            maxTmp = maxVal[i, k] * maxVal[k + 1, j];
          }

          //  updating array values by tmp
          //  variables
          if (minTmp < minVal[i, j])
            minVal[i, j] = minTmp;
          if (maxTmp > maxVal[i, j])
            maxVal[i, j] = maxTmp;
        }
      }
    }

    //  last element of first row will store the result
    Console.Write("Minimum value : " +
                  minVal[0, len - 1] +
                  ", Maximum value : " +
                  maxVal[0,len - 1]);

  }

  //  Driver code to test above methods
  static public void Main ()
  {
    string expression = "1+2*3+4*5";
    printMinAndMaxValueOfExp(expression);
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// JavaScript program to get maximum and minimum
// values of an expression

// Utility method to check whether a character
// is operator or not
function isOperator(op)
{
    return (op == '+' || op == '*');
}

 // method prints minimum and maximum value
  // obtainable from an expression
function printMinAndMaxValueOfExp(exp)
{
    let num = [];
    let opr = [];
    let tmp = "";

    //  store operator and numbers in different vectors
    for (let i = 0; i < exp.length; i++)
    {
      if (isOperator(exp[i]))
      {
        opr.push(exp[i]);
        num.push(parseInt(tmp));
        tmp = "";
      }
      else
      {
        tmp += exp[i];
      }
    }

    //  storing last number in vector
    num.push(parseInt(tmp));

    let len = num.length;
    let minVal = new Array(len);
    let maxVal = new Array(len);

    //  initializing minval and maxval 2D array
    for (let i = 0; i < len; i++)
    {
        minVal[i]=new Array(len);
        maxVal[i]=new Array(len);
      for (let j = 0; j < len; j++)
      {
        minVal[i][j] = Number.MAX_VALUE;
        maxVal[i][j] = 0;

        //  initializing main diagonal by num values
        if (i == j)
          minVal[i][j] = maxVal[i][j]
          = num[i];
      }
    }

    // looping similar to matrix chain multiplication
    // and updating both 2D arrays
    for (let L = 2; L <= len; L++)
    {
      for (let i = 0; i < len - L + 1; i++)
      {
        let j = i + L - 1;
        for (let k = i; k < j; k++)
        {
          let minTmp = 0, maxTmp = 0;

          // if current operator is '+', updating
          // tmp variable by addition
          if (opr[k] == '+')
          {
            minTmp = minVal[i][k]
              + minVal[k + 1][j];
            maxTmp = maxVal[i][k]
              + maxVal[k + 1][j];
          }

          // if current operator is '*', updating
          // tmp variable by multiplication
          else if (opr[k] == '*')
          {
            minTmp = minVal[i][k]
              * minVal[k + 1][j];
            maxTmp = maxVal[i][k]
              * maxVal[k + 1][j];
          }

          //  updating array values by tmp
          //  variables
          if (minTmp < minVal[i][j])
            minVal[i][j] = minTmp;
          if (maxTmp > maxVal[i][j])
            maxVal[i][j] = maxTmp;
        }
      }
    }

    //  last element of first row will store the result
    document.write(
      "Minimum value : " + minVal[0][len - 1]
      + ", Maximum value : " + maxVal[0][len - 1]);
}

//  Driver code to test above methods
let expression = "1+2*3+4*5";
printMinAndMaxValueOfExp(expression);

// This code is contributed by ab2127

</script>
```

**输出:**

```
Minimum value : 27, Maximum value : 105
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。