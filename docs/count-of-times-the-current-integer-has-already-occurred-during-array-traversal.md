# 数组遍历期间当前整数已经出现的次数

> 原文:[https://www . geesforgeks . org/当前整数在数组遍历期间已经发生的次数/](https://www.geeksforgeeks.org/count-of-times-the-current-integer-has-already-occurred-during-array-traversal/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出当前整数在数组遍历过程中已经出现的次数。

**示例**:

> **输入** : arr[] = {2，3，3，200，175，2，200，2，175，3}
> **输出**:0 0 1 0 1 1 2 1 2
> **说明**:第 0 次索引前，遇到 20 次。在第二个索引之前，在索引 1 处会遇到一次 3。同样，在第 7 个索引之前，2 出现了两次，以此类推。
> 
> **输入** : arr[] = {200，200，55，200，55，2，3，2}
> **输出**:0 1 0 2 1 0 1

**接近**:可以通过使用 [HashMap](http://www.geeksforgeeks.org/java-util-hashmap-in-java/) 跟踪不同元素的**频率**直到**当前**元素来解决任务。按照以下步骤解决问题:

*   创建一个散列表，比如“ **occ** ”，存储不同元素的[频率，直到当前元素](https://www.geeksforgeeks.org/find-frequency-of-each-element-in-a-limited-range-array-in-less-than-on-time/)
*   对于**当前的**元素，检查其是否已经存在于**散列表**中的**而不是**中。
*   如果存在，存储与之对应的**频率**，否则存储 **0** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above appproach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of
// times current integer has already
// occurred during array traversal.
void getOccurrences(vector<int>& arr)
{
    // Store the size of array
    int n = arr.size();

    // Hashmap to keep track of
    // the frequencies
    unordered_map<int, int> occ;

    for (int i = 0; i < n; ++i) {

        // If element is already
        // present inside hashmap
        if (occ.find(arr[i]) != occ.end()) {
            cout << occ[arr[i]] << " ";
        }
        else {
            cout << 0 << " ";
        }

        // Increment the frequency
        occ[arr[i]]++;
    }
}

// Driver Code
int main()
{
    vector<int> arr
        = { 2, 3, 3, 200, 175,
            2, 200, 2, 175, 3 };
    getOccurrences(arr);

    return 0;
}
```

**Output**

```
0 0 1 0 0 1 1 2 1 2 
```

***时间复杂度** : O(N)*
***辅助空间** : O(N)*