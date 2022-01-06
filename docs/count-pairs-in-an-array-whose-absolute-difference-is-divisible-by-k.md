# 对绝对差可被 K 整除的数组中的对进行计数

> 原文:[https://www . geesforgeks . org/count-pairs-in-a-array-其绝对差可被 k 整除/](https://www.geeksforgeeks.org/count-pairs-in-an-array-whose-absolute-difference-is-divisible-by-k/)

给定一个数组 **arr[]** 和一个正整数 **K** 。任务是统计数组中绝对差可被 k 整除的对的总数。

**示例:**

> **输入:** arr[] = {1，2，3，4}，K = 2
> **输出:** 2
> **解释:**
> 数组中总共存在 2 对，绝对差可被 2 整除。
> 配对为:(1，3)、(2，4)。
> 
> **输入:** arr[] = {3，3，3}，K = 3
> **输出:** 3
> **说明:**
> 这个数组总共有 3 对，绝对差可被 3 整除。
> 配对为:(3，3)，(3，3)，(3，3)。

**天真方法:**想法是逐个检查数组中的每一对，统计绝对差可被 k 整除的对的总数。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// function to count pairs in an array
// whose absolute difference is
// divisible by k
void countPairs(int arr[], int n, int k)
{

    // initialize count as zero.
    int i, j, cnt = 0;

    // loop to count the valid pair
    for (i = 0; i < n - 1; i++) {
        for (j = i + 1; j < n; j++) {
            if ((arr[i] - arr[j] + k) % k == 0)
                cnt += 1;
        }
    }
    cout << cnt << endl;
}

// Driver code
int main()
{
    // input array
    int arr[] = {3, 3, 3};
    int k = 3;

    // calculate the size of array
    int n = sizeof(arr) / sizeof(arr[0]);

    // function to count the valid pair
    countPairs(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG
{

// function to count pairs in an array
// whose absolute difference is
// divisible by k
static void countPairs(int arr[], int n, int k)
{

    // initialize count as zero.
    int i, j, cnt = 0;

    // loop to count the valid pair
    for (i = 0; i < n - 1; i++)
    {
        for (j = i + 1; j < n; j++)
        {
            if ((arr[i] - arr[j] + k) % k == 0)
                cnt += 1;
        }
    }
    System.out.print(cnt +"\n");
}

// Driver code
public static void main(String[] args)
{
    // input array
    int arr[] = {3, 3, 3};
    int k = 3;

    // calculate the size of array
    int n = arr.length;

    // function to count the valid pair
    countPairs(arr, n, k);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 Code implementation of the above approach

# function to count pairs in an array
# whose absolute difference is
# divisible by k
def countPairs(arr, n, k) :

    # initialize count as zero.
    cnt = 0;

    # loop to count the valid pair
    for i in range(n - 1) :
        for j in range(i + 1, n) :
            if ((arr[i] - arr[j] + k) % k == 0) :
                cnt += 1;

    print(cnt) ;

# Driver code
if __name__ == "__main__" :

    # input array
    arr = [3, 3, 3];
    k = 3;

    # calculate the size of array
    n = len(arr);

    # function to count the valid pair
    countPairs(arr, n, k);

# This code is contributed by AnkitRai01
```

## C#

```
using System;

class GFG
{

// function to count pairs in an array
// whose absolute difference is
// divisible by k
static void countPairs(int []arr, int n, int k)
{

    // initialize count as zero.
    int i, j, cnt = 0;

    // loop to count the valid pair
    for (i = 0; i < n - 1; i++)
    {
        for (j = i + 1; j < n; j++)
        {
            if ((arr[i] - arr[j] + k) % k == 0)
                cnt += 1;
        }
    }
    Console.Write(cnt +"\n");
}

// Driver code
public static void Main(String[] args)
{
    // input array
    int []arr = {3, 3, 3};
    int k = 3;

    // calculate the size of array
    int n = arr.Length;

    // function to count the valid pair
    countPairs(arr, n, k);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Function to count pairs in an array
// whose absolute difference is
// divisible by k
function countPairs(arr, n, k)
{

    // Initialize count as zero.
    var i, j, cnt = 0;

    // Loop to count the valid pair
    for(i = 0; i < n - 1; i++)
    {
        for(j = i + 1; j < n; j++)
        {
            if ((arr[i] - arr[j] + k) % k == 0)
                cnt += 1;
        }
    }
    document.write(cnt + "\n");
}

// Driver code

// Input array
var arr = [ 3, 3, 3 ];
var k = 3;

// Calculate the size of array
var n = arr.length;

// Function to count the valid pair
countPairs(arr, n, k);

// This code is contributed by umadevi9616

</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(**N<sup>2</sup>T5)
T7】空间复杂度:** O(1)

**有效方法:**

> **算法:**
> 
> 1.  将数组的每个元素(A[i])转换为((A[i]+K)%K)
> 2.  使用散列技术存储数组中出现的次数
> 3.  现在，如果一个元素 A[i]在数组中出现 x 次，那么在计数对中添加 x*(x-1)/2(从 **x** 元素中选择任意 **2** 元素)，其中 1 < =i < =n。这是因为数组中每个元素的值位于 **0** 到 **K-1** 之间，所以只有当一对元素的值相等时，绝对差才是可分的

## C++

```
// Write CPP code here
#include <bits/stdc++.h>
using namespace std;

// function to Count pairs in an array whose
// absolute difference is divisible by k
void countPair(int arr[], int n, int k)
{

    // initialize the count
    int cnt = 0;

    // making every element of arr in
    // range 0 to k - 1
    for (int i = 0; i < n; i++) {
        arr[i] = (arr[i] + k) % k;
    }

    // create an array hash[]
    int hash[k] = { 0 };

    // store to count of element of arr
    // in hash[]
    for (int i = 0; i < n; i++) {
        hash[arr[i]]++;
    }

    // count the pair whose absolute
    // difference is divisible by k
    for (int i = 0; i < k; i++) {
        cnt += (hash[i] * (hash[i] - 1)) / 2;
    }

    // print the value of count
    cout << cnt << endl;
}

// Driver Code
int main()
{
    // input array
    int arr[] = {1, 2, 3, 4};
    int k = 2;

    // calculate the size of array
    int n = sizeof(arr) / sizeof(arr[0]);
    countPair(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Implementation of above approach
import java.util.*;

class GFG
{

// function to Count pairs in an array whose
// absolute difference is divisible by k
static void countPair(int arr[], int n, int k)
{

    // initialize the count
    int cnt = 0;

    // making every element of arr in
    // range 0 to k - 1
    for (int i = 0; i < n; i++)
    {
        arr[i] = (arr[i] + k) % k;
    }

    // create an array hash[]
    int hash[] = new int[k];

    // store to count of element of arr
    // in hash[]
    for (int i = 0; i < n; i++)
    {
        hash[arr[i]]++;
    }

    // count the pair whose absolute
    // difference is divisible by k
    for (int i = 0; i < k; i++)
    {
        cnt += (hash[i] * (hash[i] - 1)) / 2;
    }

    // print the value of count
    System.out.print(cnt +"\n");
}

// Driver Code
public static void main(String[] args)
{
    // input array
    int arr[] = {1, 2, 3, 4};
    int k = 2;

    // calculate the size of array
    int n = arr.length;
    countPair(arr, n, k);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 Implementation of above approach

# function to Count pairs in an array whose
# absolute difference is divisible by k
def countPair(arr, n, k):

    # initialize the count
    cnt = 0;

    # making every element of arr in
    # range 0 to k - 1
    for i in range(n):
        arr[i] = (arr[i] + k) % k;

    # create an array hash
    hash = [0]*k;

    # store to count of element of arr
    # in hash
    for i in range(n):
        hash[arr[i]] += 1;

    # count the pair whose absolute
    # difference is divisible by k
    for i in range(k):
        cnt += (hash[i] * (hash[i] - 1)) / 2;

    # print value of count
    print(int(cnt));

# Driver Code
if __name__ == '__main__':

    # input array
    arr = [1, 2, 3, 4];
    k = 2;

    # calculate the size of array
    n = len(arr);
    countPair(arr, n, k);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# Implementation of above approach
using System;

class GFG
{

// function to Count pairs in an array whose
// absolute difference is divisible by k
static void countPair(int []arr, int n, int k)
{

    // initialize the count
    int cnt = 0;

    // making every element of arr in
    // range 0 to k - 1
    for (int i = 0; i < n; i++)
    {
        arr[i] = (arr[i] + k) % k;
    }

    // create an array hash[]
    int []hash = new int[k];

    // store to count of element of arr
    // in hash[]
    for (int i = 0; i < n; i++)
    {
        hash[arr[i]]++;
    }

    // count the pair whose absolute
    // difference is divisible by k
    for (int i = 0; i < k; i++)
    {
        cnt += (hash[i] * (hash[i] - 1)) / 2;
    }

    // print the value of count
    Console.Write(cnt +"\n");
}

// Driver Code
public static void Main(String[] args)
{
    // input array
    int []arr = {1, 2, 3, 4};
    int k = 2;

    // calculate the size of array
    int n = arr.Length;
    countPair(arr, n, k);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript Implementation of above approach

// function to Count pairs in an array whose
// absolute difference is divisible by k
function countPair(arr, n, k)
{
    // let initialize the count
    let cnt = 0;

    // making every element of arr in
    // range 0 to k - 1
    for (let i = 0; i < n; i++)
    {
        arr[i] = (arr[i] + k) % k;
    }

    // create an array hash[]
    let hash =  Array.from({length: k}, (_, i) => 0);

    // store to count of element of arr
    // in hash[]
    for (let i = 0; i < n; i++)
    {
        hash[arr[i]]++;
    }

    // count the pair whose absolute
    // difference is divisible by k
    for (let i = 0; i < k; i++)
    {
        cnt += (hash[i] * (hash[i] - 1)) / 2;
    }

    // prlet the value of count
    document.write(cnt +"<br/>");
}

// Driver code

      // input array
    let arr = [1, 2, 3, 4];
    let k = 2;

    // calculate the size of array
    let n = arr.length;
    countPair(arr, n, k);

</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(**n+k**)
T5】辅助空间: O( **k** )