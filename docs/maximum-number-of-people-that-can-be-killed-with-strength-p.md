# 力量 P

可以击杀的最大人数

> 原文:[https://www . geesforgeks . org/最大强度杀伤人数-p/](https://www.geeksforgeeks.org/maximum-number-of-people-that-can-be-killed-with-strength-p/)

有无限个人站成一排，从 1 开始索引。一个拥有指数 **i** 的人，拥有**I<sup>2</sup>T5 的实力。你有实力 **P** ，任务是告诉你用实力 **P** 最多能杀多少人。
只有 **P ≥ X** 你才能用力量 **X** 击杀一个人，击杀后你的力量减少 **X** 。**

**示例:**

> **输入:** P = 14
> **输出:** 3
> 第一人会有实力 1 <sup>2</sup> = 1 也就是< P
> P 在第一次击杀后减为 13。
> 第二次击杀，P = 13–2<sup>2</sup>= 9
> 第三次击杀，P = 9–3<sup>2</sup>= 0
> 
> **输入:**P = 58
> T3】输出: 5

**天真的做法:**从 1 开始检查每一个单杀，直到强度 **P** 大于等于被杀者的强度。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// number of people that can be killed
int maxPeople(int p)
{
    int tmp = 0, count = 0;

    // Loop will break when the ith person
    // cannot be killed
    for (int i = 1; i * i <= p; i++) {
        tmp = tmp + (i * i);
        if (tmp <= p)
            count++;
        else
            break;
    }
    return count;
}

// Driver code
int main()
{
    int p = 14;
    cout << maxPeople(p);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{   
// Function to return the maximum
// number of people that can be killed
static int maxPeople(int p)
{
    int tmp = 0, count = 0;

    // Loop will break when the ith person
    // cannot be killed
    for (int i = 1; i * i <= p; i++)
    {
        tmp = tmp + (i * i);
        if (tmp <= p)
            count++;
        else
            break;
    }
    return count;
}

// Driver code
public static void main(String args[])
{
    int p = 14;
    System.out.println(maxPeople(p));

}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach

from math import sqrt

# Function to return the maximum
# number of people that can be killed
def maxPeople(p) :

    tmp = 0; count = 0;

    # Loop will break when the ith person
    # cannot be killed
    for i in range(1, int(sqrt(p)) + 1) :
        tmp = tmp + (i * i);
        if (tmp <= p) :
            count += 1;
        else :
            break;

    return count;

# Driver code
if __name__ == "__main__" :

    p = 14;
    print(maxPeople(p));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum
// number of people that can be killed
static int maxPeople(int p)
{
    int tmp = 0, count = 0;

    // Loop will break when the ith person
    // cannot be killed
    for (int i = 1; i * i <= p; i++)
    {
        tmp = tmp + (i * i);
        if (tmp <= p)
            count++;
        else
            break;
    }
    return count;
}

// Driver code
public static void Main()
{
    int p = 14;
    Console.WriteLine(maxPeople(p));
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function to return the maximum
// number of people that can be killed
function maxPeople(p)
{
    var tmp = 0, count = 0;

    // Loop will break when the ith person
    // cannot be killed
    for (var i = 1; i * i <= p; i++)
    {
        tmp = tmp + (i * i);
        if (tmp <= p)
            count++;
        else
            break;
    }
    return count;
}

// Driver code

var p = 14;
document.write(maxPeople(p));

// This code is contributed by Amit Katiyar

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)

**高效的方法:**我们可以看到如果我们杀了**I<sup>th</sup>T5】人那么我们已经杀了**(I–1)<sup>th</sup>T9】人。这意味着它是单调函数 **f** ，其定义域是整数集。现在我们可以在这个单调函数上应用二分搜索法，其中我们现在寻找的不是数组查找，而是一些 **x** ，使得 **f(x)** 等于目标值。时间复杂度降低到 0(对数(n))。****

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <algorithm>
#include <bits/stdc++.h>
using namespace std;
#define ll long long

static constexpr int kN = 1000000;

// Function to return the maximum
// number of people that can be killed
int maxPeople(int p)
{
    // Storing the sum beforehand so that
    // it can be used in each query
    ll sums[kN];
    sums[0] = 0;
    for (int i = 1; i < kN; i++)
        sums[i] = (ll)(i * i) + sums[i - 1];

    // lower_bound returns an iterator pointing to the
    // first element greater than or equal to your val
    auto it = std::lower_bound(sums, sums + kN, p);
    if (*it > p) {

        // Previous value
        --it;
    }

    // Returns the index in array upto which
    // killing is possible with strength P
    return (it - sums);
}

// Driver code
int main()
{
    int p = 14;
    cout << maxPeople(p);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

static int kN = 1000000;

// Function to return the maximum
// number of people that can be killed
static int maxPeople(int p)
{
    // Storing the sum beforehand so that
    // it can be used in each query
    long []sums = new long[kN];
    sums[0] = 0;
    for (int i = 1; i < kN; i++)
        sums[i] = (long)(i * i) + sums[i - 1];

    // lower_bound returns an iterator pointing to the
    // first element greater than or equal to your val
    int it = lower_bound(sums, 0, kN, p);
    if (sums[it] > p)
    {

        // Previous value
        --it;
    }

    // Returns the index in array upto which
    // killing is possible with strength P
    return it;
}
private static int lower_bound(long[] a, int low,
                            int high, int element)
{
    while(low < high)
    {
        int middle = low + (high - low)/2;
        if(element > a[middle])
            low = middle + 1;
        else
            high = middle;
    }
    return low;
}

// Driver code
public static void main(String[] args)
{
    int p = 14;
    System.out.println(maxPeople(p));
}
}

/* This code is contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach
kN = 1000000;

# Function to return the maximum
# number of people that can be killed
def maxPeople(p):

    # Storing the sum beforehand so that
    # it can be used in each query
    sums = [0] * kN;
    sums[0] = 0;
    for i in range(1, kN):
        sums[i] = (i * i) + sums[i - 1];

    # lower_bound returns an iterator
    # pointing to the first element
    # greater than or equal to your val
    it = lower_bound(sums, 0, kN, p);
    if (it > p):

        # Previous value
        it -= 1;

    # Returns the index in array upto which
    # killing is possible with strength P
    return it;

def lower_bound(a, low, high, element):
    while(low < high):
        middle = int(low + (high - low) / 2);
        if(element > a[middle]):
            low = middle + 1;
        else:
            high = middle;
    return low;

# Driver code
if __name__ == '__main__':
    p = 14;
    print(maxPeople(p));

# This code contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;    

public class GFG
{

static int kN = 1000000;

// Function to return the maximum
// number of people that can be killed
static int maxPeople(int p)
{
    // Storing the sum beforehand so that
    // it can be used in each query
    long []sums = new long[kN];
    sums[0] = 0;
    for (int i = 1; i < kN; i++)
        sums[i] = (long)(i * i) + sums[i - 1];

    // lower_bound returns an iterator pointing to the
    // first element greater than or equal to your val
    int it = lower_bound(sums, 0, kN, p);
    if (it > p)
    {

        // Previous value
        --it;
    }

    // Returns the index in array upto which
    // killing is possible with strength P
    return it;
}
private static int lower_bound(long[] a, int low,
                            int high, int element)
{
    while(low < high)
    {
        int middle = low + (high - low)/2;
        if(element > a[middle])
            low = middle + 1;
        else
            high = middle;
    }
    return low;
}

// Driver code
public static void Main(String[] args)
{
    int p = 14;
    Console.WriteLine(maxPeople(p));
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

const kN = 1000000;

// Function to return the maximum
// number of people that can be killed
function maxPeople(p)
{
    // Storing the sum beforehand so that
    // it can be used in each query
    let sums = new Array(kN);
    sums[0] = 0;
    for (let i = 1; i < kN; i++)
        sums[i] = (i * i) + sums[i - 1];

    // lower_bound returns an iterator pointing to the
    // first element greater than or equal to your val
    let it = lower_bound(sums, 0, kN, p);
    if (it > p) {

        // Previous value
        --it;
    }

    // Returns the index in array upto which
    // killing is possible with strength P
    return it;
}

function lower_bound(a, low, high, element)
{
    while(low < high)
    {
        let middle = low + parseInt((high - low)/2);
        if(element > a[middle])
            low = middle + 1;
        else
            high = middle;
    }
    return low;
}

// Driver code
    let p = 14;
    document.write(maxPeople(p));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(Log(n))

**更有效的方法:**
我们可以在时间复杂度 O(logn)和空间复杂度 O(1)上做同样的问题。考虑低至 0 和高至 10^15.的值，开始你的二分搜索法我们将计算中间值，根据中间值，我们将改变低和高的位置。

下面是上述方法的实现。

## C++

```
// C++ implementation of the approach
#include <algorithm>
#include <bits/stdc++.h>
using namespace std;

// Helper function which returns the sum
// of series (1^2 + 2^2 +...+ n^2)
long squareSeries(long n)
{
    return(n * (n + 1) * (2 * n + 1)) / 6;
}

// maxPeople function which returns
// appropriate value using Binary Search
// in O(logn)
long maxPeople(long n)
{

    // Set the lower and higher values
    long low = 0;
    long high = 1000000L;
    long ans = 0L;

    while (low <= high)
    {

        // Calculate the mid using
        // low and high
        long mid = low + ((high - low) / 2);
        long value = squareSeries(mid);

        // Compare value with n
        if (value <= n)
        {
            ans = mid;
            low = mid + 1;
        }
        else
        {
            high = mid - 1;
        }
    }

    // Return the ans
    return ans;
}

// Driver code
int main()
{
    long p = 14;

    cout<<maxPeople(p);
    return 0;
}

// This code contributed by shikhasingrajput
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG{

// Helper function which returns the sum
// of series (1^2 + 2^2 +...+ n^2)
static long squareSeries(long n)
{
    return(n * (n + 1) * (2 * n + 1)) / 6;
}

// maxPeople function which returns
// appropriate value using Binary Search
// in O(logn)
static long maxPeople(long n)
{

    // Set the lower and higher values
    long low = 0;
    long high = 1000000L;
    long ans = 0L;

    while (low <= high)
    {

        // Calculate the mid using
        // low and high
        long mid = low + ((high - low) / 2);
        long value = squareSeries(mid);

        // Compare value with n
        if (value <= n)
        {
            ans = mid;
            low = mid + 1;
        }
        else
        {
            high = mid - 1;
        }
    }

    // Return the ans
    return ans;
}

// Driver code
public static void main(String[] args)
{
    long p = 14;

    System.out.println(maxPeople(p));
}}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# helper function which returns the sum
# of series (1^2 + 2^2 +...+ n^2)
def squareSeries(n):
    return (n*(n+1)*(2*n+1))//6

# maxPeople function which returns
# appropriate value using Binary Search
# in O(logn)

def maxPeople(n):

    # Set the lower and higher values
    low = 0
    high = 1000000000000000
    while low<=high:

        # calculate the mid using
        # low and high

        mid = low + ((high-low)//2)
        value = squareSeries(mid)

        #compare value with n
        if value<=n:
            ans = mid
            low = mid+1
        else:
            high = mid-1

    # return the ans
    return ans

if __name__=='__main__':
    p=14
    print(maxPeople(p))

# This code is contributed bu chaudhary_19
# (* Mayank Chaudhary)
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Helper function which returns the sum
// of series (1^2 + 2^2 +...+ n^2)
static long squareSeries(long n)
{
    return(n * (n + 1) * (2 * n + 1)) / 6;
}

// maxPeople function which returns
// appropriate value using Binary Search
// in O(logn)
static long maxPeople(long n)
{

    // Set the lower and higher values
    long low = 0;
    long high = 1000000L;
    long ans = 0L;

    while (low <= high)
    {

        // Calculate the mid using
        // low and high
        long mid = low + ((high - low) / 2);
        long value = squareSeries(mid);

        // Compare value with n
        if (value <= n)
        {
            ans = mid;
            low = mid + 1;
        }
        else
        {
            high = mid - 1;
        }
    }

    // Return the ans
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    long p = 14;

    Console.Write(maxPeople(p));
}}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Helper function which returns the sum
// of series (1^2 + 2^2 +...+ n^2)
function squareSeries(n)
{
    return Math.floor((n * (n + 1) * (2 * n + 1)) / 6);
}

// maxPeople function which returns
// appropriate value using Binary Search
// in O(logn)
function maxPeople(n)
{

    // Set the lower and higher values
    let low = 0;
    let high = 1000000;
    let ans = 0;

    while (low <= high)
    {

        // Calculate the mid using
        // low and high
        let mid = low + Math.floor((high - low) / 2);
        let value = squareSeries(mid);

        // Compare value with n
        if (value <= n)
        {
            ans = mid;
            low = mid + 1;
        }
        else
        {
            high = mid - 1;
        }
    }

    // Return the ans
    return ans;
}

// Driver code
let p = 14;

document.write(maxPeople(p));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(Log(n))
**空间复杂度:** O(1)