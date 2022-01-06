# 找出一个数组中的元素出现在另一个数组中的频率

> 原文:[https://www . geeksforgeeks . org/find-一个数组的元素出现在另一个数组中的频率/](https://www.geeksforgeeks.org/find-frequencies-of-elements-of-an-array-present-in-another-array/)

给定两个大小分别为 **N** 和 **M** 的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 和 **brr[]** ，任务是在 **arr[]** 中找到阵列**元素的**频率 **brr[]** 。

**示例**:

> **输入** : N = 8，arr[] = {29，8，8，8，7，7，8，7}，M = 3，brr[] = {7，8，29}
> **输出** : {3，4，1}
> **解释**:arr[]
> **输入** : arr[] = N = 6，{4，5，6，5，5，5 3}
> **输出** : {0，0，1}
> **说明**:arr[]中 1，2，3 的频率分别为 0，0，1

**逼近**:将数组**arr【】**元素的**频率**存储在 [hashmap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) 中，就可以轻松解决任务。迭代数组 **brr[]** ，检查 hashmap 中是否有**存在**，并存储相应的频率。
以下是上述方法的实施:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the frequencies of
// elements of brr[] in array arr[]
void solve(int arr[], int brr[], int N, int M)
{

    // Stores the frequency of elements
    // of array arr[]
    unordered_map<int, int> occ;

    for (int i = 0; i < N; i++)
        occ[arr[i]]++;

    // Iterate over brr[]
    for (int i = 0; i < M; i++) {

        // Check if brr[i] is present in
        // occ or not
        if (occ.find(brr[i]) != occ.end()) {
            cout << occ[brr[i]] << " ";
        }
        else {
            cout << 0 << " ";
        }
    }
}

// Driver Code
int main()
{
    int N = 8;
    int arr[N] = { 29, 8, 8, 8, 7, 7, 8, 7 };
    int M = 3;
    int brr[M] = { 7, 8, 29 };

    solve(arr, brr, N, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the frequencies of
// elements of brr[] in array arr[]
static void solve(int arr[], int brr[], int N, int M)
{

    // Stores the frequency of elements
    // of array arr[]
    HashMap<Integer,Integer> occ=new HashMap<Integer,Integer>();

    for (int i = 0; i < N; i++)
    {
        if(occ.containsKey(arr[i])){
            occ.put(arr[i], occ.get(arr[i])+1);
        }
        else{
            occ.put(arr[i], 1);
        }
    }

    // Iterate over brr[]
    for (int i = 0; i < M; i++) {

        // Check if brr[i] is present in
        // occ or not
        if (occ.containsKey(brr[i])) {
            System.out.print(occ.get(brr[i])+ " ");
        }
        else {
            System.out.print(0+ " ");
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 8;
    int arr[] = { 29, 8, 8, 8, 7, 7, 8, 7 };
    int M = 3;
    int brr[] = { 7, 8, 29 };

    solve(arr, brr, N, M);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the frequencies of
# elements of brr[] in array arr[]
def solve(arr, brr, N, M) :

    # Stores the frequency of elements
    # of array arr[]
    occ = dict.fromkeys(arr,0);

    for i in range(N) :
        occ[arr[i]] += 1;

    # Iterate over brr[]
    for i in range(M) :

        # Check if brr[i] is present in
        # occ or not
        if brr[i] in occ :
            print(occ[brr[i]], end= " ");

        else :
            print(0, end = " ");

# Driver Code
if __name__ == "__main__" :

    N = 8;
    arr = [ 29, 8, 8, 8, 7, 7, 8, 7 ];
    M = 3;
    brr = [ 7, 8, 29 ];

    solve(arr, brr, N, M);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find the frequencies of
    // elements of brr[] in array arr[]
    static void solve(int[] arr, int[] brr, int N, int M)
    {

        // Stores the frequency of elements
        // of array arr[]
        Dictionary<int, int> occ = new Dictionary<int, int>();

        for (int i = 0; i < N; i++)
        {
            if (occ.ContainsKey(arr[i]))
            {
                occ[arr[i]] = occ[arr[i]] + 1;
            }
            else
            {
                occ[arr[i]] = 1;
            }
        }

        // Iterate over brr[]
        for (int i = 0; i < M; i++)
        {

            // Check if brr[i] is present in
            // occ or not
            if (occ.ContainsKey(brr[i]))
            {
                Console.Write(occ[brr[i]] + " ");
            }
            else
            {
                Console.Write(0 + " ");
            }
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 8;
        int[] arr = { 29, 8, 8, 8, 7, 7, 8, 7 };
        int M = 3;
        int[] brr = { 7, 8, 29 };

        solve(arr, brr, N, M);
    }
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the frequencies of
// elements of brr[] in array arr[]
function solve(arr, brr, N, M) {

  // Stores the frequency of elements
  // of array arr[]
  let occ = new Map();

  for (let i = 0; i < N; i++) {
    if (occ.has(arr[i])) {
      occ.set(arr[i], occ.get(arr[i]) + 1)
    } else {
      occ.set(arr[i], 1)
    }
  }

  // Iterate over brr[]
  for (let i = 0; i < M; i++) {

    // Check if brr[i] is present in
    // occ or not
    if (occ.has(brr[i])) {
      document.write(occ.get(brr[i]) + " ");
    }
    else {
      document.write(0 + " ");
    }
  }
}

// Driver Code
let N = 8;
let arr = [ 29, 8, 8, 8, 7, 7, 8, 7 ];
let M = 3;
let brr = [ 7, 8, 29 ];

solve(arr, brr, N, M);

// This code is contributed by gfgking.
</script>
```

**Output**

```
3 4 1 
```

***时间复杂度*** : O(N)
***辅助空间*** : O(N)