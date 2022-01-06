# 为使数组良好应移除的元素的最小数量

> 原文:[https://www . geeksforgeeks . org/最小应移除元素数使阵列良好/](https://www.geeksforgeeks.org/minimum-number-of-elements-that-should-be-removed-to-make-the-array-good/)

给定一个数组 **arr[]** ，任务是找到必须移除的元素的最小数量，以使数组良好。a 序列 a <sub>1</sub> ，a <sub>2</sub> … a <sub>n</sub> 被称为好如果对于每个元素 **a <sub>i</sub>** ，存在一个元素 **a <sub>j</sub>** (i 不等于 j)，使得**a<sub>I</sub>+a<sub>j</sub>T21 是两个** i 的**幂**

> **输入:** arr[] = {4，7，1，5，4，9}
> **输出:** 1
> 从阵中移除 5 使阵好。
> **输入:** arr[] = {1，3，1，1}
> **输出:** 0

**方法:**我们应该只删除没有**a<sub>j</sub>T9】(I 不等于 j)这样的**a<sub>I</sub>T5，这样**a<sub>I</sub>+a<sub>j</sub>T15】就是 2 的幂。
对于每个值，让我们找出它在数组中出现的次数。我们可以使用[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)数据结构。
现在我们可以很容易的查到 **a <sub>i</sub>** 没有一对 **a <sub>j</sub>** 。让我们迭代所有可能的和， **S = 2 <sup>0</sup> ，2 <sup>1</sup> ，…，2<sup>30</sup>T35】并为每个 **S** 计算**S–a【I】**是否存在于地图中。
以下是上述方法的实施:******** 

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number
// of elements that must be removed
// to make the given array good
int minimumRemoval(int n, int a[])
{

    map<int, int> c;

    // Count frequency of each element
    for (int i = 0; i < n; i++)
        c[a[i]]++;

    int ans = 0;

    // For each element check if there
    // exists another element that makes
    // a valid pair
    for (int i = 0; i < n; i++) {
        bool ok = false;
        for (int j = 0; j < 31; j++) {
            int x = (1 << j) - a[i];
            if (c.count(x) && (c[x] > 1
                       || (c[x] == 1 && x != a[i]))) {
                ok = true;
                break;
            }
        }

        // If does not exist then
        // increment answer
        if (!ok)
            ans++;
    }

    return ans;
}

// Driver code
int main()
{
    int a[] = { 4, 7, 1, 5, 4, 9 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << minimumRemoval(n, a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the minimum number
// of elements that must be removed
// to make the given array good
static int minimumRemoval(int n, int a[])
{

    Map<Integer,Integer> c = new HashMap<>();

    // Count frequency of each element
    for (int i = 0; i < n; i++)
        if(c.containsKey(a[i]))
        {
            c.put(a[i], c.get(a[i])+1);
        }
        else
        {
            c.put(a[i], 1);
        }

    int ans = 0;

    // For each element check if there
    // exists another element that makes
    // a valid pair
    for (int i = 0; i < n; i++)
    {
        boolean ok = false;
        for (int j = 0; j < 31; j++)
        {
            int x = (1 << j) - a[i];
            if ((c.get(x) != null && (c.get(x) > 1)) ||
                c.get(x) != null && (c.get(x) == 1 && x != a[i]))
            {
                ok = true;
                break;
            }
        }

        // If does not exist then
        // increment answer
        if (!ok)
            ans++;
    }

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 4, 7, 1, 5, 4, 9 };
    int n = a.length;
    System.out.println(minimumRemoval(n, a));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum number
# of elements that must be removed
# to make the given array good
def minimumRemoval(n, a) :

    c = dict.fromkeys(a, 0);

    # Count frequency of each element
    for i in range(n) :
        c[a[i]] += 1;

    ans = 0;

    # For each element check if there
    # exists another element that makes
    # a valid pair
    for i in range(n) :
        ok = False;
        for j in range(31) :

            x = (1 << j) - a[i];
            if (x in c and (c[x] > 1 or
               (c[x] == 1 and x != a[i]))) :

                ok = True;
                break;

        # If does not exist then
        # increment answer
        if (not ok) :
            ans += 1;

    return ans;

# Driver Code
if __name__ == "__main__" :

    a = [ 4, 7, 1, 5, 4, 9 ];
    n = len(a) ;

    print(minimumRemoval(n, a));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System.Linq;
using System;

class GFG
{
// Function to return the minimum number
// of elements that must be removed
// to make the given array good
static int minimumRemoval(int n, int []a)
{

    int[] c = new int[1000];

    // Count frequency of each element
    for (int i = 0; i < n; i++)
        c[a[i]]++;

    int ans = 0;

    // For each element check if there
    // exists another element that makes
    // a valid pair
    for (int i = 0; i < n; i++)
    {
        bool ok = true;
        for (int j = 0; j < 31; j++)
        {
            int x = (1 << j) - a[i];
            if (c.Contains(x) && (c[x] > 1 ||
                    (c[x] == 1 && x != a[i])))
            {
                ok = false;
                break;
            }
        }

        // If does not exist then
        // increment answer
        if (!ok)
            ans++;
    }

    return ans;
}

// Driver code
static void Main()
{
    int []a = { 4, 7, 1, 5, 4, 9 };
    int n = a.Length;
    Console.WriteLine(minimumRemoval(n, a));
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the minimum number
// of elements that must be removed
// to make the given array good
function minimumRemoval( n, a)
{

    var c = {};

    // Count frequency of each element
    for (let i = 0; i < n; i++){
        if(a[i] in c)
          c[a[i]]++;
        else
          c[a[i]] = 1;
    }

    var ans = 0;

    // For each element check if there
    // exists another element that makes
    // a valid pair
    for (let i = 0; i < n; i++) {
        var ok = false;
        for (let j = 0; j < 31; j++) {
            let x = (1 << j) - a[i];

            if ((x in c && c[x] > 1)
                       || (c[x] == 1 && x != a[i])) {

                ok = true;
                break;
            }
        }

        // If does not exist then
        // increment answer
        if (!ok)
            ans++;
    }

    return ans;
}

// Driver code
var a = new Array( 4, 7, 1, 5, 4, 9 );
var n = a.length;
console.log(minimumRemoval(n, a));

// This ode is contributed by ukasp.   
</script>
```

**Output:** 

```
1
```