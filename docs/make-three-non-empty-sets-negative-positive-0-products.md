# 用负、正、0 积做三个非空套

> 原文:[https://www . geesforgeks . org/make-三-非空-集-负-正-0-积/](https://www.geeksforgeeks.org/make-three-non-empty-sets-negative-positive-0-products/)

给你一个 n 个不同整数的数组。你的任务是把这个数组分成三个非空的集合，这样以下条件成立:

1.  第一组应该包含元素，这样它们的乘积应该小于 0。
2.  第二个集合应该包含这样的元素，它们的乘积应该大于 0。
3.  第三组应该包含这样的元素，它们的乘积应该等于 0。

**注释:-**

1.  在给定数组中，每个数字必须恰好出现在一个集合中。
2.  可以假设我们总是可以做三个集合(输入数组中至少有一个负元素和一个 0)。

**例:**

```
Input : 4
        arr[] = -1 -2 -3 0
Output :  -1
          -3 -2 
           0
In this example, product of first
set is negative, product of second
set is positive and product of third
set is 0.
```

在这个问题中，我们只需要将输入数据分成 3 个向量:第一个向量包含负数，第二个包含正数，第三个包含零。如果第一个向量的大小是偶数，则将一个数字从它移到第三个向量。如果第二个向量只包含 1，则将两个数字从第一个向量移到第二个向量。

## C++

```
// CPP program to make three non-empty sets
// as per the given conditions.
#include <bits/stdc++.h>
using namespace std;

void makeSets(int arr[], int n)
{
    vector<int> first, second, third;

    // insert number equal to 0 to third set.
    // numbers greater than 0 to second set.
    // insert numbers less than 0 to first set.
    for (int i = 0; i < n; i++) {
        if (arr[i] == 0)
            third.push_back(arr[i]);
        if (arr[i] > 0)
            second.push_back(arr[i]);
        if (arr[i] < 0)
            first.push_back(arr[i]);
    }

    if (first.size() == 0 || third.size() == 0)
    {
        cout << "Not Possible";
        return;
    }

    // if second set is empty.
    if (second.size() == 0) {
        for (int i = 0; i < 2; i++)
        {
            second.push_back(first.back());
            first.pop_back();
        }
    }

    // if length of first set is even.
    if (first.size() % 2 == 0) {
        third.push_back(first.back());
        first.pop_back();
    }

    // output the first set elements.
    for (int i = 0; i < first.size(); i++)
        cout << first[i] << " ";   

    // output the second set elements.
    cout << endl;
    for (int i = 0; i < second.size(); i++)
        cout << second[i] << " ";   

    // output the third set elements.
    cout << endl;
    for (int i = 0; i < third.size(); i++)
        cout << third[i] << " ";   
}

// Driver Function
int main()
{
    int arr[] = { -1, 2, 0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    makeSets(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to make three non-empty sets
// as per the given condition.
import java.util.*;

class GFG
{

    static void makeSets(int arr[], int n)
    {
        Vector<Integer> first = new Vector<Integer>();
        Vector<Integer> second = new Vector<Integer>();
        Vector<Integer> third = new Vector<Integer>();

        // insert number equal to 0 to third set.
        // numbers greater than 0 to second set.
        // insert numbers less than 0 to first set.
        for (int i = 0; i < n; i++)
        {
            if (arr[i] == 0)
            {
                third.add(arr[i]);
            }
            if (arr[i] > 0)
            {
                second.add(arr[i]);
            }
            if (arr[i] < 0)
            {
                first.add(arr[i]);
            }
        }

        if (first.size() == 0 || third.size() == 0)
        {
            System.out.print("Not Possible");
            return;
        }

        // if second set is empty.
        if (second.size() == 0)
        {
            for (int i = 0; i < 2; i++)
            {
                second.add(first.lastElement());
                first.remove(first.size() - 1);
            }
        }

        // if length of first set is even.
        if (first.size() % 2 == 0)
        {
            third.add(first.lastElement());
            first.remove(first.size() - 1);
        }

        // output the first set elements.
        for (int i = 0; i < first.size(); i++)
        {
            System.out.print(first.get(i) + " ");
        }

        // output the second set elements.
        System.out.println();
        for (int i = 0; i < second.size(); i++)
        {
            System.out.print(second.get(i) + " ");
        }

        // output the third set elements.
        System.out.println();
        for (int i = 0; i < third.size(); i++)
        {
            System.out.print(third.get(i) + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {-1, 2, 0};
        int n = arr.length;
        makeSets(arr, n);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to make three non-empty sets
# as per the given conditions.
def makeSets(arr, n):
    first = []
    second = []
    third = []

    # insert number equal to 0 to third set.
    # numbers greater than 0 to second set.
    # insert numbers less than 0 to first set.
    for i in range(n):
        if (arr[i] == 0):
            third.append(arr[i])
        if (arr[i] > 0):
            second.append(arr[i])
        if (arr[i] < 0):
            first.append(arr[i])

    if (len(first) == 0 or len(third) == 0):
        print("Not Possible")
        return

    # if second set is empty.
    if (len(second)== 0):
        for i in range(2):
            second.append(first[-1])
            first.pop()

    # if length of first set is even.
    if (len(first) % 2 == 0):
        third.append(first[-1])
        first.pop()

    # output the first set elements.
    for i in range(len(first)):
        print(first[i], end = " ")

    # output the second set elements.
    print()
    for i in range(len(second)):
        print(second[i], end = " ")

    # output the third set elements.
    print()
    for i in range(len(third)):
        print(third[i], end = " ")

# Driver Function
arr = [-1, 2, 0]
n = len(arr)
makeSets(arr, n)

# This Code is contributed by SHUBHAMSINGH10
```

## C#

```
// C# program to make three non-empty sets
// as per the given condition.
using System;
using System.Collections.Generic;

class GFG
{

    static void makeSets(int []arr, int n)
    {
        List<int> first = new List<int>();
        List<int> second = new List<int>();
        List<int> third = new List<int>();

        // insert number equal to 0 to third set.
        // numbers greater than 0 to second set.
        // insert numbers less than 0 to first set.
        for (int i = 0; i < n; i++)
        {
            if (arr[i] == 0)
            {
                third.Add(arr[i]);
            }
            if (arr[i] > 0)
            {
                second.Add(arr[i]);
            }
            if (arr[i] < 0)
            {
                first.Add(arr[i]);
            }
        }

        if (first.Count == 0 || third.Count == 0)
        {
            Console.Write("Not Possible");
            return;
        }

        // if second set is empty.
        if (second.Count == 0)
        {
            for (int i = 0; i < 2; i++)
            {
                second.Add(first[first.Count-1]);
                first.Remove(first.Count - 1);
            }
        }

        // if length of first set is even.
        if (first.Count % 2 == 0)
        {
            third.Add(first[first.Count-1]);
            first.Remove(first.Count - 1);
        }

        // output the first set elements.
        for (int i = 0; i < first.Count; i++)
        {
            Console.Write(first[i] + " ");
        }

        // output the second set elements.
        Console.WriteLine();
        for (int i = 0; i < second.Count; i++)
        {
            Console.Write(second[i] + " ");
        }

        // output the third set elements.
    Console.WriteLine();
        for (int i = 0; i < third.Count; i++)
        {
            Console.Write(third[i] + " ");
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {-1, 2, 0};
        int n = arr.Length;
        makeSets(arr, n);
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to make three non-empty sets
// as per the given conditions.

function makeSets(arr, n) {
    let first = [], second = [], third = [];

    // insert number equal to 0 to third set.
    // numbers greater than 0 to second set.
    // insert numbers less than 0 to first set.
    for (let i = 0; i < n; i++) {
        if (arr[i] == 0)
            third.push(arr[i]);
        if (arr[i] > 0)
            second.push(arr[i]);
        if (arr[i] < 0)
            first.push(arr[i]);
    }

    if (first.length == 0 || third.length == 0) {
        document.write("Not Possible");
        return;
    }

    // if second set is empty.
    if (second.length == 0) {
        for (let i = 0; i < 2; i++) {
            second.push(first[first.length - 1]);
            first.pop();
        }
    }

    // if length of first set is even.
    if (first.length % 2 == 0) {
        third.push(first[first.length - 1]);
        first.pop();
    }

    // output the first set elements.
    for (let i = 0; i < first.length; i++)
        document.write(first[i] + " ");

    // output the second set elements.
    document.write("<br>");
    for (let i = 0; i < second.length; i++)
        document.write(second[i] + " ");

    // output the third set elements.
    document.write("<br>");
    for (let i = 0; i < third.length; i++)
        document.write(third[i] + " ");
}

// Driver Function

let arr = [-1, 2, 0];
let n = arr.length;
makeSets(arr, n);

</script>
```

**输出:**

```
-1 
2 
0
```

**时间复杂度** :- O(n)