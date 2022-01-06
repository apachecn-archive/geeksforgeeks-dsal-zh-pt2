# c++中的 find_by_order()

> 原文:[https://www.geeksforgeeks.org/find_by_order-in-cpp/](https://www.geeksforgeeks.org/find_by_order-in-cpp/)

**find _ by _ order()**是 [<u>有序集</u>](https://www.geeksforgeeks.org/ordered-set-gnu-c-pbds/) 的内置功能，它是 C++中基于策略的数据结构[](https://www.geeksforgeeks.org/policy-based-data-structures-g/)<u>。基于策略的数据结构不是 [C++标准模板库](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/) 的一部分，但是g++编译器支持它们。</u>

<u>[有序集](https://www.geeksforgeeks.org/ordered-set-gnu-c-pbds/)是 g++ 中基于 [<u>策略的数据结构，以有序的顺序维护**唯一的**元素。它执行所有在 ***O(logN)*** 复杂度中由 STL</u>](https://www.geeksforgeeks.org/policy-based-data-structures-g/) 中设置的[执行的操作。
除此之外， ***O(logN)*** 复杂度中还执行了以下两个操作:](https://www.geeksforgeeks.org/set-in-cpp-stl/)</u>

> <u>*   [**Sequence _ of _ key**](https://www.geeksforgeeks.org/order_of_key-in-c/) **(k):** The quantity of goods is strictly less than **k** .*   **Find _ by _ order (k): The th element in the** k <sup>set (counting from zero).</sup></u>

<u>**find_by_order()** 函数接受一个键，比如 **K** ，作为参数，并将迭代器返回到集合中第 K 个<sup>最大的元素。</sup></u>

<u>**示例:**</u>

> <u>*考虑一个集合 S = {1，5，6，17，88}，*
> *S . find _ by _ order(0):返回第 0 个<sup>最大元素，即最小元素，即 1。</sup>*
> *s . find _ by _ order(2):返回 2 <sup>nd</sup> 最大的元素，即 6。*</u>
> 
> <u>**注意:**如果 **K > = N** ，其中 **N** 是集合的大小，那么函数返回 **0** 或者在某些编译器中，返回最小元素的迭代器。</u>

<u>下面是 C++中 **find_by_order()** 函数的实现:</u>

## <u>C++14</u>

```
// C++ program to implement find_by_order()
// for Policy Based Data Structures

#include <bits/stdc++.h>

// Importing header files
#include <ext/pb_ds/assoc_container.hpp>
using namespace std;
using namespace __gnu_pbds;

// Declaring Ordered Set
typedef tree<int, null_type, less<int>, rb_tree_tag,
        tree_order_statistics_node_update>
    pbds;

// Driver Code
int main()
{

      int arr[] = {1, 5, 6, 17, 88};
     int n = sizeof(arr)/sizeof(arr[0]);

    pbds S;

      // Traverse the array
    for (int i = 0; i < n; i++) {

          // Insert array elements
          // into the ordered set
        S.insert(arr[i]);
    }

      // Returns iterator to 0-th
      // largest element in the set
    cout << *S.find_by_order(0) << " ";

    // Returns iterator to 2-nd
      // largest element in the set
    cout << *S.find_by_order(2);

    return 0;
}
```

<u>**Output:**

```
1 6

```</u>