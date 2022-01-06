# 数组中两个数的最大异或

> 原文:[https://www . geesforgeks . org/数组中两个数的最大异或/](https://www.geeksforgeeks.org/maximum-xor-of-two-numbers-in-an-array/)

给定大小为 **N** 的非负整数数组 **Arr** 。任务是找出数组中两个数之间最大可能的异或。
**例** :

> **输入:** Arr = {25，10，2，8，5，3}
> **输出:** 28
> 最大结果为 5 ^ 25 = 28
> **输入:** Arr = {1，2，3，4，5，6，7}
> **输出:** 7
> 最大结果为 1 ^ 6 = 7

**天真方法:**一个简单的解决方案是生成给定数组的所有对，并计算这些对的异或。最后，返回最大异或值。这个解决方案需要![O(N^{2})        ](img/1c436e91a4414aad0145e7e7e4679887.png "Rendered by QuickLaTeX.com")时间。
以下是上述办法的实施:

## C++

```
// C++ implementation
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// maximum xor
int max_xor(int arr[], int n)
{

    int maxXor = 0;

    // Calculating xor of each pair
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            maxXor = max(maxXor,
                         arr[i] ^ arr[j]);
        }
    }
    return maxXor;
}

// Driver Code
int main()
{

    int arr[] = { 25, 10, 2, 8, 5, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << max_xor(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the
    // maximum xor
    static int max_xor(int arr[], int n)
    {
        int maxXor = 0;

        // Calculating xor of each pair
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                maxXor = Math.max(maxXor,
                        arr[i] ^ arr[j]);
            }
        }
        return maxXor;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = {25, 10, 2, 8, 5, 3};
        int n = arr.length;

        System.out.println(max_xor(arr, n));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation

# Function to return the
# maximum xor
def max_xor(arr, n):

    maxXor = 0;

    # Calculating xor of each pair
    for i in range(n):
        for j in range(i + 1, n):
            maxXor = max(maxXor,\
                         arr[i] ^ arr[j]);

    return maxXor;

# Driver Code
if __name__ == '__main__':

    arr = [ 25, 10, 2, 8, 5, 3 ];
    n = len(arr);

    print(max_xor(arr, n));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the
// maximum xor
static int max_xor(int []arr, int n)
{
    int maxXor = 0;

    // Calculating xor of each pair
    for (int i = 0; i < n; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            maxXor = Math.Max(maxXor,
                              arr[i] ^ arr[j]);
        }
    }
    return maxXor;
}

// Driver Code
public static void Main()
{
    int []arr = {25, 10, 2, 8, 5, 3};
    int n = arr.Length;

    Console.WriteLine(max_xor(arr, n));
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation

// Function to return the
// maximum xor
function max_xor(arr, n)
{

    let maxXor = 0;

    // Calculating xor of each pair
    for (let i = 0; i < n; i++) {
        for (let j = i + 1; j < n; j++) {
            maxXor = Math.max(maxXor,
                         arr[i] ^ arr[j]);
        }
    }
    return maxXor;
}

// Driver Code

    let arr = [ 25, 10, 2, 8, 5, 3 ];
    let n = arr.length;

    document.write(max_xor(arr, n));

</script>
```

**Output:** 

```
28
```

**时间复杂度:** ![O(N^{2})        ](img/1c436e91a4414aad0145e7e7e4679887.png "Rendered by QuickLaTeX.com")，这里 **N** 就是阵的大小

**辅助空间:** O(1)
**高效进场:**进场类似于本文中的任务是寻找**最大 AND 值对**。
所以思路是把问题语句从求数组中两个数的最大 xor 改为- >求数组中两个数，这样其 xor 等于一个数 **X** 。在这种情况下， **X** 将是我们想要达到的最大数量，直到第 I 位。
为了找到异或运算的最大值，异或的值应该是每一位都是一个设置位，即 1。在 32 位数字中，目标是从左到右获得最多 1 个集合。
为了评估每个位，该位需要一个**掩码**。**掩码**定义了哪个位应该出现在答案中，哪个位不应该出现。这里，我们将使用**掩码**来保留输入中每个数字的前缀(通过使用带有掩码的**和**来表示该数字还剩多少位)，直到第 I 位，然后使用我们集合中可能的数字列表，在插入该数字后，我们将评估是否可以将该位位置的最大值更新为 1。
以下是上述方法的实施:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the
// maximum xor
int max_xor(int arr[], int n)
{
    int maxx = 0, mask = 0;

    set<int> se;

    for (int i = 30; i >= 0; i--) {

        // set the i'th bit in mask
        // like 100000, 110000, 111000..
        mask |= (1 << i);

        for (int i = 0; i < n; ++i) {

            // Just keep the prefix till
            // i'th bit neglecting all
            // the bit's after i'th bit
            se.insert(arr[i] & mask);
        }

        int newMaxx = maxx | (1 << i);

        for (int prefix : se) {

            // find two pair in set
            // such that a^b = newMaxx
            // which is the highest
            // possible bit can be obtained
            if (se.count(newMaxx ^ prefix)) {
                maxx = newMaxx;
                break;
            }
        }

        // clear the set for next
        // iteration
        se.clear();
    }

    return maxx;
}

// Driver Code
int main()
{

    int arr[] = { 25, 10, 2, 8, 5, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << max_xor(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
class GFG
{

// Function to return the
// maximum xor
static int max_xor(int arr[], int n)
{
    int maxx = 0, mask = 0;

    HashSet<Integer> se = new HashSet<Integer>();

    for (int i = 30; i >= 0; i--)
    {

        // set the i'th bit in mask
        // like 100000, 110000, 111000..
        mask |= (1 << i);

        for (int j = 0; j < n; ++j)
        {

            // Just keep the prefix till
            // i'th bit neglecting all
            // the bit's after i'th bit
            se.add(arr[j] & mask);
        }

        int newMaxx = maxx | (1 << i);

        for (int prefix : se)
        {

            // find two pair in set
            // such that a^b = newMaxx
            // which is the highest
            // possible bit can be obtained
            if (se.contains(newMaxx ^ prefix))
            {
                maxx = newMaxx;
                break;
            }
        }

        // clear the set for next
        // iteration
        se.clear();
    }
    return maxx;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 25, 10, 2, 8, 5, 3 };
    int n = arr.length;

    System.out.println(max_xor(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return the
# maximum xor
def max_xor( arr , n):

    maxx = 0
    mask = 0;

    se = set()

    for i in range(30, -1, -1):

        # set the i'th bit in mask
        # like 100000, 110000, 111000..
        mask |= (1 << i)
        newMaxx = maxx | (1 << i)

        for i in range(n):

            # Just keep the prefix till
            # i'th bit neglecting all
            # the bit's after i'th bit
            se.add(arr[i] & mask)

        for prefix in se:

            # find two pair in set
            # such that a^b = newMaxx
            # which is the highest
            # possible bit can be obtained
            if (newMaxx ^ prefix) in se:
                maxx = newMaxx
                break

        # clear the set for next
        # iteration
        se.clear()
    return maxx

# Driver Code
arr = [ 25, 10, 2, 8, 5, 3 ]
n = len(arr)
print(max_xor(arr, n))

# This code is contributed by ANKITKUMAR34
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the
// maximum xor
static int max_xor(int []arr, int n)
{
    int maxx = 0, mask = 0;

    HashSet<int> se = new HashSet<int>();

    for (int i = 30; i >= 0; i--)
    {

        // set the i'th bit in mask
        // like 100000, 110000, 111000..
        mask |= (1 << i);

        for (int j = 0; j < n; ++j)
        {

            // Just keep the prefix till
            // i'th bit neglecting all
            // the bit's after i'th bit
            se.Add(arr[j] & mask);
        }

        int newMaxx = maxx | (1 << i);

        foreach (int prefix in se)
        {

            // find two pair in set
            // such that a^b = newMaxx
            // which is the highest
            // possible bit can be obtained
            if (se.Contains(newMaxx ^ prefix))
            {
                maxx = newMaxx;
                break;
            }
        }

        // clear the set for next
        // iteration
        se.Clear();
    }
    return maxx;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 25, 10, 2, 8, 5, 3 };
    int n = arr.Length;

    Console.WriteLine(max_xor(arr, n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to return the
// maximum xor
function max_xor(arr, n)
{
    let maxx = 0, mask = 0;

    var se = new Set();

    for (let i = 30; i >= 0; i--)
    {

        // set the i'th bit in mask
        // like 100000, 110000, 111000..
        mask |= (1 << i);

        for (let j = 0; j < n; ++j)
        {

            // Just keep the prefix till
            // i'th bit neglecting all
            // the bit's after i'th bit
            se.add(arr[j] & mask);
        }

        let newMaxx = maxx | (1 << i);

        //for (let prefix in se)
        for (let prefix of se.keys())
        {

            // find two pair in set
            // such that a^b = newMaxx
            // which is the highest
            // possible bit can be obtained
            if (se.has(newMaxx ^ prefix))
            {
                maxx = newMaxx;
                break;
            }
        }

        // clear the set for next
        // iteration
        se.clear();
    }
    return maxx;
}

// Driver code
    let arr = [ 25, 10, 2, 8, 5, 3 ];
    let n = arr.length;

    document.write(max_xor(arr, n));

// This code is contributed by target_2.
</script>
```

**Output:** 

```
28
```

**时间复杂度:** ![O(Nlog(M))        ](img/a0f3e645b4f386b840bd79949e847433.png "Rendered by QuickLaTeX.com")，其中 **N** 为数组大小， **M** 为数组中存在的最大数量
**辅助空间:** O(logM)