# 计数四胞胎(甲、乙、丙、丁)直到 N，使得甲和乙的平方和等于丙和丁的平方和

> 原文:[https://www . geeksforgeeks . org/count-four letsa-b-c-d-till-n 这样 a 和 b 的平方和等于 c 和 d 的平方和/](https://www.geeksforgeeks.org/count-quadrupletsa-b-c-d-till-n-such-that-sum-of-square-of-a-and-b-is-equal-to-that-of-c-and-d/)

给定一个数字 **N** ，任务是找出正方形的数量，使得**a<sup>2</sup>+b<sup>2</sup>= c<sup>2</sup>+d<sup>2</sup>**其中(1 < = a、b、c、d < = N)。

**示例:**

> **输入:** N = 2
> **输出:** 6
> **说明:**
> 有 6 个有效的四元(1，1，1，1，1)，(1，2，1，2，1)，(2，1，1，2，2)，(2，1，1，2)，(2，1，2，1)，(2，2，2，2，2)。
> 
> **输入:** N = 4
> **输出** 28
> **说明:**
> N = 4 有 28 个有效样方。

**天真法:**天真法是在范围**【1，N】**内使用 4 个嵌套循环，对那些四胞胎 **(a，b，c，d)** 进行计数，使得**a<sup>2</sup>+b<sup>2</sup>= c<sup>2</sup>+d<sup>2</sup>**

***时间复杂度:**O(N<sup>4</sup>)*
***辅助空间:** O(1)*

**有效的方法而不是幼稚的方法:**使用一些数学方法可以在时间复杂度方面降低上述解决方案。找到四胞胎，使 a<sup>2</sup>+b<sup>2</sup>= c<sup>2</sup>+d<sup>2</sup>。

> a<sup>2</sup>+b<sup>2</sup>= c<sup>2</sup>+d<sup>2</sup>T8】a<sup>2</sup>+b<sup>2</sup>–c<sup>2</sup>= d<sup>2</sup>T17】两边取平方根
> (a<sup>2</sup>+b<sup>2</sup>–c<sup>2</sup>

利用上述公式，我们可以得出 **d** 只存在于(a<sup>2</sup>+b<sup>2</sup>–c<sup>2</sup>)<sup>1/2</sup>为正整数的情况下。

***时间复杂度:** O(N <sup>3</sup> )*

**高效方法:**想法是使用 [**哈希**](https://www.geeksforgeeks.org/hashing-data-structure/) 。以下是步骤:

1.  遍历所有对(如 **(a，b)** )到**【1，N】**上，并将 **a <sup>2</sup> + b <sup>2</sup>** 的值存储在[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
2.  迭代所有对**【1，N】**，如果地图上存在总和，则计算地图上存储的每对的总和。
3.  打印计数。

以下是该方法的实施情况:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
typedef long long int ll;

// Function to count the quadruples
ll countQuadraples(ll N)
{
    // Counter variable
    ll cnt = 0;

    // Map to store the
    // sum of pair (a^2 + b^2)
    map<ll, ll> m;

    // Iterate till N
    for (ll a = 1; a <= N; a++) {

        for (ll b = 1; b <= N; b++) {

            // Calculate a^2 + b^2
            ll x = a * a + b * b;

            // Increment the value in map
            m[x] += 1;
        }
    }

    for (ll c = 1; c <= N; c++) {
        for (ll d = 1; d <= N; d++) {

            ll x = c * c + d * d;

            // Check if this sum
            // was also in a^2 + b^2
            if (m.find(x) != m.end())
                cnt += m[x];
        }
    }

    // Return the count
    return cnt;
}

// Driver Code
int main()
{
    // Given N
    ll N = 2;

    // Function Call
    cout << countQuadraples(N)
        << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count the quadruples
static long countQuadraples(long N)
{

    // Counter variable
    long cnt = 0;

    // Map to store the
    // sum of pair (a^2 + b^2)
    Map<Long, Long> m = new HashMap<>();

    // Iterate till N
    for(long a = 1; a <= N; a++)
    {
        for(long b = 1; b <= N; b++)
        {

            // Calculate a^2 + b^2
            long x = a * a + b * b;

            // Increment the value in map
            m.put(x, m.getOrDefault(x, 0l) + 1);
        }
    }

    for(long c = 1; c <= N; c++)
    {
        for(long d = 1; d <= N; d++)
        {
            long x = c * c + d * d;

            // Check if this sum
            // was also in a^2 + b^2
            if (m.containsKey(x))
                cnt += m.get(x);
        }
    }

    // Return the count
    return cnt;
}

// Driver code
public static void main(String[] args)
{

    // Given N
    long N = 2;

    // Function call
    System.out.println(countQuadraples(N));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for
# the above approach
from collections import defaultdict

# Function to count
# the quadruples
def countQuadraples(N):

    # Counter variable
    cnt = 0

    # Map to store the
    # sum of pair (a^2 + b^2)
    m = defaultdict (int)

    # Iterate till N
    for a in range (1, N + 1):

        for b in range (1, N + 1):

            # Calculate a^2 + b^2
            x = a * a + b * b

            # Increment the value in map
            m[x] += 1

    for c in range (1, N + 1):
        for d in range (1, N + 1):

            x = c * c + d * d

            # Check if this sum
            # was also in a^2 + b^2
            if x in m:
                cnt += m[x]

    # Return the count
    return cnt

# Driver Code
if __name__ == "__main__":

    # Given N
    N = 2

    # Function Call
    print (countQuadraples(N))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count the quadruples
static long countQuadraples(long N)
{

    // Counter variable
    long cnt = 0;

    // Map to store the
    // sum of pair (a^2 + b^2)
    Dictionary<long,
               long> m = new Dictionary<long,
                                        long>();

    // Iterate till N
    for(long a = 1; a <= N; a++)
    {
        for(long b = 1; b <= N; b++)
        {

            // Calculate a^2 + b^2
            long x = a * a + b * b;

            // Increment the value in map
            if (m.ContainsKey(x))
                m[x] = m[x] + 1;
            else
                m.Add(x, 1);
        }
    }

    for(long c = 1; c <= N; c++)
    {
        for(long d = 1; d <= N; d++)
        {
            long x = c * c + d * d;

            // Check if this sum
            // was also in a^2 + b^2
            if (m.ContainsKey(x))
                cnt += m[x];
        }
    }

    // Return the count
    return cnt;
}

// Driver code
public static void Main(String[] args)
{

    // Given N
    long N = 2;

    // Function call
    Console.WriteLine(countQuadraples(N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the quadruples
function countQuadraples(N)
{
    // Counter variable
    var cnt = 0;

    // Map to store the
    // sum of pair (a^2 + b^2)
    var m = new Map(); 

    // Iterate till N
    for (var a = 1; a <= N; a++) {

        for (var b = 1; b <= N; b++) {

            // Calculate a^2 + b^2
            var x = a * a + b * b;

            // Increment the value in map
            if(m.has(x))
                m.set(x, m.get(x)+1)
            else
                m.set(x, 1)
        }
    }

    for (var c = 1; c <= N; c++) {
        for (var d = 1; d <= N; d++) {

            var x = c * c + d * d;

            // Check if this sum
            // was also in a^2 + b^2
            if (m.has(x))
                cnt += m.get(x);
        }
    }

    // Return the count
    return cnt;
}

// Driver Code
// Given N
var N = 2;
// Function Call
document.write( countQuadraples(N))

</script>
```

**Output:** 

```
6
```

**时间复杂度:***O(N<sup>2</sup>log N)*
**辅助空间:** *O(N)*