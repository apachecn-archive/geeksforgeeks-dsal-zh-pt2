# 最大化数组中所选数字的总和，使其为空

> 原文:[https://www . geesforgeks . org/maximum-sum-selected-numbers-performance-follow-operation/](https://www.geeksforgeeks.org/maximize-sum-selected-numbers-performing-following-operation/)

给定一个 N 个数字的数组，我们需要最大化所选数字的总和。在每一步，你需要选择一个数字 A <sub>i</sub> ，删除其中的一个出现，并删除数组中所有出现的 **A <sub>i</sub> -1** 和 **A <sub>i</sub> +1** (如果存在的话)。重复这些步骤，直到数组变空。问题是最大化所选数字的总和。
**注意:**如果数组中存在 A <sub>i</sub> +1 和 A <sub>i</sub> -1 元素，而不是 A <sub>i+1</sub> 和 A <sub>i-1</sub> ，我们必须删除所有出现的 A<sub>I</sub>+1 和 A<sub>I</sub>-1 元素。
**例:**

```
Input : a[] = {1, 2, 3} 
Output : 4
Explanation: At first step we select 1, so 1 and 
2 are deleted from the sequence leaving us with 3\. 
Then we select 3 from the sequence and delete it.
So the sum of selected numbers is 1+3 = 4\. 

Input : a[] =  {1, 2, 2, 2, 3, 4}
Output : 10 
Explanation : Select one of the 2's from the array, so 
2, 2-1, 2+1 will be deleted and we are left with {2, 2, 4}, 
since 1 and 3 are deleted. Select 2 in next two steps, 
and then select 4 in the last step.
We get a sum of 2+2+2+4=10 which is the maximum possible. 
```

我们的目标是最大化所选数字的总和。其思想是预先计算数组 a[]中所有数字 x 的出现次数。

**进场:**

*   计算数组中的最大值。
*   创建一个最大大小的数组，并在其中存储每个元素的出现次数。
*   因为我们想最大化我们的答案，我们将开始从最大值迭代到 0。
*   如果第 I<sup>元素的出现次数大于 0，那么将其添加到我们的答案中，将第 i-1 <sup>元素的出现次数减少 1，并且还将第 i <sup>元素的出现次数减少 1，因为我们已经将其添加到我们的答案中。</sup></sup></sup>
*   我们不必减少第 i+1 <sup>个</sup>元素的出现，因为我们已经从末尾开始了，所以第 i+1 <sup>个</sup>已经被处理了。
*   i <sup>第</sup>元素可能会多次出现，这就是为什么不减少 I，保持在同一个元素上。

以下是上述思路的实现:

## C++

```
// CPP program to Maximize the sum of selected
// numbers by deleting three consecutive numbers.
#include <bits/stdc++.h>
using namespace std;

// function to maximize the sum of selected numbers
int maximizeSum(int arr[], int n) {

      // Largest element in the array
    int mx = -1;
    for(int i = 0; i < n; i++)
    {
        mx = max(mx, arr[i]);
    }   

    // An array to count the occurence of each element
    int freq[mx + 1];

    memset(freq, 0, sizeof(freq));

    for(int i = 0; i < n; i++)
    {
        freq[arr[i]]++;
    }

    // ans to store the result
    int ans = 0, i=mx;

    // Using the above mentioned approach
    while(i>0){

        // if occurence is greater than 0
        if(freq[i] > 0){
            // add it to ans
            ans += i;

            // decrease i-1th element by 1
            freq[i-1]--;

            // decrease ith element by 1
            freq[i]--;
        }else{
            // decrease i
            i--;
        }       
    }

    return ans;
}

// Driver code
int main()
{
  int a[] = {1, 2, 3};
  int n = sizeof(a) / sizeof(a[0]);
  cout << maximizeSum(a, n);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.math.*;

class GFG
{
      // Function to maximise the sum of selected numbers
      //by deleting occurences of Ai-1 and Ai+1
    public static int getMaximumSum (int arr[]) {

        // Number of elements in the array
        int n = arr.length;

        // Largest element in the array
        int max = -1;
        for(int i = 0; i < n; i++)
        {
            max = Math.max(max, arr[i]);
        }

        // An array to count the occurence of each element
        int []freq = new int[max + 1];

        for(int i = 0; i < n; i++)
        {
            freq[arr[i]]++;
        }

        // ans to store the result
        int ans = 0, i=max;

        // Using the above mentioned approach
        while(i>0){

            // if occurence is greater than 0
            if(freq[i] > 0){
                // add it to ans
                ans += i;

                // decrease i-1th element by 1
                freq[i-1]--;

                // decrease ith element by 1
                freq[i]--;
            }else{               
                // decrease i
                i--;
            }           
        }

        return ans;
    }

      // Driver code
      public static void main(String[] args)
      {
          int []a = {1, 2, 3};

          System.out.println(getMaximumSum(a));
      }
}
```

## 蟒蛇 3

```
# Python3 program to Maximize the sum of selected
# numbers by deleting three consecutive numbers.

# function to maximize the sum of
# selected numbers
def maximizeSum(a, n) :

        # maximum in the sequence
    maximum = max(a)

    # stores the occurrences of the numbers
    ans = dict.fromkeys(range(0, n + 1), 0)

    # marks the occurrence of every
    # number in the sequence
    for i in range(n) :
        ans[a[i]] += 1

    # ans to store the result
    result = 0
    i = maximum

    # Using the above mentioned approach
    while i > 0:

        # if occurence is greater than 0
        if ans[i] > 0:
            # add it to ans
            result += i;

            # decrease i-1th element by 1
            ans[i-1] -= 1;

            # decrease ith element by 1
            ans[i] -= 1;
        else:          
            # decrease i
            i -= 1;

    return result;

# Driver code
if __name__ == "__main__" :

    a = [1, 2, 3]
    n = len(a)
    print(maximizeSum(a, n))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;

class GFG
{

// Function to maximise the sum of selected numbers
//by deleting occurences of Ai-1 and Ai+1
static int getMaximumSum(int []arr)
{
    // Number of elements in the array
    int n = arr.Length;

    // Largest element in the array
    int max = arr.Max();

    // An array to count the occurence of each element
    int []freq = new int[max + 1];

    for(int j = 0; j < n; j++)
    {
      freq[arr[j]]++;
    }

    // ans to store the result
    int ans = 0, i=max;

    // Using the above mentioned approach
    while(i>0){

      // if occurence is greater than 0
      if(freq[i] > 0){
        // add it to ans
        ans += i;

        // decrease i-1th element by 1
        freq[i-1]--;

        // decrease ith element by 1
        freq[i]--;
      }else{               
        // decrease i
        i--;
      }           
    }

    return ans;
}

// Driver code
public static void Main(string[] args)
{
    int []a = {1, 2, 3};

    Console.Write(getMaximumSum(a));
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to maximise the sum of selected numbers
    //by deleting occurences of Ai-1 and Ai+1
    function getMaximumSum(arr)
    {
        // Number of elements in the array
        let n = arr.length;

        // Largest element in the array
        let max = Number.MIN_VALUE;
        for(let i = 0; i < n; i++)
        {
            max = Math.max(max, arr[i]);
        }

        // An array to count the occurence of each element
        let freq = new Array(max + 1);
        freq.fill(0);

        for(let j = 0; j < n; j++)
        {
          freq[arr[j]]++;
        }

        // ans to store the result
        let ans = 0, i=max;

        // Using the above mentioned approach
        while(i>0){

          // if occurence is greater than 0
          if(freq[i] > 0){
            // add it to ans
            ans += i;

            // decrease i-1th element by 1
            freq[i-1]--;

            // decrease ith element by 1
            freq[i]--;
          }else{              
            // decrease i
            i--;
          }          
        }

        return ans;
    }

    let a = [1, 2, 3];

    document.write(getMaximumSum(a));

    // This code is contributed by suresh07.
</script>
```

**输出:**

```
4
```

**时间复杂度:**时间复杂度将是(A<sub>max</sub>+<sub>T5【arr 中元素的最高出现次数】的总和，因为如果频率大于 1，那么我们将多次处理该元素。</sub>

-其中 A <sub>max</sub> 是数组 A[]中存在的最大元素。

**空间复杂度:** O(A <sub>max</sub> ，其中 A <sub>max</sub> 是数组 A[]中存在的最大元素。