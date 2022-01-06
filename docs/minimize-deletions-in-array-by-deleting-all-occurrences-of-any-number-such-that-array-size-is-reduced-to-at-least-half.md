# 通过删除任何数量的所有出现，使数组大小至少减少一半，从而最大限度地减少数组中的删除

> 原文:[https://www . geeksforgeeks . org/通过删除任意数量的所有出现次数来最小化阵列中的删除，以便将阵列大小减少到至少一半/](https://www.geeksforgeeks.org/minimize-deletions-in-array-by-deleting-all-occurrences-of-any-number-such-that-array-size-is-reduced-to-at-least-half/)

给定一个正整数数组 **arr[]** ，任务是**从数组中选择**一个元素，**删除**所有出现的元素，这样选择的元素数量是**最小**并且数组大小变成**原始大小的至少一半**。
**注意:**给定数组的大小总是偶数。

**示例:**

> **输入:** arr[] = {2，2，2，2，4，4，6，7，7，3，3}
> **输出:** 2
> **解释**:首先我们选择 2，在 arr[]变成–{ 4，4，6，7，7，3，3，3}大小= 8 之后，删除它的所有出现。由于大小仍然大于一半，我们选择 3 并删除它的所有出现，然后 arr[]变成–{ 4，4，6，7，7}，大小= 5。
> 
> **输入:** arr[] = {3，3，3，3，3}
> **输出:** 1
> **解释**:选择 3 并移除其所有出现。

**方法:**移除出现频率最大的元素即可轻松完成任务，只要数组大小至少变成实际大小的一半，我们就返回到目前为止删除的唯一元素数量。

按照以下步骤解决问题:

*   使用[哈希映射](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/)存储数组中元素出现的频率。
*   将频率存储在列表中。
*   **对列表**进行排序，从后面遍历。
*   选择**最大频率**元素，并从数组大小中减去它，**增加**被删除的唯一元素的计数。
*   如果新的数组大小变成**-至少是原始数组大小的一半**，则返回到目前为止唯一元素的数量。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

    // Function to calculate the minimum
    // elements removed
     int reduceArrSize(int arr[],int n)
    {
        unordered_map<int,int> hm;

        // Making frequency map of elements
        for (int i = 0; i < n; i++) {
            hm[arr[i]]++;
        }

        // Storing frequencies in a list
        vector<int> freq;

        for(auto it = hm.begin(); it != hm.end(); it++)
        {
            freq.push_back(it->second);
        }

        // Sorting the list
        sort(freq.begin(), freq.end());

        int size = n;
        int idx = freq.size() - 1;
        int count = 0;

        // Counting number of elements to be deleted
        while (size > n/ 2) {
            size -= arr[idx--];
            count++;
        }
        return count;
    }

    // Driver Code
    int main()
    {
        int arr[] = { 2, 2, 2, 2, 4, 4,
                      6, 7, 7, 3, 3, 3 };
        int n = sizeof(arr)/sizeof(arr[0]);
        int count = reduceArrSize(arr, n);
        cout<<(count);
        return 0;
    }

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to calculate the minimum
    // elements removed
    public static int reduceArrSize(int[] arr)
    {
        HashMap<Integer, Integer> hm = new HashMap<>();

        // Making frequency map of elements
        for (int i = 0; i < arr.length; i++) {
            hm.put(arr[i], hm.getOrDefault(arr[i], 0) + 1);
        }

        // Storing frequencies in a list
        ArrayList<Integer> freq
            = new ArrayList<Integer>(hm.values());

        // Sorting the list
        Collections.sort(freq);

        int size = arr.length;
        int idx = freq.size() - 1;
        int count = 0;

        // Counting number of elements to be deleted
        while (size > arr.length / 2) {
            size -= arr[idx--];
            count++;
        }
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 2, 2, 2, 2, 4, 4,
                      6, 7, 7, 3, 3, 3 };
        int count = reduceArrSize(arr);
        System.out.println(count);
    }
}
```

## 蟒蛇 3

```
# python 3 Program to implement
# the above approach

# Function to calculate the minimum
# elements removed
def reduceArrSize(arr,n):
    hm = {}

    # Making frequency map of elements
    for i in range(n):
        if arr[i] in hm:
            hm[arr[i]] += 1
        else:
            hm[arr[i]] = 1

    # Storing frequencies in a list
    freq = []

    for key,value in hm.items():
        freq.append(value)

    # Sorting the list
    freq.sort()

    size = n
    idx = len(freq) - 1
    count = 0

    # Counting number of elements to be deleted
    while (size > n// 2):
        size -= arr[idx]
        idx -= 1
        count += 1
    return count

# Driver Code
if __name__ == '__main__':
    arr = [2, 2, 2, 2, 4, 4,6, 7, 7, 3, 3, 3]
    n = len(arr)
    count = reduceArrSize(arr, n)
    print(count)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG {

    // Function to calculate the minimum
    // elements removed
    public static int reduceArrSize(int[] arr)
    {
        Dictionary<int, int> hm = new Dictionary<int, int>();

        // Making frequency map of elements
        for (int i = 0; i < arr.Length; i++) {
            if(hm.ContainsKey(arr[i])){
                hm[arr[i]] = hm[arr[i]]+1;
            }
            else{
                hm.Add(arr[i], 1);
            }
        }

        // Storing frequencies in a list
        List<int> freq
            = new List<int>(hm.Values);

        // Sorting the list
        freq.Sort();

        int size = arr.Length;
        int idx = freq.Count - 1;
        int count = 0;

        // Counting number of elements to be deleted
        while (size > arr.Length / 2) {
            size -= arr[idx--];
            count++;
        }
        return count;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = { 2, 2, 2, 2, 4, 4,
                      6, 7, 7, 3, 3, 3 };
        int count = reduceArrSize(arr);
        Console.WriteLine(count);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach
// Function to calculate the minimum
// elements removed
function reduceArrSize(arr)
{
    var hm = new Map();

    // Making frequency map of elements
    for (var i = 0; i < arr.length; i++) {
        if(hm.has(arr[i])){
            hm.set(arr[i], hm.get(arr[i])+1);
        }
        else{
            hm.set(arr[i], 1);
        }
    }

    // Storing frequencies in a list
    var freq =[ ...hm.values()];

    // Sorting the list
    freq.sort();

    var size = arr.length;
    var idx = freq.length - 1;
    var count = 0;

    // Counting number of elements to be deleted
    while (size > arr.length / 2) {
        size -= arr[idx--];
        count++;
    }
    return count;
}

// Driver Code
var arr = [2, 2, 2, 2, 4, 4,
              6, 7, 7, 3, 3, 3];
var count = reduceArrSize(arr);
document.write(count);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
2
```

***时间复杂度*** **:** O(N*logN)，排序频率列表
***辅助空间*** **:** O(N)，hashmap 存储频率