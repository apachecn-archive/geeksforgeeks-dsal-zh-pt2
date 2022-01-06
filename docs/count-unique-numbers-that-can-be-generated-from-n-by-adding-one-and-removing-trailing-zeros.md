# 通过加 1 和去掉尾随零来计算可以从 N 生成的唯一数字

> 原文:[https://www . geesforgeks . org/count-unique-numbers-可以通过添加一个并移除尾随零从 n 生成的数字/](https://www.geeksforgeeks.org/count-unique-numbers-that-can-be-generated-from-n-by-adding-one-and-removing-trailing-zeros/)

给定一个数字 **N** 。在第一步中给数字加 1，如果数字有尾随零，则在第二步中删除所有尾随零。继续下一个生成号码的过程。任务是计算这些操作可以生成的唯一数字的数量。
**例:**

> **输入:** N = 5
> **输出:**9
> 5->6->7->8->9->1->2->3->4->5(相同序列重复)
> 注意，10 不包括在内，因为它包含尾随零
> 并且移除零给出 1 作为下一个元素。
> **输入:** N = 28
> **输出:** 11

**方法:**这个问题可以用递归来解决。使用[无序集](https://www.geeksforgeeks.org/unordered_set-in-cpp-stl/)存储所有唯一的数字。如果一个数字被达到两次，我们结束递归，因为相同的序列将被重复，我们将不会得到更多的唯一数字。否则，将数字插入集合中，在第一步中，将数字增加 1，并在下一步中删除所有尾随的零(如果有)。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the unique numbers
void count_unique(unordered_set<int>& s, int n)
{

    // If the number has
    // already been visited
    if (s.count(n))
        return;

    // Insert the number to the set
    s.insert(n);

    // First step
    n += 1;

    // Second step
    // remove trailing zeros
    while (n % 10 == 0) {
        n = n / 10;
    }

    // Recur again for the new number
    count_unique(s, n);
}

// Driver code
int main()
{
    int n = 10;
    unordered_set<int> s;
    count_unique(s, n);

    cout << s.size();

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to count the unique numbers
static void count_unique(HashSet<Integer>s, int n)
{

    // If the number has
    // already been visited
    if (s.contains(n))
        return;

    // Insert the number to the set
    s.add(n);

    // First step
    n += 1;

    // Second step
    // remove trailing zeros
    while (n % 10 == 0)
    {
        n = n / 10;
    }

    // Recur again for the new number
    count_unique(s, n);
}

// Driver code
public static void main(String[] args)
{
    int n = 10;
    HashSet<Integer>s = new HashSet<>();
    count_unique(s, n);
    System.out.println(s.size());
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to count the unique numbers
def count_unique(s, n) :

    # If the number has
    # already been visited
    if (s.count(n)) :
        return;

    # Insert the number to the set
    s.append(n);

    # First step
    n += 1;

    # Second step
    # remove trailing zeros
    while (n % 10 == 0) :
        n = n // 10;

    # Recur again for the new number
    count_unique(s, n);

# Driver code
if __name__ == "__main__" :

    n = 10
    s = []

    count_unique(s, n)

    print(len(s))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to count the unique numbers
static void count_unique(HashSet<int>s, int n)
{

    // If the number has
    // already been visited
    if (s.Contains(n))
        return;

    // Insert the number to the set
    s.Add(n);

    // First step
    n += 1;

    // Second step
    // remove trailing zeros
    while (n % 10 == 0)
    {
        n = n / 10;
    }

    // Recur again for the new number
    count_unique(s, n);
}

// Driver code
public static void Main(String[] args)
{
    int n = 10;
    HashSet<int>s = new HashSet<int>();
    count_unique(s, n);
    Console.WriteLine(s.Count);
}
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to count the unique numbers
function count_unique(s,n)
{
    // If the number has
    // already been visited
    if (s.has(n))
        return;

    // Insert the number to the set
    s.add(n);

    // First step
    n += 1;

    // Second step
    // remove trailing zeros
    while (n % 10 == 0)
    {
        n = Math.floor(n / 10);
    }

    // Recur again for the new number
    count_unique(s, n);
}

// Driver code
let n = 10;
let s = new Set();
count_unique(s, n);
document.write(s.size);

// This code is contributed by rag2127

</script>
```

**Output:** 

```
19
```