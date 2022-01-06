# 圆形数组中没有两个元素相邻的最大和|集合 2

> 原文:[https://www . geesforgeks . org/最大循环和数组-这样-没有两个元素是相邻的-set-2/](https://www.geeksforgeeks.org/maximum-sum-in-circular-array-such-that-no-two-elements-are-adjacent-set-2/)

给定一个正数的**数组 arr[]** ，求一个子序列的最大和，约束条件是序列中没有 2 个数字在假设最后一个和第一个元素相邻的数组中是相邻的。
**例:**

> **输入:** arr[] = {3，5，3}
> **输出:** 5
> **解释:**
> 我们不能取第一个和最后一个元素，因为它们被认为是相邻的，因此输出为 5。
> **输入** arr[] = {1，223，41，4，414，5，16}
> **输出:** 653
> **解释:**
> 取指数 1，4，6 的元素，我们得到最大和为 653。

**方法:**思路是用[记忆算法](https://www.geeksforgeeks.org/tabulation-vs-memoization/)解决上面提到的问题。最重要的观察是**第一个和最后一个元素永远不能一起选择**。所以，我们可以把问题分成两部分:

*   从索引 **0 到数组大小的最大和–2**
*   从索引 **1 到数组大小的最大和–1**

答案将是这两个和的最大值，可以使用 [**【动态规划】**](https://www.geeksforgeeks.org/dynamic-programming/) 求解。
**以下是上述方法的实施:**

## C++

```
// C++ program to find maximum sum
// in circular array such that
// no two elements are adjacent

#include <bits/stdc++.h>
using namespace std;

// Store the maximum possible at each index
vector<int> dp;

int maxSum(int i, vector<int>& subarr)
{

    // When i exceeds the index of the
    // last element simply return 0
    if (i >= subarr.size())
        return 0;

    // If the value has already been calculated,
    // directly return it from the dp array
    if (dp[i] != -1)
        return dp[i];

    // The next states are don't take
    // this element and go to (i + 1)th state
    // else take this element
    // and go to (i + 2)th state
    return dp[i]
           = max(maxSum(i + 1, subarr),
                 subarr[i]
                     + maxSum(i + 2, subarr));
}

// function to find the max value
int Func(vector<int> arr)
{
    vector<int> subarr = arr;

    // subarr contains elements
    // from 0 to arr.size() - 2
    subarr.pop_back();

    // Initializing all the values with -1
    dp.resize(subarr.size(), -1);

    // Calculating maximum possible
    // sum for first case
    int max1 = maxSum(0, subarr);

    subarr = arr;

    // subarr contains elements
    // from 1 to arr.size() - 1
    subarr.erase(subarr.begin());

    dp.clear();

    // Re-initializing all values with -1
    dp.resize(subarr.size(), -1);

    // Calculating maximum possible
    // sum for second case
    int max2 = maxSum(0, subarr);

    // Printing the maximum between them
    cout << max(max1, max2) << endl;
}

// Driver code
int main()
{

    vector<int> arr = { 1, 2, 3, 1 };

    Func(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum sum
// in circular array such that
// no two elements are adjacent
import java.util.*;
class GFG{

// Store the maximum
// possible at each index
static Vector<Integer> dp =
              new Vector<>();

static int maxSum(int i,
                  Vector<Integer> subarr)
{
  // When i exceeds the index of the
  // last element simply return 0
  if (i >= subarr.size())
    return 0;

  // If the value has already
  // been calculated, directly
  // return it from the dp array
  if (dp.get(i) != -1)
    return dp.get(i);

  // The next states are don't take
  // this element and go to (i + 1)th state
  // else take this element
  // and go to (i + 2)th state
  dp.add(i, Math.max(maxSum(i + 1, subarr),
                     subarr.get(i) +
                     maxSum(i + 2, subarr)));
  return dp.get(i);
}

// function to find the max value
static void Func(Vector<Integer> arr)
{
  Vector<Integer> subarr =
         new Vector<>();
  subarr.addAll(arr);

  // subarr contains elements
  // from 0 to arr.size() - 2
  subarr.remove(subarr.size() - 1);

  // Initializing all the values with -1
  dp.setSize(subarr.size());
  Collections.fill(dp, -1);

  // Calculating maximum possible
  // sum for first case
  int max1 = maxSum(0, subarr);

  subarr = arr;

  // subarr contains elements
  // from 1 to arr.size() - 1
  subarr.remove(0);

  dp.clear();

  // Re-initializing all values with -1
  dp.setSize(subarr.size());
  Collections.fill(dp, -1);

  // Calculating maximum possible
  // sum for second case
  int max2 = maxSum(0, subarr);

  // Printing the maximum between them
  System.out.print(Math.max(max1, max2) + "\n");
}

// Driver code
public static void main(String[] args)
{
  Vector<Integer> arr =new Vector<>();
  arr.add(1);
  arr.add(2);
  arr.add(3);
  arr.add(1);
  Func(arr);
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to find maximum sum
# in circular array such that
# no two elements are adjacent

# Store the maximum possible at each index
dp = []

def maxSum(i, subarr):

    # When i exceeds the index of the
    # last element simply return 0
    if (i >= len(subarr)):
        return 0

    # If the value has already been
    # calculated, directly return
    # it from the dp array
    if (dp[i] != -1):
        return dp[i]

    # The next states are don't take
    # this element and go to (i + 1)th state
    # else take this element
    # and go to (i + 2)th state
    dp[i] = max(maxSum(i + 1, subarr),
                subarr[i] +
                maxSum(i + 2, subarr))
    return dp[i]

# function to find the max value
def Func(arr):
    subarr = arr

    # subarr contains elements
    # from 0 to arr.size() - 2
    subarr.pop()
    global dp

    # Initializing all the values with -1
    dp= [-1] * (len(subarr))

    # Calculating maximum possible
    # sum for first case
    max1 = maxSum(0, subarr)

    subarr = arr

    # subarr contains elements
    # from 1 to arr.size() - 1
    subarr = subarr[:]

    del dp

    # Re-initializing all values with -1
    dp = [-1] * (len(subarr))

    # Calculating maximum possible
    # sum for second case
    max2 = maxSum(0, subarr)

    # Printing the maximum between them
    print(max(max1, max2))

# Driver code
if __name__ == "__main__":
    arr = [1, 2, 3, 1]
    Func(arr)

# This code is contributed by Chitranayal
```

## java 描述语言

```
<script>
// Javascript program to find maximum sum
// in circular array such that
// no two elements are adjacent

// Store the maximum
// possible at each index
let dp =[];
function  maxSum(i,subarr)
{
    // When i exceeds the index of the
  // last element simply return 0
  if (i >= subarr.length)
    return 0;

  // If the value has already
  // been calculated, directly
  // return it from the dp array
  if (dp[i] != -1)
    return dp[i];

  // The next states are don't take
  // this element and go to (i + 1)th state
  // else take this element
  // and go to (i + 2)th state
  dp[i] = Math.max(maxSum(i + 1, subarr),
                     subarr[i] +
                     maxSum(i + 2, subarr));
  return dp[i];
}

// function to find the max value
function Func(arr)
{
    let subarr =arr;

  // subarr contains elements
  // from 0 to arr.size() - 2
  subarr.pop();

  // Initializing all the values with -1
  dp=new Array(subarr.length);
  for(let i=0;i<subarr.length;i++)
  {
      dp[i]=-1;
  }

  // Calculating maximum possible
  // sum for first case
  let max1 = maxSum(0, subarr);

  subarr = arr;

  // subarr contains elements
  // from 1 to arr.size() - 1
  subarr.shift();

  dp=[];

  // Re-initializing all values with -1
  dp=new Array(subarr.length);
  for(let i=0;i<dp.length;i++)
  {
      dp[i]=-1;
  }

  // Calculating maximum possible
  // sum for second case
  let max2 = maxSum(0, subarr);

  // Printing the maximum between them
  document.write(Math.max(max1, max2) + "<br>");
}

// Driver code

let arr=[1,2,3,1];
  Func(arr);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)*
***辅助空间复杂度:** O(N)*
**类似冠词:** [圆形数组中的最大和使得没有两个元素相邻](https://www.geeksforgeeks.org/maximum-sum-in-circular-array-such-that-no-two-elements-are-adjacent/)