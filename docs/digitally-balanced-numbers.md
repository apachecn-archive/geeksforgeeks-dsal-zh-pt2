# 数字平衡数字

> 原文:[https://www.geeksforgeeks.org/digitally-balanced-numbers/](https://www.geeksforgeeks.org/digitally-balanced-numbers/)

给定两个整数 **N** 和 **B** ，任务是检查 **N** 是否为基数 B 中的数字平衡数

> 基数为 B 的数字平衡数是那些具有相同数量(0，1，2 …)的数。B-1)基数 b 中的数字。

**示例:**

> **输入:** N = 9，B = 2
> **输出:**是
> 9 的等价二进制数是 1001，
> 0 的个数等于 1 = 2
> 
> **输入:** N = 5，N = 2
> T3】输出:否
> 5 的等价二进制数为 101。

**方法:**想法是遍历基数 B 中数字的位数，并将位数的频率存储在[哈希图](https://www.geeksforgeeks.org/hashing-data-structure/)中。最后，迭代散列图并检查散列图中每个数字的频率是否相同，那么这个数字被称为基数 b 中的数字平衡数

下面是上述方法的实现:

## C++

```
// C++ implementation to check if a
// number is a digitally balanced number

#include <bits/stdc++.h>
using namespace std;

// Function to check if the digits in the
// number is the same number of digits
int checkSame(int n, int b)
{
    map<int, int> m;

    // Loop to iterate over the
    // digits of the number N
    while (n != 0) {
        int r = n % b;
        n = n / b;
        m[r]++;
    }
    int last = -1;

    // Loop to iterate over the map
    for (auto i = m.begin(); i != m.end(); i++) {
        if (last != -1 && i->second != last) {
            return false;
        }
        else {
            last = i->second;
        }
    }
}

// Driver Code
int main()
{
    int n = 9;
    int base = 2;

    // function to check
    if (checkSame(n, base))
        cout << "Yes";
    else
        cout << "NO";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if a
// number is a digitally balanced number
import java.util.*;
class GFG{

// Function to check if the digits in the
// number is the same number of digits
static boolean checkSame(int n, int b)
{
    HashMap<Integer,
            Integer> m = new HashMap<Integer,
                                     Integer>();

    // Loop to iterate over the
    // digits of the number N
    while (n != 0)
    {
        int r = n % b;
        n = n / b;
        if(m.containsKey(r))
        {
            m.put(r, m.get(r) + 1);
        }
        else
        {
            m.put(r, 1);
        }
    }
    int last = -1;

    // Loop to iterate over the map
    for (Map.Entry<Integer,
                   Integer> i : m.entrySet())
    {
        if (last != -1 && i.getValue() != last)
        {
            return false;
        }
        else
        {
            last = i.getValue();
        }
    }
    return true;
}

// Driver Code
public static void main(String[] args)
{
    int n = 9;
    int base = 2;

    // function to check
    if (checkSame(n, base))
        System.out.print("Yes");
    else
        System.out.print("NO");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to check if a
# number is a digitally balanced number

# Function to check if the digits in the
# number is the same number of digits
def checkSame(n, b):

    m = {}

    # Loop to iterate over the
    # digits of the number N
    while (n != 0):
        r = n % b
        n = n // b

        if r in m:
            m[r] += 1
        else:
            m[r] = 1

    last = -1

    # Loop to iterate over the map
    for i in m:
        if last != -1 and m[i] != last:
            return False
        else:
            last = m[i]

    return True

# Driver code
n = 9
base = 2

# Function to check
if (checkSame(n, base)):
    print("Yes")
else:
    print("NO")

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation to check if a
// number is a digitally balanced number
using System;
using System.Collections.Generic;

class GFG{

// Function to check if the digits in the
// number is the same number of digits
static bool checkSame(int n, int b)
{
    Dictionary<int,
               int> m = new Dictionary<int,
                                       int>();

    // Loop to iterate over the
    // digits of the number N
    while (n != 0)
    {
        int r = n % b;
        n = n / b;
        if(m.ContainsKey(r))
        {
            m[r] = m[r] + 1;
        }
        else
        {
            m.Add(r, 1);
        }
    }
    int last = -1;

    // Loop to iterate over the map
    foreach(KeyValuePair<int, int> i in m)
    {
        if (last != -1 && i.Value != last)
        {
            return false;
        }
        else
        {
            last = i.Value;
        }
    }
    return true;
}

// Driver Code
public static void Main(String[] args)
{
    int n = 9;
    int Base = 2;

    // Function to check
    if (checkSame(n, Base))
        Console.Write("Yes");
    else
        Console.Write("NO");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation
// Function to check if the digits in the
// number is the same number of digits
function checkSame( n,  b)
{
    var m = {};

    // Loop to iterate over the
    // digits of the number N
    while (n != 0) {
        var r = n % b;
        n = n / b;
        if (r in m)
            m[r] += 1
        else
            m[r] = 1
    }
    var last = -1;

    // Loop to iterate over the map
    for (var i in m) {
        if (last != -1 && m[i] != last) {
            return false;
        }
        else {
            last = m[i];
        }
    }
    return true;
}

// Driver Code
var n = 9;
var base = 2;

// function to check
if (checkSame(n, base))
document.write("Yes");
else
document.write("NO");

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:** O(N * log N)*

***辅助空间:** O(N)*

**参考:**T2https://oeis.org/A031443