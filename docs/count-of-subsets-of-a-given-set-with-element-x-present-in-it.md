# 给定集合中存在元素 X 的子集的计数

> 原文:[https://www . geesforgeks . org/给定元素集的子集计数-x-present-in-it/](https://www.geeksforgeeks.org/count-of-subsets-of-a-given-set-with-element-x-present-in-it/)

给定一个由 **N** 个唯一正整数组成的数组 **arr[]** 和一个元素 **X** ，任务是计算元素 X 所在的给定集合的可能子集总数。

**示例:**

> **输入:**arr[]=【4，5，6，7】，X = 5
> **输出:** 8
> **解释:**
> 存在元素 5 的所有子集为:
> {5}、{4，5}、{5，6}、{5，7}、{4，5，6}、{4，5，7}、{5，6，7}、{5，7，7}
> 
> **输入:**arr[]=【1，2，3】，X = 1
> **输出:** 4
> **解释:**
> 存在元素 1 的所有子集为:
> {1}、{1，2}、{1，3}、{1，2，3}

**天真的方法:**
简单的解决方案是生成给定集合的所有可能子集，它们是 2^n，其中 n 是给定集合的大小，并计算元素 x 存在的子集的数量。
以下是上述办法的实施情况。

## C++

```
// C++ code to implement the above approach

#include <bits/stdc++.h>
using namespace std;

int CountSubSet(int arr[], int n, int X)
{
    // N stores total number of subsets
    int N = pow(2, n);
    int count = 0;

    // Generate each subset one by one
    for (int i = 0; i < N; i++) {

        // Check every bit of i
        for (int j = 0; j < n; j++) {

            // if j'th bit of i is set,
            // check arr[j] with X
            if (i & (1 << j))
                if (arr[j] == X)
                    count += 1;
        }
    }
    return count;
}

// Driver code
int main()
{
    int arr[] = { 4, 5, 6, 7 };
    int X = 5;
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << CountSubSet(arr, n, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement the above approach
class GFG
{

static int CountSubSet(int arr[], int n, int X)
{
    // N stores total number of subsets
    int N = (int) Math.pow(2, n);
    int count = 0;

    // Generate each subset one by one
    for (int i = 0; i < N; i++)
    {

        // Check every bit of i
        for (int j = 0; j < n; j++)
        {

            // if j'th bit of i is set,
            // check arr[j] with X
            if ((i & (1 << j)) != 0)
                if (arr[j] == X)
                    count += 1;
        }
    }
    return count;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 5, 6, 7 };
    int X = 5;
    int n = arr.length;

    System.out.print(CountSubSet(arr, n, X));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 code to implement the above approach
def CountSubSet(arr, n, X) :

    # N stores total number of subsets
    N = 2 ** n;
    count = 0;

    # Generate each subset one by one
    for i in range(N) :

        # Check every bit of i
        for j in range(n) :

            # if j'th bit of i is set,
            # check arr[j] with X
            if (i & (1 << j)) :
                if (arr[j] == X) :
                    count += 1;

    return count;

# Driver code
if __name__ == "__main__" :

    arr = [ 4, 5, 6, 7 ];
    X = 5;
    n = len(arr);

    print(CountSubSet(arr, n, X));

# This code is contributed by AnkitRai01
```

## C#

```
// C# code to implement the above approach
using System;

class GFG
{

static int CountSubSet(int []arr, int n, int X)
{
    // N stores total number of subsets
    int N = (int) Math.Pow(2, n);
    int count = 0;

    // Generate each subset one by one
    for (int i = 0; i < N; i++)
    {

        // Check every bit of i
        for (int j = 0; j < n; j++)
        {

            // if j'th bit of i is set,
            // check arr[j] with X
            if ((i & (1 << j)) != 0)
                if (arr[j] == X)
                    count += 1;
        }
    }
    return count;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 4, 5, 6, 7 };
    int X = 5;
    int n = arr.Length;

    Console.Write(CountSubSet(arr, n, X));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript code to implement the above approach

function CountSubSet(arr, n, X) {
    // N stores total number of subsets
    let N = Math.pow(2, n);
    let count = 0;

    // Generate each subset one by one
    for (let i = 0; i < N; i++) {

        // Check every bit of i
        for (let j = 0; j < n; j++) {

            // if j'th bit of i is set,
            // check arr[j] with X
            if (i & (1 << j))
                if (arr[j] == X)
                    count += 1;
        }
    }
    return count;
}

// Driver code

let arr = [4, 5, 6, 7];
let X = 5;
let n = arr.length;

document.write(CountSubSet(arr, n, X));
</script>
```

**Output:** 

```
8
```

**时间复杂度:** O(n * 2^n).

**高效解决方案:**

*   一个有效的解决方案是利用集合中的每个元素都恰好存在于 2^(n-1 子集的事实。
*   这里，在这个解决方案中，首先，检查给定值 X 是否存在于给定的元素集合中。
*   如果 x 存在，则计算并返回 2^(n-1)，(使用模幂运算计算幂 2^n-1).
*   否则，返回 0。

下面是上述方法的实现。

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate (2^(n-1))
int calculatePower(int b, int e)

{

    // Initially initialize answer to 1
    int ans = 1;

    while (e > 0) {

        // If e is odd,
        // multiply b with answer
        if (e % 2 == 1)
            ans = ans * b;

        e = e / 2;
        b = b * b;
    }
    return ans;
}

// Function to count subsets in which
// X element is present
int CountSubSet(int arr[], int n, int X)
{
    int count = 0, checkX = 0;

    // Check if X is present in
    // given subset or not
    for (int i = 0; i < n; i++) {

        if (arr[i] == X) {
            checkX = 1;
            break;
        }
    }

    // If X is present in set
    // then calculate 2^(n-1) as count
    if (checkX == 1)
        count = calculatePower(2, n - 1);

    // if X is not present in a given set
    else
        count = 0;

    return count;
}

// Driver Function
int main()
{
    int arr[] = { 4, 5, 6, 7 };
    int X = 5;
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << CountSubSet(arr, n, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG
{

    // Function to calculate (2^(n-1))
    static int calculatePower(int b, int e)
    {

        // Initially initialize answer to 1
        int ans = 1;
        while (e > 0)
        {

            // If e is odd,
            // multiply b with answer
            if (e % 2 == 1)
                ans = ans * b;

            e = e / 2;
            b = b * b;
        }
        return ans;
    }

    // Function to count subsets in which
    // X element is present
    static int CountSubSet(int arr[], int n, int X)
    {
        int count = 0, checkX = 0;

        // Check if X is present in
        // given subset or not
        for (int i = 0; i < n; i++)
        {
            if (arr[i] == X)
            {
                checkX = 1;
                break;
            }
        }

        // If X is present in set
        // then calculate 2^(n-1) as count
        if (checkX == 1)
            count = calculatePower(2, n - 1);

        // if X is not present in a given set
        else
            count = 0;

        return count;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 4, 5, 6, 7 };
        int X = 5;
        int n = arr.length;

        System.out.println(CountSubSet(arr, n, X));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to calculate (2^(n-1))
def calculatePower(b, e) :

    # Initially initialize answer to 1
    ans = 1;

    while (e > 0) :

        # If e is odd,
        # multiply b with answer
        if (e % 2 == 1) :
            ans = ans * b;

        e = e // 2;
        b = b * b;

    return ans;

# Function to count subsets in which
# X element is present
def CountSubSet(arr, n, X) :

    count = 0; checkX = 0;

    # Check if X is present in
    # given subset or not
    for i in range(n) :

        if (arr[i] == X) :
            checkX = 1;
            break;

    # If X is present in set
    # then calculate 2^(n-1) as count
    if (checkX == 1) :
        count = calculatePower(2, n - 1);

    # if X is not present in a given set
    else :
        count = 0;

    return count;

# Driver code
if __name__ == "__main__" :

    arr = [ 4, 5, 6, 7 ];
    X = 5;
    n = len(arr);

    print(CountSubSet(arr, n, X));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

    // Function to calculate (2^(n-1))
    static int calculatePower(int b, int e)
    {

        // Initially initialize answer to 1
        int ans = 1;
        while (e > 0)
        {

            // If e is odd,
            // multiply b with answer
            if (e % 2 == 1)
                ans = ans * b;

            e = e / 2;
            b = b * b;
        }
        return ans;
    }

    // Function to count subsets in which
    // X element is present
    static int CountSubSet(int []arr, int n, int X)
    {
        int count = 0, checkX = 0;

        // Check if X is present in
        // given subset or not
        for (int i = 0; i < n; i++)
        {
            if (arr[i] == X)
            {
                checkX = 1;
                break;
            }
        }

        // If X is present in set
        // then calculate 2^(n-1) as count
        if (checkX == 1)
            count = calculatePower(2, n - 1);

        // if X is not present in a given set
        else
            count = 0;

        return count;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 4, 5, 6, 7 };
        int X = 5;
        int n = arr.Length;

        Console.WriteLine(CountSubSet(arr, n, X));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript code to implement the above approach

// Function to calculate (2^(n-1))
function calculatePower(b, e)
{

    // Initially initialize answer to 1
    let ans = 1;
    while (e > 0) {

        // If e is odd,
        // multiply b with answer
        if (e % 2 == 1)
            ans = ans * b;

        e = e / 2;
        b = b * b;
    }
    return ans;
}

// Function to count subsets in which
// X element is present
function CountSubSet(arr, n, X)
{
    let count = 0, checkX = 0;

    // Check if X is present in
    // given subset or not
    for (let i = 0; i < n; i++) {

        if (arr[i] == X) {
            checkX = 1;
            break;
        }
    }

    // If X is present in set
    // then calculate 2^(n-1) as count
    if (checkX == 1)
        count = calculatePower(2, n - 1);

    // if X is not present in a given set
    else
        count = 0;

    return count;
}

// Driver code

let arr = [4, 5, 6, 7];
let X = 5;
let n = arr.length;

document.write(CountSubSet(arr, n, X));

// This code is contributed by shivanisinghss2110
</script>
```

**Output:** 

```
8
```

**时间复杂度:** O(n)