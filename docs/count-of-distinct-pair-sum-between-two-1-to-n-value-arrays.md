# 两个 1 到 N 值数组之间不同对和的计数

> 原文:[https://www . geesforgeks . org/distinct-pair-sum-two-1 到-n-value-arrays/](https://www.geeksforgeeks.org/count-of-distinct-pair-sum-between-two-1-to-n-value-arrays/)

给定一个正整数 **N** ，使得存在两个数组 **a[]** 和 **b[]** ，每个数组包含值{1，2，3，..，N}，任务是找到所有对(a[i]，b[j])的计数，使得 a[i] + b[j]在所有对中是唯一的，即如果两对具有相等的和，那么结果中将只计数一对。
**举例:**

> **输入:** N = 2
> **输出:** 3
> **解释:**
> a[] = {1，2}，b[] = {1，2}
> 三种可能的对是(a[0]，b[0])，(a[1]，b[0])和(a[1]，b[1])。
> 对 1: 1 + 1 = 2
> 对 2: 2 + 1 = 3
> 对 3: 2 + 2 = 4
> **输入:** N = 3
> **输出:** 5
> a[] = {1，2，3}，b[] = {1，2，3}
> 具有不同和的可能对是:
> 对 1: 1 + 1 = 2
> 对 2: 2 + 1 = 3

**天真方法:**
为了解决上面提到的问题，天真方法是使用到一个[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)来存储{1，2，3，..N}和{1，2，3，..N}通过使用两个循环。
以下是上述方法的实施:

## C++

```
// C++ implementation to count
// of distinct pair sum between
// two Array with values 1 to N

#include <bits/stdc++.h>
using namespace std;

// Function to find the distinct sums
int findDistinctSums(int n)
{
    // Set to store distinct sums
    set<int> s;

    for (int i = 1; i <= n; i++) {
        for (int j = i; j <= n; j++) {

            // Inserting every sum
            s.insert(i + j);
        }
    }

    // returning distinct sums
    return s.size();
}

// Driver code
int main()
{

    int N = 3;

    cout << findDistinctSums(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count
// of distinct pair sum between
// two Array with values 1 to N
import java.util.*;

class GFG{

// Function to find the distinct sums
static int findDistinctSums(int n)
{

    // Set to store distinct sums
    HashSet<Integer> s = new HashSet<>();

    for(int i = 1; i <= n; i++)
    {
        for(int j = i; j <= n; j++)
        {

            // Inserting every sum
            s.add(i + j);
        }
    }

    // Returning distinct sums
    return s.size();
}

// Driver code
public static void main(String[] args)
{
    int N = 3;

    System.out.print(findDistinctSums(N));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation to count
# of distinct pair sum between
# two Array with values 1 to N

# Function to find the distinct sums
def findDistinctSums(n):

    # Set to store distinct sums
    s = set()

    for i in range(1, n + 1):
        for j in range(i, n + 1):

            # Inserting every sum
            s.add(i + j)

    # Returning distinct sums
    return len(s)

# Driver code
N = 3
print(findDistinctSums(N))

# This code is contributed by divyamohan123
```

## C#

```
// C# implementation to count
// of distinct pair sum between
// two Array with values 1 to N
using System;
using System.Collections.Generic;

class GFG{

// Function to find the distinct sums
static int findDistinctSums(int n)
{

    // Set to store distinct sums
    HashSet<int> s = new HashSet<int>();

    for(int i = 1; i <= n; i++)
    {
        for(int j = i; j <= n; j++)
        {

            // Inserting every sum
            s.Add(i + j);
        }
    }

    // Returning distinct sums
    return s.Count;
}

// Driver code
public static void Main(String[] args)
{
    int N = 3;

    Console.Write(findDistinctSums(N));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript implementation to count
// of distinct pair sum between
// two Array with values 1 to N

// Function to find the distinct sums
function findDistinctSums(n)
{
    // Set to store distinct sums
    s = new Set();

    for (var i = 1; i <= n; i++) {
        for (var j = i; j <= n; j++) {

            // Inserting every sum
            s.add(i + j);
        }
    }

    // returning distinct sums
    return s.size;
}

// Driver code
var N = 3;
document.write( findDistinctSums(N));

</script>
```

**Output:** 

```
5
```