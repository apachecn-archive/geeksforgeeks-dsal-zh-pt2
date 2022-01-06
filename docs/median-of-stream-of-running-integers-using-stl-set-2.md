# 使用 STL 的运行整数流的中间值|集合 2

> 原文:[https://www . geesforgeks . org/running-integers-use-STL-set-2 的流中值/](https://www.geeksforgeeks.org/median-of-stream-of-running-integers-using-stl-set-2/)

给定一个大小为 **N** 的数组 **arr[]** ，表示需要作为数据流读取的整数，任务是在读取每个整数后计算并打印中位数。

**示例:**

> **输入:** arr[] = { 5，10，15 }
> **输出:** 5 7.5 10
> **解释:**
> 从数据流中读取 arr[0]后，中位数为 5。
> 从数据流中读取 arr[1]后，中位数为 7.5。
> 从数据流中读取 arr[2]后，中位数为 10。
> 
> **输入:** arr[] = { 1，2，3，4 }
> **输出:** 1 1.5 2 2.5

**方法:**使用[有序集](https://www.geeksforgeeks.org/ordered-set-gnu-c-pbds/)可以解决问题。按照以下步骤解决问题:

*   初始化一个多有序集，比如说 **mst** 以存储有序的数组元素。
*   使用变量 **i** 遍历数组。对于每一个**I<sup>th</sup>T5【元素】插入**arr【I】**到 **mst** 和[检查变量 **i** 是否为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。如果发现为真，则使用**(* MST . find _ by _ order(I/2))**打印中位数。**
*   否则，取**(* MST . find _ by _ order(I/2))**和**(* MST . find _ by _ order((I+1)/2))**的平均值打印中位数。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <iostream>
#include <ext/pb_ds/assoc_container.hpp> 
#include <ext/pb_ds/tree_policy.hpp> 
using namespace __gnu_pbds; 
using namespace std;
typedef tree<int, null_type, 
less_equal<int>, rb_tree_tag,
tree_order_statistics_node_update> idxmst;

// Function to find the median
// of running integers
void findMedian(int arr[], int N)
{
    // Initialise a multi ordered set
    // to store the array elements 
    // in sorted order
    idxmst mst;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Insert arr[i] into mst
        mst.insert(arr[i]);

        // If i is an odd number
        if (i % 2 != 0) {

            // Stores the first middle
            // element of mst
            double res 
             = *mst.find_by_order(i / 2);

            // Stores the second middle
            // element of mst
            double res1 
              = *mst.find_by_order(
                             (i + 1) / 2);

            cout<< (res + res1) / 2.0<<" ";
        }
        else {

            // Stores middle element of mst
            double res
               = *mst.find_by_order(i / 2);

            // Print median
            cout << res << " ";
        }
    }
}

// Driver Code
int main()
{
    // Given stream of integers
    int arr[] = { 1, 2, 3, 3, 4 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    findMedian(arr, N);
}
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*