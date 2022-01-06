# 最小化给定多项式的根的和

> 原文:[https://www . geesforgeks . org/minimum-sum-root-给定-多项式/](https://www.geeksforgeeks.org/minimize-sum-roots-given-polynomial/)

给定一个数组，它的元素代表 n 次多项式的系数，如果多项式有 n 次，那么这个数组将有 n+1 个元素(一个多项式常数多一个元素)。交换数组的一些元素并打印结果数组，使得给定多项式的根之和尽可能最小，而不考虑根的性质。
注意:除了数组元素的第一个元素也可以是 0，多项式的次数总是大于 1。

**示例:**

```
Input : -4 1 6 -3 -2 -1
Output : 1 6 -4 -3 -2 -1
        Here, the array is -4, 1, 6, -3, -2, -1
        i.e the polynomial is -4.x^5 + 1.x^4 + 6.x^3 - 3.x^2 - 2.x^1 - 1
        minimum sum = -6 

Input : -9 0 9
Output :-9 0 9
       Here polynomial is 
       -9.x^2 + 0.x^1 + 9
       minimum sum = 0
```

**解:**让我们回忆一下关于多项式的根之和的事实如果多项式 p(x) = a.x^n + b.x^n-1 + c.x^n-2 + … + k，那么多项式的根之和由 **-b/a** 给出。详见[维埃塔公式](https://en.wikipedia.org/wiki/Vieta%27s_formulas)。
我们必须最小化-b/a，即最大化 b/a，即最大化 b 和最小化 a。因此，如果我们能够最大化 b 和最小化 a，我们将交换系数的值，并原样复制数组的其余部分。

> 会有四种情况:
> **情况#1:当正系数的个数和负系数的个数都大于等于 2 时**
> 在这种情况下，我们会从正元素和负元素中找到一个最大值和最小值，我们会检查-(maxPos)/(minPos)是更小还是-( abs(maxNeg) )/ ( abs(minNeg))更小，并在对换后相应打印答案。
> **情况 2:当正系数个数大于等于 2 但负系数个数小于 2 时**
> 在这种情况下，我们只考虑正元素的最大值和正元素的最小值的情况。因为如果我们从正元素中选取一个，从负元素中选取另一个，那么-b/a 的结果将是一个正值，这个值不是最小值。(由于我们要求较大的负值)
> **情况 3:当负系数个数大于等于 2 但正系数个数小于 2 时**
> 在这种情况下，我们将只考虑负元素的最大值和最小值的情况。因为如果我们从正元素中选取一个，从负元素中选取另一个，那么-b/a 的结果将是一个正值，这个值不是最小值。(因为我们需要一个大的负值)
> **情况 4:当两个计数都小于或等于 1 时**
> 仔细观察，在这种情况下不能交换元素。

## C++

```
// C++ program to find minimum sum of roots of a
// given polynomial
#include <bits/stdc++.h>
using namespace std;

void getMinimumSum(int arr[], int n)
{
    // resultant vector
    vector<int> res;

    // a vector that store indices of the positive
    // elements
    vector<int> pos;

    // a vector that store indices of the negative
    // elements
    vector<int> neg;

    for (int i = 0; i < n; i++) {
        if (arr[i] > 0)
            pos.push_back(i);       
        else if (arr[i] < 0)
            neg.push_back(i);       
    }

    // Case - 1:
    if (pos.size() >= 2 && neg.size() >= 2) {
        int posMax = INT_MIN, posMaxIdx = -1;
        int posMin = INT_MAX, posMinIdx = -1;

        int negMax = INT_MIN, negMaxIdx = -1;
        int negMin = INT_MAX, negMinIdx = -1;

        for (int i = 0; i < pos.size(); i++) {
            if (arr[pos[i]] > posMax) {
                posMaxIdx = pos[i];
                posMax = arr[posMaxIdx];
            }
        }

        for (int i = 0; i < pos.size(); i++) {
            if (arr[pos[i]] < posMin &&
                pos[i] != posMaxIdx) {
                posMinIdx = pos[i];
                posMin = arr[posMinIdx];
            }
        }

        for (int i = 0; i < neg.size(); i++) {
            if (abs(arr[neg[i]]) > negMax) {
                negMaxIdx = neg[i];
                negMax = abs(arr[negMaxIdx]);
            }
        }

        for (int i = 0; i < neg.size(); i++) {
            if (abs(arr[neg[i]]) < negMin &&
                neg[i] != negMaxIdx) {
                negMinIdx = neg[i];
                negMin = abs(arr[negMinIdx]);
            }
        }

        double posVal = -1.0 * (double)posMax / (double)posMin;
        double negVal = -1.0 * (double)negMax / (double)negMin;

        if (posVal < negVal) {
            res.push_back(arr[posMinIdx]);
            res.push_back(arr[posMaxIdx]);

            for (int i = 0; i < n; i++) {
                if (i != posMinIdx && i != posMaxIdx) {
                    res.push_back(arr[i]);
                }
            }
        }
        else {
            res.push_back(arr[negMinIdx]);
            res.push_back(arr[negMaxIdx]);

            for (int i = 0; i < n; i++) {
                if (i != negMinIdx && i != negMaxIdx) {
                    res.push_back(arr[i]);
                }
            }
        }
        for (int i = 0; i < res.size(); i++) {
            cout << res[i] << " ";
        }
        cout << "\n";
    }

    // Case - 2:
    else if (pos.size() >= 2) {
        int posMax = INT_MIN, posMaxIdx = -1;
        int posMin = INT_MAX, posMinIdx = -1;

        for (int i = 0; i < pos.size(); i++) {
            if (arr[pos[i]] > posMax) {
                posMaxIdx = pos[i];
                posMax = arr[posMaxIdx];
            }
        }

        for (int i = 0; i < pos.size(); i++) {
            if (arr[pos[i]] < posMin &&
                pos[i] != posMaxIdx) {
                posMinIdx = pos[i];
                posMin = arr[posMinIdx];
            }
        }

        res.push_back(arr[posMinIdx]);
        res.push_back(arr[posMaxIdx]);

        for (int i = 0; i < n; i++) {
            if (i != posMinIdx && i != posMaxIdx) {
                res.push_back(arr[i]);
            }
        }
        for (int i = 0; i < res.size(); i++) {
            cout << res[i] << " ";
        }
        cout << "\n";
    }

    // Case - 3:
    else if (neg.size() >= 2) {
        int negMax = INT_MIN, negMaxIdx = -1;
        int negMin = INT_MAX, negMinIdx = -1;

        for (int i = 0; i < neg.size(); i++) {
            if (abs(arr[neg[i]]) > negMax) {
                negMaxIdx = neg[i];
                negMax = abs(arr[negMaxIdx]);
            }
        }

        for (int i = 0; i < neg.size(); i++) {
            if (abs(arr[neg[i]]) < negMin &&
                neg[i] != negMaxIdx) {
                negMinIdx = neg[i];
                negMin = abs(arr[negMinIdx]);
            }
        }

        res.push_back(arr[negMinIdx]);
        res.push_back(arr[negMaxIdx]);

        for (int i = 0; i < n; i++)
            if (i != negMinIdx && i != negMaxIdx)
                res.push_back(arr[i]);

        for (int i = 0; i < res.size(); i++)
            cout << res[i] << " ";

        cout << "\n";
    }

    // Case - 4:
    else {
        cout << "No swap required\n";
    }
}

int main()
{
    int arr[] = { -4, 1, 6, -3, -2, -1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    getMinimumSum(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java  program to find minimum sum of roots of a
// given polynomial
import java.io.*;
import java.util.*;

class GFG
{   
  static void getMinimumSum(int arr[], int n)
  {

    // resultant vector
    ArrayList<Integer> res = new ArrayList<Integer>();

    // a vector that store indices of the positive
    // elements
    ArrayList<Integer> pos = new ArrayList<Integer>();

    // a vector that store indices of the negative
    // elements
    ArrayList<Integer> neg = new ArrayList<Integer>();

    for (int i = 0; i < n; i++)
    {
      if (arr[i] > 0)
        pos.add(i);       
      else if (arr[i] < 0)
        neg.add(i);       
    }

    // Case - 1:
    if (pos.size() >= 2 && neg.size() >= 2) {
      int posMax = Integer.MIN_VALUE, posMaxIdx = -1;
      int posMin = Integer.MAX_VALUE, posMinIdx = -1;

      int negMax = Integer.MIN_VALUE, negMaxIdx = -1;
      int negMin = Integer.MAX_VALUE, negMinIdx = -1;

      for (int i = 0; i < pos.size(); i++) {
        if (arr[pos.get(i)] > posMax) {
          posMaxIdx = pos.get(i);
          posMax = arr[posMaxIdx];
        }
      }

      for (int i = 0; i < pos.size(); i++) {
        if (arr[pos.get(i)] < posMin &&
            pos.get(i) != posMaxIdx) {
          posMinIdx = pos.get(i);
          posMin = arr[posMinIdx];
        }
      }

      for (int i = 0; i < neg.size(); i++) {
        if (Math.abs(arr[neg.get(i)]) > negMax) {
          negMaxIdx = neg.get(i);
          negMax = Math.abs(arr[negMaxIdx]);
        }
      }

      for (int i = 0; i < neg.size(); i++) {
        if (Math.abs(arr[neg.get(i)]) < negMin &&
            neg.get(i) != negMaxIdx) {
          negMinIdx = neg.get(i);
          negMin = Math.abs(arr[negMinIdx]);
        }
      }

      double posVal = -1.0 * (double)posMax / (double)posMin;
      double negVal = -1.0 * (double)negMax / (double)negMin;

      if (posVal < negVal) {
        res.add(arr[posMinIdx]);
        res.add(arr[posMaxIdx]);

        for (int i = 0; i < n; i++) {
          if (i != posMinIdx && i != posMaxIdx) {
            res.add(arr[i]);
          }
        }
      }
      else {
        res.add(arr[negMinIdx]);
        res.add(arr[negMaxIdx]);

        for (int i = 0; i < n; i++) {
          if (i != negMinIdx && i != negMaxIdx) {
            res.add(arr[i]);
          }
        }
      }
      for (int i = 0; i < res.size(); i++) {
        System.out.print(res.get(i) + " ");

      }
      System.out.println();

    }

    // Case - 2:
    else if (pos.size() >= 2) {
      int posMax = Integer.MIN_VALUE, posMaxIdx = -1;
      int posMin = Integer.MAX_VALUE, posMinIdx = -1;

      for (int i = 0; i < pos.size(); i++) {
        if (arr[pos.get(i)] > posMax) {
          posMaxIdx = pos.get(i);
          posMax = arr[posMaxIdx];
        }
      }

      for (int i = 0; i < pos.size(); i++) {
        if (arr[pos.get(i)] < posMin &&
            pos.get(i) != posMaxIdx) {
          posMinIdx = pos.get(i);
          posMin = arr[posMinIdx];
        }
      }

      res.add(arr[posMinIdx]);
      res.add(arr[posMaxIdx]);

      for (int i = 0; i < n; i++) {
        if (i != posMinIdx && i != posMaxIdx) {
          res.add(arr[i]);
        }
      }
      for (int i = 0; i < res.size(); i++) {
        System.out.print(res.get(i)+" ");

      }
      System.out.println();

    }

    // Case - 3:
    else if (neg.size() >= 2) {
      int negMax = Integer.MIN_VALUE, negMaxIdx = -1;
      int negMin = Integer.MAX_VALUE, negMinIdx = -1;

      for (int i = 0; i < neg.size(); i++) {
        if (Math.abs(arr[neg.get(i)]) > negMax) {
          negMaxIdx = neg.get(i);
          negMax = Math.abs(arr[negMaxIdx]);
        }
      }

      for (int i = 0; i < neg.size(); i++) {
        if (Math.abs(arr[neg.get(i)]) < negMin &&
            neg.get(i) != negMaxIdx) {
          negMinIdx = neg.get(i);
          negMin = Math.abs(arr[negMinIdx]);
        }
      }

      res.add(arr[negMinIdx]);
      res.add(arr[negMaxIdx]);

      for (int i = 0; i < n; i++)
        if (i != negMinIdx && i != negMaxIdx)
          res.add(arr[i]);

      for (int i = 0; i < res.size(); i++)
        System.out.println(res.get(i)+" ");

      System.out.println();

    }

    // Case - 4:
    else {
      System.out.println("No swap required");

    }
  }

  // Driver code
  public static void main (String[] args)
  {
    int arr[] = { -4, 1, 6, -3, -2, -1 };
    int n = arr.length;
    getMinimumSum(arr, n);
  }
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 program to find
# minimum sum of roots of a
# given polynomial
import sys

def getMinimumSum(arr, n):

    # resultant list
    res = []

    # a lis that store indices
    # of the positive
    # elements
    pos = []

    # a list that store indices
    # of the negative
    # elements
    neg = []

    for i in range(n):
        if (arr[i] > 0):
            pos.append(i)
        elif (arr[i] < 0):
            neg.append(i)

    # Case - 1:
    if (len(pos) >= 2 and
        len(neg) >= 2):
        posMax = -sys.maxsize-1
        posMaxIdx = -1
        posMin = sys.maxsize
        posMinIdx = -1
        negMax = -sys.maxsize-1
        negMaxIdx = -1
        negMin = sys.maxsize
        negMinIdx = -1

        for i in range(len(pos)):
            if (arr[pos[i]] > posMax):
                posMaxIdx = pos[i]
                posMax = arr[posMaxIdx]

        for i in range(len(pos)):
            if (arr[pos[i]] < posMin and
                    pos[i] != posMaxIdx):
                posMinIdx = pos[i]
                posMin = arr[posMinIdx]

        for i in range(len(neg)):
            if (abs(arr[neg[i]]) > negMax):
                negMaxIdx = neg[i]
                negMax = abs(arr[negMaxIdx])

        for i in range(len(neg)):
            if (abs(arr[neg[i]]) < negMin and
                    neg[i] != negMaxIdx):
                negMinIdx = neg[i]
                negMin = abs(arr[negMinIdx])

        posVal = (-1.0 * posMax /
                         posMin)
        negVal = (-1.0 * negMax /
                         negMin)

        if (posVal < negVal):
            res.append(arr[posMinIdx])
            res.append(arr[posMaxIdx])

            for i in range(n):
                if (i != posMinIdx and
                    i != posMaxIdx):
                    res.append(arr[i])
        else:
            res.append(arr[negMinIdx])
            res.append(arr[negMaxIdx])

            for i in range(n):
                if (i != negMinIdx and
                    i != negMaxIdx):
                    resal.append(arr[i])

        for i in range(len(res)):
            print(res[i], end = " ")

        print()

    # Case - 2:
    elif (len(pos) >= 2):
        posMax = -sys.maxsize
        posMaxIdx = -1
        posMin = sys.maxsize
        posMinIdx = -1

        for i in range(len(pos)):
            if (arr[pos[i]] > posMax):
                posMaxIdx = pos[i]
                posMax = arr[posMaxIdx]

        for i in range(len(pos)):
            if (arr[pos[i]] < posMin and
                    pos[i] != posMaxIdx):
                posMinIdx = pos[i]
                posMin = arr[posMinIdx]

        res.append(arr[posMinIdx])
        res.append(arr[posMaxIdx])

        for i in range(n):
            if (i != posMinIdx and
                i != posMaxIdx):
                res.append(arr[i])

        for i in range(len(res)):
            print(res[i], end = " ")

        print()

    # Case - 3:
    elif (len(neg) >= 2):
        negMax = -sys.maxsize
        negMaxIdx = -1
        negMin = sys.maxsize
        negMinIdx = -1

        for i in range(len(neg)):
            if (abs(arr[neg[i]]) > negMax):
                negMaxIdx = neg[i]
                negMax = abs(arr[negMaxIdx])

        for i in range(len(neg)):
            if (abs(arr[neg[i]]) < negMin and
                    neg[i] != negMaxIdx):
                negMinIdx = neg[i]
                negMin = abs(arr[negMinIdx])

        res.append(arr[negMinIdx])
        res.append(arr[negMaxIdx])

        for i in range(n):
            if (i != negMinIdx and
                i != negMaxIdx):
                res.append(arr[i])

        for i in range(len(res)):
            print(res[i], end = " ")

        print()

    # Case - 4:
    else:
        print("No swap required")

# Driver code
if __name__ == "__main__":

    arr = [-4, 1, 6,
           -3, -2, -1]
    n = len(arr)
    getMinimumSum(arr, n)

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find minimum sum of
// roots of a given polynomial
using System;
using System.Collections.Generic;

class GFG{

static void getMinimumSum(int[] arr, int n)
{

    // resultant vector
    List<int> res = new List<int>();

    // a vector that store indices of the positive
    // elements
    List<int> pos = new List<int>();

    // a vector that store indices of the negative
    // elements
    List<int> neg = new List<int>();

    for(int i = 0; i < n; i++)
    {
        if (arr[i] > 0)
            pos.Add(i);       
        else if (arr[i] < 0)
            neg.Add(i);       
    }

    // Case - 1:
    if (pos.Count >= 2 && neg.Count >= 2)
    {
        int posMax = Int32.MinValue, posMaxIdx = -1;
        int posMin = Int32.MaxValue, posMinIdx = -1;

        int negMax = Int32.MinValue, negMaxIdx = -1;
        int negMin = Int32.MaxValue, negMinIdx = -1;

        for(int i = 0; i < pos.Count; i++)
        {
            if (arr[pos[i]] > posMax)
            {
                posMaxIdx = pos[i];
                posMax = arr[posMaxIdx];
            }
        }

        for(int i = 0; i < pos.Count; i++)
        {
            if (arr[pos[i]] < posMin &&
                pos[i] != posMaxIdx)
            {
                posMinIdx = pos[i];
                posMin = arr[posMinIdx];
            }
        }

        for(int i = 0; i < neg.Count; i++)
        {
            if (Math.Abs(arr[neg[i]]) > negMax)
            {
                negMaxIdx = neg[i];
                negMax = Math.Abs(arr[negMaxIdx]);
            }
        }

        for(int i = 0; i < neg.Count; i++)
        {
            if (Math.Abs(arr[neg[i]]) < negMin &&
                             neg[i] != negMaxIdx)
            {
                negMinIdx = neg[i];
                negMin = Math.Abs(arr[negMinIdx]);
            }
        }

        double posVal = -1.0 * (double)posMax / (double)posMin;
        double negVal = -1.0 * (double)negMax / (double)negMin;

        if (posVal < negVal)
        {
            res.Add(arr[posMinIdx]);
            res.Add(arr[posMaxIdx]);

            for(int i = 0; i < n; i++)
            {
                if (i != posMinIdx && i != posMaxIdx)
                {
                    res.Add(arr[i]);
                }
            }
        }
        else
        {
            res.Add(arr[negMinIdx]);
            res.Add(arr[negMaxIdx]);

            for(int i = 0; i < n; i++)
            {
                if (i != negMinIdx && i != negMaxIdx)
                {
                    res.Add(arr[i]);
                }
            }
        }
        for(int i = 0; i < res.Count; i++)
        {
            Console.Write(res[i] + " ");
        }
        Console.WriteLine();
    }

    // Case - 2:
    else if (pos.Count >= 2)
    {
        int posMax = Int32.MinValue, posMaxIdx = -1;
        int posMin = Int32.MaxValue, posMinIdx = -1;

        for(int i = 0; i < pos.Count; i++)
        {
            if (arr[pos[i]] > posMax)
            {
                posMaxIdx = pos[i];
                posMax = arr[posMaxIdx];
            }
        }

        for(int i = 0; i < pos.Count; i++)
        {
            if (arr[pos[i]] < posMin &&
                    pos[i] != posMaxIdx)
            {
                posMinIdx = pos[i];
                posMin = arr[posMinIdx];
            }
        }

        res.Add(arr[posMinIdx]);
        res.Add(arr[posMaxIdx]);

        for(int i = 0; i < n; i++)
        {
            if (i != posMinIdx && i != posMaxIdx)
            {
                res.Add(arr[i]);
            }
        }
        for(int i = 0; i < res.Count; i++)
        {
            Console.Write(res[i] + " ");
        }
        Console.WriteLine();
    }

    // Case - 3:
    else if (neg.Count >= 2)
    {
        int negMax = Int32.MinValue, negMaxIdx = -1;
        int negMin = Int32.MaxValue, negMinIdx = -1;

        for(int i = 0; i < neg.Count; i++)
        {
            if (Math.Abs(arr[neg[i]]) > negMax)
            {
                negMaxIdx = neg[i];
                negMax = Math.Abs(arr[negMaxIdx]);
            }
        }

        for(int i = 0; i < neg.Count; i++)
        {
            if (Math.Abs(arr[neg[i]]) < negMin &&
                             neg[i] != negMaxIdx)
            {
                negMinIdx = neg[i];
                negMin = Math.Abs(arr[negMinIdx]);
            }
        }

        res.Add(arr[negMinIdx]);
        res.Add(arr[negMaxIdx]);

        for(int i = 0; i < n; i++)
            if (i != negMinIdx && i != negMaxIdx)
                res.Add(arr[i]);

        for(int i = 0; i < res.Count; i++)
            Console.WriteLine(res[i] + " ");

        Console.WriteLine();
    }

    // Case - 4:
    else
    {
        Console.WriteLine("No swap required");
    }
}

// Driver code
static public void Main()
{
    int[] arr = { -4, 1, 6, -3, -2, -1 };
    int n = arr.Length;

    getMinimumSum(arr, n);
}
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// Javascript  program to find minimum sum of roots of a
// given polynomial

function getMinimumSum(arr,n)
{
    // resultant vector
    let res = [] ;

    // a vector that store indices of the positive
    // elements
    let pos = [] ;

    // a vector that store indices of the negative
    // elements
    let neg = [];

    for (let i = 0; i < n; i++)
    {
      if (arr[i] > 0)
        pos.push(i);      
      else if (arr[i] < 0)
        neg.push(i);      
    }

    // Case - 1:
    if (pos.length >= 2 && neg.length >= 2) {
      let posMax = Number.MIN_VALUE, posMaxIdx = -1;
      let posMin = Number.MAX_VALUE, posMinIdx = -1;

      let negMax = Number.MIN_VALUE, negMaxIdx = -1;
      let negMin = Number.MAX_VALUE, negMinIdx = -1;

      for (let i = 0; i < pos.length; i++) {
        if (arr[pos[i]] > posMax) {
          posMaxIdx = pos[i];
          posMax = arr[posMaxIdx];
        }
      }

      for (let i = 0; i < pos.length; i++) {
        if (arr[pos[i]] < posMin &&
            pos[i] != posMaxIdx) {
          posMinIdx = pos[i];
          posMin = arr[posMinIdx];
        }
      }

      for (let i = 0; i < neg.length; i++) {
        if (Math.abs(arr[neg[i]]) > negMax) {
          negMaxIdx = neg[i];
          negMax = Math.abs(arr[negMaxIdx]);
        }
      }

      for (let i = 0; i < neg.length; i++) {
        if (Math.abs(arr[neg[i]]) < negMin &&
            neg[i] != negMaxIdx) {
          negMinIdx = neg[i];
          negMin = Math.abs(arr[negMinIdx]);
        }
      }

      let posVal = -1.0 * posMax / posMin;
      let negVal = -1.0 * negMax / negMin;

      if (posVal < negVal) {
        res.push(arr[posMinIdx]);
        res.push(arr[posMaxIdx]);

        for (let i = 0; i < n; i++) {
          if (i != posMinIdx && i != posMaxIdx) {
            res.push(arr[i]);
          }
        }
      }
      else {
        res.push(arr[negMinIdx]);
        res.push(arr[negMaxIdx]);

        for (let i = 0; i < n; i++) {
          if (i != negMinIdx && i != negMaxIdx) {
            res.push(arr[i]);
          }
        }
      }
      for (let i = 0; i < res.length; i++) {
        document.write(res[i] + " ");

      }
      document.write("<br>");

    }

    // Case - 2:
    else if (pos.length >= 2) {
      let posMax = Number.MIN_VALUE, posMaxIdx = -1;
      let posMin = Number.MAX_VALUE, posMinIdx = -1;

      for (let i = 0; i < pos.length; i++) {
        if (arr[pos[i]] > posMax) {
          posMaxIdx = pos[i];
          posMax = arr[posMaxIdx];
        }
      }

      for (let i = 0; i < pos.length; i++) {
        if (arr[pos[i]] < posMin &&
            pos[i] != posMaxIdx) {
          posMinIdx = pos[i];
          posMin = arr[posMinIdx];
        }
      }

      res.push(arr[posMinIdx]);
      res.push(arr[posMaxIdx]);

      for (let i = 0; i < n; i++) {
        if (i != posMinIdx && i != posMaxIdx) {
          res.push(arr[i]);
        }
      }
      for (let i = 0; i < res.length; i++) {
        document.write(res[i]+" ");

      }
      document.write("<br>");

    }

    // Case - 3:
    else if (neg.length >= 2) {
      let negMax = Number.MIN_VALUE, negMaxIdx = -1;
      let negMin = Number.MAX_VALUE, negMinIdx = -1;

      for (let i = 0; i < neg.length; i++) {
        if (Math.abs(arr[neg[i]]) > negMax) {
          negMaxIdx = neg[i];
          negMax = Math.abs(arr[negMaxIdx]);
        }
      }

      for (let i = 0; i < neg.length; i++) {
        if (Math.abs(arr[neg[i]]) < negMin &&
            neg[i] != negMaxIdx) {
          negMinIdx = neg[i];
          negMin = Math.abs(arr[negMinIdx]);
        }
      }

      res.push(arr[negMinIdx]);
      res.push(arr[negMaxIdx]);

      for (let i = 0; i < n; i++)
        if (i != negMinIdx && i != negMaxIdx)
          res.push(arr[i]);

      for (let i = 0; i < res.length; i++)
        document.write(res[i]+" ");

      document.write("<br>");

    }

    // Case - 4:
    else {
      document.write("No swap required");

    }

}

// Driver code
let arr=[-4, 1, 6, -3, -2, -1];
let n = arr.length;
getMinimumSum(arr, n);

    // This code is contributed by unknown2108
</script>
```

**Output:** 

```
1 6 -4 -3 -2 -1
```