# 在大小为 N 的排列中，元素与其各自位置的按位异或的最大和

> 原文:[https://www . geeksforgeeks . org/元素的最大按位异或与它们各自的大小排列位置 n/](https://www.geeksforgeeks.org/maximum-sum-of-bitwise-xor-of-elements-with-their-respective-positions-in-a-permutation-of-size-n/)

给定一个正整数 **N** ，任何大小为 **N** 的排列，只要元素在范围**【0，N–1】**内，其任务就是计算所有元素与其各自位置的 [**【按位异或】**](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 之和。

> **例如:**对于排列{3，4，2，1，0}，**总和= (0^3 + 1^4 + 2^2 + 3^1 + 4^0) = 2** 。

**示例:**

> **输入:** N = 3
> **输出:** 6
> **解释:**对于排列 **{1，2，0}** 和 **{2，0，1}** ，和为 **6** 。
> 
> **输入:**N = 2
> T3】输出: 2

**方法:**解决这个问题，思路是[递归](https://www.geeksforgeeks.org/recursion/)到[生成整数**【0，N–1】**的所有可能的排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)，计算每一个排列的得分，然后在所有形成的排列中找到最大得分。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to calculate the score
int calcScr(vector<int>arr){

  // Stores the possible score for
  // the current permutation
  int ans = 0;

  // Traverse the permutation array
  for(int i = 0; i < arr.size(); i++)
    ans += (i ^ arr[i]);

  // Return the final score
  return ans;
}

// Function to generate all the possible
// permutation and get the max score
int getMax(vector<int> arr, int ans, vector<bool> chosen, int N)
{

  // If arr[] length is equal to N
  // process the permutation
  if (arr.size() == N){
    ans = max(ans, calcScr(arr));
    return ans;

  }

  // Generating the permutations
  for (int i = 0; i < N; i++)
  {

    // If the current element is
    // chosen
    if(chosen[i])
      continue;

    // Mark the current element
    // as true
    chosen[i] = true;
    arr.push_back(i);

    // Recursively call for next
    // possible permutation
    ans = getMax(arr, ans, chosen, N);

    // Backtracking
    chosen[i] = false;
    arr.pop_back();
  }

  // Return the ans
  return ans;
}

// Driver Code
int main()
{

  int N = 2;

  // Stores the permutation
  vector<int> arr;

  // To display the result
  int ans = -1;
  vector<bool>chosen(N,false);
  ans = getMax(arr, ans, chosen, N);

  cout << ans << endl;
}

// This code is contributed by bgangwar59.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to calculate the score
static int calcScr(ArrayList<Integer>arr)
{

  // Stores the possible score for
  // the current permutation
  int ans = 0;

  // Traverse the permutation array
  for(int i = 0; i < arr.size(); i++)
    ans += (i ^ arr.get(i));

  // Return the final score
  return ans;
}

// Function to generate all the possible
// permutation and get the max score
static int getMax(ArrayList<Integer> arr, int ans, ArrayList<Boolean> chosen, int N)
{

  // If arr[] length is equal to N
  // process the permutation
  if (arr.size() == N)
  {
    ans = Math.max(ans, calcScr(arr));
    return ans;

  }

  // Generating the permutations
  for (int i = 0; i < N; i++)
  {

    // If the current element is
    // chosen
    if(chosen.get(i))
      continue;

    // Mark the current element
    // as true
    chosen.set(i, true);
    arr.add(i);

    // Recursively call for next
    // possible permutation
    ans = getMax(arr, ans, chosen, N);

    // Backtracking
    chosen.set(i, false);
    arr.remove(arr.size()-1);
  }

  // Return the ans
  return ans;
}

// Driver Code
public static void main(String[] args)
{

  int N = 2;

  // Stores the permutation
  ArrayList<Integer> arr = new ArrayList<Integer>();

  // To display the result
  int ans = -1;
  ArrayList<Boolean> chosen = new ArrayList<Boolean>(Collections.nCopies(N, false));
  ans = getMax(arr, ans, chosen, N);

  System.out.print(ans +"\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to generate all the possible
# permutation and get the max score
def getMax(arr, ans, chosen, N):

    # If arr[] length is equal to N
    # process the permutation
    if len(arr) == N:
        ans = max(ans, calcScr(arr))
        return ans

    # Generating the permutations
    for i in range(N):

        # If the current element is
        # chosen
        if chosen[i]:
            continue

        # Mark the current element
        # as true
        chosen[i] = True
        arr.append(i)

        # Recursively call for next
        # possible permutation
        ans = getMax(arr, ans, chosen, N)

        # Backtracking
        chosen[i] = False
        arr.pop()

    # Return the ans
    return ans

# Function to calculate the score
def calcScr(arr):

    # Stores the possible score for
    # the current permutation
    ans = 0

    # Traverse the permutation array
    for i in range(len(arr)):
        ans += (i ^ arr[i])

    # Return the final score
    return ans

# Driver Code
N = 2

# Stores the permutation
arr = []

# To display the result
ans = -1

chosen = [False for i in range(N)]

ans = getMax(arr, ans, chosen, N)

print(ans)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG
{

  // Function to calculate the score
  static int calcScr(List<int>arr)
  {

    // Stores the possible score for
    // the current permutation
    int ans = 0;

    // Traverse the permutation array
    for(int i = 0; i < arr.Count; i++)
      ans += (i ^ arr[i]);

    // Return the readonly score
    return ans;
  }

  // Function to generate all the possible
  // permutation and get the max score
  static int getMax(List<int> arr, int ans, List<Boolean> chosen, int N)
  {

    // If []arr length is equal to N
    // process the permutation
    if (arr.Count == N)
    {
      ans = Math.Max(ans, calcScr(arr));
      return ans;

    }

    // Generating the permutations
    for (int i = 0; i < N; i++)
    {

      // If the current element is
      // chosen
      if(chosen[i])
        continue;

      // Mark the current element
      // as true
      chosen[i] = true;
      arr.Add(i);

      // Recursively call for next
      // possible permutation
      ans = getMax(arr, ans, chosen, N);

      // Backtracking
      chosen[i] = false;
      arr.Remove(arr.Count-1);
    }

    // Return the ans
    return ans;
  }

  // Driver Code
  public static void Main(String[] args)
  {

    int N = 2;

    // Stores the permutation
    List<int> arr = new List<int>();

    // To display the result
    int ans = -1;
    List<bool> chosen = new List<bool>(N);
    for(int i = 0; i < N; i++)
      chosen.Add(false);
    ans = getMax(arr, ans, chosen, N);

    Console.Write(ans +"\n");
  }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to calculate the score
function calcScr(arr) {

    // Stores the possible score for
    // the current permutation
    let ans = 0;

    // Traverse the permutation array
    for (let i = 0; i < arr.length; i++)
        ans += (i ^ arr[i]);

    // Return the final score
    return ans;
}

// Function to generate all the possible
// permutation and get the max score
function getMax(arr, ans, chosen, N) {

    // If arr[] length is equal to N
    // process the permutation
    if (arr.length == N) {
        ans = Math.max(ans, calcScr(arr));
        return ans;

    }

    // Generating the permutations
    for (let i = 0; i < N; i++) {

        // If the current element is
        // chosen
        if (chosen[i])
            continue;

        // Mark the current element
        // as true
        chosen[i] = true;
        arr.push(i);

        // Recursively call for next
        // possible permutation
        ans = getMax(arr, ans, chosen, N);

        // Backtracking
        chosen[i] = false;
        arr.pop();
    }

    // Return the ans
    return ans;
}

// Driver Code

let N = 2;

// Stores the permutation
let arr = [];

// To display the result
let ans = -1;
let chosen = new Array(N).fill(false);
ans = getMax(arr, ans, chosen, N);

document.write(ans + "<br>");

// This code is contributed by gfgking

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N*N！)*
***辅助空间:** O(N)*