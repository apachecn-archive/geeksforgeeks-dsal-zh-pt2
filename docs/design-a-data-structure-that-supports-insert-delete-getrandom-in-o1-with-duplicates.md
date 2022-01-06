# 设计一个支持插入、删除、获取 O(1)中随机重复的数据结构

> 原文:[https://www . geesforgeks . org/design-a-data-structure-the-support-insert-delete-get random-in-O1-with-duplicates/](https://www.geeksforgeeks.org/design-a-data-structure-that-supports-insert-delete-getrandom-in-o1-with-duplicates/)

设计一个[数据结构](https://www.geeksforgeeks.org/data-structures/)，可以支持 O(1) [时间复杂度](https://www.geeksforgeeks.org/understanding-time-complexity-simple-examples/)中的以下操作。

1.  **插入(x):** 在数据结构中插入 x。如果 x 不存在，返回**真**，如果 x 已经存在，返回**假**。
2.  **移除(x):** 从数据结构中移除 x(如果存在)。
3.  **getRandom():** 随机返回流中存在的任何值。每个元素被返回的概率应该是**与流包含的相同值元素的数量成线性比例**。

**方法:**在[之前的文章](https://www.geeksforgeeks.org/design-a-data-structure-that-supports-insert-delete-search-and-getrandom-in-constant-time/)中，我们已经讨论了这种数据结构的方法。但是，以前的数据结构仅适用于唯一值。在本文中，我们将设计一个也可以处理重复元素的数据结构。

本文中使用的方法与之前的方法非常相似，但是为了处理重复的元素，使用了[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)的[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来存储[动态数组](https://www.geeksforgeeks.org/how-do-dynamic-arrays-work/)中存在的元素的索引。让我们独立理解每一种方法。

*   **插入(int x):**
    1.  在动态数组 nums[]的末尾插入 x。
    2.  将 x(即)nums . size()–1 的索引插入 **mp[x]** 。这个集合图存储了动态数组**nums【】**中元素 **x** 的所有索引。
*   **移除(int x):**
    1.  通过 mp.count(x)检查流中是否存在 x。如果不存在，则返回**假**。
    2.  如果 x 存在，则集合 mp[x]的第一个元素被删除，其值存储在变量 **indexRemoved** 中。现在，如果此元素(即)indexRemoved 与 nums . length()–1 相同，则直接转到**步骤 6** ，因为这意味着该元素已经在最后一个索引处，并且该元素在恒定时间内被删除。
    3.  如果不是，那么为了在恒定时间内删除这个元素，这个元素与动态数组中的最后一个元素交换。因此，从**MP【nums[nums . size()–1]】**集合中删除值**nums . size()–1**。
    4.  将值索引插入 MP[nums[nums . size()–1]]集合。
    5.  交换索引 nums . size()–1 和 indexRemoved of nums 处的元素。
    6.  从 nums 中删除最后一个元素(从动态数组末尾删除是一个恒定时间操作)。
    7.  如果 mp[val]设置为空，从 mp 中清除 val。
    8.  返回**真**
*   **getrandom():t1**
    1.  获取一个介于 0 和 nums . size()–1 之间的随机数。
    2.  返回此 nums 索引处的值。

下面是上述方法的实现:

```
// C++ program to design a data structure
// that supports insert, delete,
// getRandom in O(1) with duplicates

#include <bits/stdc++.h>

using namespace std;

class Stream {

private:
    // Stores all the numbers present
    // currently in the stream
    vector<int> nums;

    // Unordered ensure O(1) operation
    unordered_map<int, unordered_set<int> > mp;

public:
    // Function to insert values
    // in the stream
    bool insert(int val)
    {
        // Inserting val to the end of array
        nums.push_back(val);

        // Index at which val was inserted
        int index = nums.size() - 1;

        // Inserting the index inside the
        // set mp[val]
        mp[val].insert(index);

        // Return True if only one val
        // is present in the stream
        return mp[val].size() == 1;
    }

    // Function to remove the value
    // from the stream
    bool remove(int val)
    {

        // If the value is not present
        // in the stream
        if (!mp.count(val))
            return 0;

        // Get the value of the first element
        // of the mp[val] and store it
        // in a variable named index
        int index = *(mp[val].begin());

        // Last Index of nums
        int lastIndex = nums.size() - 1;

        // Erase the index from mp[val] set
        mp[val].erase(index);

        // If index == lastIndex, then the
        // element was already deleted
        // from the stream
        if (index != lastIndex) {

            // Delete the lastIndex from
            // mp[nums[lastIndex]] set
            mp[nums[lastIndex]].erase(lastIndex);

            // Insert index into mp[nums[lastIndex]] set
            mp[nums[lastIndex]].insert(index);

            // Swap the values at index and lastIndex
            swap(nums[index], nums[lastIndex]);
        }

        // Delete the last element from nums
        // This operation is O(1) operation
        nums.pop_back();

        // If the size of mp[val] is 0,
        // val is absent from the stream
        // and hence it is removed
        if (mp[val].size() == 0)
            mp.erase(val);
        return 1;
    }

    // Function to get a random number
    // from the stream of data
    int getRandom()
    {

        // Get any random index from 0 to
        // nums.length() - 1
        int randomIndex = rand() % nums.size();

// Return the value at that index
        return nums[randomIndex]; 
    }
};

// Driver code
int main()
{

    Stream myStream;

    cout << myStream.insert(5) << endl;
    cout << myStream.insert(6) << endl;
    cout << myStream.insert(5) << endl;
    cout << myStream.remove(6) << endl;
    cout << myStream.remove(6) << endl;
    cout << myStream.getRandom() << endl;

    return 0;
}
```

**Output:**

```
1
1
0
1
0
5

```