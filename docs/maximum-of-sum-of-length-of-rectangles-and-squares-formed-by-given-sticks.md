# 给定棒条形成的矩形和正方形长度之和的最大值

> 原文:[https://www . geeksforgeeks . org/给定棒形成的矩形和正方形的最大长度之和/](https://www.geeksforgeeks.org/maximum-of-sum-of-length-of-rectangles-and-squares-formed-by-given-sticks/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，代表棒的长度，任务是找到使用这些棒构造的正方形和矩形的所有长度的最大可能和。
***注**单个面可以只用一根棍子来表示。*

**示例:**

> **输入:** arr[] = {5，3，2，3，6，3，3}
> **输出:** 12
> 方块长度之和= 3 * 4 = 12
> 矩形长度之和= 0
> **输入:** arr[] = {5，3，2，3，6，4，4，5，5，5 }
> **输出:** 34
> 方块长度之和= 0

**方法:**按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)统计所有数组元素的[频率，比如**频率**。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   计数至少为 **2** 的频率。
*   将频率转换为最近的较小偶数值。
*   按降序将频率转换为一维数组。
*   现在，将元素求和到 4 的倍数。
*   打印所有这些元素的总和

下面是上述方法的实现:

## C++14

```
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum of sum
// of lengths of rectangles and squares
// formed using given set of sticks
void findSumLength(vector<int> arr,int n)
{

    // Stores the count of frequencies
    // of all the array elements
    map<int,int> freq;
    for(int i:arr) freq[i] += 1;

    // Stores frequencies which are at least 2
    map<int,int> freq_2;

    for (auto i:freq)
    {
        if (freq[i.first] >= 2)
            freq_2[i.first] = freq[i.first];
    }

    // Convert all frequencies to nearest
    // smaller even values.
    vector<int> arr1;
    for (auto i:freq_2)
        arr1.push_back((i.first) * (freq_2[(i.first)]/2)*2);
    sort(arr1.begin(), arr1.end());

    // Sum of elements up to
    // index of multiples of 4
    int summ = 0;
    for (int i:arr1)
        summ += i;

    // Print the sum
    cout << summ;
}

// Driver Code
int main()
{
  vector<int> arr = {5, 3, 2, 3, 6, 4, 4, 4, 5, 5, 5};
  int n = arr.size();
  findSumLength(arr, n);
  return 0;
}

// This code is contributed by mohit kumar 29.
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach 

from collections import Counter

# Function to find the maximum of sum
# of lengths of rectangles and squares
# formed using given set of sticks
def findSumLength(arr, n) : 

    # Stores the count of frequencies
    # of all the array elements
    freq = dict(Counter(arr))

    # Stores frequencies which are at least 2
    freq_2 = {}

    for i in freq:
        if freq[i]>= 2:
            freq_2[i] = freq[i]

    # Convert all frequencies to nearest
    # smaller even values.
    arr1 = []
    for i in freq_2:
      arr1.extend([i]*(freq_2[i]//2)*2)

    # Sort the array in descending order
    arr1.sort(reverse = True)

    # Sum of elements up to
    # index of multiples of 4
    summ = 0
    for i in range((len(arr1)//4)*4):
        summ+= arr1[i]

    # Print the sum
    print(summ)

# Driver Code 
if __name__ == "__main__" : 

    arr = [5, 3, 2, 3, 6, 4, 4, 4, 5, 5, 5]; 
    n = len(arr); 
    findSumLength(arr, n);
```

## C#

```
using System;
using System.Collections.Generic;
class GFG{

  // Function to find the maximum of sum
  // of lengths of rectangles and squares
  // formed using given set of sticks
  static void findSumLength(List<int> arr, int n)
  {

    // Stores the count of frequencies
    // of all the array elements
    Dictionary<int,int> freq = new Dictionary<int,int>();
    foreach (int i in arr){
      if(freq.ContainsKey(i))
        freq[i] += 1;
      else
        freq[i] = 1;
    }

    // Stores frequencies which are at least 2
    Dictionary<int,int> freq_2 = new Dictionary<int,int>();
    foreach(KeyValuePair<int, int> entry in freq)
    {
      if (freq[entry.Key] >= 2)
        freq_2[entry.Key] = freq[entry.Key];
    }

    // Convert all frequencies to nearest
    // smaller even values.
    List<int> arr1 = new List<int>();
    foreach(KeyValuePair<int, int> entry in freq_2)
      arr1.Add(entry.Key * (freq_2[entry.Key]/2)*2);
    arr1.Sort();

    // Sum of elements up to
    // index of multiples of 4
    int summ = 0;
    foreach (int i in arr1){
      summ += i;
    }

    // Print the sum
    Console.WriteLine(summ);
  }

  // Driver Code
  public static void Main()
  {
    List<int> arr = new List<int>(){5, 3, 2, 3, 6, 4, 4, 4, 5, 5, 5};
    int n = arr.Count;
    findSumLength(arr, n);

  }
}

// THIS CODE IS CONTRIBUTED BY SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// Function to find the maximum of sum
  // of lengths of rectangles and squares
  // formed using given set of sticks
function findSumLength(arr, n)
{

    // Stores the count of frequencies
    // of all the array elements
    let freq = new Map();
    for(let i = 0; i < arr.length; i++)
    {
          if(freq.has(arr[i]))
            freq.set(arr[i], freq.get(arr[i])+1);
          else
            freq.set(arr[i], 1);
    }

    // Stores frequencies which are at least 2
    let freq_2 = new Map();
    for(let [key, value] of freq.entries())
    {
          if (freq.get(key) >= 2)
              freq_2.set(key,freq.get(key));
    }

    // Convert all frequencies to nearest
    // smaller even values.
    let arr1 = [];
    for(let [key, value] of freq_2.entries())
          arr1.push(key * Math.floor(freq_2.get(key)/2)*2);

    arr1.sort(function(a, b){return a - b;});

    // Sum of elements up to
    // index of multiples of 4
    let summ = 0;
    for(let i = 0; i < arr1.length; i++){
      summ += arr1[i];
    }

    // Print the sum
    document.write(summ);
}

 // Driver Code
let arr=[5, 3, 2, 3, 6, 4, 4, 4, 5, 5, 5];
let n = arr.Count;
findSumLength(arr, n);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
34
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(1)*