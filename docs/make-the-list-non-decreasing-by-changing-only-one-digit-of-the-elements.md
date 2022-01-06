# 通过只改变元素的一个数字使列表不减少

> 原文:[https://www . geeksforgeeks . org/上榜-非减非改-仅一位数的元素/](https://www.geeksforgeeks.org/make-the-list-non-decreasing-by-changing-only-one-digit-of-the-elements/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，其中每个元素都来自于范围**【1000，9999】**。任务是通过仅改变数组元素中的一个数字来使数组**不减少**，并且结果列表的元素必须来自给定的元素范围。如果可以通过给定的操作使数组不减少，则打印更新的列表，否则打印 **-1** 。

**示例:**

> **输入:**arr[]=【1095，1094，1095】
> T3【输出:1005 1014 1015
> 10**9**【5】>10**0**5】
> 
> **输入:** arr[] = {5555，4444，3333，2222，1111 }
> T3】输出: 1555 2444 3033 3222 4111

**做法:**思路是改变第一个元素的一个数字，使其尽可能小。为此，从 **1000** 开始，存储最小的号码，最多需要更改 **1** 位。同样，对于下一个元素，找出最小的可能数，不要小于上一个元素，上一个元素的数字变化数最多为 **1** 。如果最后一个元素没有超过 **9999** ，那么列表是可能的。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int DIGITS = 4, MIN = 1000, MAX = 9999;

// Function to return the minimum element
// from the range [prev, MAX] such that
// it differs in at most 1 digit with cur
int getBest(int prev, int cur)
{
    // To start with the value
    // we have achieved in the last step
    int maximum = max(MIN, prev);

    for (int i = maximum; i <= MAX; i++) {
        int cnt = 0;

        // Store the value with which the
        // current will be compared
        int a = i;

        // Current value
        int b = cur;

        // There are at most 4 digits
        for (int k = 0; k < DIGITS; k++) {

            // If the current digit differs
            // in both the numbers
            if (a % 10 != b % 10)
                cnt += 1;

            // Eliminate last digits in
            // both the numbers
            a /= 10;
            b /= 10;
        }

        // If the number of different
        // digits is at most 1
        if (cnt <= 1)
            return i;
    }

    // If we can't find any number for which
    // the number of change is less than or
    // equal to 1 then return -1
    return -1;
}

// Function to get the non-decreasing list
void getList(int arr[], int n)
{
    // Creating a vector for the updated list
    vector<int> myList;

    int i, cur;

    // Let's assume that it is possible to
    // make the list non-decreasing
    bool possible = true;

    myList.push_back(0);

    for (i = 0; i < n; i++) {

        // Element of the original array
        cur = arr[i];

        myList.push_back(getBest(myList.back(), cur));

        // Can't make the list non-decreasing
        if (myList.back() == -1) {
            possible = false;
            break;
        }
    }

    // If possible then print the list
    if (possible) {
        for (i = 1; i < myList.size(); i++)
            cout << myList[i] << " ";
    }

    else
        cout << "-1";
}

// Driver code
int main()
{
    int arr[] = { 1095, 1094, 1095 };
    int n = sizeof(arr) / sizeof(arr[0]);

    getList(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
static int DIGITS = 4, MIN = 1000, MAX = 9999;

// Function to return the minimum element
// from the range [prev, MAX] such that
// it differs in at most 1 digit with cur
static int getBest(int prev, int cur)
{
    // To start with the value
    // we have achieved in the last step
    int maximum = Math.max(MIN, prev);

    for (int i = maximum; i <= MAX; i++)
    {
        int cnt = 0;

        // Store the value with which the
        // current will be compared
        int a = i;

        // Current value
        int b = cur;

        // There are at most 4 digits
        for (int k = 0; k < DIGITS; k++)
        {

            // If the current digit differs
            // in both the numbers
            if (a % 10 != b % 10)
                cnt += 1;

            // Eliminate last digits in
            // both the numbers
            a /= 10;
            b /= 10;
        }

        // If the number of different
        // digits is at most 1
        if (cnt <= 1)
            return i;
    }

    // If we can't find any number for which
    // the number of change is less than or
    // equal to 1 then return -1
    return -1;
}

// Function to get the non-decreasing list
static void getList(int arr[], int n)
{
    // Creating a vector for the updated list
    Vector<Integer> myList = new Vector<Integer>();

    int i, cur;

    // Let's assume that it is possible to
    // make the list non-decreasing
    boolean possible = true;

    myList.add(0);

    for (i = 0; i < n; i++)
    {

        // Element of the original array
        cur = arr[i];

        myList.add(getBest(myList.lastElement(), cur));

        // Can't make the list non-decreasing
        if (myList.lastElement() == -1)
        {
            possible = false;
            break;
        }
    }

    // If possible then print the list
    if (possible)
    {
        for (i = 1; i < myList.size(); i++)
            System.out.print(myList.get(i) + " ");
    }

    else
        System.out.print("-1");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1095, 1094, 1095 };
    int n = arr.length;

    getList(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach
DIGITS = 4; MIN = 1000; MAX = 9999;

# Function to return the minimum element
# from the range [prev, MAX] such that
# it differs in at most 1 digit with cur
def getBest(prev, cur) :

    # To start with the value
    # we have achieved in the last step
    maximum = max(MIN, prev);

    for i in range(maximum, MAX + 1) :
        cnt = 0;

        # Store the value with which the
        # current will be compared
        a = i;

        # Current value
        b = cur;

        # There are at most 4 digits
        for k in range(DIGITS) :

            # If the current digit differs
            # in both the numbers
            if (a % 10 != b % 10) :
                cnt += 1;

            # Eliminate last digits in
            # both the numbers
            a //= 10;
            b //= 10;

        # If the number of different
        # digits is at most 1
        if (cnt <= 1) :
            return i;

    # If we can't find any number for which
    # the number of change is less than or
    # equal to 1 then return -1
    return -1;

# Function to get the non-decreasing list
def getList(arr, n) :

    # Creating a vector for the updated list
    myList = [];

    # Let's assume that it is possible to
    # make the list non-decreasing
    possible = True;

    myList.append(0);

    for i in range(n) :

        # Element of the original array
        cur = arr[i];

        myList.append(getBest(myList[-1], cur));

        # Can't make the list non-decreasing
        if (myList[-1] == -1) :
            possible = False;
            break;

    # If possible then print the list
    if (possible) :
        for i in range(1, len(myList)) :
            print(myList[i], end = " ");
    else :
        print("-1");

# Driver code
if __name__ == "__main__" :

    arr = [ 1095, 1094, 1095 ];
    n = len(arr);

    getList(arr, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;            

class GFG
{
static int DIGITS = 4, MIN = 1000, MAX = 9999;

// Function to return the minimum element
// from the range [prev, MAX] such that
// it differs in at most 1 digit with cur
static int getBest(int prev, int cur)
{
    // To start with the value
    // we have achieved in the last step
    int maximum = Math.Max(MIN, prev);

    for (int i = maximum; i <= MAX; i++)
    {
        int cnt = 0;

        // Store the value with which the
        // current will be compared
        int a = i;

        // Current value
        int b = cur;

        // There are at most 4 digits
        for (int k = 0; k < DIGITS; k++)
        {

            // If the current digit differs
            // in both the numbers
            if (a % 10 != b % 10)
                cnt += 1;

            // Eliminate last digits in
            // both the numbers
            a /= 10;
            b /= 10;
        }

        // If the number of different
        // digits is at most 1
        if (cnt <= 1)
            return i;
    }

    // If we can't find any number for which
    // the number of change is less than or
    // equal to 1 then return -1
    return -1;
}

// Function to get the non-decreasing list
static void getList(int []arr, int n)
{
    // Creating a vector for the updated list
    List<int> myList = new List<int>();

    int i, cur;

    // Let's assume that it is possible to
    // make the list non-decreasing
    bool possible = true;

    myList.Add(0);

    for (i = 0; i < n; i++)
    {

        // Element of the original array
        cur = arr[i];

        myList.Add(getBest(myList[myList.Count - 1], cur));

        // Can't make the list non-decreasing
        if (myList[myList.Count - 1] == -1)
        {
            possible = false;
            break;
        }
    }

    // If possible then print the list
    if (possible)
    {
        for (i = 1; i < myList.Count; i++)
            Console.Write(myList[i] + " ");
    }

    else
        Console.Write("-1");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1095, 1094, 1095 };
    int n = arr.Length;

    getList(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var DIGITS = 4, MIN = 1000, MAX = 9999;

// Function to return the minimum element
// from the range [prev, MAX] such that
// it differs in at most 1 digit with cur
function getBest(prev, cur)
{

    // To start with the value
    // we have achieved in the last step
    var maximum = Math.max(MIN, prev);

    for(var i = maximum; i <= MAX; i++)
    {
        var cnt = 0;

        // Store the value with which the
        // current will be compared
        var a = i;

        // Current value
        var b = cur;

        // There are at most 4 digits
        for(var k = 0; k < DIGITS; k++)
        {

            // If the current digit differs
            // in both the numbers
            if (a % 10 != b % 10)
                cnt += 1;

            // Eliminate last digits in
            // both the numbers
            a = parseInt(a / 10);
            b = parseInt(b / 10);
        }

        // If the number of different
        // digits is at most 1
        if (cnt <= 1)
            return i;
    }

    // If we can't find any number for which
    // the number of change is less than or
    // equal to 1 then return -1
    return -1;
}

// Function to get the non-decreasing list
function getList(arr, n)
{

    // Creating a vector for the updated list
    var myList = [];

    var i, cur;

    // Let's assume that it is possible to
    // make the list non-decreasing
    var possible = true;

    myList.push(0);

    for(i = 0; i < n; i++)
    {

        // Element of the original array
        cur = arr[i];

        myList.push(getBest(
            myList[myList.length - 1], cur));

        // Can't make the list non-decreasing
        if (myList[myList.length - 1] == -1)
        {
            possible = false;
            break;
        }
    }

    // If possible then print the list
    if (possible)
    {
        for(i = 1; i < myList.length; i++)
            document.write( myList[i] + " ");
    }
    else
        document.write("-1");
}

// Driver code
var arr = [ 1095, 1094, 1095 ];
var n = arr.length;

getList(arr, n);

// This code is contributed by itsok

</script>
```

**Output:** 

```
1005 1014 1015
```