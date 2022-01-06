# 满足给定条件的[L，R]范围内的数字计数

> 原文:[https://www . geeksforgeeks . org/范围内满足给定条件的数字计数/](https://www.geeksforgeeks.org/count-of-numbers-in-the-range-l-r-which-satisfy-the-given-conditions/)

给定一个范围**【L，R】**，任务是从这个范围中找出满足以下条件的数的个数:

1.  数字中的所有数字都是不同的。
2.  所有数字都小于或等于 5。

**例:**

> **输入:** L = 4，R = 13
> **输出:** 5
> 4、5、10、12 和 13 是范围【4、13】内唯一的
> 有效数字。
> **输入:** L = 100，R = 1000
> **输出:** 100

**方法:**如果范围很小，问题似乎很简单，因为在这种情况下，范围内的所有数字都可以迭代，并检查它们是否有效。但是由于范围可能很大，可以观察到有效数字的所有数字都必须是不同的，并且与范围[0，5]不同，这表明最大数字不能超过 543210。
现在可以从之前生成的数字中生成序列中的下一个有效数字，而不是检查每个数字。这个想法类似于这里讨论的方法。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Maximum possible valid number
#define MAX 543210

// To store all the required number
// from the range [1, MAX]
vector<string> ans;

// Function that returns true if x
// satisfies the given conditions
bool isValidNum(string x)
{

    // To store the digits of x
    map<int, int> mp;

    for (int i = 0; i < x.length(); i++) {

        // If current digit appears more than once
        if (mp.find(x[i] - '0') != mp.end()) {
            return false;
        }

        // If current digit is greater than 5
        else if (x[i] - '0' > 5) {
            return false;
        }

        // Put the digit in the map
        else {
            mp[x[i] - '0'] = 1;
        }
    }
    return true;
}

// Function to generate all the required
// numbers in the range [1, MAX]
void generate()
{

    // Insert first 5 valid numbers
    queue<string> q;
    q.push("1");
    q.push("2");
    q.push("3");
    q.push("4");
    q.push("5");

    bool flag = true;

    // Inserting 0 externally because 0 cannot
    // be the leading digit in any number
    ans.push_back("0");

    while (!q.empty()) {
        string x = q.front();
        q.pop();

        // If x satisfies the given conditions
        if (isValidNum(x)) {
            ans.push_back(x);
        }

        // Cannot append anymore digit as
        // adding a digit will repeat one of
        // the already present digits
        if (x.length() == 6)
            continue;

        // Append all the valid digits one by
        // one and push the new generated
        // number to the queue
        for (int i = 0; i <= 5; i++) {
            string z = to_string(i);

            // Append the digit
            string temp = x + z;

            // Push the newly generated
            // number to the queue
            q.push(temp);
        }
    }
}

// Function to copmpare two strings
// which represent a numerical value
bool comp(string a, string b)
{
    if (a.size() == b.size())
        return a < b;
    else
        return a.size() < b.size();
}

// Function to return the count of
// valid numbers in the range [l, r]
int findcount(string l, string r)
{

    // Generate all the valid numbers
    // in the range [1, MAX]
    generate();

    // To store the count of numbers
    // in the range [l, r]
    int count = 0;

    // For every valid number in
    // the range [1, MAX]
    for (int i = 0; i < ans.size(); i++) {

        string a = ans[i];

        // If current number is within
        // the required range
        if (comp(l, a) && comp(a, r)) {
            count++;
        }

        // If number is equal to either l or r
        else if (a == l || a == r) {
            count++;
        }
    }

    return count;
}

// Driver code
int main()
{

    string l = "1", r = "1000";

    cout << findcount(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Maximum possible valid number
static int MAX = 543210;

// To store all the required number
// from the range [1, MAX]
static Vector<String> ans = new Vector<String>();

// Function that returns true if x
// satisfies the given conditions
static boolean isValidNum(String x)
{

    // To store the digits of x
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();

    for (int i = 0; i < x.length(); i++)
    {

        // If current digit appears more than once
        if (mp.containsKey(x.charAt(i) - '0'))
        {
            return false;
        }

        // If current digit is greater than 5
        else if (x.charAt(i) - '0' > 5)
        {
            return false;
        }

        // Put the digit in the map
        else
        {
            mp.put(x.charAt(i) - '0', 1);
        }
    }
    return true;
}

// Function to generate all the required
// numbers in the range [1, MAX]
static void generate()
{

    // Insert first 5 valid numbers
    Queue<String> q = new LinkedList<String>();
    q.add("1");
    q.add("2");
    q.add("3");
    q.add("4");
    q.add("5");

    boolean flag = true;

    // Inserting 0 externally because 0 cannot
    // be the leading digit in any number
    ans.add("0");

    while (!q.isEmpty())
    {
        String x = q.peek();
        q.remove();

        // If x satisfies the given conditions
        if (isValidNum(x))
        {
            ans.add(x);
        }

        // Cannot append anymore digit as
        // adding a digit will repeat one of
        // the already present digits
        if (x.length() == 6)
            continue;

        // Append all the valid digits one by
        // one and push the new generated
        // number to the queue
        for (int i = 0; i <= 5; i++)
        {
            String z = String.valueOf(i);

            // Append the digit
            String temp = x + z;

            // Push the newly generated
            // number to the queue
            q.add(temp);
        }
    }
}

// Function to copmpare two Strings
// which represent a numerical value
static boolean comp(String a, String b)
{
    if (a.length()== b.length())
    {
        int i = a.compareTo(b);

        return i < 0 ? true : false;
    }
    else
        return a.length() < b.length();
}

// Function to return the count of
// valid numbers in the range [l, r]
static int findcount(String l, String r)
{

    // Generate all the valid numbers
    // in the range [1, MAX]
    generate();

    // To store the count of numbers
    // in the range [l, r]
    int count = 0;

    // For every valid number in
    // the range [1, MAX]
    for (int i = 0; i < ans.size(); i++)
    {

        String a = ans.get(i);

        // If current number is within
        // the required range
        if (comp(l, a) && comp(a, r))
        {
            count++;
        }

        // If number is equal to either l or r
        else if (a == l || a == r)
        {
            count++;
        }
    }
    return count;
}

// Driver code
public static void main (String[] args)
{
    String l = "1", r = "1000";

    System.out.println(findcount(l, r));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import deque

# Maximum possible valid number
MAX = 543210

# To store all the required number
# from the range [1, MAX]
ans = []

# Function that returns true if x
# satisfies the given conditions
def isValidNum(x):

    # To store the digits of x
    mp = dict()

    for i in range(len(x)):

        # If current digit appears more than once
        if (ord(x[i]) - ord('0') in mp.keys()):
            return False

        # If current digit is greater than 5
        elif (ord(x[i]) - ord('0') > 5):
            return False

        # Put the digit in the map
        else:
            mp[ord(x[i]) - ord('0')] = 1

    return True

# Function to generate all the required
# numbers in the range [1, MAX]
def generate():

    # Insert first 5 valid numbers
    q = deque()
    q.append("1")
    q.append("2")
    q.append("3")
    q.append("4")
    q.append("5")

    flag = True

    # Inserting 0 externally because 0 cannot
    # be the leading digit in any number
    ans.append("0")

    while (len(q) > 0):
        x = q.popleft()

        # If x satisfies the given conditions
        if (isValidNum(x)):
            ans.append(x)

        # Cannot append anymore digit as
        # adding a digit will repeat one of
        # the already present digits
        if (len(x) == 6):
            continue

        # Append all the valid digits one by
        # one and append the new generated
        # number to the queue
        for i in range(6):
            z = str(i)

            # Append the digit
            temp = x + z

            # Push the newly generated
            # number to the queue
            q.append(temp)

# Function to copmpare two strings
# which represent a numerical value
def comp(a, b):
    if (len(a) == len(b)):
        if a < b:
            return True
    else:
        return len(a) < len(b)

# Function to return the count of
# valid numbers in the range [l, r]
def findcount(l, r):

    # Generate all the valid numbers
    # in the range [1, MAX]
    generate()

    # To store the count of numbers
    # in the range [l, r]
    count = 0

    # For every valid number in
    # the range [1, MAX]
    for i in range(len(ans)):

        a = ans[i]

        # If current number is within
        # the required range
        if (comp(l, a) and comp(a, r)):
            count += 1

        # If number is equal to either l or r
        elif (a == l or a == r):
            count += 1

    return count

# Driver code
l = "1"
r = "1000"

print(findcount(l, r))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;    

class GFG
{

// Maximum possible valid number
static int MAX = 543210;

// To store all the required number
// from the range [1, MAX]
static List<String> ans = new List<String>();

// Function that returns true if x
// satisfies the given conditions
static bool isValidNum(String x)
{

    // To store the digits of x
    Dictionary<int, int> mp = new Dictionary<int, int>();

    for (int i = 0; i < x.Length; i++)
    {

        // If current digit appears more than once
        if (mp.ContainsKey(x[i] - '0'))
        {
            return false;
        }

        // If current digit is greater than 5
        else if (x[i] - '0' > 5)
        {
            return false;
        }

        // Put the digit in the map
        else
        {
            mp.Add(x[i] - '0', 1);
        }
    }
    return true;
}

// Function to generate all the required
// numbers in the range [1, MAX]
static void generate()
{

    // Insert first 5 valid numbers
    Queue<String> q = new Queue<String>();
    q.Enqueue("1");
    q.Enqueue("2");
    q.Enqueue("3");
    q.Enqueue("4");
    q.Enqueue("5");

    bool flag = true;

    // Inserting 0 externally because 0 cannot
    // be the leading digit in any number
    ans.Add("0");

    while (q.Count!=0)
    {
        String x = q.Peek();
        q.Dequeue();

        // If x satisfies the given conditions
        if (isValidNum(x))
        {
            ans.Add(x);
        }

        // Cannot append anymore digit as
        // adding a digit will repeat one of
        // the already present digits
        if (x.Length == 6)
            continue;

        // Append all the valid digits one by
        // one and push the new generated
        // number to the queue
        for (int i = 0; i <= 5; i++)
        {
            String z = i.ToString();

            // Append the digit
            String temp = x + z;

            // Push the newly generated
            // number to the queue
            q.Enqueue(temp);
        }
    }
}

// Function to copmpare two Strings
// which represent a numerical value
static bool comp(String a, String b)
{
    if (a.Length == b.Length)
    {
        int i = a.CompareTo(b);

        return i < 0 ? true : false;
    }
    else
        return a.Length < b.Length;
}

// Function to return the count of
// valid numbers in the range [l, r]
static int findcount(String l, String r)
{

    // Generate all the valid numbers
    // in the range [1, MAX]
    generate();

    // To store the count of numbers
    // in the range [l, r]
    int count = 0;

    // For every valid number in
    // the range [1, MAX]
    for (int i = 0; i < ans.Count; i++)
    {

        String a = ans[i];

        // If current number is within
        // the required range
        if (comp(l, a) && comp(a, r))
        {
            count++;
        }

        // If number is equal to either l or r
        else if (a == l || a == r)
        {
            count++;
        }
    }
    return count;
}

// Driver code
public static void Main (String[] args)
{
    String l = "1", r = "1000";

    Console.WriteLine(findcount(l, r));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Maximum possible valid number
let MAX = 543210;

// To store all the required number
// from the range [1, MAX]
let ans = [];

// Function that returns true if x
// satisfies the given conditions
function isValidNum(x)
{
    // To store the digits of x
    let mp = new Map();

    for (let i = 0; i < x.length; i++)
    {

        // If current digit appears more than once
        if (mp.has(x[i].charCodeAt(0) - '0'.charCodeAt(0)))
        {
            return false;
        }

        // If current digit is greater than 5
        else if (x[i].charCodeAt(0) - '0'.charCodeAt(0) > 5)
        {
            return false;
        }

        // Put the digit in the map
        else
        {
            mp.set(x[i].charCodeAt(0) - '0'.charCodeAt(0), 1);
        }
    }
    return true;
}

// Function to generate all the required
// numbers in the range [1, MAX]
function generate()
{
    // Insert first 5 valid numbers
    let q = [];
    q.push("1");
    q.push("2");
    q.push("3");
    q.push("4");
    q.push("5");

    let flag = true;

    // Inserting 0 externally because 0 cannot
    // be the leading digit in any number
    ans.push("0");

    while (q.length!=0)
    {
        let x = q.shift();

        // If x satisfies the given conditions
        if (isValidNum(x))
        {
            ans.push(x);
        }

        // Cannot append anymore digit as
        // adding a digit will repeat one of
        // the already present digits
        if (x.length == 6)
            continue;

        // Append all the valid digits one by
        // one and push the new generated
        // number to the queue
        for (let i = 0; i <= 5; i++)
        {
            let z = (i).toString();

            // Append the digit
            let temp = x + z;

            // Push the newly generated
            // number to the queue
            q.push(temp);
        }
    }
}

// Function to copmpare two Strings
// which represent a numerical value
function comp(a,b)
{
    if (a.length== b.length)
    {

        return a < b ? true : false;
    }
    else
        return a.length < b.length;
}

// Function to return the count of
// valid numbers in the range [l, r]
function findcount(l,r)
{
    // Generate all the valid numbers
    // in the range [1, MAX]
    generate();

    // To store the count of numbers
    // in the range [l, r]
    let count = 0;

    // For every valid number in
    // the range [1, MAX]
    for (let i = 0; i < ans.length; i++)
    {

        let a = ans[i];

        // If current number is within
        // the required range
        if (comp(l, a) && comp(a, r))
        {
            count++;
        }

        // If number is equal to either l or r
        else if (a == l || a == r)
        {
            count++;
        }
    }
    return count;
}

// Driver code
let l = "1", r = "1000";

document.write(findcount(l, r));

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
130
```