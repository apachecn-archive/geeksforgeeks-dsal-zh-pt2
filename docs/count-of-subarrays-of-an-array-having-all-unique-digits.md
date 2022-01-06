# 具有所有唯一数字的数组的子序列计数

> 原文:[https://www . geeksforgeeks . org/具有所有唯一数字的数组的子数组计数/](https://www.geeksforgeeks.org/count-of-subarrays-of-an-array-having-all-unique-digits/)

给定一个包含正整数 **N** 的数组 **A** ，任务是找到这个数组的子序列数，使得在每个子序列中，没有一个数字重复两次，即子序列的所有数字必须是唯一的。
**例:**

> **输入:**A =【1，12，23，34】
> **输出:** 7
> 子序列为:{1}、{12}、{23}、{34}、{1，23}、{1，34}、{12，34}
> 因此此类子序列的计数= 7
> 
> **输入:**A =【5，12，2，1，165，2323，7】
> **输出:** 33

**朴素方法:**生成数组的所有子序列，并遍历它们来检查给定条件是否满足。在末尾打印此类子序列的计数。

下面是上述方法的实现:

## C++

```
// C++ program to find the count
// of subsequences  of an Array
// having all unique digits

#include <bits/stdc++.h>
using namespace std;

// Function to check whether
// the subsequences  has all unique digits
bool check(vector<int>& v)
{

    // Storing all digits occurred
    set<int> digits;

    // Traversing all the numbers of v
    for (int i = 0; i < v.size(); i++) {
        // Storing all digits of v[i]
        set<int> d;

        while (v[i]) {
            d.insert(v[i] % 10);
            v[i] /= 10;
        }

        // Checking whether digits of v[i]
        // have already occurred
        for (auto it : d) {
            if (digits.count(it))
                return false;
        }

        // Inserting digits of v[i] in the set
        for (auto it : d)
            digits.insert(it);
    }

    return true;
}

// Function to count the number
// subarray with all digits unique
int numberOfSubarrays(int a[], int n)
{

    int answer = 0;

    // Traverse through all the subarrays
    for (int i = 1; i < (1 << n); i++) {
        // To store elements of this subarray
        vector<int> temp;

        // Generate all subarray
        // and store it in vector
        for (int j = 0; j < n; j++) {
            if (i & (1 << j))
                temp.push_back(a[j]);
        }

        // Check whether this subarray
        // has all digits unique
        if (check(temp))

            // Increase the count
            answer++;
    }

    // Return the count
    return answer;
}

// Driver code
int main()
{
    int N = 4;
    int A[] = { 1, 12, 23, 34 };

    cout << numberOfSubarrays(A, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count
// of subarrays of an Array
// having all unique digits

import java.util.*;

class GFG{

// Function to check whether
// the subarray has all unique digits
static boolean check(Vector<Integer> v)
{

    // Storing all digits occurred
    HashSet<Integer> digits = new HashSet<Integer>();

    // Traversing all the numbers of v
    for (int i = 0; i < v.size(); i++) {
        // Storing all digits of v[i]
        HashSet<Integer> d = new HashSet<Integer>();

        while (v.get(i)>0) {
            d.add(v.get(i) % 10);
            v.set(i, v.get(i)/10);
        }

        // Checking whether digits of v[i]
        // have already occurred
        for (int it : d) {
            if (digits.contains(it))
                return false;
        }

        // Inserting digits of v[i] in the set
        for (int it : d)
            digits.add(it);
    }

    return true;
}

// Function to count the number
// subarray with all digits unique
static int numberOfSubarrays(int a[], int n)
{

    int answer = 0;

    // Traverse through all the subarrays
    for (int i = 1; i < (1 << n); i++) {
        // To store elements of this subarray
        Vector<Integer> temp = new Vector<Integer>();

        // Generate all subarray
        // and store it in vector
        for (int j = 0; j < n; j++) {
            if ((i & (1 << j))>0)
                temp.add(a[j]);
        }

        // Check whether this subarray
        // has all digits unique
        if (check(temp))

            // Increase the count
            answer++;
    }

    // Return the count
    return answer;
}

// Driver code
public static void main(String[] args)
{
    int N = 4;
    int A[] = { 1, 12, 23, 34 };

    System.out.print(numberOfSubarrays(A, N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the count
# of subarrays of an Array
# having all unique digits

# Function to check whether
# the subarray has all unique digits
def check(v):

    # Storing all digits occurred
    digits = set()

    # Traversing all the numbers of v
    for i in range(len(v)):

        # Storing all digits of v[i]
        d = set()

        while (v[i] != 0):
            d.add(v[i] % 10)
            v[i] //= 10

        # Checking whether digits of v[i]
        # have already occurred
        for it in d:
            if it in digits:
                return False

        # Inserting digits of v[i] in the set
        for it in d:
            digits.add(it)

    return True

# Function to count the number
# subarray with all digits unique
def numberOfSubarrays(a, n):

    answer = 0

    # Traverse through all the subarrays
    for i in range(1, 1 << n):

        # To store elements of this subarray
        temp = []

        # Generate all subarray
        # and store it in vector
        for j in range(n):
            if (i & (1 << j)):
                temp.append(a[j])

        # Check whether this subarray
        # has all digits unique
        if (check(temp)):

            # Increase the count
            answer += 1

    # Return the count
    return answer

# Driver code
if __name__=="__main__":

    N = 4
    A = [ 1, 12, 23, 34 ]

    print(numberOfSubarrays(A, N))

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find the count
// of subarrays of an Array
// having all unique digits
using System;
using System.Collections.Generic;

class GFG{

// Function to check whether
// the subarray has all unique digits
static bool check(List<int> v)
{

    // Storing all digits occurred
    HashSet<int> digits = new HashSet<int>();

    // Traversing all the numbers of v
    for(int i = 0; i < v.Count; i++)
    {

        // Storing all digits of v[i]
        HashSet<int> d = new HashSet<int>();

        while (v[i] > 0)
        {
            d.Add(v[i] % 10);
            v[i] = v[i] / 10;
        }

        // Checking whether digits of v[i]
        // have already occurred
        foreach(int it in d)
        {
            if (digits.Contains(it))
                return false;
        }

        // Inserting digits of v[i] in the set
        foreach(int it in d)
            digits.Add(it);
    }
    return true;
}

// Function to count the number
// subarray with all digits unique
static int numberOfSubarrays(int []a, int n)
{
    int answer = 0;

    // Traverse through all the subarrays
    for(int i = 1; i < (1 << n); i++)
    {

        // To store elements of this subarray
        List<int> temp = new List<int>();

        // Generate all subarray
        // and store it in vector
        for(int j = 0; j < n; j++)
        {
            if ((i & (1 << j)) > 0)
                temp.Add(a[j]);
        }

        // Check whether this subarray
        // has all digits unique
        if (check(temp))

            // Increase the count
            answer++;
    }

    // Return the count
    return answer;
}

// Driver code
public static void Main(String[] args)
{
    int N = 4;
    int []A = { 1, 12, 23, 34 };

    Console.Write(numberOfSubarrays(A, N));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// Javascript program to find the count
// of subarrays of an Array
// having all unique digits

// Function to check whether
// the subarray has all unique digits
function check(v) {

    // Storing all digits occurred
    let digits = new Set();

    // Traversing all the numbers of v
    for (let i = 0; i < v.length; i++) {
        // Storing all digits of v[i]
        let d = new Set();

        while (v[i]) {
            d.add(v[i] % 10);
            v[i] = Math.floor(v[i] / 10);
        }

        // Checking whether digits of v[i]
        // have already occurred
        for (let it of d) {
            if (digits.has(it))
                return false;
        }

        // Inserting digits of v[i] in the set
        for (let it of d)
            digits.add(it);
    }

    return true;
}

// Function to count the number
// subarray with all digits unique
function numberOfSubarrays(a, n) {

    let answer = 0;

    // Traverse through all the subarrays
    for (let i = 1; i < (1 << n); i++) {
        // To store elements of this subarray
        let temp = new Array();

        // Generate all subarray
        // and store it in vector
        for (let j = 0; j < n; j++) {
            if (i & (1 << j))
                temp.push(a[j]);
        }

        // Check whether this subarray
        // has all digits unique
        if (check(temp))

            // Increase the count
            answer++;
    }

    // Return the count
    return answer;
}

// Driver code

let N = 4;
let A = [1, 12, 23, 34];

document.write(numberOfSubarrays(A, N));

// This code is contributed by gfgking
</script>
```

**Output:** 

```
7
```

**时间复杂度:** *O(N * 2 <sup>N</sup> )*

**有效方法:**这种方法依赖于十进制数字系统中只有 10 个唯一数字的事实。因此，最长的子序列将只有 10 位数字，以满足要求的条件。

*   我们将使用[位屏蔽和动态编程](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)来解决这个问题。
*   因为只有 10 位数字，所以考虑每个数字的 10 位表示，其中如果对应于该位的数字出现在该数字中，则每个位为 1。
*   假设，I 是当前数组元素(从 1 到 i-1 的元素已经被处理)。整数变量“**掩码**”表示子序列中已经出现的数字。如果在掩码中设置了第 I 位，那么第 I 位已经出现，否则不会出现。
*   在**递归关系**的每一步，元素可以包含在子序列中，也可以不包含在子序列中。如果元素不包含在子数组中，那么只需移动到下一个索引。如果包含，通过将掩码中与当前元素的数字对应的所有位设置为开来更改掩码。
    **注意:**当前要素只有在所有数字之前都没有出现过的情况下才能包含。
*   只有当掩码中对应于当前元素数字的位为“关”时，此条件才会得到满足。
*   如果画出完整的[递归树](https://www.geeksforgeeks.org/analysis-algorithm-set-4-master-method-solving-recurrences/)，可以观察到很多子问题正在一次又一次的被解决。所以我们使用[动态编程](http://www.geeksforgeeks.org/dynamic-programming/)。使用表 **dp[][]** 使得对于每个索引 dp[i][j]，I 是元素在数组中的位置，j 是掩码。

下面是上述方法的实现:

## C++

```
// C++ program to find the count
// of subsequences  of an Array
// having all unique digits

#include <bits/stdc++.h>
using namespace std;

// Dynamic programming table
int dp[5000][(1 << 10) + 5];

// Function to obtain
// the mask for any integer
int getmask(int val)
{
    int mask = 0;

    if (val == 0)
        return 1;

    while (val) {
        int d = val % 10;
        mask |= (1 << d);
        val /= 10;
    }
    return mask;
}

// Function to count the number of ways
int countWays(int pos, int mask,
              int a[], int n)
{
    // Subarray must not be empty
    if (pos == n)
        return (mask > 0 ? 1 : 0);

    // If subproblem has been solved
    if (dp[pos][mask] != -1)
        return dp[pos][mask];

    int count = 0;

    // Excluding this element in the subarray
    count = count
            + countWays(pos + 1, mask, a, n);

    // If there are no common digits
    // then only this element can be included
    if ((getmask(a[pos]) & mask) == 0) {

        // Calculate the new mask
        // if this element is included
        int new_mask
            = (mask | (getmask(a[pos])));

        count = count
                + countWays(pos + 1,
                            new_mask,
                            a, n);
    }

    // Store and return the answer
    return dp[pos][mask] = count;
}

// Function to find the count of
// subarray with all digits unique
int numberOfSubarrays(int a[], int n)
{
    // initializing dp
    memset(dp, -1, sizeof(dp));

    return countWays(0, 0, a, n);
}

// Driver code
int main()
{
    int N = 4;
    int A[] = { 1, 12, 23, 34 };

    cout << numberOfSubarrays(A, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count
// of subarrays of an Array
// having all unique digits
import java.util.*;

class GFG{

// Dynamic programming table
static int [][]dp = new int[5000][(1 << 10) + 5];

// Function to obtain
// the mask for any integer
static int getmask(int val)
{
    int mask = 0;

    if (val == 0)
        return 1;

    while (val > 0) {
        int d = val % 10;
        mask |= (1 << d);
        val /= 10;
    }
    return mask;
}

// Function to count the number of ways
static int countWays(int pos, int mask,
              int a[], int n)
{
    // Subarray must not be empty
    if (pos == n)
        return (mask > 0 ? 1 : 0);

    // If subproblem has been solved
    if (dp[pos][mask] != -1)
        return dp[pos][mask];

    int count = 0;

    // Excluding this element in the subarray
    count = count
            + countWays(pos + 1, mask, a, n);

    // If there are no common digits
    // then only this element can be included
    if ((getmask(a[pos]) & mask) == 0) {

        // Calculate the new mask
        // if this element is included
        int new_mask
            = (mask | (getmask(a[pos])));

        count = count
                + countWays(pos + 1,
                            new_mask,
                            a, n);
    }

    // Store and return the answer
    return dp[pos][mask] = count;
}

// Function to find the count of
// subarray with all digits unique
static int numberOfSubarrays(int a[], int n)
{
    // initializing dp
    for(int i = 0;i<5000;i++)
    {
        for (int j = 0; j < (1 << 10) + 5; j++) {
            dp[i][j] = -1;
        }
    }

    return countWays(0, 0, a, n);
}

// Driver code
public static void main(String[] args)
{
    int N = 4;
    int A[] = { 1, 12, 23, 34 };

    System.out.print(numberOfSubarrays(A, N));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 program to find the count
# of subarrays of an Array having all
# unique digits

# Function to obtain
# the mask for any integer
def getmask(val):

    mask = 0

    if val == 0:
        return 1

    while (val):
        d = val % 10;
        mask |= (1 << d)
        val = val // 10

    return mask

# Function to count the number of ways
def countWays(pos, mask, a, n):

    # Subarray must not be empty
    if pos == n :
        if mask > 0:
            return 1
        else:
            return 0

    # If subproblem has been solved
    if dp[pos][mask] != -1:
        return dp[pos][mask]

    count = 0

    # Excluding this element in the subarray
    count = (count +
             countWays(pos + 1, mask, a, n))

    # If there are no common digits
    # then only this element can be included
    if (getmask(a[pos]) & mask) == 0:

        # Calculate the new mask
        # if this element is included
        new_mask = (mask | (getmask(a[pos])))

        count = (count +
                 countWays(pos + 1,
                           new_mask,
                           a, n))

    # Store and return the answer
    dp[pos][mask] = count
    return count

# Function to find the count of
# subarray with all digits unique
def numberOfSubarrays(a, n):

    return countWays(0, 0, a, n)

# Driver Code
N = 4
A = [ 1, 12, 23, 34 ]

rows = 5000
cols = 1100

# Initializing dp
dp = [ [ -1 for i in range(cols) ]
            for j in range(rows) ]

print( numberOfSubarrays(A, N))

# This code is contributed by sarthak_eddy.
```

## C#

```
// C# program to find the count
// of subarrays of an Array
// having all unique digits
using System;

public class GFG{

// Dynamic programming table
static int [,]dp = new int[5000, (1 << 10) + 5];

// Function to obtain
// the mask for any integer
static int getmask(int val)
{
    int mask = 0;

    if (val == 0)
        return 1;

    while (val > 0) {
        int d = val % 10;
        mask |= (1 << d);
        val /= 10;
    }
    return mask;
}

// Function to count the number of ways
static int countWays(int pos, int mask,
            int []a, int n)
{
    // Subarray must not be empty
    if (pos == n)
        return (mask > 0 ? 1 : 0);

    // If subproblem has been solved
    if (dp[pos, mask] != -1)
        return dp[pos, mask];

    int count = 0;

    // Excluding this element in the subarray
    count = count
        + countWays(pos + 1, mask, a, n);

    // If there are no common digits
    // then only this element can be included
    if ((getmask(a[pos]) & mask) == 0) {

        // Calculate the new mask
        // if this element is included
        int new_mask
            = (mask | (getmask(a[pos])));

        count = count
            + countWays(pos + 1,
            new_mask, a, n);
    }

    // Store and return the answer
    return dp[pos, mask] = count;
}

// Function to find the count of
// subarray with all digits unique
static int numberOfSubarrays(int []a, int n)
{
    // initializing dp
    for(int i = 0; i < 5000; i++)
    {
        for (int j = 0; j < (1 << 10) + 5; j++) {
            dp[i,j] = -1;
        }
    }

    return countWays(0, 0, a, n);
}

// Driver code
public static void Main(String[] args)
{
    int N = 4;
    int []A = { 1, 12, 23, 34 };

    Console.Write(numberOfSubarrays(A, N));
}
}
// This code contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript program to find the count
// of subarrays of an Array
// having all unique digits

// Dynamic programming table
var dp = Array.from(Array(5000), ()=>Array((1 << 10) + 5).fill(-1));

// Function to obtain
// the mask for any integer
function getmask(val)
{
    var mask = 0;

    if (val == 0)
        return 1;

    while (val) {
        var d = val % 10;
        mask |= (1 << d);
        val = parseInt(val/10);
    }
    return mask;
}

// Function to count the number of ways
function countWays(pos, mask, a, n)
{
    // Subarray must not be empty
    if (pos == n)
        return (mask > 0 ? 1 : 0);

    // If subproblem has been solved
    if (dp[pos][mask] != -1)
        return dp[pos][mask];

    var count = 0;

    // Excluding this element in the subarray
    count = count
            + countWays(pos + 1, mask, a, n);

    // If there are no common digits
    // then only this element can be included
    if ((getmask(a[pos]) & mask) == 0) {

        // Calculate the new mask
        // if this element is included
        var new_mask
            = (mask | (getmask(a[pos])));

        count = count
                + countWays(pos + 1,
                            new_mask,
                            a, n);
    }

    // Store and return the answer
    return dp[pos][mask] = count;
}

// Function to find the count of
// subarray with all digits unique
function numberOfSubarrays(a, n)
{
    // initializing dp
    dp = Array.from(Array(5000), ()=>Array((1 << 10) + 5).fill(-1));

    return countWays(0, 0, a, n);
}

// Driver code
var N = 4;
var A = [1, 12, 23, 34];
document.write( numberOfSubarrays(A, N));

</script>
```

**Output:** 

```
7
```

**时间复杂度:** *O(N * 2 <sup>10</sup> )*